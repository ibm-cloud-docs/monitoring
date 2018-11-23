---

copyright:
  years: 2018
lastupdated: "2018-11-21"

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


## Overview
{: #ov}

To add monitoring features with IBM Cloud Monitoring with Sysdig in the {{site.data.keyword.Bluemix_notm}}, you must provision an instance of the IBM Cloud Monitoring with Sysdig service.

Before you provision an instance, consider the following information:

* Your data is sent to a third party.
* The account owner can create, view, and delete an instance of a service in the {{site.data.keyword.Bluemix_notm}}, and can grant permissions to other users to work with the IBM Cloud Monitoring with Sysdig service.
* Other {{site.data.keyword.Bluemix_notm}} users with `administrator` or `editor` permissions can manage the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix_notm}}. These users must also have platform permissions to create resources within the context of the resource group where they plan to provision the instance.

You provision an instance within the context of a resource group. A resource group lets you organize your services for access control and billing purposes. You can provision the IBM Cloud Monitoring with Sysdig instance in the *default* resource group or in a custom resource group.

When you [provision an instance](/docs/services/Monitoring-with-Sysdig/provision.html#provision), you automatically get an ingestion key,known as the [*Sysdig access key*](/docs/services/Monitoring-with-Sysdig/access_key.html#access_key).

After you provision an instance, you must configure a IBM Cloud Monitoring with Sysdig agent for each metric source. A metric source is a cloud resource that you want to monitor and control its performance and health. You must configure a IBM Cloud Monitoring with Sysdig agent in each environment that you want to monitor. For example, a metric source can be a Kubernetes cluster. You use the access key to configure the Sysdig agent that is responsible for collecting and forwarding metric data to your instance.

After the IBM Cloud Monitoring with Sysdig agent is deployed in a metric source, collection and forwarding of metrics to the instance is automatic. The IBM Cloud Monitoring with Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in an environment.

You can [monitor](/docs/services/Monitoring-with-Sysdig/monitoring.html#monitoring), and [manage](/docs/services/Monitoring-with-Sysdig/manage.html#manage)  data through the IBM Cloud Monitoring with Sysdig Web UI.  

The following figure shows the components overview for the IBM Cloud Monitoring with Sysdig service that is running on {{site.data.keyword.Bluemix_notm}}:

![IBM Cloud Monitoring with Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}](images/components.png "IBM Cloud Monitoring with Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}")



## Data collection
{: #collection}

When you configure a Sysdig agent to collect and forward data to an IBM Cloud Monitoring with Sysdig instance, data is automatically collected and available for analysis through the web UI.

Data is collected at 10 seconds frequency. 

## Data availability
{: #availability}

Data is available for a maximum of 15 months.

After you remove a Sysdig agent from a host or container, historical data is not deleted. Data is available for analysis through the web UI for the time period that the agent was installed and reporting.

After you delete an instance of the IBM Cloud Monitoring with Sysdig service, data is not available for search and analysis.



## Data retention
{: #retention}

Data is retained for each instance based on a *roll-up* policy.

As time progresses, the data is rolled up from a fine granularity to a coarser one by the end 3 months.

The roll-up policy describes the granularity of the data over time:

* Data is retained at 10 second resolution for the first 6 hours.
* Data is retained at 1 minute resolution for 2 days.
* Data is retained at 10 minute resolution for 2 weeks.
* Data is retained at 1 hour resolution for 3 months.
* Data is retained at 1 day resolution for one year.

## Data deletion
{: #data_deletion}

When you delete an instance of IBM Cloud Monitoring with Sysdig from the {{site.data.keyword.Bluemix_notm}}, all the data is deleted.


## Data location
{: #data_location}

IBM Cloud Monitoring with Sysdig collects and aggregates metrics. 

* Metric data is hosted on the {{site.data.keyword.Bluemix_notm}}.
* Each multi-zone region (MZR) location collects and aggregates metrics for each instance of the IBM Cloud Monitoring with Sysdig that runs in that location.
* Data is colocated in the region where the IBM Cloud Monitoring with Sysdig instance is provisioned. For example, metric data for an instance provisioned in US South is hosted in the US South region.



## IBM Cloud Monitoring with Sysdig agents
{: #sysdig_agent}

The IBM Cloud Monitoring with Sysdig agent automatically collects and reports on pre-defined metrics. 

The following list outlines IBM Cloud Monitoring with Sysdig agents that are available:

* IBM Cloud Monitoring with Sysdig agent for Kubernetes, GKE, and OpenShift.
* IBM Cloud Monitoring with Sysdig agent for Docker containers or for non-containerized services.
* IBM Cloud Monitoring with Sysdig agent for Mesos, Marathon, and DCOS.
* IBM Cloud Monitoring with Sysdig agent for manual Linux installations.

For more information, see [Configuring a Sysdig agent](/docs/services/Monitoring-with-Sysdig/config_agent.html#config_agent) and [Removing a Sysdig agent](/docs/services/Monitoring-with-Sysdig/remove_agent.html#remove_agent).


## Features
{: #features}

**Accelerate the diagnosis and resolution of performance incidents.**

By using IBM Cloud Monitoring with Sysdig, Developers and DevOps teams monitor and troubleshoot performance issues in real-time, identify the source of errors, and eliminate problems. IBM Cloud Monitoring with Sysdig offers deep visibility into your system, applications and services, service-oriented views for each one, and pre-defined metrics that you can use to determine potential threats or problems.

**Get critical insight from dynamic service–level monitoring and automatic correlation of data.**
 
IBM Cloud Monitoring with Sysdig collects metrics from multiple sources into a centralize location. Per source (host), you can deploy an agent that dynamically discovers the different resources in your environment and collects their pre-defined and custom metrics. Customize dashboards to visualize your environment.

**Mitigate the impact of abnormal situations with proactive notifications.**

Define alerts to reduce the impact on your day to day operations and accelerate your reaction and response time to anomalies, downtime, and performance degradation. 

**Control costs by customizing what cloud sources to manage through IBM Cloud Monitoring with Sysdig.**

Control the cost of your monitoring infrastructure in the {{site.data.keyword.Bluemix_notm}} by configuring the metric sources for which you want to monitor their performance. 



## Monitor usage
{: #usage}

To monitor the usage and costs of your service, see [Viewing your usage](/docs/billing-usage/viewing_usage.html#viewingusage).


## Service plans
{: #plans}

Different pricing plans are available for an IBM Cloud Monitoring with Sysdig instance. For more information, see [Pricing](/docs/services/Monitoring-with-Sysdig/pricing.html#pricing_plans).



