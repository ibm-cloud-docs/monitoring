---

copyright:
  years: 2018, 2020
lastupdated: "2020-03-16"

keywords: activity tracker for IBM Cloud Monitoring with Sysdig, Sysdig, IBM Cloud, audit, activity tracker, events, audit logs

subcollection: Monitoring-with-Sysdig

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}


# Auditing events
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.mon_full_notm}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started).

{{site.data.keyword.mon_full_notm}} automatically generates events so that you can track activity on your service instance.


## Alerts: List of management events
{: #at_events_alerts}

| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.alert.create`         | An event is created when you create an alert definition |
| `sysdig-monitor.alert.read`           | An event is created when you read an alert definition |
| `sysdig-monitor.alert.update`         | An event is created when you update an alert definition |
| `sysdig-monitor.alert.delete`         | An event is created when you delete an alert definition |
{: caption="Table 1. Alerts: List of activity tracker actions" caption-side="top"} 

## Captures: List of management events
{: #at_events_captures}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.capture.create`       | An event is created when you create a Sysdig capture |
| `sysdig-monitor.capture.read`         | An event is created when you load a Sysdig capture in the dashboard |
| `sysdig-monitor.capture.update`       | An event is created when you update a Sysdig capture |
| `sysdig-monitor.capture.delete`       | An event is created when you delete a Sysdig capture |
{: caption="Table 2. Captures: List of activity tracker actions" caption-side="top"} 


## Dashboards: List of management events
{: #at_events_dashboards}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.dashboard.create`     | An event is created when you create a dashboard |
| `sysdig-monitor.dashboard.read`       | An event is created when you load a dashboard |
| `sysdig-monitor.dashboard.update`     | An event is created when you update a dashboard |
| `sysdig-monitor.dashboard.delete`     | An event is created when you delete a dashboard |
{: caption="Table 3. Dashboards: List of activity tracker actions" caption-side="top"} 



## Teams: List of management events
{: #at_events_teams}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.team.create`          | An event is created when you create a Sysdig team |
| `sysdig-monitor.team.read`            | An event is created when you view a Sysdig team definition |
| `sysdig-monitor.team.update`          | An event is created when you update a Sysdig team definition |
| `sysdig-monitor.team.delete`          | An event is created when you delete a Sysdig team |
{: caption="Table 4. Captures: List of activity tracker actions" caption-side="top"} 




## Where to view the events
{: #ui}

Events that are generated by an instance of the {{site.data.keyword.mon_full_notm}} service are automatically forwarded to the {{site.data.keyword.at_full_notm}} service instance that is available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-launch).

