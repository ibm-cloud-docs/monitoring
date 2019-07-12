---

copyright:
  years:  2018, 2019
lastupdated: "2019-07-12"

keywords: Sysdig, IBM Cloud, monitoring, overview

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


# {{site.data.keyword.mon_full_notm}}
{: #about}

{{site.data.keyword.mon_full}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}


To add monitoring features with {{site.data.keyword.mon_full_notm}} in the {{site.data.keyword.cloud_notm}}, you must provision an instance of the {{site.data.keyword.mon_full_notm}} service.

Before you provision an instance, consider the following information:

* Your data is sent to a third party.
* The account owner can create, view, and delete an instance of a service in the {{site.data.keyword.cloud_notm}}. This user can also grant permissions to other users to work with the {{site.data.keyword.mon_full_notm}} service.
* Other {{site.data.keyword.cloud_notm}} users with `administrator` or `editor` permissions can manage the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}. These users must also have platform permissions to create resources within the context of the resource group where they plan to provision the instance.

You provision an instance within the context of a resource group. You use a resource group to organize your services for access control and billing purposes. You can provision the {{site.data.keyword.mon_full_notm}} instance in the *default* resource group or in a custom resource group.

When you [provision an instance](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision), you automatically get an ingestion key, known as the [Sysdig access key](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key).

After you provision an instance, you must configure an {{site.data.keyword.mon_full_notm}} agent for each metric source. A metric source is a cloud resource that you want to monitor and control its performance and health. You must configure an {{site.data.keyword.mon_full_notm}} agent in each environment that you want to monitor. For example, a metric source can be a Kubernetes cluster. You use the access key to configure the Sysdig agent that is responsible for collecting and forwarding metric data to your instance.

The agent can be configured to push metrics to Sysdig via the public or private endpoints by using the appropriate ingestion URL. Details can found in the [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints) section.

After the {{site.data.keyword.mon_full_notm}} agent is deployed in a metric source, collection and forwarding of metrics to the instance is automatic. The {{site.data.keyword.mon_full_notm}} agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in an environment.

You can [monitor](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring), and [manage](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)  data through the {{site.data.keyword.mon_full_notm}} Web UI.  

The following figure shows the components overview for the {{site.data.keyword.mon_full_notm}} service that is running on {{site.data.keyword.cloud_notm}}:

![{{site.data.keyword.mon_full_notm}} component overview on the {{site.data.keyword.cloud_notm}}](images/components.png "{{site.data.keyword.mon_full_notm}} component overview on the {{site.data.keyword.cloud_notm}}")



## Data collection
{: #overview_collection}

When you configure a Sysdig agent to collect and forward data to an {{site.data.keyword.mon_full_notm}} instance, data is automatically collected and available for analysis through the web UI. 

You can configure the Sysdig agent to connect to the monitoring instance via the public network and the private network. 
{: note}

By default, you connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network. To configure an agent to send metrics by using a public endpoint, the environment where the agent is running requires internet access to use the public endpoint.

You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. To configure an agent to send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account. Once the account is VRF and service endpoint enabled, the Sysdig agent can be configured to use the private network by using the [Private Endpoint](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion) as the ingestion URL.
* Private endpoints are not accessible from the public internet. 
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network. 


Data is collected at 10-seconds frequency. 
{: note}



## Data availability
{: #overview_availability}

Data is available for a maximum of 15 months.

After you remove a Sysdig agent from a host or container, historical data is not deleted. Data is available for analysis through the web UI for the time period that the agent was installed and reporting.

After you delete an instance of the {{site.data.keyword.mon_full_notm}} service, data is not available for search and analysis.



## Data retention
{: #overview_retention}

Data is retained for each instance based on a *roll-up* policy.

As time progresses, the data is rolled up from a fine granularity to a coarser one by the end 3 months.

The roll-up policy describes the granularity of the data over time:

* Data is retained at 10-second resolution for the first 6 hours.
* Data is retained at 1-minute resolution for 2 days.
* Data is retained at 10-minute resolution for 2 weeks.
* Data is retained at 1-hour resolution for 3 months.
* Data is retained at 1-day resolution for one year.

## Data deletion
{: #overview_data_deletion}

When you delete an instance of {{site.data.keyword.mon_full_notm}} from the {{site.data.keyword.cloud_notm}}, you must open a case through support to request the data to be  deleted. For more information, see [contacting support](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp).

When you delete a capture, the data file for that capture is automatically deleted.

Deletion of data that is collected from one single Sysdig agent in a {{site.data.keyword.mon_short}} instance is not supported.
{: note}



## Data location
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}} collects and aggregates metrics. 

* Metric data is hosted on the {{site.data.keyword.cloud_notm}}.
* Each multi-zone region (MZR) location collects and aggregates metrics for each instance of the {{site.data.keyword.mon_full_notm}} that runs in that location.
* Data is colocated in the region where the {{site.data.keyword.mon_full_notm}} instance is provisioned. For example, metric data for an instance that is provisioned in US South is hosted in the US South region.



## {{site.data.keyword.mon_full_notm}} agents
{: #overview_sysdig_agent}

The {{site.data.keyword.mon_full_notm}} agent automatically collects and reports on pre-defined metrics. 

The following list outlines {{site.data.keyword.mon_full_notm}} agents that are available:

* {{site.data.keyword.mon_full_notm}} agent for Kubernetes, GKE, and OpenShift.
* {{site.data.keyword.mon_full_notm}} agent for Docker containers or for non-containerized services.
* {{site.data.keyword.mon_full_notm}} agent for Mesos, Marathon, and DCOS.
* {{site.data.keyword.mon_full_notm}} agent for manual Linux installations.

For more information, see [Configuring a Sysdig agent](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) and [Removing a Sysdig agent](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove).


## Viewing usage
{: #overview_usage}

To monitor the usage and costs of your service, see [Viewing your usage](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).


## Service plans
{: #overview_plans}

Different pricing plans are available for an {{site.data.keyword.mon_full_notm}} instance. [Learn more](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).


## Security considerations
{: #overview_security}

**Captures**

A capture is a trace file that you can generate to analyze what happens in a host during a time frame. Captures contain system calls, and other OS events. You can enable or disable this feature per node when you configure the Sysdig agent that collects metrics from that node. By default, *Captures* are enabled when you configure a Sysdig agent. A node can be a host, a container, a virtual machine, a bare metal, or any metrics source where you install a Sysdig agent.

When Captures are enabled, notice that Sysdig will have deep visibility into your operations. To avoid a security incident and potentially exposing data outside of your organization, check your organization's security policies before you enable captures on a node. Consider disabling the *Capture* feature for all your Sysdig agents.
{: important}

