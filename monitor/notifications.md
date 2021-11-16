---

copyright:
  years:  2018, 2021
lastupdated: "2021-11-15"

keywords: IBM Cloud, monitoring, notification channel

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Working with notification channels
{: #notifications}

Configure notification channels to be notified when an alert is triggered. You manage notification channels through the *Settings* panel in the web UI.
{: shortdesc}
 

## Configuring a notification channel
{: #notifications_create}

Complete the following steps to add a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/monitoring?topic=monitoring-launch#launch). 
    
2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Select **Notification Channels**.

4. Click **Add Notification Channel**.

5. Configure a notification channel:

    1. Select the type of notification, for example, `Webhook`.

    2. Enter the name of the channel.

    3. Enable the *Notify when Resolved* condition to receive a notification when the alert is manually resolved by a user.

    4. Enable the *Notify when Acknowledged* field to receive a notification when the alert is manually acknowledged by the user.

    5. Configure the notification according to the selected notification type:

        * For an **Email** notification channel, add the list of recipients, separated by commas.

        * For a **Slack** notification channel, add the URL of the *Slack channel*.
    
        * For **{{site.data.keyword.openwhisk_short}}** notification channel, specify the channel URL when you set up a IBM Cloud Function Channel. For more information, see [Configure IBM Cloud Function Channel](https://docs.sysdig.com/en/configure-ibm-cloud-functions-channel.html){: external}.

        * For a **Webhook** notification channel, add the *Webhook URL*. **Note:** When an alert is triggered, the notification is sent as a POST in JSON format to your webhook endpoint. For more information, see [Configuring a Webhook channel](https://docs.sysdig.com/en/configure-a-webhook-channel.html){: external}. For example, {{site.data.keyword.mon_full_notm}}can be integrated with ServiceNow using a custom webhook. To learn about configuring {{site.data.keyword.mon_full_notm}} with ServiceNow, see [Configure ServiceNow](https://docs.sysdig.com/en/configure-servicenow.html){: external}.

        * For a **VictorOps** notification channel, add the *API Key* and the *Routing Key*.

        * For an **OpsGenie** notification channel, add the *OpsGenie API key*. Notice that you must configure in OpsGenie the integration with {{site.data.keyword.mon_full_notm}}. For more information, see [Add {{site.data.keyword.mon_full_notm}} Integration in Opsgenie](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){: external}.

        * For an **Amazon SNS Topic** notification channel, add the *SNS Topic*.
        
        * For a **Microsoft Teams** notification channel, add the *Microsoft Teams* URL.

        * For a **PagerDuty** notification channel, first you must authorize {{site.data.keyword.mon_full_notm}} to integrate with your account. When you select PagerDuty, a wizard to configure the integration with {{site.data.keyword.mon_full_notm}} opens. Click either **Authorize Integration** or **Sign In Using Your Identity Provider** to authorize PagerDuty. Choose an existing service or set up a new service for {{site.data.keyword.mon_full_notm}} notifications, then click **Finish Integration**. Select the escalation policy to use for {{site.data.keyword.mon_full_notm}}  incidents. Then, on the *Notifications* tab, confirm your PagerDuty account, your service name, and the service key. For more information, see [Add {{site.data.keyword.mon_full_notm}} Integration in PagerDuty](https://www.pagerduty.com/docs/guides/sysdig-integration-guide/).

            To retrieve the required permissions automatically by clicking **Auto-fetch**, first you must authorize {{site.data.keyword.mon_full_notm}} to integrate with your account. When you select PagerDuty, a wizard to configure the integration with {{site.data.keyword.mon_full_notm}} opens. Click either **Sign in** or **Sign In Using Your Identity Provider** to authorize PagerDuty. Choose an existing service or set up a new service for {{site.data.keyword.mon_full_notm}} notifications, then click **Finish Integration**. Select the escalation policy to use for {{site.data.keyword.mon_full_notm}} incidents. Then, on the *Notifications* tab, confirm your PagerDuty *Account*, *Service Key*, and *Service Name*. 

        * For a **Teams Email** notification channel, select the name of the team to receive notifications. 

        * For an **IBM Event Notifications** channel you must first have an [{{site.data.keyword.en_full_notm}} instance configured.](/docs/event-notifications?topic=event-notifications-en-create-en-instance) 

            To configure the notification channel you need to specify the {{site.data.keyword.en_full_notm}} instance name and specify your choice of a channel name.  You will also indicate if the notification channel is enabled and when notifications should be sent, for example, when an alert is resolved. Notifications can be shared with one or all teams.

            [{{site.data.keyword.en_full_notm}} is available in a limited number of regions](/docs/event-notifications?topic=event-notifications-en-regions-endpoints). Your {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.en_full_notm}} instances must be in the same region to communicate with one another.  Because of this, support for integration with {{site.data.keyword.en_full_notm}} is limited to the regions where {{site.data.keyword.en_full_notm}} is supported and where {{site.data.keyword.mon_full_notm}} is also installed.
            {: important}


    6. Optionally, and for integrations that allow a test, enable the *Test notification* condition to receive a test notification. If you do not receive a test notification in 10 minutes, review your channel configuration. 

6. Click **Save**.



## Modifying a notification channel
{: #notifications_update}

Complete the following steps to modify a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/monitoring?topic=monitoring-launch#launch). 
    
2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Select **Notification Channels**.

4. Click the channel you want to edit.

5. After you make changes, click **Save**.



## Testing a notification channel
{: #notifications_test}

Complete the following steps to test a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/monitoring?topic=monitoring-launch#launch). 
    
2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Select **Notification Channels**.

4. Click the channel you want to edit.

5. Enable the **Test notification** option.

6. After you make changes, click **Save**.



## Disabling a notification channel
{: #notifications_disable}

Complete the following steps to temporarily disable a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/monitoring?topic=monitoring-launch#launch). 
    
2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Select **Notification Channels**.

4. For the channel you want to disable, toggle **Enabled** for the channel so it is disabled.  Alerts are temporarily disabled and notifications muted.

## Deleting a notification channel
{: #notifications_delete}

Complete the following steps to delete a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/monitoring?topic=monitoring-launch#launch). 
    
2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Select **Notification Channels**.

4. Identify the target channel that you want to modify and the **Actions** icon ![Actions icon](../../icons/action-menu-icon.svg "Actions").

5. Click **Delete Channel**.

6. Confirm the deletion of the channel by clicking **Yes, delete**.




