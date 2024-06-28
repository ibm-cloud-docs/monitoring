---

copyright:
  years:  2018, 2023
lastupdated: "2023-09-19"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Collecting metrics by infrastructure
{: #collect-metrics-by-host}

You can collect metrics from a number of platforms, orchestrators, and a wide range of applications such as Prometheus, JMX, StatsD, Kubernetes, and other application stacks, that are available in the {{site.data.keyword.cloud}}, outside the {{site.data.keyword.cloud_notm}}, or on-prem. You can also add more metrics by creating custom metrics and adding integrations.
{: shortdesc}

## Metrics collected
{: #collect-metrics-by-host-1}


| Type                         | Infrastructure       | Metrics info |
|------------------------------|----------------------|------------------|
| Orchestrated environment     | Kubernetes clusters  | [Metrics for orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/) |
| Orchestrated environment     | OpenShift clusters   | [Metrics for orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/) |
| Non-Orchestrated environment | Virtual Machines (VM)  | [Metrics for non-orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/) |
| Non-Orchestrated environment | Bare metal servers | [Metrics for non-orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/) |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) | [Metrics for non-orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/) |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) on VPC | [Metrics for non-orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/) |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) on VMware | [Metrics for non-orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/) |
| Windows environment          | Windows-based servers | [Metrics for Windows environments]https://docs.sysdig.com/en/docs/sysdig-monitor/integrations/integration-library/infrastructure-integrations/windows/) |
{: caption="Table 1. Metrics by infrastructure" caption-side="top"}

## Colletion method
{: #collect-metrics-by-host-2}

The following table shows the options that you can choose to monitor a host by type of infratsructure:


| Type                         | Infrastructure       | Agent for Non-Orchestrated environments | Agent for Orchestrated environments | Prometheus remote write |
|------------------------------|----------------------|------------------|-----------------|------------------------|
| Orchestrated environment     | Kubernetes clusters  |  | Supported |
| Orchestrated environment     | OpenShift clusters   |  | Supported |
| Non-Orchestrated environment | Virtual Machines (VM)  | Supported | Supported |
| Non-Orchestrated environment | Bare metal servers | Supported | Supported |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) on IBM Cloud, on-prem, other clouds | Supported | Supported |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) on VPC | Supported | Supported |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) on VMware | Supported | Supported |
| Windows environment          | Windows-based servers |  |  | Supported by using the Windows exporter |
{: caption="Table 2. Mode by infrastructure" caption-side="top"}

## Checking the number of time series that are collected per agent
{: #collect-metrics-by-host-3}

In {{site.data.keyword.mon_full_notm}}, you can monitor your monitoring agent by using the dashboard template **monitoring agent Health & Status** that is available in **Host Infrastructure**. In this dashboard, you can see the number of monitoring agents that are deployed and connected to the instance, check the version of the monitoring agents, and find out how many metrics per host the agent is collecting. For more information, see [Checking the number of custom time series that are collected per agent](/docs/monitoring?topic=monitoring-agent_ts_limits).

## Finding out the agent version that runs on a host
{: #collect-metrics-by-host-4}

You can use the the *Sysdig Agent Health & Status* dashboard to determine the {{site.data.keyword.mon_short}} agent versions that are running in your hosts. For more information, see [Determining the version of an agent](/docs/monitoring?topic=monitoring-agent_version_host).
