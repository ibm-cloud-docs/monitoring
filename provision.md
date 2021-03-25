---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-24"

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
{:external: target="_blank" .external}

# Provisioning an instance
{: #provision}

Before you can monitor and manage metrics, you must provision an instance of the service in {{site.data.keyword.cloud_notm}}.
{:shortdesc}


## Provisioning an instance from the catalog
{: #provision_ui}

To provision an instance from the {{site.data.keyword.cloud_notm}} catalog, complete the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.

2. Click **Catalog**. The list of the services that are available on {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Logging and Monitoring** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile. The *Observability* dashboard opens.

5. Select **Create instance**. 

6. Select the region. 

7. Select a service plan. By default, the **Lite** plan is set.

    To provision an instance that only includes the *Monitor* component, select the plan **Graduated Tier**.

    To provision an instance that include the *Monitor* and the *Secure* components, select the plan **Graduated Tier - Sysdig Secure + Monitor**.

    For more information about the service plans, see [Service plans](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-pricing_plans#pricing_plans).

8. Enter a service name.

9. Select a resource group. By default, the **Default** resource group is set.

10. Set on automatic collection of platform metrics by clicking **Enable**.

11. Click **Create**.

After you provision an instance, 

* The *Observability* dashboard opens. 
* A service ID is automatically created. You can use this service ID to get the access key for your instance. The name of the service ID has the following format: `{InstanceName}-key-admin`.

Next, configure a metric source by adding an agent. This agent is responsible for collecting and forwarding metrics to the monitoring instance. 



## Provisioning an instance through the CLI
{: #provision_cli}

To provision an instance through the command line, complete the following steps:

1. [Pre-requisite] [Installion of the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli). If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where you want to provision the instance. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where you want to provision the instance. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Create the instance. Run the [ibmcloud resource service-instance-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command:

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION  -p '{"default_receiver": false,"external_api_auth": "API_AUTH"}'
    ```
    {: pre}

    Where

    `NAME` is the name of the instance.
    
    `sysdig-monitor` is the name of the {{site.data.keyword.mon_full_notm}} service name in the {{site.data.keyword.cloud_notm}}.
    
    `SERVICE_PLAN_NAME` is the type of plan. See [Service plans](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-pricing_plans) to get the plan name.
    
    `LOCATION` is the region where the instance is created.

    `default_receiver` is set to `false` by default. Set to `true` to collect platform metrics automatically through this instance in a region.

    `API_AUTH` is set to the authorization model that is enabled to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the REST API. Valid values are: `ANY`, and `IAM_ONLY`.

    For example, to provision an instance with the paid plan, run the following command:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south -p '{"default_receiver": false}'
    ```
    {: pre}

    To provision an instance with the paid plan that only allows IAM tokens, run the following command:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south -p '{"default_receiver": false,"external_api_auth": "IAM_ONLY"}'
    ```
    {: pre}

5. Create the service key that connects to the instance [ibmcloud resource service-key-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_key_create)

    ```
    ibmcloud resource service-key-create NAME ROLE_NAME --instance-name SERVICE_INSTANCE_NAME
    ```
    {: pre}

    Where

    `NAME` is the name of your new service key

    `ROLE_NAME` is either `Administrator`, `Manager`, `Writer`, or `Reader`

    `SERVICE_INSTANCE_NAME` is the name of the instance you created

    This will gain you access to the instance's access key.


