---

copyright:
  years:  2018, 2019
lastupdated: "2019-06-11"

keywords: Sysdig, IBM Cloud, monitoring, notifications, api

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

# Notification API Operations

## Working with cURL
{: #curl-guide}

```shell
curl -X <METHOD> <SYSDIG_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```

An example being:
```shell
curl -X POST \
  https://us-south.monitoring.test.cloud.ibm.com/api/notificationChannels \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @notification.json
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

## Fetch all user notifications

### Using curl

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| GET | `api/notificationChannels` | |

## Fetch specific user notification

### Using curl

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| GET | `api/notificationChannels/<ID>` | |

#### Sample output for notification type email

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
        "jhon@us.ibm.com"
      ],
      "notifyOnOk": false
    }
  }
}
```

#### Response body parameters

- `id`: NotificationChannel ID
- `type`: Type of notification channels; Valid values are:
  - `EMAIL` for email notifications
  - `PAGER_DUTY` for pager duty notifications
  - `SLACK` for slack notifications
  - `VICTOROPS` for victorOps notifications
  - `WEBHOOK` for generic notification channel
- `name`: Name of the notification channel. Note that notification channel names must be unique and no more than 255 characters
- `enabled`: true if the notification channel is being processed and events can fire; false otherwise
- `options`: this contains different properties related to the different notification channel type:
  - **EMAIL**
    - `emailRecipients` is a list of email addresses
  - **SLACK**
    - `channel` slack channel name
    - `notifyOnOk` boolean flag to receive a notification message when the notification state changed from ACTIVE to OK
    - `url`  slack [incoming webhook](https://api.slack.com/incoming-webhooks) url endpoint
  - **PAGER_DUTY**
    - `channel` pagerDuty channel name
    - `resolveOnOk` boolean flag to send a notification to resolve the incident in PD when the notification state changed from ACTIVE to OK
  - **VICTOROPS**
    - `apiKey` mandatory api key retrieved from VictorOps integration settings page
    - `routingKey` mandatory routing key retrieved from VictorOps integration settings page
    - `resolveOnOk` boolean flag to send a notification to resolve the incident in VictorOps when the notification state changed from ACTIVE to OK
  - **WEBHOOK**
    - `url` generic url endpoint
    - `notifyOnOk` boolean flag to send a notification to resolve the incident in VictorOps when the notification state changed from ACTIVE to OK

## Create a notification

### Using curl to create a new notification channel from json body

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| POST | `api/notificationChannels` | notification.json |

**Request body parameters:** All the response body parameters specified in Get notification channel except:

- id
- version
- createdOn
- modifiedOn

Example notification.json:

```json
{
  "notificationChannel": {
      "type": "WEBHOOK",
      "enabled": false,
      "name": "test-tip-webhook",
      "options": {
        "notifyOnOk": true,
        "url": "https://tip.endpoint.com",
        "notifyOnResolve": true,
      }
    }
  }
  ```

## Update a notification

Updating an existing notification requires the user to know the ID of that notification.

### Using curl to update an existing notification from json body

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| PUT | `api/notificationChannels/<ID>` | notification.json |

**Request body parameters:** All the response body parameters specified in GET notification channel except:

- createdOn
- modifiedOn

Example notification.json:

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

**Note:** Notification version can get through response body of [notificationChannels API](#fetch-specific-user-notification). User can also add [customHeaders & customData](https://docs.sysdig.com/en/configure-a-webhook-channel.html#al_UUID-a6715905-0530-a08a-a3ab-cb10b2c5d19b_UUID-f9896786-62e5-c4c3-d2ef-38d3a2f7dfab) to notfications based on their requirements.

## Delete a notification

Deletion of an existing notification requires the user to know the ID of that notification.

### Using curl to delete notification

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| DELETE | `api/notificationChannels/<ID>` | |
