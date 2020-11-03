---

copyright:
  years:  2018, 2020
lastupdated: "2020-07-16"

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

You can use Prometheus exporters with {{site.data.keyword.mon_full_notm}} to collect metrics from hosts for which a Sysdig agent is not available. You can also use exporters to collect metrics that the Sysdig agent does not collect automatically.
{:shortdesc}

Sysdig curates and maintains [PromCat](https://promcat.io/){: external}. PromCat is an enterprise resource catalog where you can find supported monitoring integrations for Kubernetes platforms and cloud-native services.
{: note}

The following table lists some Prometheus exporters that you can use to monitor your infrastructure:

| Exporters                | Use case                               | Source |
|--------------------------|----------------------------------------|---------|
| `Blackbox exporter`       | Allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP. The Sysdig agent can be used in conjunction with the Blackbox exporter to collect availability metrics.  | [Prometheus Blackbox exporter](){: external} |
| `IPMI exporter`          | Collects Intelligent Platform Management Interface (IPMI) device sensor metrics.  | [Prometheus IPMI exporter](https://github.com/soundcloud/ipmi_exporter){: external}  |
| `Windows WMI exporter`   | Collects Windows system metrics. | [PromCat: Windows Exporter](https://promcat.io/apps/windows){: external} |
{: caption="Table 1. Collectors" caption-side="top"} 


| Exporters                | Service agent | Docker agent | Kubernetes agent |
|--------------------------|---------------|--------------|------------------|
| `Blackbox exporter`      |  |  | ![Checkmark icon](images/checkmark-icon.svg) (Promscrap v2) |
| `IPMI exporter`          |  |  |  |
| `Windows WMI exporter`   |  |  |  |
{: caption="Table 1. Collectors" caption-side="top"} 


## WMI exporter
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

For example, to learn how to configure the WMI exporter, see [Monitoring a Windows environment](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-windows).

## IPMI exporter
{: #prometheus_ipmi}

In addition to the set of metrics that are automatically collected by the Sysdig agent, you might want to collect other metrics such as sensor metrics. 

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


For example, to learn how to configure the IPMI exporter, see [Configure the Prometheus IPMI Exporter to monitor sensor metrics in a Bare metal](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-baremetal_linux#baremetal_linux_step3).



## Blackbox exporter
{: #prometheus_blackbox}

Allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP. The Sysdig agent can be used in conjunction with the Blackbox exporter to collect availability metrics.






