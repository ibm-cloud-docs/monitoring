---

copyright:
  years:  2018, 2024
lastupdated: "2024-06-28"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Event alerts
{: #alert-event}

You can define {{site.data.keyword.mon_full_notm}} event alerts in the alert editor by using a form.
{: shortdesc}

You can monitor occurrences of specific events, and alert if the total number of occurrences exceeds a threshold. This is useful for alerting on container, orchestration, and service events such as restarts and deployments.

Alerts on events support one or more segmentation labels. An alert is generated for each segment.

## Guidelines when defining event alerts
{: #alert-event-guidelines}

Consider the following when defining event alerts:

* Count Events That Match: Specify a meaningful filter text to count the number of related events.
* Set a severity level for your alert. The *Alert Severity* (`High`, `Medium`, `Low`, and `Info`) are reflected in the Alerts list. You can sort alerts by severity. You can use severity as a criteria when creating alerts. For example, you want to be alerted if there are more than 10 high severity events.
* Filter by one or more event sources that should be considered by the alert. Predefined options are included for infrastructure event sources (`kubernetes`, `docker`, and `containerd`), but you can also specify other values to match custom event sources. 
* Use *Alert if* to specify the trigger condition in terms of the number of events for a given range.
* Specify a meaningful name and description that helps recipients to easily identify the alert.

## Configuring the scope
{: #alert-event-scope}

Filter the environment where this alert will apply. Use advanced operators to include, exclude, or pattern-match groups, tags, and entities. You can also create alerts directly from **Explore** and **Dashboards** to automatically populating the scope.

## Configuring triggers
{: #alert-event-trigger}

Define the threshold and time window for assessing the alert condition. A single alert sends an alert for your entire scope, while multiple alerts send if any, or every, segment passes the threshold at once.

For example, if the number of events triggered in the monitored entity is greater than 5 for the last 10 minutes, recipients will be notified through the selected channel.

