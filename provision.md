---

copyright:
  years: 2018
lastupdated: "2018-11-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Provisioning an instance
{: #sysdig_provision}

Before you can monitor and manage metrics with Sysdig, you must first provision an instance of the service in {{site.data.keyword.Bluemix}}.
{:shortdesc}

To provision a Sysdig instance in a Public Cloud region, you must select the service plan that is associated with the instance, the region where your metrics are collected, and the plan that determines the number of metrics that you can monitor and their retention period.



## Provisioning a Sysdig instance from the catalog
{: #provision_ui}

To provision an instance of Sysdig from the {{site.data.keyword.Bluemix_notm}} catalog, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available on {{site.data.keyword.Bluemix_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **IBM Cloud Monitoring with Sysdig** tile. The *Observability* dashboard opens.

5. Select **Create instance**. 

6. Select a service plan. By default, the **Trial** plan is set.

    For more information about the service plans, see [Service plans](/docs/services/Monitoring-with-Sysdig/overview.html#pricing_plans).

7. Select a resource group. By default, the **Default** resource group is set.

8. Click **Create**.

After you provision an instance, 

* The *Observability* dashboard opens. 
* A service ID is automatically created. You can use this service ID to get the Sysdig access key for your instance.

Next, configure a metric source by adding a Sysdig agent. This agent is responsible for collecting and forwarding metrics to Sysdig. 



## Provisioning a Sysdig instance through the CLI
{: #provision_cli}

To provision an instance of Sysdig through the command line, complete the following steps:

1. [Pre-requisite] Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview).

   If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.Bluemix_notm}} where you want to provision the instance. Run the following command: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Set the resource group where you want to provision the instance. Run the following command: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    By default, the `default` resource group is set.

4. Create the Sysdig instance. Run the [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) command:

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    where

    * NAME is the name of the Sysdig instance
    
    * *sysdig-monitor* is the name of the IBM Cloud Monitoring with Sysdig service name in the {{site.data.keyword.Bluemix_notm}}
    
    * SERVICE_PLAN_NAME is the type of plan. Valid values are: *lite*, *graduated-tier*
    
    * LOCATION is the region where the instance is created

    For example, to provision an instance with the paid plan, run the following command:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

