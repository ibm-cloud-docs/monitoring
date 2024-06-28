---

copyright:
  years:  2018, 2024
lastupdated: "2024-02-01"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an instance
{: #provision}

Before you can monitor and manage metrics, you must provision an instance of the service in {{site.data.keyword.cloud_notm}}. You can optionally connect an {{site.data.keyword.sysdigsecure_full_notm}} instance to your {{site.data.keyword.mon_full_notm}} instance.
{: shortdesc}


## Provisioning an instance from the catalog
{: #provision_ui}



{{_include-segments/provision_ui.md}}

Next, configure a metric source by adding an agent. This agent is responsible for collecting and forwarding metrics to the monitoring instance.



## Provisioning an instance through the CLI
{: #provision_cli}

To provision an instance through the command line, complete the following steps:

1. [Pre-requisite] [Installion of the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli). If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where you want to provision the instance. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where you want to provision the instance. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Create the instance. Run the [ibmcloud resource service-instance-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command:

    ```text
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION  -p '{"default_receiver": false,"external_api_auth": "API_AUTH", "workload_protection_connected_instance": "WP_CRN"}'
    ```
    {: pre}

    Where

    `NAME` is the name of the instance.

    `service-name` is the name of the {{site.data.keyword.mon_full_notm}} service name in the {{site.data.keyword.cloud_notm}}.

    `SERVICE_PLAN_NAME` is the type of plan. See [Service plans](/docs/monitoring?topic=monitoring-pricing_plans) to get the plan name.

    `LOCATION` is the region where the instance is created.

    `default_receiver` is set to `false` by default. Set to `true` to collect platform metrics automatically through this instance in a region.

    `API_AUTH` is set to the authorization model that is enabled to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the REST API. Valid values are: `ANY`, and `IAM_ONLY`.

    `workload_protection_connected_instance` (optional) connects an existing {{site.data.keyword.sysdigsecure_full_notm}} instance to the {{site.data.keyword.mon_full_notm}} instance being created. For more information on connecting instances, see [Can {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.sysdigsecure_full_notm}} be used together?](/docs/monitoring?topic=monitoring-faq#faq_4)

    `WP_CRN`(required when specifying `workload_protection_connected_instance`) the CRN of the {{site.data.keyword.sysdigsecure_full_notm}} instance to be connected.

    For example, to provision an instance with the paid plan, run the following command:

    ```text
    ibmcloud resource service-instance-create monitoring-instance-01 service-name graduated-tier us-south -p '{"default_receiver": false}'
    ```
    {: pre}

    To provision an instance with the paid plan that only allows IAM tokens, run the following command:

    ```text
    ibmcloud resource service-instance-create monitoring-instance-01 service-name graduated-tier us-south -p '{"default_receiver": false,"external_api_auth": "IAM_ONLY"}'
    ```
    {: pre}

5. Create the service key that connects to the instance [ibmcloud resource service-key-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_key_create)

    ```text
    ibmcloud resource service-key-create NAME ROLE_NAME --instance-name SERVICE_INSTANCE_NAME
    ```
    {: pre}

    Where

    `NAME` is the name of your new service key

    `ROLE_NAME` is either `Administrator`, `Manager`, `Writer`, or `Reader`

    `SERVICE_INSTANCE_NAME` is the name of the instance you created

    This will gain you access to the instance's access key.
