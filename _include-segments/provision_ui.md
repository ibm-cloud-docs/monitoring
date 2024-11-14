Provision an {{site.data.keyword.mon_full_notm}} instance from the {{site.data.keyword.cloud_notm}} catalog by completing the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.

2. Click **Catalog**. The list of the services that are available on {{site.data.keyword.cloud_notm}} opens.

3. Filter the list of services by selecting the **Logging and Monitoring** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile.

5. Select **Create**.

6. Select the location where the {{site.data.keyword.mon_full_notm}} is to be created.

7. Select a service plan. By default, the **Lite** plan is set.

    To provision an instance with the full monitoring funnctionality, select the **Graduated Tier** plan.

    For more information about the service plans, see [Service plans](/docs/monitoring?topic=monitoring-pricing_plans#pricing_plans).

8. In **Configure resource details** enter a name for your instance.

9. Select a resource group. By default, the **Default** resource group is set.

10. Optionally specify any desired [tags](/docs/account?topic=account-tag&interface=ui) or [access management tags](/docs/account?topic=account-access-tags-tutorial).

11. You can have one {{site.data.keyword.mon_full_notm}} instance in a region configured to receive [platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling). To configure the instance to receive platform metric, set the **Enable platform metrics** switch to on.

12. (Optional) Connect an {{site.data.keyword.sysdigsecure_full_notm}} instance to your {{site.data.keyword.mon_full_notm}} instance.

    An {{site.data.keyword.sysdigsecure_full_notm}} instance can be linked to your {{site.data.keyword.mon_full_notm}} instance so that a single agent can collect both metrics and security data both provisioned services.

    To link an {{site.data.keyword.sysdigsecure_full_notm}} instance to your {{site.data.keyword.mon_full_notm}} instance:

    1. Set the **Connect a Workload Protection instance** switch to on.

    2. If you have an existing {{site.data.keyword.sysdigsecure_full_notm}} instance you can connect to the existing instance or create a new instance.

       * To create a new instance:

          1. Select **Connect new instance**.

          2. To change any of the default details for the new {{site.data.keyword.sysdigsecure_full_notm}} instance, click **Edit**, make any required changes and click **Save** to save your changes.

       * To use an existing instance, select **Connect existing instance**.

          1. Select **Connect existing instance**.

          2. Select the instance to be connected from the list.

13. Confirm that you have read and agreed to the license agreements.

14. Click **Create**.

After you provision an instance:

* The details for the {{site.data.keyword.mon_full_notm}} instance are displayed along with whether or not an {{site.data.keyword.sysdigsecure_full_notm}} instance is connected.
* A service ID is automatically created. You can use this service ID to get the access key for your instance. The name of the service ID has the following format: `{InstanceName}-key-Administrator`.
