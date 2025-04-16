---

copyright:
  years:  2018, 2025
lastupdated: "2025-04-16"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.mon_full_notm}}
{: #at_events}


{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.mon_full_notm}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}



{{site.data.keyword.mon_full_notm}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}



## Viewing activity tracking events for {{site.data.keyword.mon_full_notm}}
{: #at-viewing}



You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)


## Alerts: List of management events
{: #at_events_alerts}

| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.alert.create`         | An event is created when you create an alert definition |
| `sysdig-monitor.alert.read`           | An event is created when you read an alert definition |
| `sysdig-monitor.alert.update`         | An event is created when you update an alert definition |
| `sysdig-monitor.alert.delete`         | An event is created when you delete an alert definition |
| `sysdig-monitor.alert.list`           | An event is created when you view the alerts in the monitoring instance  |
{: caption="Alerts: List of activity tracking actions" caption-side="top"}

## Captures: List of management events
{: #at_events_captures}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.capture.create`       | An event is created when you create a Monitoring capture |
| `sysdig-monitor.capture.read`         | An event is created when you load a Monitoring capture in the dashboard |
| `sysdig-monitor.capture.update`       | An event is created when you update a Monitoring capture |
| `sysdig-monitor.capture.delete`       | An event is created when you delete a Monitoring capture |
{: caption="Captures: List of activity tracking actions" caption-side="top"}


## Dashboards: List of management events
{: #at_events_dashboards}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.dashboard.create`     | An event is created when you create a dashboard |
| `sysdig-monitor.dashboard.read`       | An event is created when you load a dashboard |
| `sysdig-monitor.dashboard.update`     | An event is created when you update a dashboard |
| `sysdig-monitor.dashboard.delete`     | An event is created when you delete a dashboard |
| `sysdig-monitor.dashboard.list`       | An event is created when you view the dashboards in the monitoring instance |
{: caption="Dashboards: List of activity tracking actions" caption-side="top"}

## Teams: List of management events
{: #at_events_teams}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-monitor.team.create`          | An event is created when you create a Monitoring team |
| `sysdig-monitor.team.read`            | An event is created when you view a Monitoring team definition |
| `sysdig-monitor.team.update`          | An event is created when you update a Monitoring team definition |
| `sysdig-monitor.team.delete`          | An event is created when you delete a Monitoring team |
| `sysdig-monitor.team.list`            | An event is created when you view the Monitoring teams |
{: caption="Teams: List of activity tracking actions" caption-side="top"}
