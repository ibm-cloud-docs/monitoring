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

# Alerting by using REST API operations
{: #alerting-api}

You can manage alerts in a {{site.data.keyword.mon_full_notm}} instance through REST API operations that you can run by using a Python client or a cURL command.
{:shortdesc}


## Create an alert (POST)
{: #alerting-api-create-alert}


### Creating an alert by using a Python client
{: #alerting-api-create-alert-python}

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
    # Number from 0 to 7 where 0 means 'emergency' and 7 is 'debug'
    severity=<SEVERITY>,
    # The alert will fire if the condition is met for at least number of consecutive seconds
    for_atleast_s=<FOR_ATLEAST_S>,
    # The alert condition
    condition=<CONDITION>,
    # For example, segmenting a CPU alert by ['host.mac', 'proc.name'] we want to check this metric for every process on every machine
    segmentby=<SEGMENTBY>,
    # Optional Default value `ANY`
    segment_condition=<SEGMENT_CONDITION>,
    # Filter. We want to receive a notification only if the name of the process meets the condition
    user_filter=<USER_FILTER>,
    # Type of notification you want this alert to generate, Mention Notification channel ID's
    notify=<NOTIFICATION_CHANNEL_IDS>,
    # If the alert will be enabled when created. True by default
    enabled=<ENABLED>,
    # Custom properties to associate with the alert
    annotations=<ANNOTATIONS>,
    # Use an Alert object instead of specifying the individual parameters
    alert_obj=<ALERT_OBJ>
)

if not res[0]:
    print("Alert creation failed")
```
{: codeblock}

Consider the following information when you create a Python script:

* You must include the following information: `<SYSDIG-ENDPOINT>`, `<IAM_APIKEY>`, and `<GUID>` These data is required to authenticate the request with the monitoring instance. To get the monitoring instance information, see [Authenticate your user or service ID by using IAM](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client#python-client-iam-auth).

* You must define the notification channels by which you want to be notified on the alert.

    Valid notification channel types are `SLACK`, and `EMAIL`.

    When you define the notification channels, the channels must be configured in the monitoring instance.

    When you add an email notification channel, you can add multiple recipients. You separate values by using a comma.

    When you define a Slack channel, replace `<SLACK_CHANNEL_NAME>` with the name of your channel. Do not include the symbol `#`.

* You must define the name of the alert name by replacing `<ALERT_NAME>`.


<ALERT_DESCRIPTION>
<SEVERITY>,
# Number from 0 to 7 where 0 means 'emergency' and 7 is 'debug'
<FOR_ATLEAST_S>  The alert will fire if the condition is met for at least number of consecutive seconds
<CONDITION>
<SEGMENT_CONDITION>  Default value `ANY`
<USER_FILTER> Filter. We want to receive a notification only if the name of the process meets the condition

<NOTIFICATION_CHANNEL_IDS>  Type of notification you want this alert to generate, Mention Notification channel ID's
<ENABLED> If the alert will be enabled when created. True by default
<ANNOTATIONS> Custom properties to associate with the alert
<ALERT_OBJ> Use an Alert object instead of specifying the individual parameters


### Create an alert by using a cURL command from a json
{: #alerting-api-create-alert-curl}

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| POST | `api/alerts` | alert.json |

Example alert.json:

```json
{
  "alert": {
    "version": null,
    "name": "My Exciting Alert!",
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

#### Request body parameters

- **type**: Type of alert; Valid values are:
  - `MANUAL` for manual alerts
  - `BASELINE` for baseline alerts
  - `HOST_COMPARISON` for host comparison alerts
- **name**: Name of the alert. This will appear in the Sysdig Monitor UI and in notification emails.
- **description**: The alert description. This will appear in the Sysdig Monitor UI and in notification emails.
- **severity**: syslog-encoded alert severity. This is a number from 0 to 7 where 0 means 'emergency' and 7 is 'debug'.
- **timespan**: The number of consecutive seconds the condition must be satisfied for the alert to fire.
- **condition**: The alert condition, as described here [post_api_alerts](https://app.sysdigcloud.com/apidocs/#!/Alerts/post_api_alerts)
- **segmentby**: A list of Sysdig Monitor segmentation criteria that can be used to apply the alert to multiple entities. For
  example, segmenting a CPU alert by ['host.mac', 'proc.name'] allows to apply it to any process in any machine.
- **segmentConditionn**: When *segmentby* is specified (and therefore the alert will cover multiple entities) this field is used to determine when it will fire. In particular, you have two options for *segment_condition*: **ANY** (the alert will fire when at least one of the monitored entities satisfies the condition) and **ALL** (the alert will fire when all of the monitored entities satisfy the condition).
- **filter**: A boolean expression combining Sysdig Monitor segmentation criteria that makes it possible to reduce the
  scope of the alert. For example: *kubernetes.namespace.name='production' and container.image='nginx'*.
- **notificationChannelIds**: the type of notification you want this alert to generate. Options are *EMAIL*,*PAGER_DUTY*, *WEBHOOK*. To fetch channelID's, Please refer to section `Fetch specific user notification` under [notificationChannelIds](observability-monitoring?topic=observability-monitoring-notification-api-operations#fetch-specific-user-notification)
- **enabled**: if True, the alert will be enabled when created.





## Update an alert

Updating an existing alerts requires the user to know the ID of that alert.

### Using the python client to update existing alerts

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

### Using curl to update an existing alert from a json

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






## Delete an alert

Deletion of an existing alerts requires the user to know the ID of that alert.

### Using the python client

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

### Using curl to delete an existing alert

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



