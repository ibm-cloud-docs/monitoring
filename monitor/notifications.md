---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# Working with notification channels
{: #notifications}

Configure notification channels to be notified when an alert is triggered. You manage notification channels through the *Settings* panel in the web UI.
{:shortdesc}
 

## Configuring a notification channel
{: #notifications_create}

Complete the following steps to add a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, choose **Settings**.

3. Select **Notification Channels**.

4. Click **MY CHANNELS** ![add icon](../images/add.png). Then, select a channel.

    **Note:** The first time you configure a notification channel, click on any of the channels.

5. Configure a notification channel:

    * Enter the name of the channel.

    * Enable the *Notify when OK* field to receive a notification when the alert condition is no longer triggered.

    * Enable the *Notify when Resolved* condition to receive a notification when the alert is manually resolved by a user.

    * For an **email** notification channel, add the list of recipients, separated by comma.

    * For a **slack** notification channel, add the name of the *Slack channel*.
    
    * For **{{site.data.keyword.openwhisk_short}}** notification channel, specify the channel URL when you set up a IBM Cloud Function Channel. For more information, see [Configure IBM Cloud Function Channel ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.sysdig.com/en/configure-ibm-cloud-functions-channel.html).

    * For a **Webhook** notification channel, add the *Webhook URL*. **Note:** When an alert is triggered, the notification is sent as a POST in JSON format to your webhook endpoint. For more information, see [Configuring a Webhook channel ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.sysdig.com/en/configure-a-webhook-channel.html){:new_window}. For example, {{site.data.keyword.mon_full_notm}}can be integrated with ServiceNow using a custom webhook. To learn about configuring {{site.data.keyword.mon_full_notm}}with ServiceNow, see [Configure ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.sysdig.com/en/configure-servicenow.html){:new_window}.

    * For a **VictorOps** notification channel, add the *API key* and the *Routing key*.

    * For an **OpsGenie** notification channel, add the *OpsGenie API key*. Notice that you must configure in OpsGenie the integration with Sysdig. For more information, see [Add {{site.data.keyword.mon_full_notm}}Cloud Integration in Opsgenie ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}.

    * For a **PagerDuty** notification channel, first you must authorize {{site.data.keyword.mon_full_notm}}to integrate with your account. When you select PagerDuty, a wizard to configure the integration with {{site.data.keyword.mon_full_notm}}opens. Click either **Authorize Integration** or **Sign In Using Your Identity Provider** to authorize PagerDuty. Choose an existing service or set up a new service for {{site.data.keyword.mon_full_notm}}notifications, then click **Finish Integration**. Select the escalation policy to use for {{site.data.keyword.mon_full_notm}}incidents. Then, on the *Notifications* tab, confirm your PagerDuty account, your service name, and the service key. 

    * Optionally, and for integrations that allow a test, enable the *Test notification* condition to receive a test notification. If you do not receive a test notification in 10 minutes, review your channel configuration. 

6. Click **CREATE CHANNEL**. 



## Modifying a notification channel
{: #notifications_update}

Complete the following steps to modify a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, choose **Settings**.

3. Select **Notification Channels**.

4. Identify the target channel that you want to modify and click **EDIT**.

5. After you make changes, click **SAVE CHANGES**.



## Testing a notification channel
{: #notifications_test}

Complete the following steps to test a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, choose **Settings**.

3. Select **Notification Channels**.

4. Identify the target channel that you want to modify and click **TEST**.



## Disabling a notification channel
{: #notifications_disable}

Complete the following steps to temporarily disable a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, choose **Settings**.

3. Select **Notification Channels**.

4. In the *Notifications* section, enable *Downtime* to disable alerts temporarily and mute all notifications.

## Deleting a notification channel
{: #notifications_delete}

Complete the following steps to delete a notification channel:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, choose **Settings**.

3. Select **Notification Channels**.

4. Identify the target channel that you want to modify and click **EDIT**.

5. Click **DELETE CHANNEL**.

6. Confirm the deletion of the channel. Click **SAVE CHANGES**.




