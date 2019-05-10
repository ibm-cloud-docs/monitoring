---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring

subcollection: Sysdig

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

# Monitoring your environment
{: #monitoring}

You can monitor your infrastructure, and the applications that run on it with the {{site.data.keyword.mon_full_notm}} service. You can request a capture to analyze what happens in a node during a time frame.
{:shortdesc}

First, you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}. Then, you configure Sysdig agents for your metrics sources. After the sources are configured, you can view, monitor, and manage data through the service's web UI.

Data for default metrics is automatically collected. You can configure custom metrics and add labels to those metrics to describe their characteristics. Data for these custom metrics is also automatically collected.

You can analyze data in the *Explore* tab and in the *Dashboard* tab of the web UI. You monitor the data through metric views and dashboards. 

* Use a metric view to monitor an individual metric.
* Use dashboards to get a specialized insight into network data, application data, topology, services, hosts, and containers by monitoring data through panels. A panel displays a metric or group of metrics in a dashboard.

For each metric view and dashboard, you can define the scope of the data, how to aggregate data, and what time and group filters to apply to the data. For more information, see [Managing data](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

In the *Explore* tab, you can monitor data by using default metrics and default dashboards. You can use labels to define new infrastructure groups that you can then use to aggregate data differently and monitor your environment. You can also use custom dashboards that you define through the *Dashboard* tab.

In the *Dashboards* tab, you can monitor data by using any of the default dashboards or by creating new ones.

You can configure a default dashboard as the default entry point for a team, unifying a team's experience, and allowing users to focus their immediate attention on the most relevant information for them. 
{: tip}

You can use alerts to notify users of problems that require attention through one or more notification channels.
* The *Alerts* section in the web UI shows the list of pre-defined alerts. From this view, you can enable and disable pre-defined alerts; you can modify existing alerts; and you can create new alerts.
* The *Settings* section in the web UI is where you configure notification channels.
 
You can request a capture on a node to analyze what happens in that node during a time frame. For example, you can use it to analyze bottlenecks, or component interactions.

## Metrics
{: #monitoring_metrics}

A metric is a quantitative measure that has one or more labels to define its characteristics. Use metrics to analyze statistically data that has numerical values. 

A metric is represented by time series. A time series is a set of numeric data points over a period. 

Metrics are classified into two groups: 

* [Default metrics](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [Custom metrics](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

Labels are classified as infrastructure labels and metric descriptor labels. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels. 

You can use labels to identify and differentiate characteristics of a metric, for example,
* You can group infrastructure objects into logical hierarchies. 
* You can filter out data. 
* You can split aggregated data into segments. 

For more information, see [Labels](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels).

## Panels
{: #monitoring_panels}

A panel displays a metric or group of metrics in a dashboard. 

You can use any of the following panel types to visualize metrics:

| Type | Description |
|------|-------------|
| `Line` | Use this panel to view trends over time for one or more metrics.  |
| `Area` | Use this panel to view trends over time for one or more metrics.  |
| `Top list` | Use this panel to compare a metric across groups of entities. The bar chart is sorted in descending order.  |
| `Histogram` | Use this panel to view the frequency distribution of a metric in buckets.  |
| `Topology` | Use this panel to visualize the infrastructure as a topology map, and the relations between entities in the map.  |
| `Number` | Use this panel to view a single number that represents the value of an aggregated metric over time for one or more entities.  |
| `Table` | Use this panel to display numerical data for your infrastructure based on metrics and segments.  |
| `Text` | Use this panel to add text. Use markdown to add your text.  |
{: caption="Table 1. Panel types" caption-side="top"} 

You can copy, change the scope, duplicate, delete, export, and explore panels.

You can export data from a panel. Consider the following information when you export data:

* You can export data to a **json file** from a line chart.
* You can export data to a **csv file** from a table chart or from a line chart.


The following table lists the tasks that you can run with panels:

| Task | Description |
|------|-------------|
| [Copy panel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | Copy a panel into a new dashboard.  |
| [Change scope](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Change the scope of a panel. |
| [Duplicate panel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | Copy a panel in the same dashboard.  |
| [Delete panel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | Delete a panel from the dashboard.  |
| [Export data](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | Export data from a panel into a csv file or a json file.  |
| [Create alert](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | Define an alert on a metric. |
{: caption="Table 2. Panel tasks" caption-side="top"} 


## Dashboards
{: #monitoring_dashboards}

A **dashboard** shows groups of metrics that report on the health, performance, and state of your infrastructure, applications, and services for a single host or a group of hosts. Dashboards offer a specialized insight into network data, application data, topology, services, hosts, and containers. Use dashboards to monitor your infrastructure, applications, and services.


In the **DASHBOARDS** section of the web UI, dashboards are organized into three main groups:

* **My Dashboards**: These dashboards are created by the user who is currently logged in.
* **My Shared Dashboards**: These dashboards are created by the user who is currently logged in, and are shared with other users.
* **Dashboards Shared With Me**: These dashboards are created by other users, and shared with the current user.

In the **EXPLORE** section of the web UI, dashboards are organized into two groups:
* **Default dashboards**: These dashboards are pre-defined dashboards.
* **My Dashboards**: These dashboards are created by the user who is currently logged in.

You can use pre-defined dashboards. You can also create custom dashboards through the web UI or programmatically. You can back up and restore dashboards by using Python scripts or the Sysdig REST API.

You can also copy and share dashboards through the web UI. 

The following table outlines tasks that you can run to work with dashboards from the UI:

| Task | Description |
|------|-------------|
| [Create dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | Create a custom dashboard in the web UI. |
| [Copy a dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | Make a copy of a dashboard in the current team where the dashboard is available, or copy a dashboard to another team. |
| [Changing the scope](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Chang the scope of a dashboard.       |
| [Delete dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  Delete a dashboard. |
| [Share a dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | Share dashboards between users in a team, and externally, by configuring a public URL for the dashboard. |
{: caption="Table 3. Dashboard tasks that you can run in the web UI" caption-side="top"} 

The following table outlines tasks that you can run programmatically to work with dashboards:

| Task                    |	Using REST API                |
|-------------------------|-------------------------------|
| Create a dashboard      | [Creating a dashboard by using the API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Delete a dashboard      | [Deleting a dashboard by using the API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Saving dashboards       | [Saving the dashboards of a team by using the API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Table 4. Tasks to manage dashboards programmatically" caption-side="top"} 



## Events
{: #monitoring_events}

An event is a notification that informs about something that occurs in any of the nodes that forward data to your {{site.data.keyword.mon_full_notm}} instance. Use events to review, track, and resolve issues. 

The following list outlines different types of events: 

* *Alert events* are events that are triggered by user-configured alerts. For more information, see [Working with alerts](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* *Infrastructure-based events* are events that are collected from Docker and Kubernetes nodes. By default, the Sysdig agent automatically discovers and collects data from a select group of events. You can edit the agent configuration file to enable more events.
* *Custom events* that you configure through any of the following integrations: Slackbot, pre-built Python scripts, custom user-created Python scripts, or cURL requests.

By default, an event has a state: 
* **Active**: This state indicates that the circumstances that triggered the event remain in place, for example, a node continues to be down.
* **OK**: This state indicates that the situation is back to normal, for example, a node is up and running.

You manage events in the *Events* section of the web UI. 
* You can view alert events through the *Alert Events* tab.
* You can view infrastructure-based events through the *Custom events* tab.
* You can view custom events through the *Custom events* tab.
* You can send custom events to any of your teams by using the [API token for that team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token). For more information, see [Custom events ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.
* You can set the event as **Resolved** to notify other users that the issue has been addressed instead of waiting for the status to be set to **OK**.
{: #tip}



## Alerts
{: #monitoring_alerts}

An alert is a notification event that you can use to warn about situations that require attention. Each alert has a severity status. This status informs you about the criticality of the information it reports on. 

When you define an alert, you must define the condition that triggers the notification, and one or more notification channels through which you want to be notified. You must also define the severity of the alert, and the type of alert. 

You can define alerts for any of the following alert types:

| Type              | Description |
|-------------------|-------------|
| Anomaly Detection | Use to monitor hosts based on their historical behaviors, and alert when they deviate. |
| Downtime          | Use to monitor any type of entity, for example, host, container, process, or service, and alert when the entity goes down. |
| Event             | Use to monitor occurrences of specific events, and alert if the total number of occurrences violates a threshold. For example, you can use it to alert on restarts and deployments of containers, orchestrations, and service events.|
| Group Outlier     | Use to monitor a group of hosts and be notified when one acts differently from the rest. |
| Metric            | Use to monitor time series metrics, and alert if they violate user-defined thresholds. |
{: caption="Table 5. Alert types" caption-side="top"} 

By default, severity is set to *warning*. You can set the severity of an alert to any of the following values: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *informational*, debug* 

You can define one or more notification channels for any of the following notification integrations:
* Email Notifications
* PagerDuty Notifications
* Slack Notifications
* VictorOps Notifications
* OpsGenie Notifications
* Configure a Webhook Channel

For more information, see [Configuring a notification channel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create).


You can enable predefined alerts, modify alerts, and create custom alerts in the web UI and by using the Sysdig API.

You manage alerts in the *Alerts* view of the web UI. You can configure the table columns that are displayed in the *Alerts* view. Valid column options are *Name*, *Scope*, *Alert When*, *Segment By*, *Notifications*, *Enabled*, *Modified*, *Captures*, *Channels*, *Created*, *Description*, *Email recipients*, *For at least*, *OpsGenie*, *PagerDuty*, *Severity*, *Slack*, *WebHook*, *SNS topics*, *Type*, and *VictorOps*.

The following list outlines the main tasks when you work with alerts:
* [Configure an alert ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [Enable or disable an alert ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [Search for an alert ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [Modify an alert ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [Copy an Alert to the same team ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [Copy an Alert to a Different Team ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [Export an alert ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [Delete an alert ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [Define alert thresholds as custom boolean expressions ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## Captures
{: #monitoring_captures}

A capture is a trace file that you can generate to analyze what happens in a node during a time frame. The capture file size limit is 100 MB. For example, you can use it to analyze bottlenecks, or component interactions. 

Captures contain system calls, and other OS events such as system-level latencies, batch jobs duration, deployments interruption times, autoscaling latencies, container startup times, or application transaction time. Captures include detailed information from every container on a node. 

Depending on your organization’s guidelines, consider disabling captures. By default, captures are enabled when you configure a Sysdig agent in a node.
{: tip}

You can create, explore, download, and delete *captures* for individual nodes. A node can be a host, a container, a virtual machine, a bare metal, or any metrics source where you install a Sysdig agent. 

* In the web UI, you create captures in the *Explore* section and manage capture files through the *Captures* section.
* You can visualize data from a capture by using *Csysdig* (the curses-based command-line UI for sysdig) or the open source Sysdig utilities to analyze the data in a capture.
* You can search data in a capture by using filters.
* You can manipulate data in a capture by using chisels (scripts). 

When you enable the capture feature for a team, capture files are only visible to members of that team.

The following list outlines the main tasks when you work with captures:
* [Creating a capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [Deleting a capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [Explore a capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [Download a capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


