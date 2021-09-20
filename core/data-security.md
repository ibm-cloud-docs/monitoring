---

copyright:
  years: 2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, overview, personal data, data deletion, PHI, data, data security, _service-name_

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Managing data
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.mon_full_notm}}, it is important to know exactly what data is stored and encrypted, and how you can delete any stored personal data.
{: shortdesc}


## How your data is collected in {{site.data.keyword.mon_full_notm}}
{: #data-collection}

When you configure a monitoring agent to collect and forward data to an {{site.data.keyword.mon_full_notm}} instance, data is automatically collected and available for analysis through the web UI. You can configure the monitoring agent to connect to the monitoring instance via the public network or the private network. 

To connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network, you can configure an agent to send metrics by using a public endpoint. The environment where the agent is running requires internet access to use the public endpoint.

You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. To configure an agent to send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account. Once the account is VRF enabled, the monitoring agent can be configured to use the private network by using the [Private Endpoint](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion) as the ingestion URL.
* Private endpoints are not accessible from the public internet. 
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network. 


monitoring agent data is collected at 10-seconds frequency. Data that is published by platform metrics is collected on a 1-minute frequency.
{: note}


### Captures
{: #capture}

In {{site.data.keyword.mon_full_notm}}, you can also enable captures when you configure a monitoring agent. A capture is a trace file that you can use to analyze what happens in a host during a time frame. 
* Captures contain system calls, and other OS events. 
* You can enable or disable this feature per node when you configure the monitoring agent that collects metrics from that node. A node can be a host, a container, a virtual machine, a bare metal, or any metrics source where you install a monitoring agent.

By default, the IBM instructions for configuring the monitoring agents disables the capture feature. If you choose to follow other instructions, IBM recommends disabling capture by setting the `sysdig_capture_enabled: false` in your dragent.yaml for Linux installations or the Kubernetes sysdig-agent Deployment custom resource.
{: note}

When Captures are enabled, to avoid a security incident and potentially exposing data outside of your organization, check your organization's security policies before you enable captures on a node. Consider disabling the *Capture* feature for all your monitoring agents.
{: important}



## How your data is stored in {{site.data.keyword.mon_full_notm}}
{: #data-storage}

{{site.data.keyword.mon_full_notm}} collects and aggregates metrics. 

### Data location
{: #data_storage_location}

Metric data is hosted on the {{site.data.keyword.cloud_notm}}.
* Each multi-zone region (MZR) location collects and aggregates metrics for each instance of the {{site.data.keyword.mon_full_notm}} that runs in that location.
* Data is colocated in the region where the {{site.data.keyword.mon_full_notm}} instance is provisioned. For example, metric data for an instance that is provisioned in US South is hosted in the US South region.


### Data retention
{: #data_storage_retention}

Data is retained for each instance based on a *roll-up* policy.

As time progresses, the data is rolled up from a fine granularity to a coarser one by the end 3 months.

The roll-up policy describes the granularity of the data over time:

* Data is retained at 10-second resolution for the first 4 hours.
* Data is retained at 1-minute resolution for 2 days.
* Data is retained at 10-minute resolution for 2 weeks.
* Data is retained at 1-hour resolution for 2 months.
* Data is retained at 1-day resolution for 15 months.



### Data availability
{: #data-storage-availability}

Data is available for a maximum of 15 months.

User metadata is always available.

After you remove a monitoring agent from a host or container, historical data is not deleted. 
* Data is available for a maximum of 15 months. 
* Data is available for analysis through the web UI for the time period that the agent was installed and reporting.

After you delete an instance of the {{site.data.keyword.mon_full_notm}} service, data is not available for search and analysis.



## Deleting your data
{: #data-delete}

### Deleting metric data
{: #service-delete-metrics}

Metric data is deleted automatically after 15 months. 

### Deleting user metadata
{: #service-delete-metadata}

User metadata, such as alerts, dashboards, teams, and users, is never deleted. 

You must open a case through support to request the metadata to be deleted. For more information, see [Open a support ticket](/docs/get-support?topic=get-support-open-case).


### Deleting a subset of data 
{: #service-delete-agent}

Deletion of a subset of data is not supported.

For example, deletion of data that is collected from 1 monitoring agent in a {{site.data.keyword.mon_short}} instance is not supported.


### Deleting captures
{: #service-delete-capture}

When you delete a capture, the data file for that capture is automatically deleted.


### Deleting an {{site.data.keyword.mon_full_notm}} instance
{: #service-delete}

When you delete an instance of {{site.data.keyword.mon_full_notm}} from the {{site.data.keyword.cloud_notm}}, you must open a case through support to request the data to be deleted. For more information, see [contacting support](/docs/monitoring?topic=monitoring-gettinghelp#gettinghelp).



