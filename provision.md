---

copyright:
  years:  2018, 2020
lastupdated: "2020-02-12"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

subcollection: Monitoring-with-Sysdig

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

# Provisioning an instance
{: #provision}

Before you can monitor and manage metrics with Sysdig, you must provision an instance of the service in {{site.data.keyword.cloud_notm}}.
{:shortdesc}


## Provisioning a Sysdig instance from the catalog
{: #provision_ui}

To provision an instance of Sysdig from the {{site.data.keyword.cloud_notm}} catalog, complete the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}.

2. Click **Catalog**. The list of the services that are available on {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile. The *Observability* dashboard opens.

5. Select **Create instance**. 

6. Select the region. 

7. Select a service plan. By default, the **Trial** plan is set.

    For more information about the service plans, see [Service plans](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-pricing_plans#pricing_plans).

8. Enter a service name.

9. Select a resource group. By default, the **Default** resource group is set.

10. Set on automatic collection of platform metrics by clicking **Enable**.

11. Click **Create**.

After you provision an instance, 

* The *Observability* dashboard opens. 
* A service ID is automatically created. You can use this service ID to get the Sysdig access key for your instance. The name of the service ID has the following format: `{InstanceName}-key-admin`.

Next, configure a metric source by adding a Sysdig agent. This agent is responsible for collecting and forwarding metrics to Sysdig. 



## Provisioning a Sysdig instance through the CLI
{: #provision_cli}

To provision an instance of Sysdig through the command line, complete the following steps:

1. [Pre-requisite] [Installion of the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started). If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where you want to provision the instance. Run the following command: [`ibmcloud login`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where you want to provision the instance. Run the following command: [`ibmcloud target`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Create the Sysdig instance. Run the [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command:

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION  -p '{"default_receiver": false}'
    ```
    {: codeblock}

    Where

    * `NAME` is the name of the Sysdig instance.
    
    * `sysdig-monitor` is the name of the {{site.data.keyword.mon_full_notm}} service name in the {{site.data.keyword.cloud_notm}}.
    
    * `SERVICE_PLAN_NAME` is the type of plan. Valid values are *lite*, and *graduated-tier*.
    
    * `LOCATION` is the region where the instance is created.

    * `default_receiver` is set to `false` by default. Set to `true` to collect platform metrics automatically through this instance in a region.

    For example, to provision an instance with the paid plan, run the following command:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south -p '{"default_receiver": false}'
    ```
    {: pre}

5. Create the service key that connects to the instance [`ibmcloud resource service-key-create`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_resource#ibmcloud_resource_service_key_create)

    ```
    ibmcloud resource service-key-create NAME ROLE_NAME --instance-name SERVICE_INSTANCE_NAME
    ```
    {: codeblock}

    Where

    * `NAME` is the name of your new service key

    * `ROLE_NAME` is either `Administrator`, `Manager`, `Writer`, or `Reader`

    * `SERVICE_INSTANCE_NAME` is the name of the instance you created

    This will gain you access to the instance's Sysdig access key.


