---

copyright:
  years:  2018, 2021
lastupdated: "2021-04-14"

keywords: IBM Cloud, monitoring, alerts

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Working with alerts
{: #alerts}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify about problems that may require attention. When an alert is triggered, you can be notified through 1 or more notification channels. An alert definition can generate multi-channel notifications.
{: shortdesc}

You can define an alert on a single metric or a set of metrics to notify of events or issues that you want to monitor.
- You can define a single condition alert.
- You can define a multi-condition alert. The alert threshold is configured by using complex conditions.
- You can define how the data is aggregated.
- You can use boolean logic to define alerts that report on multiple metrics.
- You get a notification when the alert condition is met.
- You can configure multiple notification channels per alert.
- Alerts are executed in 1 minute or less from receipt, with the option to configure the trigger wait time by hour or day.
- For PromQL alerts only, you can optionally configure a 0 minute wait time.

## Types of alerts
{: #alerts_types}

The {{site.data.keyword.mon_full_notm}} service includes pre-defined alerts that you can enable. In addition, you can configure custom alerts from panels in a dashboard, by using the REST API, or in the *Alerts* section of the web UI.


In the {{site.data.keyword.mon_full_notm}} service, you can define any of the following types of alerts:

- Downtime: Use this type of alert to monitor sources and alert when they are down, for example, a bare metal.

- Metric: Use this type of alert to monitor time-series metrics and alert when they reach the thresholds defined.

- PromQL: Use this type of metric to monitor metrics by using a PromQL query.

- Event: Use this type of alert to monitor occurrences of specific events and alert when they reach the thresholds defined. For example, you can use this alert to monitor when a number of unauthorize access requests are reported.

- Anomaly Detection: Use this type of alert to monitor hosts based on historical behaviors and alert when they deviate from the expected pattern.

- Group Outlier: Use this type of alert to monitor hosts and be notified when 1 acts differently from the rest.


## Notification channels
{: #alerts_types_channels}

A notification channel defines where you want to receive information when an alert is triggered.

When you configure an alert, you can specify 1 or more notification channels.
{: note}

By default, when an alert is triggered, you get a notification in the *Events* section.

You can configure any of the following notification channels:
- Amazon SNS Topic
- Email
- IBM Cloud Functions
- Microsoft Teams
- OpsGenie
- PagerDuty
- Slack
- Teams Email
- VictorOps
- WebHook


## Configuring an alert
{: #alerts_configure}

Complete the following steps to configure an alert:

### Step 1.  Select the alert type
{: #alerts_configure_step1}

From the *Alert* section of the UI, select **Add Alert**. Then, choose the alert type.

### Step 2. Name the alert
{: #alerts_configure_step2}

Enter a name for the alert.

You can also add a description for the alert and the name of an alert group if you want to group you alerts.  If an alert group is not specified, the alert will be created in the default group. 


### Step 3. Define the severity
{: #alerts_configure_step3}

Add a severity level. Valid severity values are `info`, `low`, `medium`, and `high`.


### Step 4. Define the metric section
{: #alerts_configure_step4}

1. Select a metric (entity) that you want to monitor.
2. Define the alert condition. Choose any of the following options:

    Option 1: Choose a metric and a single condition such as `average`, `sum`, `minimum` or `maximum`.

    Option 2: Choose **Create multi-condition alerts**. Enter the condition, for example, `min(min(cpu.used.percent)) < = 50 OR max(max(cpu.used.percent)) >= 80`.

    ![Multi-condition alert](images/multi-condition-alerts.png "Multi-condition alert")

### Step 5. Define the scope
{: #alerts_configure_step5}

Indicate the scope of the alert. By default, the scope is set to `everywhere`. However, you can limit the scope, for example, you can limit the scope to a specific component of the infrastructure.

### Step 6. Define the trigger condition
{: #alerts_configure_step6}

Choose any of the following options:

- Choose **Single Alert** when you want this alert to be triggered when the condition is met for your entire scope.

- Choose **Multiple Alert** and configure 1 or more segments when you want this alert to be triggered when the condition is met for in any or every segment.


### Step 7. Configure the notify section
{: #alerts_configure_step7}

Select 1 or more notification channels.

By default, you get a notification in the *Events* section.

You can enable multi-channel notifications by enabling 1 or more notification channels.

Optionally, you can customize the information that is included in a notification to provide more context for the alert.
