---

copyright:
  years: 2020, 2020
lastupdated: "2020-03-09"

keywords: Sysdig, IBM Cloud, monitoring, disaster recovery

subcollection: Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.mon_full_tm}} is a highly available, regional service for monitoring your applications, platform resources and infrastructure.
{: shortdesc}


Use this page to learn more about {{site.data.keyword.mon_full_notm}}'s availability and disaster recovery strategies.

## Locations, tenancy, and availability
{: #availability}

{{site.data.keyword.mon_full_notm}} is a multi-tenant, regional service.  

You can create {{site.data.keyword.mon_full_notm}} instances in the supported [{{site.data.keyword.cloud_notm}} regions](/docs/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_regions), which represent the geographic area where your monitoring data will be processed.  Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/){: external} to meet local access, low latency, and security requirements for the region.

[Platform metrics](/docs/Monitoring-with-Sysdig?topic=Sysdig-platform_metrics_enabling) are metrics that are exposed by [Sysdig-enabled services](/docs/Monitoring-with-Sysdig?topic=Sysdig-cloud_services) and the platform in IBM Cloud. You must configure a Sysdig instance in a region to monitor your services running in that region.
{: note}

## Disaster recovery
{: #dr}

{{site.data.keyword.mon_full_notm}} follows {{site.data.keyword.cloud_notm}} requirements for [planning and recovering from disaster events](/docs/overview?topic=overview-zero-downtime#disaster-recovery).

Metric data and the monitoring metadata ( such as dashboards and alerts ) are backed up at least every 24 hours.  In the event of an un-recoverable disaster, up to 24 hours of data and changes to the monitoring instance in the failure region will be lost.

In the event of a disaster that requires rebuilding the regional site at another location, the estimated recovery time for the service is 24 hours.  Due to the large volume of data, the historical data will not be available at the time the system is restored, as this process requires additional time to recover data from the backups.  You will be able to use the service while the historical data is restored into the newly constructed region.

If you have deployed Sysdig agents on your systems and those systems are not impacted by the regional failure, you may choose to redirect metrics to another regional instance of Sysdig by provisioning a new instance and changing the access key and ingestion endpoints in the agent configuration.

If you plan to switch to another region, you should also export(backup) your alerts, notifications, dashboards and team definitions on a regular basis to make it easier to re-create your operational configuration in another region.
