---

copyright:
  years:  2018, 2020
lastupdated: "2020-01-29"

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
{: #platform_metrics_enabling}

Platform metrics are metrics that are exposed by enabled-Sysdig services and the platform in {{site.data.keyword.cloud_notm}}. You must configure a Sysdig instance in a region to monitor these metrics.
{:shortdesc}

* Platform metrics are regional. 

    You can monitor metrics from Sysdig-enabled services the {{site.data.keyword.cloud_notm}} in the region where the service is available. 

* You can configure 1 instance only of the {{site.data.keyword.mon_full_notm}} service per region to collect *platform metrics* in that location. 

    To configure a Sysdig instance, you must set on the *platform metrics* configuration setting. 

* If a Sysdig instance in a region is already enabled to collect platform metrics, metrics from enabled-Sysdig services are collected automatically and available for monitoring through this instance. For more information about enabled-Sysdig services, see [Cloud services]().


To monitor platform metrics for a service instance, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where the service instance that you want to monitor is provisioned.
{: important}

## Enabling a Sysdig instance through the UI
{: #platform_metrics_enabling_ui}

To enable platform metrics in a region, complete the following steps:

### Step 1. Provision a Sysdig instance
{: #platform_metrics_enabling_step1}

[Provision an instance of Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision) in the region where the service that you wish to monitor is running.  

For example, if you are monitoring an {{site.data.keyword.messagehub}} instance in the London region, then you must create a Sysdig instance in London.

### Step 2. Set on the platform metrics flag 
{: #platform_metrics_enabling_step2}

1. From the{{site.data.keyword.cloud_notm}} dashboard, go to the menu icon ![menu icon](../../icons/icon_hamburger.svg) &gt; **Observability** to access the *Observability* dashboard.

2. Select **Monitoring** &gt; **Configure platform metrics**. 

3. Select a [region](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_regions). 

4. Choose which Sysdig instance will collect metrics from enabled services on that location. 

5. Click **Save**. 

The main *Observability* page opens.

The instance that you choose to receive metrics shows the flag **Platform metrics**.


## Enabling a Sysdig instance from the command line
{: #platform_metrics_enabling_cli}

To enable platform metrics in a region, the instance that you want to configure to receive platform metrics must have set on the **default_receiver** property.
{: note}

Complete the following steps:

1. [Pre-requisite] [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started).

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where the Sysdig instance is running. Run the following command: [`ibmcloud login`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where the Sysdig instance is running. Run the following command: [`ibmcloud target`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Get the instance name. Run the following command: [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_resource#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Set on the **default_receiver** property. Run the following command:

    ```
    ibmcloud resource service-instance-update InstanceName -p '{"default_receiver": true}'
    ```
    {: codeblock}

    Where `InstanceName` is the name of your Sysdig instance.


