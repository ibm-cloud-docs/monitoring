---

copyright:
  years:  2018, 2020
lastupdated: "2020-11-26"

keywords: Sysdig, IBM Cloud, monitoring, prometheus, exporters, promcat

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

# Collecting metrics by using Prometheus exporters
{: #prometheus}

You can use Prometheus exporters with {{site.data.keyword.mon_full_notm}} to collect metrics from hosts for which a monitoring agent is not available. You can also use exporters to collect metrics that the monitoring agent does not collect automatically.
{:shortdesc}

Sysdig curates and maintains [PromCat](https://promcat.io/){: external}. PromCat is an enterprise resource catalog where you can find supported monitoring integrations for Kubernetes platforms and cloud-native services.
{: note}

The following table lists some Prometheus exporters that you can use to monitor your infrastructure:

| Exporters                | Use case                               | Source |
|--------------------------|----------------------------------------|---------|
| `Blackbox exporter`       | Allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP. The monitoring agent can be used in conjunction with the Blackbox exporter to collect availability metrics.  | [Prometheus Blackbox exporter](https://github.com/prometheus/blackbox_exporter){: external} |
| `IPMI exporter`          | Collects Intelligent Platform Management Interface (IPMI) device sensor metrics.  | [Prometheus IPMI exporter](https://github.com/soundcloud/ipmi_exporter){: external}  |
| `Windows WMI exporter`   | Collects Windows system metrics. | [PromCat: Windows Exporter](https://promcat.io/apps/windows){: external} |
{: caption="Table 1. Exporters" caption-side="top"} 


You can collect metrics from different exporters. However, exporters that are hosted in PromCat are supported by Sysdig.
{: important}

## Exporters
{: #prometheus-exporters}

### WMI exporter
{: #prometheus_wmi}

Configure the [Prometheus WMI exporter](https://github.com/prometheus-community/windows_exporter){: external} to collect Windows system metrics.
{: note}

The Prometheus WMI exporter runs as a Windows service. You configure the metrics that you want to monitor by enabling collectors. 

The following collectors are supported:

| Collector name | Information about metrics collected per collector | 
|----------------|---------------------------------------------------|
| `cpu`          | [CPU metrics](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.cpu.md){: external} |
| `cs`           | [Computer system metrics](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.cs.md){: external} |
| `logical_disk` | [Disk metrics](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.logical_disk.md){: external} |
| `os`           | [Operating System metrics](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.os.md){: external} |
| `system`       | [System metrics](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.system.md){: external} |
| `net`          | [Network interface metrics](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.net.md){: external} |
| `memory`       | [Memory metrics](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.memory.md){: external} |
{: caption="Table 1. Collectors" caption-side="top"} 


To learn how to configure the WMI exporter, see [Monitoring a Windows environment](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-windows).




### IPMI exporter
{: #prometheus_ipmi}

In addition to the set of metrics that are automatically collected by the monitoring agent, you might want to collect other metrics such as sensor metrics. 

Configure the [Prometheus IPMI exporter](https://github.com/soundcloud/ipmi_exporter){: external} to collect Intelligent Platform Management Interface (IPMI) device sensor metrics.
{: note}

* The Prometheus IPMI Exporter exporter supports local IPMI devices and remote devices that can be accessed by using Remote Management Control Protocol (RMCP). 
* When you use RMCP to access remote devices, you can use an IPMI exporter to monitor multiple IPMI devices. You identify each device by passing the target hostname as a parameter. 
* The IPMI exporter relies on tools from the FreeIPMI suite.

You can collect the following metrics when you configure the IPMI exporter:

* IPMI admin metrics

    The metric `ipmi_up {collector="<NAME>"}` reports `1` when data from a remote host is collected successfully. It reports `0` for collection of data in a local host. 
    
    The metric `ipmi_scrape_duration_seconds` reports the amount of time that it takes the collector to retrieve the data.

* IPMI System event log (SEL) metrics

    The metric `ipmi_sel_entries_count` reports the number of entries in the system event log. 

    The metric `ipmi_sel_free_space_bytes` reports the number of free bytes for new ystem event log entries.

* IPMI sensor data

    The IPMI exporter collects 2 metrics per sensor type: state and value. A value of `0` reports a normal state. A value of `1` reports a warning state. A value of `2` reports a critical state. A value of `NaN` reports information not available. For example, see the metrics for different sensors:

    Temperature sensor metrics: `ipmi_temperature_celsius`, `ipmi_temperature_state`
    
    Fan speed sensor metrics: `ipmi_fan_speed_rpm`, `ipmi_fan_speed_state`
    
    Voltage sensor metrics: `ipmi_voltage_state`, `ipmi_voltage_volts`

* IPMI chassis power state of the machine

    The metric `ipmi_chassis_power_state` informs about the current state of the chassis of the machine. It has a value of `1` when the power is on. It has a value of `0` when the power is off.

* DCMI data

    The metric `ipmi_dcmi_power_consumption_current_watts` informs about the live power consumption of the machine in Watts. 

* BMC details

    The metric ipmi_bmc_info includes information about the firmware revision and manufacturer in labels and has a value of `1`.

For more information, see [Prometheus IPMI Exporter](https://github.com/soundcloud/ipmi_exporter){: external}.

To learn how to configure the IPMI exporter, see [Configuring the Prometheus IPMI Exporter to monitor sensor metrics](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-ipmi).

You can also check the tutorial: [Configure the Prometheus IPMI Exporter to monitor sensor metrics in a Bare metal](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-baremetal_linux#baremetal_linux_step3).


### Blackbox exporter
{: #prometheus_blackbox}

Allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP. The monitoring agent can be used in conjunction with the Blackbox exporter to collect availability metrics.

Configure the [Prometheus Blackbox exporter](https://github.com/prometheus/blackbox_exporter){: external} to monitor host availability, such as URL sites.
{: note}


## Installing dashboards and alerts for exporters that are hosted in PromCat
{: #prometheus_exporter-ui-promcat}

To add the default dashboards and alerts that are available for an exporter that is hosted in PromCat, run the following command:

```
docker run -it --rm sysdiglabs/promcat-connect:0.1 install rancher:2.5.0 -t <SYSDIG_TOKEN>  -u <ENDPOINT>
```
{: codeblock}

Where

* `<SYSDIG_TOKEN>` is the Sysdig token. See [Getting the Sysdig API token](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-api_token#api_token_get).
* `<ENDPOINT>` is the Sysdig instance endpoint. See [Sysdig endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints).



## Sample. Kubernetes monitoring agent configmap with 2 exporters
{: premetheus-sample}

The following configmap sample shows how 2 exporters are configured in a Kubernetes monitoring agent:

```yaml
Name:         sysdig-agent
Namespace:    ibm-observe
Labels:       <none>
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"v1","data":{"dragent.yaml":"log:\n  file_priority: debug\nconfigmap: true\n### Agent tags\n# tags: linux:ubuntu,dept:dev,lo...

Data
====
dragent.yaml:
----
log:
  file_priority: debug
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
k8s_cluster_name: mycluster/xxxxxxxxxxxxxxxxxx
tags: ibm.containers-kubernetes.cluster.id:xxxxxxxxxxxxxxxxxx
collector: ingest.us-south.monitoring.cloud.ibm.com
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
- job_name: ipmi
  metrics_path: /metrics
  static_configs:
  - targets:
    - 'xxx.xxx.xxx.xxx:9290'
```
{: screen}


