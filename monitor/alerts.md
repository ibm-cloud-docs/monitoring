---

copyright:
  years:  2018, 2024
lastupdated: "2024-11-11"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Working with alerts and events
{: #alerts}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify about problems that may require attention. When an alert is triggered, you can be notified through 1 or more notification channels. An alert definition can generate multi-channel notifications.
{: shortdesc}

An alert is a notification event that you can use to warn about situations that require attention. Each alert has a severity status. This status informs you about the criticality of the information it reports on.

When you define an alert, you must define the condition that triggers the notification, and one or more notification channels through which you want to be notified. You must also define the severity of the alert, and the type of alert. For more information about how to configure an alert, see [Configuring an alert](/docs/monitoring?topic=monitoring-alert-config).

By default, severity is set to *warning*. You can set the severity of an alert to any of the following values: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *informational*, debug*

You can define an alert on a single metric or a set of metrics to notify of events or issues that you want to monitor.
- You can define a single condition alert.
- You can define a multi-condition alert. The alert threshold is configured by using complex conditions.
- You can define how the data is aggregated.
- You can use boolean logic to define alerts that report on multiple metrics.
- You get a notification when the alert condition is met.
- You can configure multiple notification channels per alert.
- Alerts are executed in 1 minute or less from receipt, with the option to configure the trigger wait time by hour or day.
- For PromQL alerts only, you can optionally configure a 0 minute wait time.


You can enable predefined alerts, modify alerts, and create custom alerts in the web UI and by using the {{site.data.keyword.mon_full_notm}} API.

You manage alerts in the *Alerts* view of the web UI. You can configure the table columns that are displayed in the *Alerts* view. Valid column options are *Name*, *Scope*, *Alert When*, *Segment By*, *Notifications*, *Enabled*, *Modified*, *Captures*, *Channels*, *Created*, *Description*, *Email recipients*, *For at least*, *OpsGenie*, *PagerDuty*, *Severity*, *Slack*, *WebHook*, *Type*, and *VictorOps*.

## Types of alerts
{: #alerts_types}

The {{site.data.keyword.mon_full_notm}} service includes pre-defined alerts that you can enable. In addition, you can configure custom alerts from panels in a dashboard, by using the REST API, or in the *Alerts* section of the web UI.


In the {{site.data.keyword.mon_full_notm}} service, you can define any of the following types of alerts:

- Downtime: Use this type of alert to monitor sources and alert when they are down, for example, a bare metal.

- Metric: Use this type of alert to monitor time-series metrics and alert when they reach the thresholds defined.

- PromQL: Use this type of metric to monitor metrics by using a PromQL query.

- Event: Use this type of alert to monitor occurrences of specific events and alert when they reach the thresholds defined. For example, you can use this alert to monitor when a number of unauthorize access requests are reported.

- Anomaly Detection: Use this type of alert to monitor hosts based on historical behaviors and alert when they deviate from the expected pattern.

    This type of alert is deprecated. You can only manage existing alerts of this type.
    {: note}

- Group Outlier: Use this type of alert to monitor hosts and be notified when 1 acts differently from the rest.

    This type of alert is deprecated. You can only manage existing alerts of this type.
    {: note}


## Notification channels
{: #alerts_types_channels}

A notification channel defines where you want to receive information when an alert is triggered.

When you configure an alert, you can specify 1 or more notification channels.
{: note}

By default, when an alert is triggered, you get a notification in the *Events* section.

You can configure any of the following notification channels:
- Email
- IBM Event Notifications
- Microsoft Teams
- OpsGenie
- PagerDuty
- Slack
- Teams Email
- VictorOps
- WebHook





## Events
{: #alerts_events}

An event is a notification that informs about something that occurs in any of the nodes that forward data to your {{site.data.keyword.mon_short}} instance. Use events to review, track, and resolve issues.
{: note}

The following list outlines different types of events:

* *Alert events* are events that are triggered by user-configured alerts.
* *Infrastructure-based events* are events that are collected from Docker and Kubernetes nodes. By default, the monitoring agent automatically discovers and collects data from a select group of events. You can edit the agent configuration file to enable more events.
* *Custom events* that you configure through any of the following integrations: Slackbot, pre-built Python scripts, custom user-created Python scripts, or cURL requests.

By default, an event has a state:
* **Active**: This state indicates that the circumstances that triggered the event remain in place, for example, a node continues to be down.
* **OK**: This state indicates that the situation is back to normal, for example, a node is up and running.

You manage events in the *Events* section of the web UI.
* You can view alert events through the *Alert Events* tab.
* You can view infrastructure-based events through the *Custom events* tab.
* You can view custom events through the *Custom events* tab.
* You can send custom events to any of your teams by using the [API token for that team](/docs/monitoring?topic=monitoring-api_token#api_token). For more information, see [Custom events)](https://docs.sysdig.com/en/events.html){: external}.
* You can set the event as **Resolved** to notify other users that the issue has been addressed instead of waiting for the status to be set to **OK**.
{: #tip}
