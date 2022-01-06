---

copyright:
  years:  2018, 2022
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, monitoring agent, event filters

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Managing custom metrics
{: #mng_metrics}

To filter custom metrics, you must customize the metrics_filter section in the agent configuration file. You can specify which metrics to include and which ones to filter out by configuring the include and exclude filtering parameters.
{: shortdesc}

A metric is a quantitative measure that has one or more labels to define its characteristics.
- A metric is represented by time series. 
- A time series is a set of numeric data points over a period of time. 

Metrics are classified into two groups: 
* Default metrics 
* Custom metrics

When you configure a monitoring agent, default metrics are collected automatically. 

In addition, you can configure custom metrics to monitor your sources through the {{site.data.keyword.mon_full_notm}} service. 
- Custom metrics are collected by the monitoring agent from third-party integrations. 
- Some examples of custom metrics are Prometheus, JMX, StatsD, and App Checks. 


## Filtering custom metrics
{: #mng_metrics_filter}

To filter custom metrics, you must customize the agent configuration file. You can specify which metrics to include and which ones to filter out by configuring the include and exclude filtering parameters.

For more information on how to configure the monitoring agent, see:
- Linux monitoring agent: [Including and excluding metrics](/docs/monitoring?topic=monitoring-change_linux_agent#change_linux_agent_inc_exc_metrics)
- Kubernetes monitoring agent: [Including and excluding metrics](/docs/monitoring?topic=monitoring-change_kube_agent#change_kube_agent_inc_exc_metrics)
- Docker container monitoring agent: [Including and excluding metrics](/docs/monitoring?topic=monitoring-change_agent#params)


## Logging into a file what metrics are included or excluded
{: #mng_metrics_log}

You can log the custom metrics that are collected by an agent. You must set the **metrics_excess_log** to **true** in the **log** section will enable logging of the custom metrics that are included or excluded.

For more information on how to configure the monitoring agent to report which metrics are collected, see:
- Linux monitoring agent: [Logging into a file what metrics are included or excluded](/docs/monitoring?topic=monitoring-change_linux_agent#change_linux_agent_log_level)
- Kubernetes monitoring agent: [Logging into a file what metrics are included or excluded](/docs/monitoring?topic=monitoring-change_kube_agent#change_kube_agent_log_metrics)
- Docker container monitoring agent: [Logging into a file what metrics are included or excluded](/docs/monitoring?topic=monitoring-change_agent#log_level)







