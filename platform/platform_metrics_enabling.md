---

copyright:
  years:  2018, 2022
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, platform metrics

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

 
# Enabling platform metrics
{: #platform_metrics_enabling}

 You can configure 1 instance only of the {{site.data.keyword.mon_full_notm}} service per region to collect *platform metrics* in that location. 
{: shortdesc}

- Platform metrics are metrics that are exposed by enabled-monitoring services and the platform in {{site.data.keyword.cloud_notm}}.
- To monitor platform metrics for a service instance, provision the {{site.data.keyword.mon_full_notm}} instance in the same region where the {{site.data.keyword.cloud_notm}} service instance that you want to monitor is provisioned. 

In a region, before you configure a monitoring instance to collect platform metrics, check with the account or service administrator if another monitoring instance has already been configured. You may not have permissions to see all monitoring instances in the region.
{: important}

## Enabling a monitoring instance through the UI
{: #platform_metrics_enabling_ui}

To enable platform metrics in a region, complete the following steps:

### Step 1. Provision a monitoring instance
{: #platform_metrics_enabling_step1}

[Provision an instance of {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-provision) in the region where the service that you wish to monitor is running.  

For example, if you are monitoring an {{site.data.keyword.messagehub}} instance in the London region, then you must create a monitoring instance in London.

### Step 2. Set on the platform metrics flag 
{: #platform_metrics_enabling_step2}

1. From the{{site.data.keyword.cloud_notm}} dashboard, go to the menu icon ![menu icon](../../../icons/icon_hamburger.svg) &gt; **Observability** to access the *Observability* dashboard.

2. Select **Monitoring** &gt; **Options** &gt; **Edit platform**. 

3. Select a [region](/docs/monitoring?topic=monitoring-endpoints#endpoints_regions). 

4. Choose the monitoring instance that will collect metrics from enabled services on that location. 

5. Click **Select**. 

The main *Observability* page opens.

<!-- The instance that you choose to receive metrics shows the flag **Platform metrics**. -->


## Enabling a monitoring instance from the command line
{: #platform_metrics_enabling_cli}

To enable platform metrics in a region, the instance that you want to configure to receive platform metrics must have set on the **default_receiver** property.
{: note}

Complete the following steps:

1. [Pre-requisite] [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where the monitoring instance is running. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where the monitoring instance is running. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Get the instance name. Run the following command: [ibmcloud resource service-instances](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instances)

    ```text
    ibmcloud resource service-instances
    ```
    {: pre}

5. Get the plan ID of the instance. 

    Run the following command. Look for the entry for the monitoring instance. Then, copy the value of the field `resource_plan_id`. This value is needed to update the instance.

    ```text
    ibmcloud resource service-instances --long --output JSON
    ```
    {: pre}

6. Set on the **default_receiver** property. Run the following command:

    ```text
    ibmcloud resource service-instance-update InstanceName --service-plan-id PlanID -p '{"default_receiver": true}'
    ```
    {: codeblock}

    Where `PlanID` is the resource plan ID of your monitoring instance.
    
