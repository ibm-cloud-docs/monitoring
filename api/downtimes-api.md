---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-12"

keywords: Sysdig, IBM Cloud, monitoring, downtimes, api

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

# Downtimes API Operations

The downtimes API allows you to determine whether there is a downtime event in progress.  You may only setup a single downtime event at a time.


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
    "downtime": {
        "id": 42,
        "start": 1576624681000,
        "notificationChannelIds": [...]
    }
}
```

Make note of the `downtime.id` field since that will be required to remove the scheduled downtime and re-enable the notifications.

## Remove a scheduled downtime event

Once the downtime has completed, you can disable the downtime event via the PUT API providing the `<id>` from the downtime record returned when the downtime event was created.

| Method | API_URL | Data File |
|----|---|----|
| PUT | `api/downtimes/<id>` |  |

Returns:

```json
{
    "downtime":{
        "id": 42,
        "start": 1576624681000,
        "end": 1576624727000,
        "notificationChannelIds": [...]
    }
}
```