---

copyright:
  years:  2018, 2023
lastupdated: "2023-07-25"

keywords: IBM Cloud, monitoring, prometheus, exporters, promcat

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# Collecting metrics by using Prometheus exporters
{: #prometheus-exporters}

You can use Prometheus exporters to collect metrics from hosts, services, or apps which do not natively expose Prometheus-formatted metrics. You can monitor these metrics through a {{site.data.keyword.mon_short}} instance.
{: shortdesc}

See the [{{site.data.keyword.IBM_notm}} support statement](/docs/monitoring?topic=monitoring-agent_support) for the use of Prometheus exporters.
{: important}

There are different sources for Prometheus exporters:
- Official exporters are available in [the official Prometheus GitHub organization](https://github.com/prometheus){: external} and are labelled **official**.
- Sysdig curates and maintains [PromCat](https://promcat.io/){: external}. PromCat is an enterprise resource catalog where you can find supported {{site.data.keyword.mon_short}} integrations for Kubernetes platforms and cloud-native services.

You can collect metrics from different sources such as:
- Hosts for which a {{site.data.keyword.mon_short}} agent is not available such as Windows systems or VMware ESXi-Host systems.
- Hosts for which a {{site.data.keyword.mon_short}} agent is available, but you need to collect other types of metrics such as IPMI sensor metrics or hardware and kernel-relaed metrics.
- Services like MySQL database

![Prometheus integration with {{site.data.keyword.mon_short}}](images/prometheus.svg "Prometheus integration with {{site.data.keyword.mon_short}}"){: caption="Figure 1. Prometheus integration with {{site.data.keyword.mon_short}}" caption-side="bottom"}

The following table lists some Prometheus exporters that you can use to monitor your infrastructure:

| Exporters                | Use case                               | Source |
|--------------------------|----------------------------------------|---------|
| `Blackbox Exporter`       | Allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP. The monitoring agent can be used in conjunction with the Blackbox exporter to collect availability metrics.  | [Prometheus Blackbox exporter](https://github.com/prometheus/blackbox_exporter){: external} (official)|
| `IPMI Exporter`          | Collects Intelligent Platform Management Interface (IPMI) device sensor metrics.  | [Prometheus IPMI exporter](https://github.com/soundcloud/ipmi_exporter){: external} (opensource)  |
| `Windows WMI Exporter`   | Collects Windows system metrics. | [PromCat: Windows Exporter](https://promcat.io/apps/windows){: external} (opensource) |
| `Node Exporter`          | Collects hardware and kernel-related metrics that are exposed by *NIX kernels. | [Node exporter](https://github.com/prometheus/node_exporter){: external} (official) |
| `VMware Exporter`        | Collects metrics from VMware vCenter deployments. | [VMWare exporter](https://github.com/pryorda/vmware_exporter){: external} (Opensource) |
{: caption="Table 1. Exporters" caption-side="top"}


## Windows exporter
{: #prometheus-exporters-wmi}

Configure the [Prometheus `windows_exporter`](https://github.com/prometheus-community/windows_exporter){: external} to collect Windows system metrics.
{: note}

The Prometheus Windows exporter runs as a Windows service. You configure the metrics that you want to monitor by enabling collectors.

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


To learn how to configure the Windows exporter, see [Monitoring a Windows environment](/docs/monitoring?topic=monitoring-windows).

The legacy Prometheus WMI Exporter is still supported, see [Monitoring a Windows environment using the legacy WMI Exporter](/docs/monitoring?topic=monitoring-windows_wmi) for information on the WMI Exporter.
{: note}




## IPMI exporter
{: #prometheus-exporters-ipmi}

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

To learn how to configure the IPMI exporter, see [Configuring the Prometheus IPMI Exporter to monitor sensor metrics](/docs/monitoring?topic=monitoring-ipmi).

You can also check the tutorial: [Configure the Prometheus IPMI Exporter to monitor sensor metrics in a Bare metal](/docs/monitoring?topic=monitoring-baremetal_linux#baremetal_linux_step3).


## Blackbox exporter
{: #prometheus-exporters-blackbox}

Allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP. The monitoring agent can be used in conjunction with the Blackbox exporter to collect availability metrics.

Configure the [Prometheus Blackbox exporter](https://github.com/prometheus/blackbox_exporter){: external} to monitor host availability, such as URL sites.
{: note}

## Node exporter
{: #prometheus-exporters-node}

In addition to the set of metrics that are automatically collected by the monitoring agent, you might want to collect other Linux host metrics that are exposed by *NIX kernels.

Configure the [Prometheus Node exporter](https://github.com/prometheus/node_exporter){: external} to collect hardware and kernel metrics that are exposed by *NIX kernels.
{: note}

For more information, see [Monitoring Linux host metrics with the Node Exporter](https://prometheus.io/docs/guides/node-exporter/){: external}.

## VMWare exporter
{: #prometheus-exporters-vmware}

For information on configuring a VMWare exporter, see [Monitoring for VMware vCenter Server deployments](/docs/monitoring?topic=monitoring-vmware-vcenter)
