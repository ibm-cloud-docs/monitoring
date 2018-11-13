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

You can monitor your infrastructure, and the applications running on it with the IBM Cloud Monitoring with Sysdig service. 
{:shortdesc}

After you provision an instance of the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix}}, and configure a Sysdig agent for a metrics source, you can view, monitor, and manage data through the IBM Cloud Monitoring with Sysdig Web UI for that source.

Data for default metrics is automatically collected. You can configure custom metrics and add labels to those metrics to describe their characteristics. Data for these custom metrics is also automatically collected.

You can analyze data in the *Explore* tab and in the *Dashboard* tab of the Web UI. You monitor the data through metric views and dashboards. 

* Use a metric view to monitor an individual metric.
* Use dashboards to get a specialized insight into network data, application data, topology, services, hosts, and containers by monitoring data through panels. A panel displays a metric or group of metrics in a dashboard.

For each metric view and dashboard, you can define the scope of the data, how to aggregate data, and what time and group filters to apply to the data. For more information, see [Managing data](https://console.test.cloud.ibm.com/docs/services/Monitoring-with-Sysdig/manage.html#manage).

In the *Explore* tab, you can monitor data by using default metrics and default dashboards. You can use labels to define new infrastructure groups that you can then use to aggregate data differently and monitor your environment. You can also use custom dashboards that you define through the *Dashboard* tab.

In the *Dashboards* tab, you can monitor data by using any of the default dashboards or by creating new ones.

You can configure a default dashboard as the the default entry point for a team, unifying a team's experience, and allowing users to focus their immediate attention on the most relevant information for them. 
{: tip}


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

The following table outlines tasks that you can run to work with dashboards from the UI:

| Task | Description |
|------|-------------|
| [Create dashboard](/docs/services/Monitoring-with-Sysdig/dashboards.html#create) | Create a custom dashboard in the Web UI. |
| [Copy a dashboard](/docs/services/Monitoring-with-Sysdig/dashboards.html#copy) | Make a copy of a dashboard in the current team where the dashboard is available, or copy a dashboard to another team. |
| [Changing the scope](/docs/services/Monitoring-with-Sysdig/dashboards.html#scope) | Chang the scope of a dashboard.       |
| [Delete dashboard](/docs/services/Monitoring-with-Sysdig/dashboards.html#delete) |  Delete a dashboard. |
| [Share a dashboard]() | Share dashboards between users in a team, and externally, by configuring a public URL for the dashboard. |
{: caption="Table 1. Dashboard tasks that you can run in the Web UI" caption-side="top"} 

The following table outlines tasks that you can run programmatically to work with dashboards:

| Task                    |	Using Python script             | Using REST API                |
|-------------------------|---------------------------------|-------------------------------|
| Create a dashboard      | [Creating custom dashboards](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#create_python) | [Creating a dashboard by using the API](/docs/services/Monitoring-with-Sysdig/Monitoring-with-Sysdig#create_api) |
| Delete a dashboard      | [Deleting a dashboard](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#delete_python) | [Deleting a dashboard by using the API](/docs/services/Monitoring-with-Sysdig/Monitoring-with-Sysdig#delete_api) |
| Saving dashboards       | [Saving dashboards for a team by using a python script](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#save_python) | [Saving the dashboards of a team by using the API](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#save_api) |
{: caption="Table 2. Tasks to manage dashboards programmatically" caption-side="top"} 



## Metrics
{: #metrics}

Use metrics to analyze statistically data that has numerical values. A metric is a quantitaive measure that has one or more labels to define its characteristics.
{: tip}

A metric is represented by time series. A time series is a set of numeric data points over a period of time. 

Metrics are classified into two groups: 

* [Default metrics](/docs/services/Monitoring-with-Sysdig/metrics.html#default) 
* [Custom metrics](/docs/services/Monitoring-with-Sysdig/metrics.html#custom)

Labels are classified as infrastructure labels and metric descriptor lables. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels. 

You can use labels to identify and differentiate characteristics of a metric, for example,
* You can group infrastructure objects into logical hierarchies. 
* You can filter out data. 
* You can split aggregated data into segments. 

For more information, see [Labels](/docs/services/Monitoring-with-Sysdig/metrics.html#labels).

## Panels
{: panels}

A panel displays a metric or group of metrics in a dashboard. 

You can use any of the following panel types to visualize metrics:

| Type | Description |
|------|-------------|
| Line | Use this panel to view trends over time for one or more metrics.  |
| Area | Use this panel to view trends over time for one or more metrics.  |
| Top list | Use this panel to compare a metric across groups of entities. The bar chart is sorted in descending order.  |
| Histogram | Use this panel to view the frequency distribution of a metric in buckets.  |
| Topology | Use this panel to visualize the infrastructure as a topology map, and the relations between entities in the map.  |
| Number | Use this panel to view a single number that represents the value of an aggregated metric over time for one or more entities.  |
| Table | Use this panel to display numerical data for your infrastructure based on metrics and segments.  |
| Text | Use this panel to add text. Use markdown to add your text.  |
{: caption="Table 3. Panel types" caption-side="top"} 

You can copy, change the scope, duplicate, delete, export, and explore panels.

You can export data from a panel. Consider the following information when you export data:

* You can export data to a **json file** from a line chart.
* You can export data to a **csv file** from a table chart or from a line chart.


The following table lists the tasks that you can run with panels:

| Task | Description |
|------|-------------|
| [Copy panel](/docs/services/Monitoring-with-Sysdig/panel.html#copy) | Copy a panel into a new dashboard.  |
| [Change scope](/docs/services/Monitoring-with-Sysdig/panel.html#change) | Change the scope of a panel. |
| [Duplicate panel](/docs/services/Monitoring-with-Sysdig/panel.html#duplicate) | Copy a panel in the same dashboard.  |
| [Delete panel](/docs/services/Monitoring-with-Sysdig/panel.html#delete) | Delete a panel from the dashboard.  |
| [Export data](/docs/services/Monitoring-with-Sysdig/panel.html#export) | Export data from a panel into a csv file or a json file.  |
| [Create alert](/docs/services/Monitoring-with-Sysdig/panel.html#alert) | Define an alert on a metric. |
{: caption="Table 4. Panel tasks" caption-side="top"} 


