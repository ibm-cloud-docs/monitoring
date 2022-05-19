---

copyright:
  years:  2018, 2022
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, {{site.data.keyword.mon_short}} agent, event filters

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Configuring which metrics to monitor
{: #mng_metrics}

You can customize a {{site.data.keyword.mon_short}} agent and specify which metrics to include and which ones to filter out.
{: shortdesc}

# Filtering custom metrics in a {{site.data.keyword.mon_short}} agent
{: #mng_metrics_filter}

To filter custom metrics, you must customize the metrics_filter section in the agent configuration file. You can specify which metrics to include and which ones to filter out by configuring the include and exclude filtering parameters.

For more information on how to configure the {{site.data.keyword.mon_short}} agent, see:
- Linux {{site.data.keyword.mon_short}} agent: [Including and excluding metrics](/docs/monitoring?topic=monitoring-change_linux_agent#change_linux_agent_inc_exc_metrics)
- Kubernetes {{site.data.keyword.mon_short}} agent: [Including and excluding metrics](/docs/monitoring?topic=monitoring-change_kube_agent#change_kube_agent_inc_exc_metrics)
- Docker container {{site.data.keyword.mon_short}} agent: [Including and excluding metrics](/docs/monitoring?topic=monitoring-change_agent#params)


## Logging into a file what metrics are included or excluded
{: #mng_metrics_log}

You can log the custom metrics that are collected by an agent. You must set the **metrics_excess_log** to **true** in the **log** section will enable logging of the custom metrics that are included or excluded.

For more information on how to configure the {{site.data.keyword.mon_short}} agent to report which metrics are collected, see:
- Linux {{site.data.keyword.mon_short}} agent: [Logging into a file what metrics are included or excluded](/docs/monitoring?topic=monitoring-change_linux_agent#change_linux_agent_log_level)
- Kubernetes {{site.data.keyword.mon_short}} agent: [Logging into a file what metrics are included or excluded](/docs/monitoring?topic=monitoring-change_kube_agent#change_kube_agent_log_metrics)
- Docker container {{site.data.keyword.mon_short}} agent: [Logging into a file what metrics are included or excluded](/docs/monitoring?topic=monitoring-change_agent#log_level)







