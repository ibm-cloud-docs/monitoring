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

# Monitoring your environment
{: #monitoring}

You can monitor your infrastructure, and the applications running on it with the IBM Cloud Monitoring with Sysdig service. You can analyze the data that is collected for metrics. You can monitor this data through panels and dashboards in the Web UI. You can aggregate and filter out data  that is displayed through metrics or by getting a specialized insight into network data, application data, topology, services, hosts, and containers trhough dashboards.
{:shortdesc}

After you provision an instance of the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix}}, and configure a Sysdig agent for a metrics source, you can view, monitor, and manage metrics through the IBM Cloud Monitoring with Sysdig Web UI.

After you configure a Sysdig agent, data is automatically collected. Default metrics are automatically collected. You can add custom metrics and labels to custom metrics to describe characteristics of a metric. 

You can use the *Explore* tab to monitor your data by using default metrics and default dasshboards. You can use labels to define new infrastructure groups that you can use to aggregate data differently.

You can also apply a *Time filter* to aggregate data differently.


You can also create new Dashboards where you can leverage  the  new groups, segments, and metrics.

You can also enable events and define alerts.




## Dashboards
{: #dashboards}

A **dashboard** shows groups of metrics that report on the health, performance, and state of your infrastructure, applications, and services for a single host or a group of hosts. Dashboards offer a specialized insight into network data, application data, topology, services, hosts, and containers.

Use dashboards to monitor your infrastructure, applications, and services. 
{: tip}

In the **DASHBOARDS** section of the Web UI, dashboards are organized into three main groups:

* *My Dashboards*: These are the dashboards that are created by the user who is currently logged in.
* *My Shared Dashboards*: These are the dashboards that are created by the user who is currently logged in, and that are shared with other users.
* *Dashboards Shared With Me*: These are the dashboards that are created by other users, and shared with the current user.

In the **EXPLORE** section of the Web UI, dashboards are organized into two groups:
* *Default dashboards*: These are the pre-defined dashboards.
* *My Dashboards*: These are the dashboards that are created by the user who is currently logged in.

You can use pre-defined dashboards. You can also create custom dashboards through the Web UI or programmatically. You can backup and restore dashboards by using Python scripts or the Sysdig REST API.

You can also copy and share dashboards through the Web UI. 


## Metrics
{: #metrics}

Use metrics to analyze statistically data that has numerical values. A metric is a quantitaive measure that has one or more labels to define its characteristics.
{: tip}

A metric is represented by time series. A time series is a set of numeric data points over a period of time. 

Metrics are classified into two groups: 

* Default metrics 
* Custom metrics

Labels are classified as infrastructure labels and metric descriptor lables. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels. 

You can use labels to identify and differentiate characteristics of a metric, for example,
* You can group infrastructure objects into logical hierarchies. 
* You can filter out data. 
* You can split aggregated data into segments. 

For more information, see [Working with metrics]().

## Panels
{: panels}


## As an administrator you can:

## As a user you can:


