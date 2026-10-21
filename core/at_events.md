---

copyright:
  years:  2018, 2026
lastupdated: "2026-10-21"

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


| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Montreal (`ca-mon`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
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


## Customer agreement: List of management events
{: #at-events-customer-agreement}

| Action                                   | Description                                       |
|------------------------------------------|---------------------------------------------------------|
| `sysdig-monitor.customer_agreement.read` | An event is created when a customer agreement is read   |
{: caption="Customer agreement: List of activity tracking actions" caption-side="top"}

### Example: Customer agreement read event
{: #at-events-customer-agreement-example}

The following example shows an activity tracking event that is generated when IBM support reads a customer agreement by using impersonation.

```json
{
  "action": "sysdig-monitor.customer_agreement.read",
  "correlationId": "eddcbb8b-d81c-4c30-85da-a3e2e355251b",
  "customerCRN": "crn:v1:bluemix:public:sysdig-monitor:au-syd:a/{account_id}:{instance_id}::",
  "dataEvent": false,
  "eventTime": "2026-10-20T13:08:17.80+0000",
  "initiator": {
    "authnId": "{authn_id}",
    "authnName": "",
    "credential": {
      "type": "token"
    },
    "host": {
      "address": "",
      "agent": ""
    },
    "id": "{initiator_id}",
    "name": "",
    "typeURI": ""
  },
  "message": "IBM Cloud Monitoring: read customer_agreement",
  "observer": {
    "name": "ActivityTracker"
  },
  "outcome": "success",
  "reason": {
    "reasonCode": 200,
    "reasonType": "OK"
  },
  "requestData": {
    "impersonatedBy": "ibm-support-user",
    "isImpersonated": true,
    "payload": "",
    "queryParams": "",
    "requestURL": "/api/v1/customer/agreement",
    "teamId": 57951,
    "teamName": "Monitor Operations"
  },
  "saveServiceCopy": true,
  "serviceName": "sysdig-monitor",
  "severity": "normal",
  "target": {
    "id": "crn:v1:bluemix:public:sysdig-monitor:au-syd:a/{account_id}:{instance_id}:customer_agreement:",
    "name": "",
    "resourceGroupId": "crn:v1:bluemix:public:resource-controller::a/{account_id}::resource-group:{resource_group_id}",
    "typeURI": "sysdig-monitor/customer_agreement"
  }
}
```
{: codeblock}

The `requestData` field contains impersonation context when IBM support accesses the instance on your behalf.

`requestData` fields:

`impersonatedBy`
:   The identity of the IBM support user who performed the impersonated action.

`isImpersonated`
:   Set to `true` when the request is made by an IBM support user on behalf of a customer.

`requestURL`
:   The API endpoint that was called during the impersonated session.

`teamId`
:   The numerical ID of the team context in which the impersonated action was performed.

`teamName`
:   The name of the team context in which the impersonated action was performed.
