---

copyright:
  years:  2018, 2024
lastupdated: "2024-12-11"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Threshold alerts
{: #alert-metric}

You can define {{site.data.keyword.mon_full_notm}} Threshold alerts (previously named Metric Alerts) in the alert editor by using a form or PromQL.
{: shortdesc}

For more information on configuring alerts, see [Configuring an alert by using the alert editor](/docs/monitoring?topic=monitoring-alert-config).
{: tip}

## Specifying the conditions when a Threshold alert is triggered
{: #alert_metrics_trigger}

In the alert editor, specify the following in the **Metric & Conditions** section.

Scope

:   The alert is set to apply by default to the *Entire Infrastructure* of your team scope. However, you can restrict the alert scope by filtering by specific labels, such as `container_name` or `kube_namespace_name`.

Metric

:   Select the metric that you want to monitor, and configure how you want the data to be aggregated. Then you can choose the aggregation method that best suits your needs. For example, if you want to understand the mean latency across the entire cluster, you can use the average aggregation. Alternatively, if you want to identify nodes with the highest latency, you can use the maximum aggregation.

Group By Segment

:   By grouping metrics by labels such as `container_name`, a unique segment is generated for each container. This allows you to quickly detect if a particular container is responsible for performance degredation.

Time Aggregation

:   Also known as the Range, the **Time Aggregation** of an alert rule determines the time window over which the selected metric is aggregated. For example, if you select the `avg` aggregation for the `cassandra_read_latency` metric with a specified range, it calculates the average value of the `cassandra_read_latency` metric over that time window. This range defines how far back in time the metric values are considered for time aggregation.

Duration

:   Duration defines the time an alert condition must continuously be satisfied before triggering an alert. For instance, a duration of 10m means the condition must be met for a continuous 10 minutes. If the alert condition is not satisfied at any time within this period, the 10-minute timer resets and must be satisfied for a full, uninterrupted 10 minutes again. Setting a longer duration reduces false positives by preventing alerts from being triggered by short-lived threshold violations.

## Time Aggregation and Duration
{: #alert-metrics-range}

The Time Aggregation of an alert query defines the time period over which the relevant metric data is evaluated. It should not be confused with the Duration of an alert rule, which refers to the length of time an alert condition must be met before it triggers an alert.

## Thresholds
{: #alert-metrics-thresholds}

Define the threshold and time range for assessing the alert condition.

| Aggregation | Description | 
| -------------- | -------------- |
| average | The average of the retrieved metric values across the time period. |
| sum | The sum of the metric across the evaluated time period. |
| maximum | The maximum of the retrieved metric values across the time period. |
| minimum | The minimum of the retrieved metric values across the time period. |
{: caption="Aggregation methods" caption-side="bottom"}

## Images in Threshold alert notifications
{: #alert-metric-image}

Threshold Alert notifications forwarded to Slack or email include a snapshot of the triggering time series data. For Slack notification channels, the snapshot can be enabled or disabled within the notification channel settings. When the channel is configured to *Notify when Resolved*, a snapshot of the time series data that resolves the alert is also provided in the notification.

## Configuring multiple thresholds
{: #alert-metric-mult-thresholds}

In addition to an alert threshold, a warning threshold can be configured. Warning thresholds and alert thresholds can be associated with different notification channels. In the following example, a user might want to send a warning and alert notification to Slack, but also page the on-call team on Pagerduty if an alert threshold is met.

If both warning and alert thresholds are associated with the same notification channel, a metric immediately exceeding the alert threshold will ignore the warning threshold and only trigger the alert threshold.

## Alerting when there is no metric data
{: #alert-metric-nodata}

When a metric stops reporting data, alerts that use those metrics cannot be evaluated. To ensure that you’re aware when this happens, you can configure alerts to notify upon *No Data* by configuring the **No Data** option in the **Settings** section to either ignore or notify.

## Translating an alert configuration to PromQL
{: #alert-metric-xlate}

You can automatically translate from the form to PromQL in order to tke advantage of the flexibility and power of PromQL. Using the **Translate to PromQL** option lets you configure complex queries.

For example, the following query looks at the percentage of available memory on a host.

```text
sysdig_host_memory_available_bytes / sysdig_host_memory_total_bytes * 100
```
{: codeblock}

Thresholds are configured separately from the query, allowing the user to specify both an alert threshold and a warning threshold.

{: note}
