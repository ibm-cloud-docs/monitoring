---

copyright:
  years:  2018, 2023
lastupdated: "2023-03-27"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Checking the number of custom time series that are collected per agent
{: #agent_ts_limits}

Use the **Sysdig Agent Health & Status** dashboard to determine the number of custom time series that are collected per agent. You can also check in this dashboard the number of time series that you are collecting.
{: shortdesc}



Complete the following steps:

1. [Access your {{site.data.keyword.mon_short}} instance](/docs/monitoring?topic=monitoring-launch).

2. Click ![Dashboard](../images/dashboards.png "Dashboard").

3. Click **Host Infrastructure** &gt; **Sysdig Agent Health & Status**.

The dashboard displays the limit of custom time series that are collected per agent for each host.

![Sysdig Agent Health & Status dashboard showing agent versions](../images/agent_version.png "Sysdig Agent Health & Status dashboard showing agent versions"){: caption="Figure 1. Sysdig Agent Health & Status dashboard showing agent versions" caption-side="bottom"}



## Checking the metrics that are collected per agent
{: #collected_pricing_agent_metrics}

In {{site.data.keyword.mon_full_notm}}, you can monitor your monitoring agent by using the dashboard template **monitoring agent Health & Status** that is available in the dashboard templates available out-of-the-box. In this dashboard, you can see the number of monitoring agents that are deployed and connected to the instance, check the version of the monitoring agents, and find out how many metrics per host the agent is collecting.

In this dashboard, the panel **TimeSeries Usage** provides the number of time-series that are collected from each category (Prometheus, JMX, StatsD, Prometheus Remote Write and Platform Metrics). This panel uses the query `sum(sysdig_ts_usage)by(metric_category)` that you can also run in PromQL Explorer, in your dashboards or for alerts.

In case you need to investigate which applications or services are contributing more to the Prometheus time-series, you can use the metric `scrape_series_added`. This metric represents the number of time series scraped and ingested from the monitoring agent via Prometheus and includes several labels to facilitate the analysis such as `kube_cluster_name`, `kube_namespace_name`, `kube_workload_name` or `container_name`.

The following query represents the number of time series ingested from the monitoring agent via Prometheus grouped by cluster, namespace, workloads and container so you can identify those applications that are contributing more time series:

```text
sum(scrape_series_added)by(kube_cluster_name, kube_namespace_name, kube_workload_name, container_name)
```
{: codeblock}
