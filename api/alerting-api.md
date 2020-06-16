---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-12"

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

You can manage alerts in a {{site.data.keyword.mon_full_notm}} instance through REST API operations that you can run by using a Python client or a cURL command.
{:shortdesc}


## Create an alert (POST)
{: #alerting-api-create-alert}


### Creating an alert by using a Python client
{: #alerting-api-create-alert-python}

To learn how to use the Pythin client, see [Using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client).

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

* [`segment_condition`]: 

* [`user_filter`]: You can define a filter that indicates when a notification is sent. For example, you could define this entry if you want to receive a notification only if the name of the process meets the condition.

* [`notify`]: You can define the type of notifications that you want the alert to generate. Set this entry to the notification IDs of the channels that you have defined.

* [`enabled`]: You can configure the status of the alert when it is created. By default, alerts are enabled and the entry is set to `true`. Set to `false` if you do not want it enabled when you create it.

* [`annotations`]: You can add custom properties that you can associate with the alert.

* [`alert_obj`]: You can attach an alert object instead of specifying the individual parameters.


### Create an alert by using a cURL command
{: #alerting-api-create-alert-curl}


You can use the following [cURL command](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl) to create an alert:


```shell
curl -X POST <SYSDIG_REST_API_ENDPOINT>/alerts -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" [-d DATA]
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).

* You can pass data to create the alert by using `-d`. 

    You can pass a JSON file that includes the alert body parameters. You can name the file `alert.json`.
    
    You can pass each body parameter individually.

* When you create an alert, you must include the following parameters: *type*, *name*,  *severity*, *timespan*, *condition*, *segmentby*, *segmentConditionn*, *filter*, *notificationChannelIds*, *enabled*

    Other parameters like *description*, are optional. For more information about the list of parameters that you can use, see [cURL command: Common parameters in the request and in the response body]().


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



## Updating an alert
{: #alerting-api-update-alert}

Updating an existing alerts requires the user to know the ID of that alert.

### Updating an alert by using a Python client
{: #alerting-api-update-alert-python}

```python
from sdcclient import IbmAuthHelper, SdMonitorClient

URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
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

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| PUT | `api/alerts/<ID>` | alert.json |

Example alert.json:

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

**Note:** alert version can be retrieved through the response body of [alerts api](#fetch-specific-user-alert).






## Deleting an alert
{: #alerting-api-delete-alert}

Deletion of an existing alerts requires the user to know the ID of that alert.

### Deleting an alert by using the python client
{: #alerting-api-delete-alert-python}

```python
from sdcclient import IbmAuthHelper, SdMonitorClient

URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
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

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| DELETE | `api/alerts/<ID>` | |



## Fetch all user alerts
{: #alerting-api-fetch-user-alerts}

### Using python client

```python
from sdcclient import IbmAuthHelper, SdMonitorClient

URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

json_res = sdclient.get_alerts()
print(json_res)
```

### Using curl

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| GET | `api/alerts` | |



## Fetch specific user alert
{: #alerting-api-fetch-user-alert}

### Using curl

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| GET | `api/alerts/<ID>` | |

#### Sample response body for alert

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

#### Response body parameters

- **id**: Alert ID
- **type**: Type of alert; Valid values are:
  - `MANUAL` for manual alerts
  - `BASELINE` for baseline alerts
  - `HOST_COMPARISON` for host comparison alerts
- **name**: Name of the alert. Note that alert names must be unique
- **enabled**: true if the alert is being processed and events can fire; false otherwise
- **filter**: String-encoded filter of the alert. The filter can be used to select nodes and/or entities
- **condition**: Valid for manual alerts only. Configures the threshold for the alert
- **segmentBy**: Segmentation to apply to condition, if needed
- **segmentCondition**: If segmentBy is set, it configures whether alert events will be triggered when all segments reach  
  the threshold or at least one does. The format is an object with a type property with ALL or ANY respectively (e.g. { "type": "ANY" }
- **timespan**: Number of microseconds. Minimum time interval for which the alert condition must be met before the alert
  will fire a event; Minimum value is 60000000 (1 minute) and values must be multiple of 60000000 (1 minute)
- **severity**: null to instruct the alert to set event severity automatically, a number from 0 (emergency) to 7 (debug) to set a manual severity
- **notificationChannelIds**: List of notification channel identifiers
- **version**: Revision version of the alert configuration
- **createdOn**: Unix-timestamp of time when the alert was created
- **modifiedOn**: Unix-timestamp of time when the alert was last modified
- **notificationCount**: Number of events fired for the alert during the past 2 weeks



## cURL command: Common parameters in the request and in the response body
{: #alerting-api-parm}


### version (string)
{: #alerting-api-parm-version}

This parameter indicates the revision version of the alert.

### name (string)
{: #alerting-api-parm-name}

This parameter defines the name of the alert. 

The name is used to identify the alert in the *Alerts* section of the Sysdig web UI, and it is included in notification emails.

### description (string)
{: #alerting-api-parm-desc}

This parameter descrines the alert. 

The description is available when you view an alert in the *Alerts* section of the Sysdig web UI, and it is included in notification emails.

### teamId (string)
{: #alerting-api-parm-teamid}

This parameter defines the team GUID that owns the alert.

### enabled (boolean)
{: #alerting-api-req-parm-enabled}

This parameter defines whether the alert is enabled once it is created.

By default, this parameter is set to `true` and the alert is enabled.

### filter (boolean)
{: #alerting-api-parm-filter}

This parameter is a boolean expression that combines segmentation criteria and makes it possible to reduce the scope of the alert. 

For example: *kubernetes.namespace.name='production' and container.image='nginx'*.


### type (string)
{: #alerting-api-parm-type}

This parameter defines the type of alert.

Valid values are the following:

* `MANUAL`: Set to this value for manual alerts. 
* `BASELINE`: Set to this value for baseline alerts. 
* `HOST_COMPARISON`: Set to this value for host comparison alerts.



### condition (string)
{: #alerting-api-parm-condition}

This parameter indicates the threshold for the alert.

For example, you can defines a consition as follows: `avg(timeAvg(uptime)) <= 0`



### timespan (microseconds)
{: #alerting-api-parm-timespan}

This parameter indicates the minimum time interval for which the alert condition must be met before the alert is triggered.

The minimum value is 60000000 microseconds, that is, 1 minute.
The value of this parameter must be a multiple of 60000000 microseconds.



### notificationChannelIds (string)
{: #alerting-api-parm-not}

This parameter indicates the type of notification you want this alert to generate. 

Valid options are `EMAIL`, `PAGER_DUTY`, `WEBHOOK`, `VICTOROPS`, and `SLACK`. 


### reNotify (boolean)
{: #alerting-api-parm-renotify}

This parameter indicates if you want to get follow up notifications until the alert condition is acknoeldged and resolved.

By default, follow up notifications are not enabled and the field is set to `false`.


### reNotifyMinutes (integer)
{: #alerting-api-parm-renotmin}

This parameter indicates how often do you want to receive notifications on an alert that is not resolved.

You specify the number of minutes before a reminder is sent.


### severity (string)
{: #alerting-api-parm-severity}

This parameter defines the syslog-encoded alert severity. 

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

This parameter defines the criticality of an alert. Valid values are `HIGH`, `MEDIUM`, `LOW`, and `INFO`.

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

### segmentBy (string)
{: #alerting-api-parm-segmentedby}

This parameter defines one or more entities that are monitored. 

For example, you can segment a CPU alert by `['host.mac', 'proc.name']` so the alert can report on any process in any machine for which you get data in the monitoring instance.

### segmentCondition (string)
{: #alerting-api-parm-segmentcondition}

This parameter defines when the alert is triggered for each monitored entity that is specified in the *segmentBy* parameter. 

Valid values are the following:
* **ANY**: The alert is triggered when at least one of the monitored entities satisfies the condition.
* **ALL**: The alert is triggered when all of the monitored entities satisfy the condition.






## cURL command: Parameters that are specific to the response body
{: #alerting-api-res-parm}

### id
{: #alerting-api-res-parm-id}

This parameter returns the alert ID.

### createdOn
{: #alerting-api-res-parm-created}

This parameter returns the Unix-timestamp when the alert was created.

### modifiedOn
{: #alerting-api-res-parm-modified}

This parameter defines the Unix-timestamp when the alert was last modified.

### notificationCount
{: #alerting-api-res-parm-not-count}

This parameter returns the number of events that are sent for the alert during the past 2 weeks.





