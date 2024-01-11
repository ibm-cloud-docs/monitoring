---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-11"

keywords: IBM Cloud, monitoring, alerts

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Change alerts
{: #alert-change}

You can define {{site.data.keyword.mon_full_notm}} change alerts in the alert editor by using a form.
{: shortdesc}

Change alerts trigger when a metric value deviates substantially compared to historical values.

Change Alerts let you receive alerts when your metrics change considerably over time. Instead of setting a fixed threshold for when a metric goes above or below a certain value, you can use change alerts to be notified when the metric changes by a certain percentage. This is useful in environments with multiple regions where traffic and usage variations occur. By setting up a change alert, you can detect changes relative to the baseline, rather than just using a static threshold.

## Considerations when using change alerts
{: #alert-change-when}

You should consider using change alerts in the following conditions:

* A historical baseline can be established. For example,where there is normally steady network traffic.
* A metric is relatively steady. For example, database disk usage.
* When there is an abrupt metric spike. For example, request latency.

You should not consider using change alerts in the following conditions:

* When a metric is expected to fluctuate significantly over time.
* When a metric is noisy and unreliable
* When a metric has a low baseline

## Defining a change alert
{: #alert-change-def}

Change alerts compare a shorter time range to a longer one and trigger an alert if the change between the two ranges exceeds a threshold that the user has defined.

For example, if you want to be alerted on an increase in database latency, you can configure a change alert on the relevant metric, such as `database_query_duration_seconds`, comparing the last 5 minutes with the last 1 hour. If the change in the metric between the two time ranges exceeds the custom-defined threshold, the change alert will trigger and you will receive an alert notification.

## Resolving change alerts
{: #alert-change-resolve}

Unlike alerts with static thresholds which resolve when the threshold is no longer met, change alerts resolve when difference between the shorter interval and the longer interval no longer violate the user-defined threshold.

To prevent an incident from being automatically closed when a change alert no longer violates the threshold, you can configure an alert to not send alert resolutions to the notification channel when an alert resolves. This can help prevent confusion in the on-call process as an alert resolution does not necessarily mean that an incident has been resolved.

