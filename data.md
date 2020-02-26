---

copyright:
  years:  2018, 2020
lastupdated: "2020-02-12"

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


# Data
{: #data}

Learn how monitoring data is collected, managed, and deleted within the {{site.data.keyword.mon_full}}.
{:shortdesc}


## Data collection
{: #overview_collection}

When you configure a Sysdig agent to collect and forward data to an {{site.data.keyword.mon_full_notm}} instance, data is automatically collected and available for analysis through the web UI. 

You can configure the Sysdig agent to connect to the monitoring instance via the public network and the private network. 
{: note}

By default, you connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network. To configure an agent to send metrics by using a public endpoint, the environment where the agent is running requires internet access to use the public endpoint.

You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. To configure an agent to send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account. Once the account is VRF and service endpoint enabled, the Sysdig agent can be configured to use the private network by using the [Private Endpoint](/docs/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion) as the ingestion URL.
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

* Data is retained at 10-second resolution for the first 4 hours.
* Data is retained at 1-minute resolution for 2 days.
* Data is retained at 10-minute resolution for 2 weeks.
* Data is retained at 1-hour resolution for 3 months.
* Data is retained at 1-day resolution for one year.

## Data deletion
{: #overview_data_deletion}

When you delete an instance of {{site.data.keyword.mon_full_notm}} from the {{site.data.keyword.cloud_notm}}, you must open a case through support to request the data to be  deleted. For more information, see [contacting support](/docs/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp).

When you delete a capture, the data file for that capture is automatically deleted.

Deletion of data that is collected from one single Sysdig agent in a {{site.data.keyword.mon_short}} instance is not supported.
{: note}



## Data location
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}} collects and aggregates metrics. 

* Metric data is hosted on the {{site.data.keyword.cloud_notm}}.
* Each multi-zone region (MZR) location collects and aggregates metrics for each instance of the {{site.data.keyword.mon_full_notm}} that runs in that location.
* Data is colocated in the region where the {{site.data.keyword.mon_full_notm}} instance is provisioned. For example, metric data for an instance that is provisioned in US South is hosted in the US South region.



## Captures
{: #capture}


A capture is a trace file that you can generate to analyze what happens in a host during a time frame. Captures contain system calls, and other OS events. You can enable or disable this feature per node when you configure the Sysdig agent that collects metrics from that node. By default, *Captures* are enabled when you configure a Sysdig agent. A node can be a host, a container, a virtual machine, a bare metal, or any metrics source where you install a Sysdig agent.

When Captures are enabled, notice that Sysdig will have deep visibility into your operations. To avoid a security incident and potentially exposing data outside of your organization, check your organization's security policies before you enable captures on a node. Consider disabling the *Capture* feature for all your Sysdig agents.
{: important}

