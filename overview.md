---

copyright:
  years: 2018
lastupdated: "2018-09-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# About Sysdig
{: #about_sysdig}

SysDig Monitor is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.Bluemix}} architecture. Use it to get visibility into the performance and health of your applications, services, and platform. Sysdig is operated in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}

SysDig offers administrators, DevOps teams, and developers advanced features to monitor and troubleshoot, define alerts, and design custom views.

For more information about Sysdig, see [Sysdig Monitor ![External link icon](../icons/launch-glyph.svg "External link icon")](https://sysdig.com/products/monitor/){: new_window}.


## Overview
{: #ov}

To add monitoring features with Sysdig in the {{site.data.keyword.Bluemix_notm}}, you must provision an instance of Sysdig.

Before you provision an instance of Sysdig, consider the following information:

* You must accept the terms and conditions that specify that your data is sent to a third party.
* The account owner can create, view, and delete an instance of a service in the {{site.data.keyword.Bluemix_notm}}, and can grant permissions to other users to work with Sysdig Monitor.
* Other {{site.data.keyword.Bluemix_notm}} users with `administrator` or `editor` permissions can manage Sysdig Monitor in the {{site.data.keyword.Bluemix_notm}}. These users must have platform permissions to create resources within the context of the resource group where you plan to provision the Sysdig instance.

You provision a Sysdig instance within the context of a resource group. A resource group lets you organize your services for access control and billing purposes. You can provision the Sysdig instance in the *default* resource group or in a custom resource group.

After you provision an instance of Sysdig, an account in created in Sysdig, and you can get the ingestion key for your account.

Then, you must configure a Sysdig agent for each metric source. A metric source is a cloud resource that you want to monitor and control its performance and health. You must configure a Sysdig agent in each environment that you want to monitor. For example, a metric source can be a Kubernetes cluster. You use the ingestion key to configure the Sysdig agent that is responsible for collecting and forwarding metric data to your Sysdig instance.

After the Sysdig agent is deployed in a metric source, collection and forwarding of metrics to the Sysdig instance is automatic. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in a environment.

You can view, monitor, and manage the data through the Sysdig Web UI.  

The following figure shows the components overview for the Sysdig service that is running on {{site.data.keyword.Bluemix_notm}}:

![Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}](images/components.png "Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}")


## Metrics data
{: #data}

Sysdig collects and aggregates metrics in one centralized system.

* Metric data is hosted on the {{site.data.keyword.Bluemix_notm}}.
* Data is colocated in the region where the Sysdig instance is provisioned. For example, metric data for an instance provisioned in US South is hosted in the US South region.

The service plan that you choose for a Sysdig instance defines the frequency at which data is collected, the maximum number of custom metrics that is collected, and the number of days that data is stored and retained in Sysdig.

When you delete an instance of Sysdig from the {{site.data.keyword.Bluemix_notm}}, all the data is deleted.



## Features
{: #features}

**Accelerate the diagnosis and resolution of performance incidents.**

By using SysDig, Developers and DevOps teams monitor and troubleshoot performance issues in real-time, identify the source of errors, and eliminate problems. SysDig offers deep visibility into your system, applications and services, service-oriented views for each one, and pre-defined metrics that you can use to determine potential threats or problems.

**Get critical insight from dynamic service–level monitoring and automatic correlation of data.**
 
Sysdig collects metrics from multiple sources into a centralize location. Per source (host), you can deploy an agent that dynamically discovers the different resources in your environment and collects their pre-defined and custom metrics. Customize dashboards to visualize your environment.

**Mitigate the impact of abnormal situations with proactive notifications.**

Define alerts to reduce the impact on your day to day operations and accelerate your reaction and response time to anomalies, downtime, and performance degradation. 

**Control costs by customizing what cloud sources to manage through SysDig.**

Control the cost of your monitoring infrastructure in the IBM Cloud by configuring the metric sources for which you want to monitor their performance. 


## Pricing plans
{: #pricing_plans}

Different pricing plans are available for a Sysdig instance. 

| Plan             | Description  |
|------------------|--------------|
| `Lite`           | Data is collected for up to 20 containers, and for a maximum of 200 custom metrics per node every 10secs. </br>The plan is free for 21 days only. </br>Lite plan services are deleted after 30 days of inactivity. |
| `Graduated tier` (*) | There are different tiers: </br>`Basic`: Data is collected for up to 20 containers, and for a maximum of 200 custom metrics per node every 10secs. This plan is suitable for one core compute. </br>`Pro`: Data is collected for up to 50 containers or 500 custom metrics per node every 10 secs. This plan is suitable for 8-16 core computes. </br>`Advanced`: Data is collected for 50+ containers or up to 1000 custom metrics per node every 10 secs. This plan is suitable for more than 16 core computes. |
{: caption="Table 1. List of service plans" caption-side="top"} 


(*) **Note:** Based on your usage of average number of containers or number of custom metrics emitted by each node every 10 seconds, {{site.data.keyword.IBM_notm} will auto-compute the tier in which the mode fits. Ay any point in time, you could have some nodes in one tier and some in another. Alerts will be provided to inform you when you are switching from one tier to another based on your consumption.

`????? where are the alerts provided   ?????????`
`??????  how long is data kept in a graduated tier ?????????`

**Note: ** For very high container density or metric volumes contact sales.  `??????????(Add link)  or should they open a support ticket????`


## Regions
{: #regions}

Monitoring with Sysdig is available in the **US South** region only.



## Support
{: #support}

For {{site.data.keyword.Bluemix_notm}} provisioning, billing, or account issues, submit a ticket through the IBM Cloud Support Center. For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](/docs/get-support/howtogetsupport.html#getting-customer-support).

For Sysdig issues, ......
