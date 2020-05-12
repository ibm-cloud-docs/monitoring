---

copyright:
  years:  2018, 2019
lastupdated: "2019-06-11"

keywords: Sysdig, IBM Cloud, monitoring, alerting, api

subcollection: Sysdig

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

# Alerting API Operations

## Working with cURL
{: #curl-guide}

```shell
curl -X <METHOD> <SYSDIG_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```

An example being:
```shell
curl -X POST \
  https://us-south.monitoring.test.cloud.ibm.com/api/alerts \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @alert.json
```

* [Sysdig endpoints](https://test.cloud.ibm.com/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_sysdig)

**Headers for IAM Tokens (Recommended)**:
```shell
-H "Authorization: Bearer $AUTH_TOKEN"
-H "IBMInstanceID: $GUID"
```
* `AUTH_TOKEN=$(ibmcloud iam oauth-tokens | awk '{print $4}')`
* `GUID=$(ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid')`

**Headers for Sysdig Token**:
```shell
-H "Authorization: Bearer $SYSDIG_TOKEN"
```
* `SYSDIG_TOKEN` can be found in the Sysdig dashboard settings under Sysdig Monitor API

## Fetch all user alerts

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

## Create an alert

### Using the python client to create new alert

  ```python
  from sdcclient import IbmAuthHelper, SdMonitorClient

  URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
  APIKEY = <IAM_APIKEY>
  GUID = <GUID>
  ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
  sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

  # Find notification channels (you need IDs to create an alert).
  notify_channels = [
    {
      'type': 'SLACK',
      'channel': '#python-sdc-test-alert'
    },
    {
      'type': 'EMAIL',
      'emailRecipients': [
        'python-sdc-testing@draios.com', 'test@sysdig.com'
      ]
    }
  ]

  res = sdclient.get_notification_ids(notify_channels)
  if not res[0]:
      print("Failed to fetch notification channel ID's")

  notification_channel_ids = res
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

### Using curl to create a new alert from a json

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
