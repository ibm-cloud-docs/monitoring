---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-18"

keywords: Sysdig, IBM Cloud, monitoring, alerting, api

subcollection: Monitoring-with-Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Managing alerts (Alerts REST API)
{: #alerting-api}

You can manage alerts in a {{site.data.keyword.mon_full_notm}} instance through REST API operations that you can run by using a Python client or by using a cURL command.
{:shortdesc}


## Create an alert (POST)
{: #alerting-api-create-alert}


### Creating an alert by using a Python client
{: #alerting-api-create-alert-python}

To learn how to use the Python client, see [Using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client).

The following code shows the structure of a Python script that you can use to create an alert:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <SYSDIG-ENDPOINT> 
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client 
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Add the notification channels to send an alert when the alert is triggered
notify_channels = [
  {
    'type': 'SLACK',
    'channel': '<SLACK_CHANNEL_NAME>'
  },
  {
    'type': 'EMAIL',
    'emailRecipients': [
      'user1@ibm.com', 'user2@ibm.com'
    ]
  }
]

# Get the IDs of the notification channels that you have configured
res = sdclient.get_notification_ids(notify_channels)
if not res[0]:
    print("Failed to fetch notification channel ID's")

notification_channel_ids = res

# Create and define the alert details
res = sdclient.create_alert(
    name=<ALERT_NAME>,
    description=<ALERT_DESCRIPTION>,
    severity=<SEVERITY>,
    for_atleast_s=<FOR_ATLEAST_S>,
    condition=<CONDITION>,
    segmentby=<SEGMENTBY>,
    segment_condition=<SEGMENT_CONDITION>,
    user_filter=<USER_FILTER>,
    notify=<NOTIFICATION_CHANNEL_IDS>,
    enabled=<ENABLED>,
    annotations=<ANNOTATIONS>,
    alert_obj=<ALERT_OBJ>
)

if not res[0]:
    print("Alert creation failed")
```
{: codeblock}

Consider the following information when you create a Python script:

* You must include the following information: `<SYSDIG-ENDPOINT>`, `<IAM_APIKEY>`, and `<GUID>` These data is required to authenticate the request with the monitoring instance. To get the monitoring instance information, see [Authenticate your user or service ID by using IAM](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client#python-client-iam-auth).

* You must define the notification channels through which you want to be notified when the alert is triggered.

    Valid notification channel types are `SLACK`, `PAGER_DUTY`, `VICTOROPS`, `WEBHOOK`, and `EMAIL`.

    When you define the notification channels, the channels must be configured in the monitoring instance.

    When you add an email notification channel, you can add multiple recipients. You separate values by using a comma.

    When you define a Slack channel, replace `<SLACK_CHANNEL_NAME>` with the name of your channel. You must include the symbol `#` with the name of the channel, for example, `#my_sysdig_alert_channel`.


When you configure the alert, complete the following sections:

* [`name` and `description`]: You must define a unique name for the alert name by replacing `<ALERT_NAME>`, and optionally, add a description by replacing `<ALERT_DESCRIPTION>`.

* [`severity`]: You must define the severity of the alert by replacing `<SEVERITY>` with a number. Valid values are `0`, `1`, `2`, `3`, `4`, `5`, `6`, and `7`.

* [`for_atleast_s`]: You must define the number of consecutive seconds that the condition is met before the alert is triggered. Replace `<FOR_ATLEAST_S>` with the number of seconds.

* [`condition`]: You must define the condition that defines when the alert is triggered. For example, you can set this parameter to `['host.mac', 'proc.name']` to check a CPU alert for every process on every machine.

    For more information, see [Multi-Condition Alerts ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.sysdig.com/en/alerts.html#al_UUID-21e3bcab-eaf2-993b-96e5-bdbc631504bc_UUID-9177b0b6-2f26-ea2f-1f3c-8b9a36192bfc){:new_window}.

* [`segmentby`]: You can define the scope of an alert by configuring the `segmentedby` section. The default value is `ANY`.

* [`segment_condition`]: When the parameter *segmentby* is specified, set this field to determine when the alert will be triggered. Valid values are **ANY** and **ALL**. [Learn more]().
            
* [`user_filter`]: You can define a filter that indicates when a notification is sent. For example, you could define this entry if you want to receive a notification only if the name of the process meets the condition.

* [`notify`]: You can define the type of notifications that you want the alert to generate. Set this entry to the notification IDs of the channels that you have defined.

* [`enabled`]: You can configure the status of the alert when it is created. By default, alerts are enabled and the entry is set to `true`. Set to `false` if you do not want it enabled when you create it.

* [`annotations`]: You can add custom properties that you can associate with the alert.

* [`alert_obj`]: You can attach an alert object instead of specifying the individual parameters.


### Create an alert by using a cURL command
{: #alerting-api-create-alert-curl}


You can use the following [cURL command](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl) to create an alert:


```shell
curl -X POST <SYSDIG_REST_API_ENDPOINT>/alerts -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -d @alert.json
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).

* You can pass data to create the alert in the `alert.json` file by using `-d`. 

    When you create an alert, include the following parameters: *type*, *name*,  *severity*, *timespan*, *condition*, *segmentby*, *segmentConditionn*, *filter*, *notificationChannelIds*, *enabled*

    For more information, see [Alert schema](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alerting-api#alerting-api-schema).


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

The following table show common error response codes:

| RC    | Description  |
|-------|--------------|
| `400` |	The alert configuration is not valid. |
| `401` | Unauthorized access. |
| `422` | The alert name is not valid. The name is already used. |
{: caption="Table 1. RC" caption-side="top"} 



## Updating an alert
{: #alerting-api-update-alert}

To update an existing alert, you need the ID of that alert.
{: note}

### Updating an alert by using a Python client
{: #alerting-api-update-alert-python}

To learn how to use the Python client, see [Using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client).

The following code shows the structure of a Python script that you can use to update an alert:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <SYSDIG-ENDPOINT> 
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client 
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

res = sdclient.get_alerts()
if not res[0]:
    print("Failed to fetch existing alerts")

alert_found = False

for alert in res['alerts']:
    if alert['name'] == alert_name:
        alert_found = True
        if 'notificationChannelIds' in alert:
            alert['notificationChannelIds'] = alert['notificationChannelIds'][0:-1]
        update_txt = '(changed by update_alert)'
        if alert['description'][-len(update_txt):] != update_txt:
            alert['description'] = alert['description'] + update_txt
        alert['timespan'] = alert['timespan'] * 2  # Note: Expressed in seconds * 1000000
        res_update = sdclient.update_alert(alert)

        if not res_update:
            print("Alert update failed")

if not alert_found:
    print('Alert to be updated not found')
```

### Updating an alert by using cURL
{: #alerting-api-update-alert-curl}


You can use the following [cURL command](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl) to update an alert:


```shell
curl -X PUT <SYSDIG_REST_API_ENDPOINT>/api/alerts/<ALERT_ID> -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -d '"alertId": "<ALERT_ID>"' -d @alert.json
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).

* `<ALERT_ID>` defines the ID of the alert that you want to modify.

* You can pass data to create the alert in the `alert.json` file by using `-d`. 

    For more information, see [Alert schema](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alerting-api#alerting-api-schema).


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

The following table show common error response codes:

| RC    | Description  |
|-------|--------------|
| `400` |	The alert configuration is not valid. |
| `401` | Unauthorized access. |
| `404` | The alert ID is not recognized. |
| `409` | There is a version mismatch. |
| `422` | The alert name is not valid. The name is already used. |
{: caption="Table 2. RC" caption-side="top"} 



## Deleting an alert
{: #alerting-api-delete-alert}

To delete an existing alert, you need the ID of that alert.
{: note}

### Deleting an alert by using the python client
{: #alerting-api-delete-alert-python}

To learn how to use the Python client, see [Using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client).

The following code shows the structure of a Python script that you can use to delete an alert:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <SYSDIG-ENDPOINT> 
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client 
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

res = sdclient.get_alerts()
if not res[0]:
    print("Failed to fetch existing alerts")

for alert in res['alerts']:
    if alert['name'] == alert_name:
        print("Deleting alert")
        res = sdclient.delete_alert(alert)
        if not res:
            print("Alert deletion failed")
```

### Deleting an alert by using cURL
{: #alerting-api-delete-alert-curl}


You can use the following [cURL command](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl) to delete an alert:


```shell
curl -X DELETE <SYSDIG_REST_API_ENDPOINT>/api/alerts/<ALERT_ID> -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" 
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).

* `<ALERT_ID>` defines the ID of the alert that you want to modify.


The following table show common error response codes:

| RC    | Description  |
|-------|--------------|
| `401` | Unauthorized access. |
| `404` | The alert ID is not recognized. |
{: caption="Table 3. RC" caption-side="top"} 


## Get all user alerts
{: #alerting-api-fetch-user-alerts}

### Get all alerts by using the python client
{: #alerting-api-fetch-user-alerts-python}

To learn how to use the Python client, see [Using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client).

The following code shows the structure of a Python script that you can use to get information about all the alerts:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <SYSDIG-ENDPOINT> 
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client 
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

json_res = sdclient.get_alerts()
print(json_res)
```

### Get all alerts by using cURL
{: #alerting-api-fetch-user-alerts-curl}

You can use the following [cURL command](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl) to get information about all the alerts:


```shell
curl -X GET <SYSDIG_REST_API_ENDPOINT>/api/alerts -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -d '"to": <START_TIMESTAMP>' -d '"from": <END_TIMESTAMP>'
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).

* `to` and `from` are query parameters that you must define to configure the period of time for which you want information on the alerts. 

| RC    | Description  |
|-------|--------------|
| `401` | Unauthorized access. |
{: caption="Table 4. RC" caption-side="top"} 


For more information about the response format, see [Alert schema](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alerting-api#alerting-api-schema).

## Get a specific user alert
{: #alerting-api-fetch-user-alert}


### Get a specific user alert by using cURL
{: #alerting-api-fetch-user-alert-curl}

You can use the following [cURL command](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl) to get information about all the alerts:


```shell
curl -X GET <SYSDIG_REST_API_ENDPOINT>/api/alerts/<ALERT_ID> -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" 
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).

* `<ALERT_ID>` defines the ID of the alert that you want to modify.


The following table show common error response codes:

| RC    | Description  |
|-------|--------------|
| `401` | Unauthorized access. |
| `404` | The alert ID is not recognized. |
{: caption="Table 5. RC" caption-side="top"} 


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



## Alerts schema: Request body
{: #alerting-api-schema-req}

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
{: codeblock}

## Alerts schema: Response body
{: #alerting-api-schema-res}

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




## Body parameters
{: #alerting-api-parm}


### id (integer)
{: #alerting-api-parm-id}

ID of an alert.
{: note}



### condition (string)
{: #alerting-api-parm-condition}

Defines the threshold that is configured for the alert. This parameter is required for `MANUAL` alerts only.
{: note}

For example, you can defines a consition as follows: `avg(timeAvg(uptime)) <= 0`


### createdOn (integer)
{: #alerting-api-parm-created}

Defines the creation time of an alert in milliseconds.
{: note}

This parameter returns the Unix-timestamp when the alert was created.


### description (string)
{: #alerting-api-parm-desc}

This parameter descrines the alert. 

The description is available when you view an alert in the *Alerts* section of the Sysdig web UI, and it is included in notification emails.



### enabled (boolean)
{: #alerting-api-req-parm-enabled}

Defines the status of an alert.
{: note}

By default, this parameter is set to `true` and the alert is enabled when it is created.



### filter (string)
{: #alerting-api-parm-filter}

Defines the scope of the alert by configuring segments.
{: note} 

When this field is empty, all the metric sources are included. The scope is set to *Everything*.

For example, you can define filters like the following ones:

```
kubernetes.namespace.name='production'
```
{: screen}

```
container.image='nginx'*.
```
{: screen}

```
kubernetes.namespace.name='production' and container.image='nginx'*.
```
{: screen}

### name (string)
{: #alerting-api-parm-name}

Name of the alert. Must be unique.
{: note}

The name is used to identify the alert in the *Alerts* section of the Sysdig web UI, and it is included in notification emails.





### modifiedOn (integer)
{: #alerting-api-parm-modified}

Defines when an alert was last modified in milliseconds.
{: note}

This parameter defines the Unix-timestamp when the alert was last modified.





### notificationChannelIds (array)
{: #alerting-api-parm-not}

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
{: #alerting-api-res-parm-not-count}

Defines the number of notifications that are sent for the alert during the past 2 weeks.
{: note}


### reNotify (boolean)
{: #alerting-api-parm-renotify}

Defines whether you want to get follow up notifications until the alert condition is acknoeldged and resolved.
{: note}

By default, follow up notifications are not enabled and the field is set to `false`.


### reNotifyMinutes (integer)
{: #alerting-api-parm-renotmin}

Defines how often do you want to receive notifications on an alert that is not resolved.
{: note}

You specify the number of minutes before a reminder is sent.


### severity (integer)
{: #alerting-api-parm-severity}

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
{: caption="Table 1. Severity values" caption-side="top"} 

### severityLabel (string)
{: #alerting-api-parm-sevlevel}

Defines the criticality of an alert. Valid values are `HIGH`, `MEDIUM`, `LOW`, and `INFO`. A lower value indicates a higher severity.
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
{: caption="Table 2. Severity level values" caption-side="top"} 

### segmentBy (array of strings)
{: #alerting-api-parm-segmentedby}

Defines additional segmentation criteria.
{: note} 

For example, you can segment a CPU alert by `['host.mac', 'proc.name']` so the alert can report on any process in any machine for which you get data in the monitoring instance.



### segmentCondition (string)
{: #alerting-api-parm-segmentcondition}

Defines when the alert is triggered for each monitored entity that is specified in the *segmentBy* parameter. This parameter is required for `MANUAL` alerts only.
{: note}

Valid values are the following:
* **ANY**: The alert is triggered when at least one of the monitored entities satisfies the condition.
* **ALL**: The alert is triggered when all of the monitored entities satisfy the condition.




### teamId (string)
{: #alerting-api-parm-teamid}

Defines the GUID of the team that owns the alert.
{: note}


### type (string)
{: #alerting-api-parm-type}

Defines the type of alert. Valid values are *MANUAL*, *BASELINE*, and *HOST_COMPARISON*.
{: note}

Set to `MANUAL` for alerts that you want to control when a notification is sent. You must define the threshold that determines when the alert is triggered.

Set to `BASELINE` for alerts that you want to notify when unexpected metric values are detected. New metric data is compared with metric values that are collected over time.

Set to `HOST_COMPARISON` for alerts that you want to notify when 1 host in a group reports metrics values that are different from the other hosts in the group.



### timespan (integer)
{: #alerting-api-parm-timespan}

Minimum time interval, in microseconds, for which the alert condition must be met before the alert is triggered.
{: note}

The minimum value is 60000000 microseconds, that is, 1 minute.

The value of this parameter must be a multiple of 60000000 microseconds.


### version (integer)
{: #alerting-api-parm-version}

Version of an alert.
{: note}

The version changes every time you update an alert.

The version is used for optimistic locking.



## Query parameters
{: #alerting-api-parm-query}


### alertId (integer)
{: #alerting-api-parm-alertid}

ID of an alert.
{: note}

### from (long)
{: #alerting-api-parm-from}

Defines the start timestamp, in microseconds, that is used when you request information about alerts that are defined.
{: note}

### to (long)
{: #alerting-api-parm-to}

Defines the end timestamp, in microseconds, that is used when you request information about alerts that are defined.
{: note}




