---

copyright:
  years:  2018, 2022
lastupdated: "2022-03-12"

keywords: IBM Cloud, monitoring, metrics, collection, ingestion

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# {{site.data.keyword.mon_short}} in {{site.data.keyword.cloud_notm}}
{: #about-monitor}

You can use {{site.data.keyword.mon_full}} to monitor the performance and overall system health of your organization. 
{: shortdesc}

You can collect metrics from a number of platforms, orchestrators, and a wide range of applications such as Prometheus, JMX, StatsD, Kubernetes, and other application stacks, that are available in the {{site.data.keyword.cloud_notm}}, outside the {{site.data.keyword.cloud_notm}}, or on-prem. You can also add more metrics by creating custom metrics and adding integrations.

You can monitor metrics through the {{site.data.keyword.mon_short}} web UI, or through other platforms like Grafana.


The following figure shows the components overview for the {{site.data.keyword.mon_full_notm}} service that is running on {{site.data.keyword.cloud_notm}}:

![{{site.data.keyword.mon_full_notm}} component overview on the {{site.data.keyword.cloud_notm}}](images/overview.svg "{{site.data.keyword.mon_full_notm}} component overview on the {{site.data.keyword.cloud_notm}}"){: caption="Figure 1. {{site.data.keyword.mon_full_notm}} component overview on the {{site.data.keyword.cloud_notm}}" caption-side="bottom"}


## Provisioning the {{site.data.keyword.mon_short}} service
{: #about-monitor-provision}

To start using the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you must provision an instance of the {{site.data.keyword.mon_short}} service in each region where you operate within {{site.data.keyword.cloud_notm}}.
{: note}

You provision an instance within the context of a resource group. You use a resource group to organize your services in the {{site.data.keyword.cloud_notm}} for access control and billing purposes. You can provision the {{site.data.keyword.mon_short}} instance in the *default* resource group or in a custom resource group. For more information, see [Provisioning an instance](/docs/monitoring?topic=monitoring-provision).

When you [provision an instance](/docs/monitoring?topic=monitoring-provision#provision), you automatically get an [access key](/docs/monitoring?topic=monitoring-access_key#access_key). The access key is used to authenticate the sender of metrics from a resource to a {{site.data.keyword.mon_short}} instance. 

## Configuring sources
{: #about-monitor-sources}

After you provision an instance, you must configure metric sources, enable platform metrics, or both.
- A metric source is any resource that you want to monitor and control its performance and health.

    When you configure a source, data for default metrics is automatically collected. You can also configure custom metrics and add labels to those metrics to describe their characteristics. Data for these custom metrics is also automatically collected. For more information on how to configure sources to collect default metrics and custom metrics, see [Collecting metrics](/docs/monitoring?topic=monitoring-about-collect-metrics). 

    {{site.data.keyword.mon_short}} agent data is collected at 10-seconds frequency. Data that is published by platform metrics is collected on a 1-minute frequency.
    {: note}
    
    For example, you can configure a {{site.data.keyword.mon_short}} agent to collect metrics from a Kubernetes cluster. You use the access key to configure the agent that is responsible for collecting and forwarding metric data to your instance. After the agent is deployed, collection and forwarding of metrics to the {{site.data.keyword.mon_short}} instance is automatic. The {{site.data.keyword.mon_short}} agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in an environment. 

- You can enable platform metrics to monitor {{site.data.keyword.cloud_notm}} services. You can only configure 1 {{site.data.keyword.mon_short}} instance per region to collect automatically platform metrics. [Learn more](/docs/monitoring?topic=monitoring-platform_metrics_enabling).


## Sending metrics
{: #about-monitor-send}

You can send metrics via the public or the private endpoints by using the appropriate ingestion URL. Details can be found in the [endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints) section.


## Viewing metrics
{: #about-monitor-sources}

You can monitor and manage metrics through the {{site.data.keyword.mon_short}} Web UI. For more information, see [Monitoring metrics](/docs/monitoring?topic=monitoring-monitoring).

Notice that there is a delay showing metric data for new time series. Data is not ready until the initial indexing of a new metric source is completed.  Therefore, new sources such as clusters, platform metrics, or systems that you configure, all take some time to become visible through the {{site.data.keyword.mon_short}} UI.
{: note}


## Data location
{: #about-monitor-location}

Metric data is hosted on the {{site.data.keyword.cloud_notm}}.
* Each multi-zone region (MZR) location collects and aggregates metrics for each instance of the {{site.data.keyword.mon_full_notm}} that runs in that location.
* Data is colocated in the region where the {{site.data.keyword.mon_full_notm}} instance is provisioned. For example, metric data for an instance that is provisioned in US South is hosted in the US South region.


## Data retention
{: #about-monitor-retention}

Data is retained for each instance based on a *roll-up* policy.

As time progresses, the data is rolled up from a fine granularity to a coarser one by the end 2 months.

The roll-up policy describes the granularity of the data over time:

* Data is retained at 10-second resolution for the first 4 hours.
* Data is retained at 1-minute resolution for 2 days.
* Data is retained at 10-minute resolution for 2 weeks.
* Data is retained at 1-hour resolution for 2 months.
* Data is retained at 1-day resolution for 15 months.



