---

copyright:
  years:  2018, 2020
lastupdated: "2020-11-26"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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
{:external: target="_blank" .external}

# Collecting availability metrics by using the Prometheus Blackbox exporter
{: #blackbox}

The Prometheus Blackbox exporter allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP. The Sysdig agent can be used in conjunction with the Blackbox exporter to collect availability metrics. The availability metrics can then be alerted upon within Sysdig to alert users on the availability of the endpoints.
{:shortdesc}

The following figure shows different configurations that you can configure when using the Blackbox exporter to monitor availability of remote hosts:

![Blackbox components](images/blackbox.svg "Blackbox components")


[Blackbox exporter configuration](https://github.com/prometheus/blackbox_exporter/blob/master/CONFIGURATION.md)

 
Complete the following steps to configure the Prometheus Blackbox Exporter:


## Step 1. Configure a Sysdig agent to collect metrics
{: #blackbox_step1}

[Install a Sysdig agent to collect and forward metrics from a server to an {{site.data.keyword.mon_full_notm}} instance](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-config_agent).



## Step 2. Install the Prometheus Blackbox exporter in the server that you want to monitor
{: #blackbox_step2}

Blackbox exporter is configured via a configuration file and command-line flags 

### Run the Blackbox exporter as a docker container
{: #blackbox_step2-1}

Complete the following steps:

1. Download the [blackbox.yml file](https://github.com/prometheus/blackbox_exporter/blob/master/blackbox.yml){: external} from Github.

    Save the file to the directory `/config/prometheus/blackbox/`.

2. Run the Blackbox exporter as a docker container:

    ```
    docker run --rm -d -p 9115:9115 -l io.prometheus.scrape=true -l io.prometheus.port=9115 -l io.prometheus.path=/probe --name blackbox_exporter -v `pwd`:/config/prometheus/blackbox prom/blackbox-exporter:master --config.file=/config/prometheus/blackbox/blackbox.yml        
    ```
    {: pre}

3. Check the exporter is up. Run the following command:

    ```
    docker container ls
    ```
    {: pre}

    You can see an output like the following one:
    ```
    CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                    NAMES
    2480a0034bb4        prom/blackbox-exporter:master   "/bin/blackbox_expor…"   36 minutes ago      Up 36 minutes       0.0.0.0:9115->9115/tcp   blackbox_exporter
    ```
    {: screen}

    To stop the blackbox container, run the following command: `docker container stop 2480a0034bb4`.



### Run the Blackbox exporter as a service in a Linux server
{: #blackbox_step2-2}

Complete the following steps:







## Step 3. Configure network settings
{: #Blackbox_step3}

If you want to collect metrics from remote servers, complete the following steps:

1. Enable the firewall to allow access to the `blackbox_exporter`.

2. [Optional] Update the VPC rules

    If you use private endpoints, add an inbound rule to the security group for port `9115` with `source type = Security Group` and choose the security group for the server.



## Step 4. Update the Sysdig agent that is running in the server
{: #Blackbox_step4}

Choose one of the following Sysdig agents:

### Kubernetes Sysdig agent
{: #Blackbox_step4-1}


Run the following command to edit the configmap and add information about the Blackbox targets that you want to monitor:

```
kubectl edit configmap sysdig-agent -n ibm-observe
```
{: pre}

```yaml
log:
  file_priority: error
configmap: true
### Agent tags
# tags: linux:ubuntu,dept:dev,local:nyc

#### Sysdig Software related config ####

# Sysdig collector address
# collector: 192.168.1.1

# Collector TCP port
# collector_port: 6666

# Whether collector accepts ssl
# ssl: true

# collector certificate validation
# ssl_verify_certificate: true

#######################################
# new_k8s: true
# k8s_cluster_name: production
security:
  k8s_audit_server_url: 0.0.0.0
  k8s_audit_server_port: 7765
k8s_cluster_name: <CLUSTER_NAME>/<CLUSTER_ID>
tags: ibm.containers-kubernetes.cluster.id:<CLUSTER_ID>
collector: <INGESTION_ENDPOINT>
collector_port: 6443
ssl: true
ssl_verify_certificate: true
sysdig_capture_enabled: false
promscrape_fastproto: true
use_promscrape: true
prometheus:
  enabled: true
  prom_service_discovery: true
  log_errors: true
  max_metrics: 200000
  max_metrics_per_process: 200000
  max_tags_per_metric: 100
  ingest_raw: true
  ingest_calculated: false
prometheus.yaml:
----
global:
  scrape_interval: 10s
scrape_configs:
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
    - https://promcat.io/apps/harbor
    - https://www.ibm.com/software/passportadvantage
  relabel_configs:
  - source_labels: [__address__]
    target_label: __param_target
  - source_labels: [__param_target]
    target_label: instance
  - source_labels: [__param_target]
    target_label: blackbox_instance
  - target_label: __address__
    replacement: blackbox-exporter.ibm-observe:9115
```
{: codeblock}

Where 

* `<IP_ADDRESS_OF_REMOTE_SERVER>` is the IP address of a server that you want to monitor.
* `<INGESTION_ENDPOINT>` is the Sysdig instance ingestion endpoint, for example, `ingest.us-south.monitoring.cloud.ibm.com`. See [Sysdig Collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion). 


When you save the file, changes are applied.



### Docker Sysdig agent
{: #Blackbox_step4-2}


### Linux service Sysdig agent
{: #Blackbox_step4-3}

Complete the following steps:

1. SSH into the server. Then, change to the directory `/opt/draios/etc/` and run the following command:

    ```
    cd /opt/draios/etc/
    ```
    {: pre}

2. Update the `/opt/draios/etc/dragent.yaml` to [enable remote scraping](https://docs.sysdig.com/en/collecting-prometheus-metrics-from-remote-hosts.html){: external}. 

    Append the following section to the `dragent.yaml` file:

    ```yaml
    prometheus:
     enabled: true
     interval: 30
     log_errors: true
     max_metrics: 3000
     max_metrics_per_process: 3000
     max_tags_per_metric: 20
     process_filter:
       - include:
           port: 9290 
           conf:
             port: 9290 
             path: "/metrics"
    ```
    {: codeblock}

3. Restart the Sysdig agent. Run the following command:

    ```
    service dragent restart
    ```
    {: pre}



## Step 5. Configure the default dashboard and alerts to analyze the Blackbox status of your server
{: #Blackbox_step5}


To configure the default dashboard and alerts to analyze the Blackbox status of your server, run the following command:

```
docker run -it --rm sysdiglabs/promcat-connect:0.1 install Blackbox:2.5.0 -t <SYSDIG_TOKEN>  -u <ENDPOINT>
```
{: codeblock}

Where

* `<SYSDIG_TOKEN>` is the Sysdig token. See [Getting the Sysdig API token](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-api_token#api_token_get).
* `<ENDPOINT>` is the Sysdig instance endpoint. See [Sysdig endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints).


Then, [launch the Sysdig web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch), and go to the *Dashboards* section.








