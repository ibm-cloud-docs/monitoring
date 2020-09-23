---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

keywords: Sysdig, IBM Cloud, monitoring, Sysdig agent, event filters

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

# Including and excluding metrics
{: #agent_mng_metrics}

When you delete an {{site.data.keyword.mon_full_notm}} instance, or if you want to stop collecting metrics from a source, you must uninstall the Sysdig agent from sources where it was installed as a service. If you deployed a Sysdig agent as a container, you must run docker commands to remove the agent.
{:shortdesc}


## Including and excluding metrics
{: #change_linux_agent_inc_exc_metrics}

To filter custom metrics, you must customize the **metrics_filter** section in the *dragent.yaml* file. You can specify which metrics to include and which ones to filter out by configuring the **include** and **exclude** filtering parameters.

**Note:** The filtering rule order is set as follows: the first rule that matches a metric is applied.

For example, if the *metrics_filter* section of a Sysdig agent looks as follows:

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* You are configuring the Sysdig agent to collect all data from metrics that start with *metricA*, *metricB*, and *haproxy.backend*. 
* You are filtering out metrics that start with *metricC* and other metrics that start with *haproxy*. 
* The entry `exclude: metricA.*` is ignored.