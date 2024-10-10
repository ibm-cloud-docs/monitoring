---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"


keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Navigating to the web UI
{: #launch}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, and configure a monitoring agent for a metrics source, you can view, monitor, and manage metrics through the {{site.data.keyword.mon_full_notm}} web UI.
{: shortdesc}


## Grant IAM policies to a user to view data
{: #launch_step1}

**Note:** You must be an administrator of the {{site.data.keyword.mon_short}} service, an administrator of the {{site.data.keyword.mon_short}} instance, or have account IAM permissions to grant other users policies.

The following table lists the minimum policies that a user must have to be able to launch the {{site.data.keyword.mon_full_notm}} web UI, and view data:

| Service                        | Role                      | Permission granted     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | Platform role: Viewer     | Allows the user to view the list of service instances in the Observability Monitoring dashboard. |
| `{{site.data.keyword.mon_full_notm}}` | Service role: Writer      | Allows the user to launch the Web UI and view metrics in the Web UI.  |
{: caption="IAM policies" caption-side="top"}

For more information on how to configure these policies for a user, see [Granting permissions to launch the monitoring UI or to make REST API calls](/docs/monitoring?topic=monitoring-iam_grant).


## Launch the {{site.data.keyword.mon_short}} UI
{: #launch_step2}

You launch the {{site.data.keyword.mon_short}} UI within the context of an {{site.data.keyword.mon_full_notm}} instance, from the {{site.data.keyword.cloud_notm}} UI.

Complete the following steps to launch the web UI:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

    Click [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/login){: external} to launch the {{site.data.keyword.cloud_notm}} dashboard.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**.

3. Select **Monitoring**.

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select one instance. Then, click **Open dashboard**.

    The {{site.data.keyword.mon_short}} UI opens.


## Launch the {{site.data.keyword.sysdigsecure_short}} UI
{: #launch_step3}

The {{site.data.keyword.sysdigsecure_short}} UI is only available for {{site.data.keyword.mon_short}} instances using the [*Graduated Tier - Sysdig Secure + Monitor* service plan](/docs/monitoring?topic=monitoring-service_plans).
{: note}

{{site.data.content.combined-plan-deprecated}}

To access the *{{site.data.keyword.sysdigsecure_short}}* UI, complete the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

    Click [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/login){: external} to launch the {{site.data.keyword.cloud_notm}} dashboard.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**.

3. Select **Monitoring**.

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select an instance with the *Graduated Tier - Sysdig Secure + Monitor* service plan. Then, click **Open dashboard**.

    The {{site.data.keyword.mon_short}} UI opens by default.

5. Click the **Monitor** icon.

    ![Monitor icon](images/monitor.png){: caption="Monitor icon" caption-side="bottom"}

    The *Switch Products* selection box opens.

    ![Switch products](images/platform.png){: caption="Switch products" caption-side="bottom"}

6. Select **Workload Protection** to launch the {{site.data.keyword.sysdigsecure_short}} UI.

For more information on using {{site.data.keyword.sysdigsecure_short}}, see the [{{site.data.keyword.sysdigsecure_full_notm}} documentation.](/docs/workload-protection)
