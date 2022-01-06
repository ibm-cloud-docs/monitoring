---

copyright:
  years:  2018, 2022
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, alerting, api

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Managing alerts by using the Alerts API
{: #alert_api}

You can manage alerts in a {{site.data.keyword.mon_full_notm}} instance by using the {{site.data.keyword.mon_short}} API.
{: shortdesc}

To learn how to use cURL, see [cURL command](/docs/monitoring?topic=monitoring-mon-curl).


## Get details about a user alert
{: #alert-api-fetch-user-alert}

You can use the following cURL command to get information about an alert:


```text
curl -X GET <REST_API_ENDPOINT>/api/alerts/<ALERT_ID> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where 

* `<REST_API_ENDPOINT>` indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. 

    `TeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.
    
    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `<ALERT_ID>` defines the ID of the alert that you want to modify.


For example, the response body for an alert looks as follows:

```json
{
  "alert": {
    "autoCreated": false,
    "condition": "min(min(dallas_prod)) = 0",
    "createdOn": 1551358413000,
    "enabled": false,
    "id": 23211,
    "modifiedOn": 1551634372000,
    "name": "Monitoring Uptime Alert",
    "filter": "env in (\"prod\")",
    "notificationChannelIds": [
      4
    ],
    "segmentBy": [
      "host.hostname"
    ],
    "segmentCondition": {
      "type": "ANY"
    },
    "notificationCount": 60,
    "rateOfChange": false,
    "reNotify": false,
    "severity": 0,
    "severityLabel": "HIGH",
    "teamId": 493,
    "timespan": 60000000,
    "type": "MANUAL",
    "version": 9
  }
}
```
{: screen}


## Create an alert
{: #alert-api-create-alert}

You can use the following cURL command to create an alert:


```text
curl -X POST <REST_API_ENDPOINT>/api/alerts -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json" -d @alert.json
```
{: codeblock}

Where 

* `<REST_API_ENDPOINT>` indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. 

    `TeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.
    
    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* You can pass data to create the alert in the `alert.json` file by using `-d`. 

    When you create an alert, include the following parameters: *type*, *name*,  *severity*, *timespan*, *condition*, *segmentby*, *segmentConditionn*, *filter*, *notificationChannelIds*, *enabled*

    For more information, see [Alert schema](/docs/monitoring?topic=monitoring-alert_api#alert-api-schema-req).


The following sample shows the request body parameters that you can set to create an alert: 

```json
{
  "alert": {
    "version": null,
    "name": "My Alert!",
    "description": null,
    "teamId": null,
    "enabled": false,
    "filter": null,
    "type": "MANUAL",
    "condition": "avg(timeAvg(uptime)) <= 0",
    "timespan": 600000000,
    "notificationChannelIds": [],
    "reNotify": false,
    "reNotifyMinutes": 30,
    "segmentBy": [
      "host.hostName"
    ],
    "segmentCondition": {
      "type": "ANY"
    },
    "severityLabel": "LOW"
  }
}
```
{: screen}



## Update an alert
{: #alert-api-update-alert}

To update an existing alert, you need the ID of that alert.
{: note}

You can use the following cURL command to update an alert:


```text
curl -X PUT <REST_API_ENDPOINT>/api/alerts/<ALERT_ID> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json" -d @alert.json
```
{: codeblock}

Where 

* `<REST_API_ENDPOINT>` indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. 

    `TeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.
    
    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `<ALERT_ID>` defines the ID of the alert that you want to modify.

* You can pass data to create the alert in the `alert.json` file by using `-d`. 

    For more information, see [Alert schema](/docs/monitoring?topic=monitoring-alert_api#alert-api-schema-req).


The following sample shows the request body parameters that you can set to update an alert: 

```json
{
  "alert": {
      "type": "MANUAL",
      "id": 23212,
      "version": 10,
      "name": "CheckNginxConnections",
      "description": "Active connections of nginx server",
      "enabled": false,
      "severity": 2,
      "timespan": 1000000,
      "condition": "avg(avg(nginx.net.connections)) > 1000",
      "segmentBy": [
          "host.hostName"
      ],
      "segmentCondition": {
          "type": "ANY"
      },
      "notificationChannelIds": [
          2
      ]
    }
}
```
{: screen}


## Delete an alert
{: #alert-api-delete-alert}

To delete an existing alert, you need the ID of that alert.
{: note}


You can use the following cURL command to delete an alert:


```text
curl -X DELETE <REST_API_ENDPOINT>/api/alerts/<ALERT_ID> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where 

* `<REST_API_ENDPOINT>` indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. 

    `TeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.
    
    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `<ALERT_ID>` defines the ID of the alert that you want to delete.


## Get all user alerts
{: #alert-api-fetch-user-alerts}

You can use the following cURL command to get information about all the alerts:


```text
curl -X GET <REST_API_ENDPOINT>/api/alerts?from=<START_TIMESTAMP>&to=<END_TIMESTAMP> -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID"
```
{: codeblock}

Where 

* `<REST_API_ENDPOINT>` indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `to` and `from` are query parameters that you must define to configure the period of time for which you want information on the alerts. 

For more information about the response format, see [Alert schema](/docs/monitoring?topic=monitoring-alert_api#alert-api-schema-res).




## Alerts schema: Request body
{: #alert-api-schema-req}

```json
{
  "alerts": [
    {
      "alert": {
        "version": null,
        "name": "",
        "description": null,
        "teamId": null,
        "enabled": false,
        "filter": null,
        "type": "",
        "condition": "",
        "timespan": 600000000,
        "notificationChannelIds": [],
        "reNotify": false,
        "reNotifyMinutes": 30,
        "segmentBy": [],
        "segmentCondition": {
          "type": ""
        },
        "severityLabel": ""
      }
    }
  ]
}
```
{: screen}

## Alerts schema: Response body
{: #alert-api-schema-res}

```json
{
  "alerts": [
    {
    "alert": {
      "autoCreated": false,
      "condition": "",
      "createdOn": 1551358413000,
      "enabled": false,
      "id": 23211,
      "modifiedOn": 1551634372000,
      "name": "",
      "filter": "",
      "notificationChannelIds": [],
      "segmentBy": [],
      "segmentCondition": {
        "type": "ANY"
      },
      "notificationCount": 60,
      "rateOfChange": false,
      "reNotify": false,
      "severity": 0,
      "severityLabel": "",
      "teamId": 493,
      "timespan": 60000000,
      "type": "",
      "version": 9
      }
    }
  ]
}
```
{: screen}


## Error response codes
{: #alert-api-rc}

The following table show common error response codes:

| RC    | Description  |
|-------|--------------|
| `400` | The alert configuration is not valid. |
| `401` | Unauthorized access. |
| `404` | The alert ID is not recognized. |
| `409` | There is a version mismatch. |
| `422` | The alert name is not valid. The name is already used. |
{: caption="Table 1. RC" caption-side="top"} 



## Body parameters
{: #alert-api-parm}


### id (integer)
{: #alert-api-parm-id}

ID of an alert.
{: note}



### condition (string)
{: #alert-api-parm-condition}

Defines the threshold that is configured for the alert. This parameter is required for `MANUAL` alerts only.
{: note}

For example, you can defines a consition as follows: `avg(timeAvg(uptime)) <= 0`


### createdOn (integer)
{: #alert-api-parm-created}

Defines the creation time of an alert in milliseconds.
{: note}

This parameter returns the Unix-timestamp when the alert was created.


### description (string)
{: #alert-api-parm-desc}

This parameter describes the alert. 

The description is available when you view an alert in the *Alerts* section of the monitoring UI, and it is included in notification emails.



### enabled (boolean)
{: #alert-api-req-parm-enabled}

Defines the status of an alert.
{: note}

By default, this parameter is set to `true` and the alert is enabled when it is created.



### filter (string)
{: #alert-api-parm-filter}

Defines the scope of the alert by configuring segments.
{: note} 

When this field is empty, all the metric sources are included. The scope is set to *Everything*.

For example, you can define filters like the following ones:

```text
kubernetes.namespace.name='production'
```
{: screen}

```text
container.image='nginx'*.
```
{: screen}

```text
kubernetes.namespace.name='production' and container.image='nginx'*.
```
{: screen}

### name (string)
{: #alert-api-parm-name}

Name of the alert. Must be unique.
{: note}

The name is used to identify the alert in the *Alerts* section of the monitoring UI, and it is included in notification emails.





### modifiedOn (integer)
{: #alert-api-parm-modified}

Defines when an alert was last modified in milliseconds.
{: note}

This parameter defines the Unix-timestamp when the alert was last modified.





### notificationChannelIds (array)
{: #alert-api-parm-not}

Lists the notification channels that are configured to notify when an alert is triggered.
{: note}

Valid options are `EMAIL`, `PAGER_DUTY`, `WEBHOOK`, `VICTOROPS`, and `SLACK`. 

```json
"notificationChannelIds": [
      "EMAIL", 
      "WEBHOOK"
    ]
```
{: codeblock}


### notificationCount (integer)
{: #alert-api-res-parm-not-count}

Defines the number of notifications that are sent for the alert during the past 2 weeks.
{: note}


### reNotify (boolean)
{: #alert-api-parm-renotify}

Defines whether you want to get follow up notifications until the alert condition is acknowledged and resolved.
{: note}

By default, follow up notifications are not enabled and the field is set to `false`.


### reNotifyMinutes (integer)
{: #alert-api-parm-renotmin}

Defines how often do you want to receive notifications on an alert that is not resolved.
{: note}

You specify the number of minutes before a reminder is sent.


### severity (integer)
{: #alert-api-parm-severity}

Defines the syslog-encoded alert severity.
{: note}

The following table lists the values that you can set:

| Severity | Info        |
|----------|-------------|
| `0`      | `emergency` |
| `1`      | `alert`     |
| `2`      | `critical`  |
| `3`      | `error`     |
| `4`      | `warning`   |
| `5`      | `notice`    |
| `6`      | `informational`|
| `7`      | `debug` |
{: caption="Table 2. Severity values" caption-side="top"} 

### severityLabel (string)
{: #alert-api-parm-sevlevel}

Defines the criticality of an alert. Valid values are `HIGH`, `MEDIUM`, `LOW`, and `INFO`. A lesser value indicates a higher severity.
{: note} 

The following table shows the severity status that must be set depending on the severity parameter value:

| Severity | Severity status   |
|----------|------------------|
| `0`      | `HIGH`           |
| `1`      | `HIGH`           |
| `2`      | `MEDIUM`         |
| `3`      | `MEDIUM`         |
| `4`      | `LOW`            |
| `5`      | `LOW`            |
| `6`      | `INFO`           |
| `7`      | `INFO`           |
{: caption="Table 3. Severity level values" caption-side="top"} 

### segmentBy (array of strings)
{: #alert-api-parm-segmentedby}

Defines additional segmentation criteria.
{: note} 

For example, you can segment a CPU alert by `['host.mac', 'proc.name']` so the alert can report on any process in any machine for which you get data in the monitoring instance.



### segmentCondition (string)
{: #alert-api-parm-segmentcondition}

Defines when the alert is triggered for each monitored entity that is specified in the *segmentBy* parameter. This parameter is required for `MANUAL` alerts only.
{: note}

Valid values are the following:
* **ANY**: The alert is triggered when at least one of the monitored entities satisfies the condition.
* **ALL**: The alert is triggered when all of the monitored entities satisfy the condition.




### teamId (string)
{: #alert-api-parm-teamid}

Defines the GUID of the team that owns the alert.
{: note}


### type (string)
{: #alert-api-parm-type}

Defines the type of alert. Valid values are *MANUAL*, *BASELINE*, and *HOST_COMPARISON*.
{: note}

Set to `MANUAL` for alerts that you want to control when a notification is sent. You must define the threshold that determines when the alert is triggered.

Set to `BASELINE` for alerts that you want to notify when unexpected metric values are detected. New metric data is compared with metric values that are collected over time.

Set to `HOST_COMPARISON` for alerts that you want to notify when 1 host in a group reports metrics values that are different from the other hosts in the group.



### timespan (integer)
{: #alert-api-parm-timespan}

Minimum time interval, in microseconds, for which the alert condition must be met before the alert is triggered.
{: note}

The minimum value is 60000000 microseconds, that is, 1 minute.

The value of this parameter must be a multiple of 60000000 microseconds.


### version (integer)
{: #alert-api-parm-version}

Version of an alert.
{: note}

The version changes every time you update an alert.

The version is used for optimistic locking.



## Query parameters
{: #alert-api-parm-query}


### alertId (integer)
{: #alert-api-parm-alertid}

ID of an alert.
{: note}

### from (long)
{: #alert-api-parm-from}

Defines the start timestamp, in microseconds, that is used when you request information about alerts that are defined.
{: note}

### to (long)
{: #alert-api-parm-to}

Defines the end timestamp, in microseconds, that is used when you request information about alerts that are defined.
{: note}




