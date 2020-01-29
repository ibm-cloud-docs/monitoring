---

copyright:
  years:  2020, 2020
lastupdated: "2020-01-28"

keywords: Sysdig, IBM Cloud, monitoring, platform metrics

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

 
# Enabling Platform Metrics
{: #enabling-platform-metrics}

Platform metrics are the metrics exposed by IBM services and the {{site.data.keyword.cloud_notm}} platform.  In order to use platform metrics, an instance of {{site.data.keyword.mon_full_notm}} must be created and enabled to support platform metrics.
{:shortdesc}

1. [Provision an instance of Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision) in the region where the service you wish to monitor is running.  For example, if you are monitoring an Event Streams instance in the London region, then you must create a Sysdig instance in London.

2. [Configure the Sysdig instance to support Platform metrics](#configure-platform-metrics)


## Configure a Sysdig instance to support Platform metrics
{: configure-platform-metrics}

Once you have an instance of Sysdig created, you can configure one instance per region to receive platform metrics.

1. From the [Observability Monitoring](https://cloud.ibm.com/observe/monitoring) page, select **Configure platform metrics**

2. Choose the region to configure and select an instance in that region to receive the platform metrics.

3. Click **Save**

4. The instance will now display the Platform metrics identifier under the Sources column in the instance table.

