---

copyright:
  years:  2018, 2024
lastupdated: "2024-06-28"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Configuring an alert by using the legacy alert editor
{: #alert-config-legacy}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify about problems that may require attention. When an alert is triggered, you can be notified through 1 or more notification channels. An alert definition can generate multi-channel notifications.
{: shortdesc}

The legacy alert editor is deprecated. See [Configuring an alert](/docs/monitoring?topic=monitoring-alert-config) for information about the current alert editor.
{: deprecated}

An alert is a notification event that you can use to warn about situations that require attention. Each alert has a severity status. This status informs you about the criticality of the information it reports on. [Learn more](/docs/monitoring?topic=monitoring-alerts).

Complete the following steps to configure an alert:

## Step 1.  Select the alert type
{: #alert-config-legacy-step1}

From the *Alert* section of the UI, select **Add Alert**. Then, choose the alert type.


## Step 2. Name the alert
{: #alert-config-legacy-step2}

Enter a name for the alert.

You can also add a description for the alert and the name of an alert group if you want to group you alerts.  If an alert group is not specified, the alert will be created in the default group.


## Step 3. Define the severity
{: #alert-config-legacy-step3}

Add a severity level. Valid severity values are `info`, `low`, `medium`, and `high`.


## Step 4. Define the metric section
{: #alert-config-legacy-step4}

1. Select a metric (entity) that you want to monitor.
2. Define the alert condition. Choose any of the following options:

    Option 1: Choose a metric and a single condition such as `average`, `sum`, `minimum` or `maximum`.

    Option 2: Choose **Create multi-condition alerts**. Enter the condition, for example, `min(min(cpu.used.percent)) < = 50 OR max(max(cpu.used.percent)) >= 80`.

    ![Multi-condition alert](images/multi-condition-alerts.png "Multi-condition alert"){: caption="Multi-condition alert" caption-side="bottom"}

## Step 5. Define the scope
{: #alert-config-legacy-step5}

Indicate the scope of the alert. By default, the scope is set to `everywhere`. However, you can limit the scope, for example, to a specific component of the infrastructure.

## Step 6. Define the trigger condition
{: #alert-config-legacy-0step6}

Choose any of the following options:

- Choose **Single Alert** when you want this alert to be triggered when the condition is met for your entire scope.

- Choose **Multiple Alert** and configure 1 or more segments when you want this alert to be triggered when the condition is met for any or every segment.


## Step 7. Configure the notify section
{: #alert-config-legacy-0step7}

Select 1 or more notification channels.

By default, you get a notification in the *Events* section.

You can enable multi-channel notifications by enabling 1 or more notification channels.

Optionally, you can customize the information that is included in a notification to provide more context for the alert.
