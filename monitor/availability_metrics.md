---

copyright:
  years:  2018, 2020
lastupdated: "2020-07-16"

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

The Prometheus Blackbox exporter allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP.  The Sysdig agent can be used in conjunction with the Blackbox exporter to collect availability metrics. The availability metrics can then be alerted upon within Sysdig to alert users on the availability of the endpoints.
{:shortdesc}

For example, you can configure the Prometheus Blackbox exporter to get information about the availability of a Windows system, or to get the availability of a URL.

## Step 1. Configuring the Blackbox exporter
{: #availability_metrics_step1}

You can run the Prometheus Blackbox exporter as an application or as a docker container from a Linux system in conjunction with the Sysdig agent.

The exporter is available as a [binary release](https://github.com/prometheus/blackbox_exporter/releases){: external}, as a [docker container](https://hub.docker.com/r/prom/blackbox-exporter/){: external}, or the [code is available in github](https://github.com/prometheus/blackbox_exporter){: external}.


As regular programs, in containers, as background services, on baremetal, on virtual machines. Because they are queried and do query over network they do need appropriate open ports. Otherwise they are frugal.

By default the prober uses IPv6 until told otherwise. But the Docker daemon blocks IPv6 until told otherwise. Hence our blackbox exporter running in a Docker container can’t connect via IPv6.

You can configure the Blackbox exporter by using a configuration file and command-line flags.
 (such as what configuration file to load, what port to listen on, and the logging format and level).

Blackbox exporter can reload its configuration file at runtime. If the new configuration is not well-formed, the changes will not be applied. A configuration reload is triggered by sending a SIGHUP to the Blackbox exporter process or by sending a HTTP POST request to the /-/reload endpoint.

To view all available command-line flags, run ./blackbox_exporter -h.

To specify which configuration file to load, use the --config.file flag.


HTTP, HTTPS (via the http prober), DNS, TCP socket and ICMP (see permissions section) are currently supported. Additional modules can be defined to meet your needs.

The timeout of each probe is automatically determined from the scrape_timeout in the Prometheus config, slightly reduced to allow for network delays. This can be further limited by the timeout in the Blackbox exporter config file. If neither is specified, it defaults to 120 seconds.

### Configure the Blackbox exporter (local docker)

For example, complete the following instructions to configure a Blackbox exporter when the container approach is used:

1. Download the [blackbox.yml file](https://github.com/prometheus/blackbox_exporter/blob/master/blackbox.yml){: external} from Github.

[Blackbox exporter configuration](https://github.com/prometheus/blackbox_exporter/blob/master/CONFIGURATION.md)

2. Start the blackbox exporter.

    ```
    docker run --rm -d -p 9115:9115 --name blackbox_exporter -v `pwd`:/config/ prom/blackbox-exporter:master --config.file=/config/blackbox.yml
    ```
    {: pre}

    ```
    $ docker container ls
    CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                    NAMES
    2480a0034bb4        prom/blackbox-exporter:master   "/bin/blackbox_expor…"   36 minutes ago      Up 36 minutes       0.0.0.0:9115->9115/tcp   blackbox_exporter
    ```
    {: screen}

    To stop a conatiner, run 
    ```
    docker conbtainer stop 2480a0034bb4
    ```

3. Test the blackbox exporter is working by manually running the probe to test your Windows system.  

    For example, you can do a simple `icmp` check to see if the system is responding. See the [documentation](https://github.com/prometheus/blackbox_exporter/blob/master/README.md){: external} for other options. 

    ```
    curl 'http://localhost:9115/probe?module=icmp&target=<system ip>'
    ```
    {: codeblock}

    where `<system ip>` is the IP of the host you are checking.

    You should get a payload back with `probe_success 1` as the last line to indicate that the system at `<system ip>` is up.

3. Update the `/opt/draios/etc/dragent.yaml` to enable `probe_success` metrics.

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

    When you enable this option, you can segment data by `windows_hostname` and build alerts upon this metric.

4. Restart the Sysdig agent. Run the following command:

    ```
    service dragent restart
    ```
    {: pre}

---------

















The Prometheus Blackbox exporter allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP.  The Sysdig agent can be used in conjunction with the Blackbox exporter to collect availability metrics.  The availability metrics can then be alerted upon within Sysdig to alert users on the availability of the endpoints.

The exporters are available as [binary releases](https://github.com/prometheus/blackbox_exporter/releases), as a [docker containers](https://hub.docker.com/r/prom/blackbox-exporter/) or the [code is available in github](https://github.com/prometheus/blackbox_exporter).

The container approach is used for this example.

1. Download the [blackbox.yml file](https://github.com/prometheus/blackbox_exporter/blob/master/blackbox.yml) from Github 

2. Start the blackbox exporter:

    `docker run --rm -d -p 9115:9115 --name blackbox_exporter -v `pwd`:/config/ prom/blackbox-exporter:master --config.file=/config/blackbox.yml`

3. Test the blackbox exporter is working by manually running the probe to test your Windows system.  In this case I'm doing a simple icmp check to see if the system is responding.  See the [documentation](https://github.com/prometheus/blackbox_exporter/blob/master/README.md) for other options and you can even build your own configuration tests for something more complex.

    `curl 'http://localhost:9115/probe?module=icmp&target=<system ip>'`

    where `<system ip>` is the IP of the host you are checking.

4. You should get a payload back with `probe_success 1` as the last line to indicate that the system at `<system ip>` is up.

5. Update the Sysdig agent to scrape the blackbox exporter - you need to provide the details of the check you want to run on the call ( hint: you can copy the one from above ).  We can add to the original prometheus configuration from above and indicate that we wish to scrape the local endpoint and provide it with the targets from above.

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
{: #windows_step5}




## Sysdig uptime alerts

The Sysdig agent provides a liveliness probe that can be used in conjunction with the Sysdig uptime alerts.  The details provided in this document explain how to perform endpoint testing for systems where the agent is not installed ( for example Windows hosts ) or potentially other service dependencies where you do not have a Sysdig agent running.





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
