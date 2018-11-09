---

copyright:
  years: 2018
lastupdated: "2018-11-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Working with metrics
{: #metrics}

After you provision an instance of the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix}}, and configure a Sysdig agent for a metrics source, you can view, monitor, and manage metrics through the IBM Cloud Monitoring with Sysdig Web UI.
{:shortdesc}

Metrics are quantitative values or measures that are divided into two groups: 

* Default metrics 
* Custom metrics

Labels define the characteristics of a metric. They are classified as infrastructure labels and metric descriptor lables. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels. 

You can use labels to identify and differentiate characteristics of a metric:
* You can group infrastructure objects into logical hierarchies. 
* You can filter out data. 
* You can split aggregated data into segments. 



## Default metrics 
{: #default}

Default metrics report on the system, the orchestrator, and the network infrastructure. 

The monitoring service automatically adds labels to each metric.

## Custom metrics
{: #custom}

Custom metrics vary based on the type of infrastructure, and the applications that you monitor. Some examples are JMX, Prometheus, and StatsD. 

These metrics have a set of pre-defined labels. You can add additional custom labels.

The monitoring service maintains an index of all custom metrics and custom labels that have reported data in the last 14 days. You can use these metrics to configure dashboards, scopes, and alerts.

Consider the following information about how the monitoring service manages the index entries:
*  A metric is automatically removed from the monitoring service index and marked as missing when any of the following conditions occur:
    
    * The monitoring service does not receive any data for a metric or label for more than 14 days.
    
    * A metric or label has never reported data.

* You cannot configure new artifacts with a missing metric or a missing label. 
* You cannot update existing artifacts until the missing metrics and labels are removed from the current configuration.
* You can use a missing metric or a missing label on data queries and charts. 
* Your existing artifacts are not affected if they include a missing metric or a missing label.
* When data is received for a missing metric or label, the metric or label is added back to the index.


## Grouping metrics
{: #group}



## Graphing metrics
{: #graph}



## Alerting on a metric
{: #alert}

