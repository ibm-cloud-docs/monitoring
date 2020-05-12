---

copyright:
  years:  2020, 2020
lastupdated: "2020-02-13"

keywords: Sysdig, IBM Cloud, monitoring, downtimes, api

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

# Downtimes API Operations

The downtimes API allows you to determine whether there is a downtime event in progress.  You may only setup a single downtime event at a time.

## Working with cURL
{: #curl-guide}

```shell
curl -X <METHOD> <SYSDIG_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```

An example being:
```shell
curl -X POST \
  https://us-south.monitoring.cloud.ibm.com/api/downtimes \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @downtimes.json
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

## Fetch active downtime event

In order to determine if notifications have been disabled due to a downtime event, query the api/downtimes endpoint to retrieve a list of the active downtime events.

| Method | API_URL | Data File |
|----|---|----|
| GET | `api/downtimes` | |

Returns:

```json
{
    "downtimes": [...]
}
```

## Schedule a downtime event

To schedule a new downtime, you can provide a list of notifications to be affected by the downtime, or provide an empty list in order to indicate that all notification channels are impacted by the downtime event.

| Method | API_URL | Data File |
|----|---|----|
| POST | `api/downtimes` | `{"downtime":{"notificationChannelIds":[...]}}` |

Returns:

```json
{ 
    "downtime":{
        "id":42,
        "start":1576624681000,
        "notificationChannelIds":[...]
    }
}
```

Make note of the `downtime.id` field since that will be required to remove the scheduled downtime and re-enable the notifications.

## Remove a scheduled downtime event

Once the downtime has completed, you can disable the downtime event via the PUT API providing the `<id>` from the downtime record returned when the downtime event was created.

| Method | API_URL | Data File |
|----|---|----|
| PUT | `api/downtimes/<id>` |  |

returns:

```json
{
    "downtime":{
        "id":42,
        "start":1576624681000,
        "end":1576624727000,
        "notificationChannelIds":[...]
    }
}
```
