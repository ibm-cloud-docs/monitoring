---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-11"

keywords: IBM Cloud, monitoring, alerts

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Downtime alerts
{: #alert-downtime}

You can define {{site.data.keyword.mon_full_notm}} downtime alerts in the alert editor by using a form.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} continuously monitors different types of entities in your infrastructure, such as a host, a container, a process, and sends notifications when the monitored entity is not available or responding. Downtime alerts focus mainly on unscheduled downtime of programs, containers, and hosts in your infrastructure.

To monitor the downtime of the entities, the following up metrics are used: `sysdig_host_up`, `sysdig_container_up`, and `sysdig_program_up`. They indicate whether the agent is able to communicate with the collector. The value 1 represents the entity is up and the agent is sending this information to the collector. The value 0 represents the entity is down, implies no communication from agent to the collector about the entity.

When an alert is configured based on ab `up` metric, two data API queries are run during the alert check. One query will retrieve the current values and the other will retrieve the values from the previous alert check interval. For any entity that was present in previous interval and is not present in current interval, the metric is marked as 0.

An aggregated value of the `up` metric is displayed on the dashboard on the Alert Editor with a value between 0 and 1.

## Defining a downtime alert
{: #alert-downtime-config}

Consider the following when configuring a downtime alert:

* Set a meaningful name and description that help recipients easily identify the alert.
* Set a severity level for your alert. The *Alert Severity* (`High`, `Medium`, `Low`, and `Info`) are reflected in the Alerts list. You can sort alerts by severity. You can use severity as a criteria when creating alerts. For example, you want to be alerted if there are more than 10 high severity events.
* Specify multiple segments. Selecting a single segment might not always supply enough information to troubleshoot the issue. Enrich the selected entity with related information by adding additional related segments. Enter hierarchical entities so you can have an understanding of what went wrong and where. For example, specifying a Kubernetes cluster alone does not provide the context necessary to troubleshoot. In order to narrow down the issue, add further contextual information, such as Kubernetes Namespace, Kubernetes Deployment, and so on.

## Downtime conditions
{: #alert-downtime-cond}

You can configure your downtime alert based on a number of conditions.

### Scope
{: #alert-downtime-scope}

You can filter the environment where the alert will apply. For example, an alert will be sent when a container associated with the agent 197288 goes down. The alert will be triggered for each container name and agent ID.

Use can use `in` or `contain` operators to match multiple different possible values.

The `contain` and `not contain` operators help you retrieve values if you know part of the values. For example, `us` retrieves values that contain strings that start with “us”, such as “us-east-1b”, “us-west-2b”, and so on.

The `in` and `not in` operators let you filter multiple values.

You can also create alerts directly from **Explore** and **Dashboards** to automatically populating the scope.

### Metric
{: #alert-downtime-metric}

Select an uptime metric associated with the entity whose downtime you want to monitor. You can select one of the following entities: `host`, `container`, or `program`.


### Entity
{: #alert-downtime-entity}

Specify additional segments by using the *Alert if any of* option.

The specified entities are segmented on, and notified with, the default notification template as well as on the Preview.


### Trigger
{: #alert-downtime-trigger}

Define the threshold and time window for assessing the alert condition. Supported time scales are `minute`, `hour`, or `day`. For example, if the monitored program is not available or not responding for the last 1 minute, alert recipients will be notified.

You can set any value for percentage (%) and a value greater than 1 for the time window. For example, if you choose 50% instead of 100%, a notification will be triggered when the entity is down for 5 minutes in the selected time window of 10 minutes.

## Example use cases
{: #alert-downtime-uses}

Some use cases where you might consider using a downtime alert are:

* When your e-commerce website is down during the peak hours of Black Friday, Christmas, or New Year season.
* When  production servers of your data center experience a critical outage.
* When a MySQL database is unreachable.
* When a file upload does not work on your marketing website.

