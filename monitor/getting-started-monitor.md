---

copyright:
  years:  2018, 2020
lastupdated: "2020-10-14"

keywords: Sysdig, IBM Cloud, monitoring, getting started

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


# Getting started tutorial
{: #getting-started-monitor}

{{site.data.keyword.mon_full_notm}} is a cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}



## Before you begin
{: #getting-started-monitor_prereqs}

You must have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://cloud.ibm.com/login){: external}.

Check the regions where the service is available. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_regions).

You can complete the getting started steps in any of the supported regions.


## Step 1. Manage user access
{: #step1}

See [Manage user access](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started#getting-started-step1).

## Step2. Provision an instance of the {{site.data.keyword.mon_full_notm}} service
{: #getting-started-monitor_step2}

See [Provision an instance of the IBM Cloud Monitoring with Sysdig service](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-provision).

## Step3. Configure a Sysdig agent
{: #getting-started-monitor_step3}

See [Configure a Sysdig agent](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-config_agent).

## Step 4. Launch the web UI
{: #getting-started-monitor_step4}

See [Launch the web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch).

## Step 5. Monitor your environment
{: #getting-started-monitor_step5}

You can analyze data in the *Explore* tab and in the *Dashboard* tab of the web UI. You monitor the data through metric views and dashboards. 

* Use a metric view to monitor an individual metric.
* Use dashboards to get a specialized insight into network data, application data, topology, services, hosts, and containers by monitoring data through panels. A panel displays a metric or group of metrics in a dashboard.
{: tip}

In the *Explore* tab, you can monitor data by using default metrics and default dashboards. You can use labels to define new infrastructure groups that you can then use to aggregate data differently and monitor your environment. [Learn more](https://docs.sysdig.com/en/explore-interface.html){: external}.

In the *Dashboards* tab, you can monitor data by using any of the default dashboards or by creating new ones. [Learn more](https://docs.sysdig.com/en/dashboards.html){: external}.



## Step 6. Manage data
{: #getting-started-monitor_step6}

You can use labels to group infrastructure resources into logical hierarchies, filter out data, and split aggregated data into segments. Customize how data is aggregated when you configure a graph or create an alert for a metric. Set the scope of a dashboard, a panel, or an alert to filter out data points. Restrict access to data by managing users' data access through teams. 

For example, for a metric view, you can define the scope of the data, how to aggregate data, and what time and group filters to apply to the data. 

For more information, see [Managing data](https://docs.sysdig.com/en/metrics.html){: external}.



## Step 7. Configure alerts and explore events
{: #getting-started-monitor_step7}

You can use events to review, track, and resolve issues. An event is a notification that informs about something that has occurred in any of the nodes that forward data to your {{site.data.keyword.mon_full_notm}} instance. 

There are different types of events: 

* *Alert events* are events that are triggered by user-configured alerts. For example, configure alerts to be notified of problems that require attention. 
* *Infrastructure-based events* are events that are collected from Docker and Kubernetes nodes. By default, the Sysdig agent automatically discovers and collects data from a select group of events. You can edit the agent configuration file to enable more events.
* *Custom events* that you configure through any of the following integrations: Slackbot, pre-built Python scripts, custom user-created Python scripts, or cURL requests.

When you define an alert, you must define the condition that triggers the notification, one or more notification channels through which you want to be notified, the severity of the alert, and the type of alert. The *Alerts* section in the web UI shows the list of pre-defined alerts. From this view, you can enable and disable pre-defined alerts; you can modify existing alerts; and you can create new alerts. For more information, see [Working with alerts](https://docs.sysdig.com/en/alerts.html){: external}.

You configure one or more notification channels in the *Settings* section in the web UI. Valid notification channels are: *email*, *slack*, *PagerDuty*, *Webhooks*, *OpsGenie*, and *VictorOps*. For more information, see [Working with notification channels](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-notifications).

Next, explore [Working with custom events](https://docs.sysdig.com/en/events.html){: external}.


