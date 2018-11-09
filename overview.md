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


# About
{: #about}

IBM Cloud Monitoring with Sysdig is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.Bluemix}} architecture. Use it to get visibility into the performance and health of your applications, services, and platform. IBM Cloud Monitoring with Sysdig is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}

IBM Cloud Monitoring with Sysdig offers administrators, DevOps teams, and developers advanced monitoring features to monitor and troubleshoot, including alerting and customizable dashboards. 

For more information about Sysdig, see [Sysdig Monitor ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdig.com/products/monitor/){: new_window}.


## Overview
{: #ov}

To add monitoring features with Sysdig in the {{site.data.keyword.Bluemix_notm}}, you must provision an instance of the IBM Cloud Monitoring with Sysdig service.

Before you provision an instance, consider the following information:

* You must accept the terms and conditions that specify that your data is sent to a third party.
* The account owner can create, view, and delete an instance of a service in the {{site.data.keyword.Bluemix_notm}}, and can grant permissions to other users to work with the IBM Cloud Monitoring with Sysdig service.
* Other {{site.data.keyword.Bluemix_notm}} users with `administrator` or `editor` permissions can manage the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix_notm}}. These users must also have platform permissions to create resources within the context of the resource group where they plan to provision the instance.

You provision an instance within the context of a resource group. A resource group lets you organize your services for access control and billing purposes. You can provision the IBM Cloud Monitoring with Sysdig instance in the *default* resource group or in a custom resource group.

When you provision an instance, you automatically get an ingestion key, also known as a *Sysdig access key*.

After you provision an instance, you must configure a Sysdig agent for each metric source. A metric source is a cloud resource that you want to monitor and control its performance and health. You must configure a Sysdig agent in each environment that you want to monitor. For example, a metric source can be a Kubernetes cluster. You use the ingestion key to configure the Sysdig agent that is responsible for collecting and forwarding metric data to your instance.

After the Sysdig agent is deployed in a metric source, collection and forwarding of metrics to the instance is automatic. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in a environment.

You can view, monitor, and manage the data through the IBM Cloud Monitoring with Sysdig Web UI.  

The following figure shows the components overview for the IBM Cloud Monitoring with Sysdig service that is running on {{site.data.keyword.Bluemix_notm}}:

![Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}](images/components.png "Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}")



## Sysdig agents
{: #sysdig_agent}

The Sysdig agent automatically collects and reports on pre-defined metrics. 

The following list outlines Sysdig agents that are available:

* Sysdig agent for Kubernetes, GKE, and OpenShift.
* Sysdig agent for Docker containers or for non-containerized services.
* Sysdig agent for Mesos, Marathon, and DCOS.
* Sysdig agent for manual Linux installations.

## Dashboards
{: #dashboards}

After you provision an instance of the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.

You can monitor the health, performance, and state of your infrastructure, applications and services through the Web UI or programmatically. You can monitor a single host or a group of hosts. You can view data for a single metric or you can use dashboards to view data across groups of related metrics into a single view.

A **dashboard** shows groups of metrics that report on the health, performance, and state of your infrastructure, applications, and services for a single host or a group of hosts. Dashboards offer a specialized insight into network data, application data, topology, services, hosts, and containers.

In the **DASHBOARDS** section of the Web UI, dashboards are organized into three main groups:

* **My Dashboards**: These are the dashboards that are created by the user who is currently logged in.
* **My Shared Dashboards**: These are the dashboards that are created by the user who is currently logged in, and that are shared with other users.
* **Dashboards Shared With Me**: These are the dashboards that are created by other users, and shared with the current user.

In the **EXPLORE** section of the Web UI, dashboards are organized into two groups:
* **Default dashboards**: These are the pre-defined dashboards.
* **My Dashboards**: These are the dashboards that are created by the user who is currently logged in.


A default dashboard can be configured by setting the default entry point for a team, unifying a team's Sysdig Monitor experience, and allowing users to focus their immediate attention on the most relevant information for them. For more information on configuring a default entry point, refer to the Configure an Entry Page or Dashboard for a Team section of the Sysdig Platform documentation.



## Metrics data
{: #data}

IBM Cloud Monitoring with Sysdig collects and aggregates metrics. 

* Metric data is hosted on the {{site.data.keyword.Bluemix_notm}}.
* Each multi-zone region (MZR) location collects and aggregates metrics for each instance of the IBM Cloud Monitoring with Sysdig that runs in that location.
* Data is colocated in the region where the IBM Cloud Monitoring with Sysdig instance is provisioned. For example, metric data for an instance provisioned in US South is hosted in the US South region.

The service plan that you choose for a Sysdig instance defines the frequency at which data is collected, the maximum number of custom metrics that is collected, and the number of days that data is stored and retained in Sysdig.

there is only one paid plan and it automatically adjusts the rate that you pay for an instance based upon the container density and the number of custom metrics

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







