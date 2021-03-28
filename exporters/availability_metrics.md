---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: Sysdig, IBM Cloud, monitoring, blackbox, prometheus, ping

subcollection: Monitoring-with-Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

---

# Testing endpoints with Blackbox exporter
{: #availability_metrics}

You can use the Prometheus Blackbox exporter allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP.  The monitoring agent can be used in conjunction with the Blackbox exporter to collect availability metrics. The availability metrics can then be alerted upon within Sysdig to alert users on the availability of the endpoints.
{:shortdesc}

For example, you can configure the Prometheus Blackbox exporter to get information about the availability of a Windows system, or to get the availability of a URL.

## Step 1. Configuring the Blackbox exporter
{: #availability_metrics_step1}

You can run the Prometheus Blackbox exporter as an application or as a docker container from a Linux system in conjunction with the monitoring agent.

The exporter is available as a [binary release](https://github.com/prometheus/blackbox_exporter/releases){: external}, as a [docker container](https://hub.docker.com/r/prom/blackbox-exporter/){: external}, or the [code is available in github](https://github.com/prometheus/blackbox_exporter){: external}.


As regular programs, in containers, as background services, on baremetal, on virtual machines. Because they are queried and do query over network they do need appropriate open ports. Otherwise they are frugal.

By default the prober uses IPv6 until told otherwise. But the Docker daemon blocks IPv6 until told otherwise. Hence our blackbox exporter running in a Docker container can’t connect via IPv6.

You can configure the Blackbox exporter by using a configuration file and command-line flags.
 (such as what configuration file to load, what port to listen on, and the logging format and level).

Blackbox exporter can reload its configuration file at runtime. If the new configuration is not well-formed, the changes will not be applied. A configuration reload is triggered by sending a SIGHUP to the Blackbox exporter process or by sending a HTTP POST request to the /-/reload endpoint.

To view all available command-line flags, run ./blackbox_exporter -h.

To specify which configuration file to load, use the --config.file flag.


The timeout of each probe is automatically determined from the scrape_timeout in the Prometheus config, slightly reduced to allow for network delays. This can be further limited by the timeout in the Blackbox exporter config file. If neither is specified, it defaults to 120 seconds.


### Configure the Blackbox exporter (local docker)

For example, complete the following instructions to configure a Blackbox exporter when the container approach is used:



docker exec –it f0c664219a5e /bin/bash
 for blabbox   -->  docker exec –it f0c664219a5e /bin/sh

get name of a container
docker ps --format "{{.Names}}"


copy a file into a docker container

docker cp c:\path\to\local\file container_name:/path/to/target/dir/


docker cp /opt/draios/etc/docker-dragent.yaml sysdig-agent:/opt/draios/etc/dragent.yaml


default dragent.yaml

1. Download the [blackbox.yml file](https://github.com/prometheus/blackbox_exporter/blob/master/blackbox.yml){: external} from Github.

    You can customize the configuration file. See [Blackbox exporter configuration](https://github.com/prometheus/blackbox_exporter/blob/master/CONFIGURATION.md){: external} to see the different options to configure the Blackbox exporter.

2. Copy the configuration YAML file to the host where you run the monitoring agent.

    For example, in a bare metal, from the `shh` session, create the directory `/usr/sysdig`. Run the following commands:

    ```
    cd /usr
    ```
    {: pre}

    ```
    mkdir sysdig
    ```
    {: pre}

    Copy the file to the bare metal. From the directory where the file is available, run the following command:

    ```
    scp blackbox.yml  root@<IP_ADDRESS>:/usr/sysdig/
    ```
    {: pre}

    Where `<IP_ADDRESS>` is the public IP address of the bare metal server.

    If the command fails, check that your VPN connection is still open.

3. Start the blackbox exporter.

    ```
    docker run --rm -d -p 9115:9115 -l io.prometheus.scrape=true -l io.prometheus.port=9115 -l io.prometheus.path=/probe --name blackbox_exporter -v `pwd`:/config/ prom/blackbox-exporter:master --config.file=/config/blackbox.yml
    ```
    {: pre}

    ```
    $ docker container ls
    CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                    NAMES
    2480a0034bb4        prom/blackbox-exporter:master   "/bin/blackbox_expor…"   36 minutes ago      Up 36 minutes       0.0.0.0:9115->9115/tcp   blackbox_exporter
    ```
    {: screen}

    To stop a conatiner, run `docker conbtainer stop 2480a0034bb4`.{: tip}

4. Test the blackbox exporter is working by manually running the probe to test your Windows system.  

    For example, you can do a simple `icmp` check to see if the system is responding. See the [documentation](https://github.com/prometheus/blackbox_exporter/blob/master/README.md){: external} for other options. 

    ```
    curl 'http://<IP_ADDRESS>:9115/probe?module=icmp&target=<system ip>'
    ```
    {: codeblock}

    where 

    * `<IP_ADDRESS>` is the IP address of the host where the blackbox exporter is running.
    
    * `<system ip>` is the IP of the host you are checking.

    You should get a payload back with `probe_success 1` as the last line to indicate that the system at `<system ip>` is up.

5. Update the `/opt/draios/etc/dragent.yaml` to enable `probe_success` metrics.

    You must add details about the check that you want to run on the call. 

    ```yaml
    prometheus:
        enabled: true
        interval: 30
        log_errors: true
        max_metrics: 3000
        max_metrics_per_process: 3000
        max_tags_per_metric: 20
        remote_services:
            - blackbox_win_1:
                always:
                conf:
                url: "http://localhost:9115/probe?module=icmp&target=10.240.0.5"
                tags:
                    service: windows_uptime
                    windows_hostname: windows-test-01
    ```
    {: codeblock}

    Update the `/etc/prometheus/proemtheus.yml` to enable `probe_success` metrics.

    ```
    global:
      scrape_interval: 10s
      external_labels:
        host-name: baremetal02
    scrape_configs:
    - job_name: blackbox-k8s
      metrics_path: /probe
      params:
        module: [http_2xx]
      kubernetes_sd_configs:
      - role: pod
      relabel_configs:
      - action: keep
        source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_probe]
        regex: true
      - action: keep
        source_labels: [__meta_kubernetes_pod_node_name]
        regex: __HOSTNAME__
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - source_labels: [__param_target]
        target_label: blackbox_instance
      - target_label: __address__
        replacement: blackbox-exporter.monitoring:9115
    - job_name: blackbox
      metrics_path: /probe
      params:
        module: [http_2xx]
      static_configs:
      - targets:
        - https://prometheus.io/
        - https://promcat.io/
        - https://api.promcat.io/apps
        - https://www.google.com/search?q=promcat
        - https://www.google.es/
        - https://promcat.io/apps/harbor
      relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - source_labels: [__param_target]
        target_label: blackbox_instance
      - target_label: __address__
        replacement: blackbox-exporter.monitoring:9115
    ```
    

    When you enable this option, you can segment data by `windows_hostname` and build alerts upon this metric.

4. Restart the monitoring agent. Run the following command:

    ```
    service dragent restart
    ```
    {: pre}



### Configure the Blackbox exporter as a service



Install the Prometheus IPMI exporter
{: #baremetal_linux_step3-1}

Complete the following steps:

1. From a local terminal,[download the Prometheus IPMI exporter](https://github.com/soundcloud/ipmi_exporter){: external}.

2. In the bare metal server, from the `shh` session, create the directory `/usr/sysdig`. Run the following commands:

    ```
    cd /usr
    ```
    {: pre}

    ```
    mkdir sysdig
    ```
    {: pre}

3. Copy the file to the bare metal. From the directory where the file is available, run the following command:

    ```
    scp ipmi_exporter-v1.2.0.linux-amd64.tar.gz  root@<IP_ADDRESS>:/usr/sysdig/
    ```
    {: pre}

    Where `<IP_ADDRESS>` is the public IP address of the bare metal server.

    If the command fails, check that your VPN connection is still open.

4. In the bare metal server, from the `shh` session, uncompress the file. Run the following commands:

    ```
    cd /usr/sysdig/
    ```
    {: pre}

    ```
    tar -xvf ipmi_exporter-v1.2.0.linux-amd64.tar.gz 
    ```
    {: pre}

5. In the bare metal server, from the `shh` session, install the FreeIPMI suite. Run the following commands:

    ```
    sudo apt-get update
    ```
    {: pre}

    ```
    sudo apt-get install freeipmi
    ```
    {: pre}

6. In the bare metal server, from the `shh` session, check the `ipmi_local.yml` file. Optionally, you can update the file to exclude sensors that you do not want to monitor.

    Change to the directory where you have extracted the IPMI exporter:

    ```
    cd ipmi_exporter-v1.2.0.linux-amd64/
    ```
    {: pre}

    Check the configuration file. Run the command: `more ipmi_local.yml` You should see a file with similar content.

    ```yaml
    # Configuration file for ipmi_exporter

    # This is an example config for scraping the local host.
    # In most cases, this should work without using a config file at all.
    modules:
            default:
                    # Available collectors are bmc, ipmi, chassis, dcmi, and sel
                    collectors:
                    - bmc
                    - ipmi
                    - dcmi
                    - chassis
                    - sel
                    # Got any sensors you don't care about? Add them here.
                    exclude_sensor_ids:
                    # - 2
    ```
    {: codeblock}

7. In the bare metal server, from the `shh` session, run the IPMI exporter.

    ```
    ./ipmi_exporter --config.file=ipmi_local.yml &
    ```
    {: pre}

8. Check the IPMI exporter is running. Run the command:

    ```
    ps -aux | grep ipmi
    ```
    {: pre}
 
    You should see the IPMI exporter running.





the Blackbox exporter only focuses on availability 

https://prometheus.io/download/

wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.17.0/blackbox_exporter-0.17.0.linux-amd64.tar.gz

tar xvzf blackbox_exporter-0.17.0.linux-amd64.tar.gz

you are going to define service files and define start and restart policies for it.

First, make your executables accessible for your user local account.

$ sudo mv blackbox_exporter /usr/local/bin

    Note : by moving files to the /usr/local/bin path, all users may have access to the blackbox exporter binary. For binaries to be restricted to your own user account, you need to add the path to your own PATH environment variable.

Next, create configuration folders for your blackbox exporter.

`/etc/blackbox`

$ sudo mkdir -p /etc/blackbox
$ sudo mv blackbox.yml /etc/blackbox

For safety purposes, the Blackbox exporter is going to be run by its own user account (named blackbox here)

As a consequence, we need to create a user account for the Blackbox exporter.

$ sudo useradd -rs /bin/false blackbox

Then, make sure that the blackbox binary can be run by your newly created user.

$ sudo chown blackbox:blackbox /usr/local/bin/blackbox_exporter

Give the correct permissions to your configuration folders recursively.

$ sudo chown -R blackbox:blackbox /etc/blackbox/*

 create your service file.

To create the Blackbox exporter service, head over to the /lib/systemd/system folder and create a service named blackbox.service

$ cd /lib/systemd/system
$ sudo touch blackbox.service















The Prometheus Blackbox exporter allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP.  The monitoring agent can be used in conjunction with the Blackbox exporter to collect availability metrics.  The availability metrics can then be alerted upon within Sysdig to alert users on the availability of the endpoints.

The exporters are available as [binary releases](https://github.com/prometheus/blackbox_exporter/releases), as a [docker containers](https://hub.docker.com/r/prom/blackbox-exporter/) or the [code is available in github](https://github.com/prometheus/blackbox_exporter).

The container approach is used for this example.

1. Download the [blackbox.yml file](https://github.com/prometheus/blackbox_exporter/blob/master/blackbox.yml) from Github 

2. Start the blackbox exporter:

    `docker run --rm -d -p 9115:9115 --name blackbox_exporter -v `pwd`:/config/ prom/blackbox-exporter:master --config.file=/config/blackbox.yml`

3. Test the blackbox exporter is working by manually running the probe to test your Windows system.  In this case I'm doing a simple icmp check to see if the system is responding.  See the [documentation](https://github.com/prometheus/blackbox_exporter/blob/master/README.md) for other options and you can even build your own configuration tests for something more complex.

    `curl 'http://localhost:9115/probe?module=icmp&target=<system ip>'`

    where `<system ip>` is the IP of the host you are checking.

4. You should get a payload back with `probe_success 1` as the last line to indicate that the system at `<system ip>` is up.

5. Update the monitoring agent to scrape the blackbox exporter - you need to provide the details of the check you want to run on the call ( hint: you can copy the one from above ).  We can add to the original prometheus configuration from above and indicate that we wish to scrape the local endpoint and provide it with the targets from above.

    ```
    prometheus:
        enabled: true
        interval: 30
        log_errors: true
        max_metrics: 3000
        max_metrics_per_process: 3000
        max_tags_per_metric: 20
        remote_services:
            - blackbox_win_1:
                always:
                conf:
                url: "http://localhost:9115/probe?module=icmp&target=10.240.0.5"
                tags:
                    service: windows_uptime
                    windows_hostname: windows-test-01
    ```

6. There will be some new prometheus `probe_success` metrics now available in Sysdig.  These are the blackbox exporter metrics.  You can segment by `windows_hostname` and build alerts upon this metric.




## Step 5. [Optional] Verifying uptime for Windows with Prometheus Blackbox exporter
{: #availability_metrics_windows_step5}




## Sysdig uptime alerts

The monitoring agent provides a liveliness probe that can be used in conjunction with the Sysdig uptime alerts.  The details provided in this document explain how to perform endpoint testing for systems where the agent is not installed ( for example Windows hosts ) or potentially other service dependencies where you do not have a monitoring agent running.





- provision a cluster
- create a namespace in the rg where the cluster is running 
`ibmcloud cr namespace-add observability-demo`

- [Creating new images that refer to a source image](/docs/Registry?topic=Registry-registry_images_#registry_images_creating)

[Pull images from another registry to your local computer ](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pulling)

$ docker pull prom/blackbox-exporter:master
master: Pulling from prom/blackbox-exporter
Digest: sha256:e4397a1543f5a51449618292fb6c75952716321b54a345f2c3dc6a0af2e96222
Status: Image is up to date for prom/blackbox-exporter:master
docker.io/prom/blackbox-exporter:master

$ docker tag prom/blackbox-exporter:master us.icr.io/observability-demo/blackbox-exporter:v1
