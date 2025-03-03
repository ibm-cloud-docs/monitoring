---

copyright:
  years:  2018, 2025
lastupdated: "2025-03-03"


keywords: IBM Cloud, monitoring, upgrade

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Changing the service plan of an instance
{: #upgrade}

When you provision an instance of the {{site.data.keyword.mon_full_notm}} service, you must choose a service plan. Different plans offer different features. You can change the service plan at any time.
{: shortdesc}

You can only upgrade from the `Lite` plan to the `Graduated Tier`. You cannot downgrade from the `Graduated Tier` plan to the `Lite` plan.
{: restriction}

[Learn more about service plans](/docs/monitoring?topic=monitoring-pricing_plans).

## Changing the service plan through the Observability dashboard
{: #upgrade_ui}

To change the service plan of an instance from the Observability dashboard in the {{site.data.keyword.cloud_notm}}, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Go to the menu icon ![Menu icon](../../icons/icon_hamburger.svg) and select **Observability** to access the *Observability* dashboard.

3. Select **Monitoring**.

4. Click the *Actions* icon ![Three dots icon](images/actions.png) next to the instance you want to change and click **Edit plan**.

5. Select a service plan.

6. Click **Save**.






## Changing the service plan through the CLI
{: #upgrade_cli}

Complete the following steps to change the service plan:

1. [Pre-requisite] Installation of the {{site.data.keyword.cloud_notm}} CLI. [Learn more](/docs/cli?topic=cli-getting-started).

2. Log in to the location in the {{site.data.keyword.cloud_notm}} where the instance is provisioned. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

    To get the latest list of locations that are available for the {{site.data.keyword.mon_full_notm}} service, see [Locations](/docs/monitoring?topic=monitoring-regions).

3. Set the resource group where the instance is available. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. [Optional] Get the current service plan ID.

    To get the current service plan of an instance, you can run the following command and check the value of the **resource_plan_id** field:

    ```text
    ibmcloud resource service-instance INSTANCE_NAME --output JSON
    ```
    {: codeblock}

5. Change the service plan. Run the [ibmcloud resource service-instance-update](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command:

    ```text
    ibmcloud resource service-instance-update NAME --service-plan-id RESOURCE_PLAN_ID
    ```
    {: codeblock}

    Where

    * `NAME` is the name of the instance

    * `service-plan-id` indicates the type of plan.

    * `RESOURCE_PLAN_ID` is the ID of the plan that you want to set. To get the service plan IDs, see [Service plans](/docs/monitoring?topic=monitoring-pricing_plans).


For example, to change the service plan of an instance to the graduated plan, run the following command:

```text
ibmcloud resource service-instance-update monitoring-instance-01 231bb072-1b2f-4d7e-ae9e-9574d382be32
```
{: codeblock}
