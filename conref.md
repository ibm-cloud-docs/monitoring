---

copyright:
  years:  2018, 2025
lastupdated: "2025-01-29"

keywords:

subcollection: monitoring

content-type: conref

---

{{site.data.keyword.attribute-definition-list}}

# Content references for monitoring subcollection
{: #conref-monitoring}





## Before you begin
{: #en-prereqs}

Your {{site.data.keyword.mon_full_notm}} instances can send events to {{site.data.keyword.en_full_notm}} instances in the same account and in other accounts. [{{site.data.keyword.en_full_notm}} is available in a limited number of regions](/docs/event-notifications?topic=event-notifications-en-regions-endpoints).
{: important}

 For this tutorial, make sure you have an {{site.data.keyword.mon_full_notm}} instance configured and collecting logs in a region where {{site.data.keyword.en_full_notm}} is supported such as  `us-south`.

## Log in to {{site.data.keyword.cloud_notm}}
{: #en-login}
{: step}

Log in to your {{site.data.keyword.cloud_notm}} account.

1. Click [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/login){: external} to launch the {{site.data.keyword.cloud_notm}} dashboard.

2. Log in with your user ID and password. The {{site.data.keyword.cloud_notm}} Dashboard opens.

## Create an {{site.data.keyword.en_full_notm}} service instance
{: #en-create-instance}
{: step}

First, create an {{site.data.keyword.en_full_notm}} service instance by doing the following:

1. Click **Catalog**.

2. In **Search the catalog** enter *Event Notifications*.

3. In the **Create** tab enter:

    * For *Select a location* select `Dallas (us-south)`.
    * For *Select a pricing plan* select `Lite`.
    * For *Service name* enter a name of your choice.  For example: `my_event_notifications`.
    * For *Select a resource group* enter your resource group.

4. Read and agree to the license agreements.

5. Click **Create**

Your {{site.data.keyword.en_full_notm}} instance is created and is displayed.

## Configure permissions
{: #en-permissions}
{: step}

To grant an instance of the {{site.data.keyword.mon_full_notm}} service access to an instance of the {{site.data.keyword.en_full_notm}} service, you must define an authorization where the **source service** is set to {{site.data.keyword.mon_full_notm}} and **Resources based on selected attributes**; the **target service** is set to {{site.data.keyword.en_full_notm}} and **Resources based on selected attributes**; and the **service access** includes both *Reader* and *Event Source Manager* access.

1. Click **Manage** > **Access (IAM)**.
2. Click **Authorizations**.
3. Click **Create**.
4. For **Source service** select *IBM Cloud Monitoring*.
5. For **How do you want to scope the access?** select **All resources**.
6. For **Target service** select *Event Notifications*.
7. For **How do you want to scope the access?** select **All resources**.
8. For **Service access** make sure *Reader* and *Event Source Manager* are selected.
9. Click **Authorize**.

For more information on how to define authorizations, see [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth&interface=ui).

## Configure a notification source in {{site.data.keyword.en_full_notm}}
{: #en-notification}
{: step}

To create a notification source in {{site.data.keyword.en_full_notm}} you will make the configuration change in {{site.data.keyword.mon_full_notm}}.  When you create the notification channel in {{site.data.keyword.mon_full_notm}} it will be available automatically in {{site.data.keyword.en_full_notm}}.

1. Click the menu icon ![Menu icon](../../icons/icon_hamburger.svg)
2. In the navigation menu, select **Observability**.
3. Select **Monitoring**.

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select an instance in the `us-south` region. Then, click **Open dashboard**.

    The Web UI opens.

5. In the navigation click the circle icon with your initials.
6. Click **Settings**.
7. Click **Notification Channels**.
8. Click **Add Notification Channel**.
9. Select *IBM Event Notifications*.
10. For **Event Notifications Instance** select the [{{site.data.keyword.en_full_notm}} you created.](#en-create-instance)
11. For **Channel Name** give your channge a unique name.  For example, `my_event_notification_channel`.
12. For this tutorial leave all options enabled and the **Shared With** team as the default value.

    ![New IBM Event Notification Channel](../images/new_en_channel.png){: caption="New IBM Event Notification Channel" caption-side="bottom"}

13. Click **Save**.
14. Click the menu icon ![Menu icon](../../icons/icon_hamburger.svg) > **Resource list**.
15. Open **Developer tools**.
16. Open the [{{site.data.keyword.en_full_notm}} instance you created.](#en-create-instance)  For example, `my_event_notifications`.
17. Click **Sources**.

    When you configure the channel in {{site.data.keyword.mon_short}}, a source, with the same name as your {{site.data.keyword.mon_short}} instance name, is automatically added to your {{site.data.keyword.en_full_notm}} **Sources** list.

## Create an {{site.data.keyword.en_full_notm}} topic
{: #en-topic}
{: step}

Next you will define an [{{site.data.keyword.en_full_notm}} topic](/docs/event-notifications?topic=event-notifications-en-create-en-topic) that will receive the notification from {{site.data.keyword.mon_full_notm}}.

1. Click **Topics**.
2. Click **Create**.  The **Topic details** panel opens.
3. In the **Topic details** enter the following:

    * Enter the **Name** for your topic.  For example, `MyMonitoringTopic`.
    * For **Source** select the {{site.data.keyword.en_full_notm}} source, which is named the same as your {{site.data.keyword.mon_full_notm}} instance.
    * Select an **Event Type**. For this tutorial select *Alert*.
    * Select an **Event subtype**. For this tutorial select *Metric*.
    * Select a **Severity**.  For this tutorial select *Info Severity*.

    ![Topic details](../images/topic_details.png){: caption="Topic details" caption-side="bottom"}

4. Click **Add a condition**.

    If you do not click **Add a condition** before you click **Create**, the topic will be created with no conditions associated with it.
    {: note}

5. Click **Create**.  Your topic will be displayed in the **Topics** list.

    ![Topics list](../images/topics_list.png){: caption="Topics list" caption-side="bottom"}

## Create an {{site.data.keyword.mon_full_notm}} alert notification
{: #en-mon-notification}
{: step}

Now, create an [{{site.data.keyword.mon_full_notm}} alert](/docs/monitoring?topic=monitoring-alerts) that will trigger the {{site.data.keyword.en_full_notm}} notification.

1. Click the menu icon ![Menu icon](../../icons/icon_hamburger.svg).
2. In the navigation menu, select **Observability**.
3. Select **Monitoring**.

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select the [{{site.data.keyword.mon_full_notm}} instance that you configured to send notifications to {{site.data.keyword.en_full_notm}}.](#en-notification). Click **Open Dashboard**.
5. Click **Alerts**.
6. Click **Add Alert**.
7. Create an alert that meets the criteria of the [{{site.data.keyword.en_full_notm}} topic that you created.](#en-topic)

   1. Click **Metric**.
   2. For the new alert specify the following:

       * For **Name** specify `MyEventNotificationAlert`.
       * For **Severity** specify `Info`.
       * Define a metric for you system that you know will trigger an alert.
       * Enable the `myEventNotificationChannel` for the alert.

   3. Click **Create**.
