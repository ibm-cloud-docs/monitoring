---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Managing notification by using the {{site.data.keyword.mon_short}} API
{: #notifications_api}

You can manage notifications in an {{site.data.keyword.mon_full_notm}} instance by using the {{site.data.keyword.mon_short}} API.
{: shortdesc}

To learn how to use cURL, see [cURL command](/docs/monitoring?topic=monitoring-mon-curl).


## Fetch all user notifications
{: #notifications_api_get_all}

You can use the following cURL command to get information about all the notification channels:


```shell
curl -X GET <REST_API_ENDPOINT>/api/notificationChannels?from=<START_TIMESTAMP>&to=<END_TIMESTAMP> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where

* `<REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `SysdigTeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `to` and `from` are query parameters that you must define to configure the period of time for which you want information on the notifications.

For more information about the response format, see [notification schema](/docs/monitoring?topic=monitoring-notifications_api#notifications-api-parm-req-schema).


## Fetch specific user notification
{: #notifications_api_get_channel}

You can use the following cURL command to get information about a notification channel:


```shell
curl -X GET <REST_API_ENDPOINT>/api/notificationChannels/<NOTIFICATION_ID> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where

* `<REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `SysdigTeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `<NOTIFICATION_ID>` defines the ID of the notification that you want to modify.


For example, the response body for an email notification channel looks as follows:


```json
{
  "notificationChannel": {
    "id": 20,
    "version": 1,
    "createdOn": 1466023669000,
    "modifiedOn": 1466023669000,
    "type": "EMAIL",
    "enabled": true,
    "name": "emailChannel",
    "options": {
      "emailRecipients": [
        "abc@xyz.com"
      ],
      "notifyOnOk": false
    }
  }
}
```
{: codeblock}


## Create a notification
{: #notifications_api_create}

You can use the following cURL command to create an notification:


```shell
curl -X POST <REST_API_ENDPOINT>/api/notificationChannels -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json" -d @notification.json
```
{: codeblock}

Where

* `<REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `SysdigTeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* You can pass data to create the notification in the `notification.json` file by using `-d`.

    Valid types are `EMAIL`, `PAGER_DUTY`, `SLACK`, and `VICTOROPS`.

The following sample shows the request body parameters that you can set to create an notification:

```json
{
  "notificationChannel": {
      "type": "SLACK",
      "enabled": true,
      "name": "my-slack-channel",
      "options": {
        "notifyOnOk": true,
        "url": "https://hooks.slack.com/services/xxx",
        "channel": "myslack"
        "notifyOnResolve": true,
      }
    }
  }
```
{: codeblock}



## Delete a notification
{: #notifications_api_delete}

To delete an existing notification, you need the ID of that notification.
{: note}


You can use the following cURL command to delete a notification:


```shell
curl -X DELETE <REST_API_ENDPOINT>/api/notificationChannels/<NOTIFICATION_ID> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where

* `<REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `SysdigTeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `<NOTIFICATION_ID>` defines the ID of the notification that you want to modify.



## Update a notification
{: #notifications_api_update}

To update an existing notification, you need the ID of that notification.
{: note}

You can use the following cURL command to update an notification:


```shell
curl -X PUT <REST_API_ENDPOINT>/api/notificationChannels/<NOTIFICATION_ID> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json" -d @notification.json
```
{: codeblock}

Where

* `<REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [{{site.data.keyword.mon_short}} REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `SysdigTeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* `<NOTIFICATION_ID>` defines the ID of the notification that you want to modify.

* You can pass data to create the notification in the `notification.json` file by using `-d`.


The following sample shows the request body parameters that you can set to update an notification:

```json
{
  "notificationChannel": {
    "id": 9,
    "version": 2,
    "type": "WEBHOOK",
    "enabled": true,
    "name": "test-tip-webhook",
    "options": {
      "notifyOnOk": false,
      "url": "https://test-tip.endpoint.com",
      "notifyOnResolve": true
    }
  }
}
```
{: codeblock}

**Request body parameters:** All the response body parameters specified in GET notification channel except:

- createdOn
- modifiedOn


**Note:** Notification version can get through response body of [notificationChannels API](#notifications_api_get_channel). User can also add [customHeaders & customData](https://docs.sysdig.com/en/configure-a-webhook-channel.html#al_UUID-a6715905-0530-a08a-a3ab-cb10b2c5d19b_UUID-f9896786-62e5-c4c3-d2ef-38d3a2f7dfab){: external} to notfications based on their requirements.



## Notifications schema: Request body
{: #notifications-api-parm-req-schema}

See schema for getting information about 1 or more notifications channels:

```json
{
  "notificationChannel": {
    "id": 20,
    "version": 1,
    "type": "",
    "enabled": true,
    "name": "",
    "options": {
      "notifyOnOk": false,
      "notifyOnResolve": true,
      "resolveOnOk": true,
      "channel": "",
      "emailRecipients": "",
      "url" : "",
      "apiKey": "",
      "routingKey": "",
      "account": "",
      "serviceKey": "",
      "serviceName": ""
    }
  }
}
```
{: codeblock}

Sww schema when you create, update, or delete a notification channel:

```json
{
  "notificationChannel": {
    "id": 20,
    "version": 1,
    "type": "",
    "enabled": true,
    "name": "",
    "options": {
      "notifyOnOk": false,
      "notifyOnResolve": true,
      "resolveOnOk": true,
      "channel": "",
      "emailRecipients": "",
      "url" : "",
      "apiKey": "",
      "routingKey": "",
      "account": "",
      "serviceKey": "",
      "serviceName": ""
    }
  }
}
```
{: codeblock}

## Notifications schema: Response body
{: #notifications-api-parm-res-schema}

```json
{
  "notificationChannel": {
    "id": 20,
    "version": 1,
    "createdOn": 1466023669000,
    "modifiedOn": 1466023669000,
    "type": "",
    "enabled": true,
    "name": "",
    "options": {
      "notifyOnOk": false,
      "notifyOnResolve": true,
      "resolveOnOk": true,
      "channel": "",
      "emailRecipients": "",
      "url" : "",
      "apiKey": "",
      "routingKey": "",
      "account": "",
      "serviceKey": "",
      "serviceName": ""
    }
  }
}
```
{: codeblock}


## Body parameters
{: #notifications-api-parm}

### id (integer)
{: #notifications-api-parm-id}

ID of an notification channel.
{: note}



### createdOn (integer)
{: #notifications-api-parm-created}

Defines the creation time of an notification in milliseconds.
{: note}

This parameter returns the Unix-timestamp when the notification was created.


### description (string)
{: #notifications-api-parm-desc}

This parameter describes the notification.

The description is available when you view an notification in the *notifications* section of the monitoring UI, and it is included in notification emails.



### enabled (boolean)
{: #notifications-api-req-parm-enabled}

Defines the status of an notification channel.
{: note}

Set this parameter to `true` if the notification channel is enabled to send events and notify when an notification is triggered.

Set to `false` to disable the notification channel so that it can not send notification events.


### name (string)
{: #notifications-api-parm-name}

Name of the notification. Must be unique.
{: note}

The name of a notification channel must be unique and no more than 255 characters.


### modifiedOn (integer)
{: #notifications-api-parm-modified}

Defines when an notification was last modified in milliseconds.
{: note}

This parameter defines the Unix-timestamp when the notification was last modified.


### Options (json)
{: #notifications-api-parm-options}

Options are different per type of notification channel.

The following JSON shows the schema model:

```json
"options": {
      "notifyOnOk": false,
      "notifyOnResolve": true,
      "resolveOnOk": true,
      "channel": "",
      "emailRecipients": "",
      "url" : "",
      "apiKey": "",
      "routingKey": "",
      "account": "",
      "serviceKey": "",
      "serviceName": ""
    }
```
{: codeblock}


| Option   | `EMAIL`  | `PAGER_DUTY` | `SLACK` | `VICTOROPS` | `WEBHOOK` | `OPSGENIE` |
|----------|----------|--------------|---------|-------------|-----------|------------|
| `name` | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)|
| `notifyOnOk` | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `notifyOnResolve` | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `resolveOnOk` |  ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `emailRecipients` | ![Checkmark icon](../images/checkmark-icon.svg) |  | | | | |
| `url` | | | ![Checkmark icon](../images/checkmark-icon.svg) | | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `apiKey` | | | | ![Checkmark icon](../images/checkmark-icon.svg) | | ![Checkmark icon](../images/checkmark-icon.svg) |
| `routingKey` | | | | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `account` |  | ![Checkmark icon](../images/checkmark-icon.svg) | |  |  |  |
| `serviceKey` |  | ![Checkmark icon](../images/checkmark-icon.svg) | |  |  |  |
| `serviceName` |  | ![Checkmark icon](../images/checkmark-icon.svg) | |  |  |  |
{: caption="Types of notification channels" caption-side="top"}


#### apiKey (string)
{: #notifications-api-parm-options-apiKey}

VictorOps's API key. You must get this key from your VictorOps integration settings page.
{: note}

#### channel (string)
{: #notifications-api-parm-options-channel}

Name of the channel.
{: note}

#### emailRecipients (string)
{: #notifications-api-parm-options-emailRecipients}

List of email addresses.
{: note}

#### notifyOnOk (boolean)
{: #notifications-api-parm-options-notifyOnOk}

Flag that indicates the status to send a notification when the notification state changes from `ACTIVE` to `OK` and the notification is manually acknowledged by a user.
{: note}

Set to `true` to send a notification.



### notifyOnResolve (boolean)
{: #notifications-api-parm-options-notifyOnResolve}

Flag that indicates the status to send a notification when the notification state changes from `ACTIVE` to `OK`, the condition is no longer triggered because it is resolved, and the notification is manually changed to resolved by a user.
{: note}

Set to `true` to send a notification.

#### resolveOnOk (boolean)
{: #notifications-api-parm-options-resolveOnOk}

Flag that indicates the status to send a notification when the notification state changes from `ACTIVE` to `OK` and the condition is no longer triggered because it is resolved.
{: note}

Set to `true` to send a notification.


#### routingKey (string)
{: #notifications-api-parm-options-routingKey}

VictorOps's routing key. You must get this key from your VictorOps integration settings page.
{: note}

#### url (string)
{: #notifications-api-parm-options-url}

URL endpoint.
{: note}


### type
{: #notifications-api-parm-type}

Defines the notification channel.
{: note}

| Type of notification          | Value              |
|-------------------------------|--------------------|
| Email                         | `EMAIL`            |
| PagerDuty                     | `PAGER_DUTY`       |
| Slack                         | `SLACK`            |
| VictorOps                     | `VICTOROPS`        |
| Webhook                       | `WEBHOOK`          |
| OpsGenie                      | `OPSGENIE`         |
{: caption="Types of notification channels" caption-side="top"}


### version (integer)
{: #notifications-api-parm-version}

Version of an notification.
{: note}

The version changes every time you update an notification.

The version is used for optimistic locking.



## Query parameters
{: #notifications-api-parm-query}


### notificationId (integer)
{: #notifications-api-parm-notificationid}

ID of an notification.
{: note}

### from (long)
{: #notifications-api-parm-from}

Defines the start timestamp, in microseconds, that is used when you request information about notifications that are defined.
{: note}

### to (long)
{: #notifications-api-parm-to}

Defines the end timestamp, in microseconds, that is used when you request information about notifications that are defined.
{: note}
