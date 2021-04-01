---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, baremetal, linux, prometheus, remote monitoring

subcollection: monitoring

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
{:external: target="_blank" .external}

# Collecting availability metrics by using the Prometheus Blackbox exporter
{: #collect_availability_metrics}

The Prometheus Blackbox exporter allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP.  The monitoring agent can be used in conjunction with the Blackbox exporter to collect availability metrics. The availability metrics can then be alerted upon within {{site.data.keyword.mon_full_notm}} to alert users on the availability of the endpoints.
{:shortdesc}



## Step 1. Configure a monitoring agent on Linux
{: #collect_availability_metrics_step1}

Complete the following steps to configure a monitoring agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. [Obtain the access key](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Deploy the monitoring agent. Run the following command from a terminal.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    For example:

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key 7ac04746-1104-4f82-8445-f71427dd2a1d --collector ingest.us-south.monitoring.cloud.ibm.com --collector_port 6443 --secure true --tags resourceType:baremetal01,region:dallas --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Where

    * ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the {{site.data.keyword.mon_full_notm}} capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

    * Set **secure** to *true* to use SSL with the communication.

If the monitoring agent fails to install correctly, install the kernel headers manually. Choose a distribution and run the command for that distribution. Then, retry the deployment of the monitoring agent.

For Debian and Ubuntu Linux distributions, run the following command:

```
apt-get -y install linux-headers-$(uname -r)
```
{: codeblock}

For RHEL, CentOS, and Fedora Linux distributions, run the following command:

```
yum -y install kernel-devel-$(uname -r)
```
{: codeblock}



## Step 2. Configiure the Blackbox exporter

pre-req - install docker
```
apt install docker.io
```

1. Download the [blackbox.yml file](https://github.com/prometheus/blackbox_exporter/blob/master/blackbox.yml){: external} from Github.

[Blackbox exporter configuration](https://github.com/prometheus/blackbox_exporter/blob/master/CONFIGURATION.md)

2. Start the blackbox exporter.

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

    To stop a container, run 
    ```
    docker container stop 2480a0034bb4
    ```

3. Test the blackbox exporter is working by manually running the probe to test your Windows system.  

    For example, you can do a simple `icmp` check to see if the system is responding. See the [documentation](https://github.com/prometheus/blackbox_exporter/blob/master/README.md){: external} for other options. 

    ```
    curl 'http://localhost:9115/probe?module=icmp&target=<system ip>'
    ```
    {: codeblock}

    where `<system ip>` is the IP of the host you are checking.

    You should get a payload back with `probe_success 1` as the last line to indicate that the system at `<system ip>` is up.




## Step 3. Edit the dragent yaml file
{: #change_linux_agent_edit_agent}

The yaml file is located in */opt/draios/etc/*.

Complete the following steps to edit the file and apply the changes:

1. Access the *dragent.yaml* directly. The file is located in `/opt/draios/etc/dragent.yaml`.
2. Edit the file. Use valid YAML syntax.
3. Restart the agent. Run the following command:

    ```
    service dragent restart
    ```
    {: codeblock}

Update the `/opt/draios/etc/dragent.yaml` to enable `probe_success` metrics.

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
            - blackbox_bm01:
                always:
                conf:
                url: "http://52.117.190.199:9115/probe?module=icmp&target=23.217.138.108"
                tags:
                    service: baremetal01_uptime
                    hostname: baremetal01
    ```
    {: codeblock}

52.117.190.199:9115/probe?target=&module=http_2xx

customerid: 7ac04746-1104-4f82-8445-f71427dd2a1d
collector: ingest.us-south.monitoring.cloud.ibm.com
collector_port: 6443
ssl: true
sysdig_capture_enabled: false
tags: resourceType:baremetal,region:dallas
prometheus:
     enabled: true
     interval: 30
     log_errors: true
     max_metrics: 3000
     max_metrics_per_process: 3000
     max_tags_per_metric: 20
     process_filter:
       - include:
        container.label.io.prometheus.scrape: "true"
        conf:
            # Custom path definition
            # If the Label doesn't exist we'll still use "/metrics"
            path: "{container.label.io.prometheus.path}"
 
            # Port definition
            # - If the Label exists, only scan the given port.
            # - If it doesn't, use port_filter instead.
            # - If there is no port_filter defined, skip this process
            port: "{container.label.io.prometheus.port}"
            port_filter:
                - include: [9115]

        - include:
           port: 9090 
           conf:
             port: 9090 
             path: "/metrics"
       - include:
           port: 9290 
           conf:
             port: 9290 
             path: "/metrics"
      - include:
           port: 9115 
           conf:
             port: 9115 
             path: "/probe"







process_filter:
    - exclude:
        process.name: docker-proxy
    - exclude:
        container.image: sysdig/agent
    # special rule to exclude processes matching configured prometheus appcheck
    - exclude:
        appcheck.match: prometheus
    - include:
        container.label.io.prometheus.scrape: "true"
        conf:
            # Custom path definition
            # If the Label doesn't exist we'll still use "/metrics"
            path: "{container.label.io.prometheus.path}"
 
            # Port definition
            # - If the Label exists, only scan the given port.
            # - If it doesn't, use port_filter instead.
            # - If there is no port_filter defined, skip this process
            port: "{container.label.io.prometheus.port}"
            port_filter:
                - exclude: [9092,9200,9300]
                - include: 9090-9500
                - include: [9913,9984,24231,42004]
    - exclude:
        container.label.io.prometheus.scrape: "false"
    - include:
        kubernetes.pod.annotation.prometheus.io/scrape: true
        conf:
            path: "{kubernetes.pod.annotation.prometheus.io/path}"
            port: "{kubernetes.pod.annotation.prometheus.io/port}"
    - exclude:
        kubernetes.pod.annotation.prometheus.io/scrape: false

4. Restart the monitoring agent. Run the following command:

    ```
    service dragent restart
    ```
    {: pre}




