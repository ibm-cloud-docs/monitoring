---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-11"

keywords: IBM Cloud, monitoring, alerts

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Configuring an alert by using the alert editor
{: #alert-config}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify about problems that might require attention. When an alert is triggered, you can be notified through 1 or more notification channels. An alert definition can generate multi-channel notifications.
{: shortdesc}

An alert is a notification event that you can use to warn about situations that require attention. Each alert has a severity status. This status informs you about the criticality of the information it reports on. [Learn more](/docs/monitoring?topic=monitoring-alerts).

Complete the following steps to configure an alert:

## Step 1.  Select the alert type
{: #alert-config-step1}

From the *Alert* section of the UI, select **+ New Alert**. Then, choose the alert type:

* [Metric](/docs/monitoring?topic=monitoring-alert-metric)
* [Change](/docs/monitoring?topic=monitoring-alert-change)
* [Downtime](/docs/monitoring?topic=monitoring-alert-downtime)
* [Event](/docs/monitoring?topic=monitoring-alert-event)
* [PromQL](/docs/monitoring?topic=monitoring-alert-promql)


## Step 2. Name the alert
{: #alert-config-step2}

Click the untitled alert name and enter a name for the alert.


## Step 3. Define the alert condition
{: #alert-config-step3}

In the **Condition** section, specify the conditions when the alert will be sent.

For **Metric** alerts
:   A metric alert is sent when a metric exceeds a configured threshold. You can specify the metric and scope for the alert as well as a threshold and duration. You can optionally specify a warning threshold when the threshold is being approached.

    You can optionally translate your alert specification from a form to PromQL.

    For more information about Metric alerts, see [Metric alerts](/docs/monitoring?topic=monitoring-alert-metric).

For **Change** alerts
:   Change alerts are sent when changes are detected to a metric over a period of time. You can specify the metric and scope for the alert as well as the period of time to monitor the change and an alert threshold percentage. You can optionally specify a warning threshold when the threshold is being approached.

    For more information about Change alerts, see [Change alerts](/docs/monitoring?topic=monitoring-alert-change).

For **Downtime** alerts
:   A downtime alert is sent when a scoped metric is determined to be down for a percentage of time during a configured monitoring time. For example, a downtime of 100% of the time over 5 minutes.

    For more information about Downtime alerts, see [Downtime alerts](/docs/monitoring?topic=monitoring-alert-downtime).

For **Event** alerts
:   An event alert is sent when a scoped metric has occurred the configured number of times during a configured monitoring time. For example, 50 times in the last hour.

    For more information about Event alerts, see [Event alerts](/docs/monitoring?topic=monitoring-alert-event).

For **PromQL** alerts
:    A PromQL alert is sent when the defined PromQL query is met during a configured duration of time. 

     A PromQL query can be configured to optionally resolve automatically after being sent after a configured period of time.

    For more information about PromQL alerts, see [PromQL alerts](/docs/monitoring?topic=monitoring-alert-promql).

## Step 4. Configure the notification
{: #alert-config-step4}

One or more notification channels can be configured for each alert.  To configure a notification channel:

1. Open the **Notifications** section.
2. Click **+ Add Channel**.
3. Select a **Notification Channel**.

   The **Notification Channel** list will only [list channels that have been configured](/docs/monitoring?topic=monitoring-notifications).
4. Toggle **Get notified every** under **When Unresolved** to specify that the alert is to be sent when the condition is reached. Specify how often the alert is to be sent until the issue is resolved. For example, every 10 minutes.
5. Notification Channels that receive alert notifications can also receive resolution notifications when the alert condition is no longer met. Toggle **Get Notified** under **When Resolved** to forward resolution notifications so that incidents can be automatically closed in incident management channels.

This setting allows an alert to override the notification channel’s default notification settings. If an override is not configured, the alert will inherit the default settings from the notification channel.


## Step 5. Configure the alert settings
{: #alert-config-step5}

Specify settings associated with the alert.

1. Open the **Settings** section.
2. For **Alert Severity** select a priority: `High`, `Medium`, `Low` or `Info`.
3. For **Alert Name** specify a meaningful name that can uniquely represent the alert you are creating. For example, Production Cluster Failed Scheduling pods. This replaces any name configured in [step 2](#alert-config-step2).
4. For **Description** optionally add any additional information about the alert.
5. For **Group** you can optionally group alerts by assigning them to a specific group name. Alerts that have no group name will be added to the *Default* group.
6. For **Orphaned Alerts** specify whether or not to automatically deactivate orphaned alert occurrences. Deactiving alerts eliminates noise caused by outdated alerts triggering for entities that are no longer reporting data. If orphaned alerts are to be deactivated, specify the period of time after which they are to be deactivated.
7. For **Link to Dashboard** optionally select a dashboard that you want to include in the alert notification.
8. For **Link to Runbook** optionally specify the URL of a runbook to be included in the alert notification.

## Step 6. Configure captures (Metric and Downtime alerts only)
{: #alert-config-step6}

For Metric and Downtime alerts you can optionally configure captures. For more information on captures, see [Managing captures](/docs/monitoring?topic=monitoring-captures).

