---

copyright:
  years: 2018
lastupdated: "2018-12-03"

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

IBM Cloud Monitoring with Sysdig is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.Bluemix}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. IBM Cloud Monitoring with Sysdig is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}


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


## Viewing usage
{: #usage}

To monitor the usage and costs of your service, see [Viewing your usage](/docs/billing-usage/viewing_usage.html#viewingusage).


## Service plans
{: #plans}

Different pricing plans are available for an IBM Cloud Monitoring with Sysdig instance. For more information, see [Pricing](/docs/services/Monitoring-with-Sysdig/pricing.html#pricing_plans).


## Security considerations
{: #security}

**Captures**

A capture is a trace file that you can generate to analyze what happens in a host during a time frame. Captures contain system calls, and other OS events. You can enable or disable this feature per node when you configure the Sysdig agent that collects metrics from that node. By default, *Captures* are enabled when you configure a Sysdig agent. A node can be a host, a container, a virtual machine, a bare metal, or any metrics source where you install a Sysdig agent.

**IMPORTANT** When Captures are enabled, notice that Sysdig will have deep visibility into your operations. To avoid a security incident and potentially exposing data outside of your organization, check your organization's security policies before you enable captures on a node. Consider disabling the *Capture* feature for all your Sysdig agents.
{: tip}






