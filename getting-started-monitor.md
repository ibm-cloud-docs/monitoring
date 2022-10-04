---

copyright:
  years:  2018, 2022
lastupdated: "2022-08-08"

keywords: IBM Cloud, monitoring, getting started

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with {{site.data.keyword.mon_short}}
{: #getting-started-monitor}

{{site.data.keyword.mon_full_notm}} is a cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
{: shortdesc}



## Before you begin
{: #getting-started-monitor-prereqs}

You must have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://cloud.ibm.com/login){: external}.

Check the regions where the service is available. [Learn more](/docs/monitoring?topic=monitoring-endpoints#endpoints_regions).

You can complete the getting started steps in any of the supported regions.


## Step 1. Manage user access
{: #step1}

See [Manage user access](/docs/monitoring?topic=monitoring-getting-started#getting-started-step1).

## Step2. Provision an instance of the {{site.data.keyword.mon_full_notm}} service
{: #getting-started-monitor-step2}

See [Provision an instance of the IBM Cloud Monitoring with monitoring service](/docs/monitoring?topic=monitoring-provision).

## Step3. Configure a monitoring agent
{: #getting-started-monitor-step3}

After you provision an instance, you must configure a monitoring agent for each host that you want to monitor. For example, a host can be a cloud resource that you want to monitor and control its performance and health such as a Kubernetes cluster. You may also monitor hosts outside the {{site.data.keyword.cloud_notm}}. For more information, see [Configure a monitoring agent](/docs/monitoring?topic=monitoring-config_agent).

The monitoring agent automatically collects and reports on pre-defined metrics. You use the *access key* to configure the monitoring agent that is responsible for collecting and forwarding metric data to your instance. For more information, see [Working with access keys](/docs/monitoring?topic=monitoring-access_key#access_key).

Data is stored in {{site.data.keyword.cloud_notm}}.
{: important}

You can configure a monitoring agent for different environments. For example, to configure your Kubernetes cluster to send metrics to your monitoring instance, you must install a `monitoring-agent` pod on each node of your cluster. The monitoring agent collects data from the pod where it is installed, and forwards it to your monitoring instance.

Complete one of the following tutorials to learn how to deploy a monitoring agent:

|	Tutorial                        | 
|---------------------------------|
| [Monitoring a Linux VPC server instance](/docs/monitoring?topic=monitoring-ubuntu#ubuntu) |
| [Monitoring a Linux bare metal server](/docs/monitoring?topic=monitoring-baremetal_linux) | 
| [Monitoring a Windows environment](/docs/monitoring?topic=monitoring-windows) |
| [Monitoring a Kubernetes cluster](/docs/monitoring?topic=monitoring-kubernetes_cluster) | 
{: caption="Table 1. Tutorials to get started working with {{site.data.keyword.mon_full_notm}}" caption-side="top"} 

For more information, see:
- [Working with the Kubernetes agent](/docs/monitoring?topic=monitoring-agent_Kube)
- [Working with the Openshift agent](/docs/monitoring?topic=monitoring-agent_openshift)
- [Working with the Linux agent](/docs/monitoring?topic=monitoring-agent_linux)
- [Working with the Docker agent](/docs/monitoring?topic=monitoring-agent_docker)


After the monitoring agent is deployed, collection and forwarding of metrics to the instance is automatic. The monitoring agent automatically collects and reports on pre-defined metrics. You can also configure which metrics to monitor in an environment. Data for custom metrics is also automatically collected.


## Step 4. Launch the web UI
{: #getting-started-monitor-step4}

See [Launch the web UI](/docs/monitoring?topic=monitoring-launch).

## Step 5. Monitor your environment
{: #getting-started-monitor-step5}

You can analyze data in the *Explore* tab and in the *Dashboard* tab of the web UI. You monitor the data through metric views and dashboards. 

* Use a metric view to monitor an individual metric.
* Use dashboards to get a specialized insight into network data, application data, topology, services, hosts, and containers by monitoring data through panels. A panel displays a metric or group of metrics in a dashboard.
{: tip}

In the *Explore* tab, you can monitor data by using default metrics and default dashboards. You can use labels to define new infrastructure groups that you can then use to aggregate data differently and monitor your environment. [Learn more](https://docs.sysdig.com/en/docs/sysdig-monitor/explore/deprecatedexplore/){: external}.

In the *Dashboards* tab, you can monitor data by using any of the default dashboards or by creating new ones. [Learn more](https://docs.sysdig.com/en/dashboards.html){: external}.



## Step 6. Manage data
{: #getting-started-monitor-step6}

You can use labels to group infrastructure resources into logical hierarchies, filter out data, and split aggregated data into segments. Customize how data is aggregated when you configure a graph or create an alert for a metric. Set the scope of a dashboard, a panel, or an alert to filter out data points. Restrict access to data by managing users' data access through teams. 

For example, for a metric view, you can define the scope of the data, how to aggregate data, and what time and group filters to apply to the data. 

To ensure that you can securely manage your data when you use {{site.data.keyword.mon_full_notm}}, it is important to know exactly what data is stored and encrypted, and how you can delete any stored personal data. For more information, see [Managing data](/docs/monitoring?topic=monitoring-mng-data).



## Step 7. Configure alerts and explore events
{: #getting-started-monitor-step7}

You can use events to review, track, and resolve issues. An event is a notification that informs about something that has occurred in any of the nodes that forward data to your {{site.data.keyword.mon_full_notm}} instance. 

There are different types of events: 

* *Alert events* are events that are triggered by user-configured alerts. For example, configure alerts to be notified of problems that require attention. 
* *Infrastructure-based events* are events that are collected from Docker and Kubernetes nodes. By default, the monitoring agent automatically discovers and collects data from a select group of events. You can edit the agent configuration file to enable more events.
* *Custom events* that you configure through any of the following integrations: Slackbot, pre-built Python scripts, custom user-created Python scripts, or cURL requests.

When you define an alert, you must define the condition that triggers the notification, one or more notification channels through which you want to be notified, the severity of the alert, and the type of alert. The *Alerts* section in the web UI shows the list of pre-defined alerts. From this view, you can enable and disable pre-defined alerts; you can modify existing alerts; and you can create new alerts. For more information, see [Working with alerts](https://docs.sysdig.com/en/alerts.html){: external}.

You configure one or more notification channels in the *Settings* section in the web UI. Valid notification channels are: *email*, *slack*, *PagerDuty*, *Webhooks*, *OpsGenie*, and *VictorOps*. For more information, see [Working with notification channels](/docs/monitoring?topic=monitoring-notifications).

Next, explore [Working with custom events](https://docs.sysdig.com/en/events.html){: external}.


