---

copyright:
  years:  2018, 2020
lastupdated: "2020-07-10"

keywords: Sysdig, IBM Cloud, monitoring, alerting, api, curl

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


# Sysdig REST APIs
{: #rest_apis}

You can use cURL, a command line tool, to make API calls to the {{site.data.keyword.mon_full_notm}} service by using URL syntax. You can also use the Python client, `sdcclient`, to automate routine tasks and monitor notifications.
{:shortdesc}

You can use public or private endpoints to make REST API calls. For more information, see [REST API endpoints]().

## Alerts REST API
{: #rest_apis_alerts}

Use this API to manage alerts.
{: note}

| Action                     | REST API Method  | API_URL                             | 
|----------------------------|------------------|-------------------------------------|
| Create an alert            | `POST`           | `<ENDPOINT>/api/alerts`             |
| Update an alert            | `PUT`            | `<ENDPOINT>/api/alerts/<ALERT_ID>`  |
| Delete an alert            | `DELETE`         | `<ENDPOINT>/api/alerts/<ALERT_ID>`  |
| Fetch a specific alert     | `GET`            | `<ENDPOINT>/api/alerts/<ALERT_ID>`  |
| Fetch all user alerts      | `GET`            | `<ENDPOINT>/api/alerts`             |
{: caption="Table 1. Alerting REST API" caption-side="top"}

For more information, see [Managing alerts (Alerts REST API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alert_api).



## Data REST API
{: #rest_apis_data}

Use this API to extract data from a Sysdig instance.
{: note}

| Action                      | REST API Method  | API_URL                                        | 
|-----------------------------|------------------|------------------------------------------------|
| Extract metrics             | `POST`           | `<ENDPOINT>/api/data`                          |
{: caption="Table 2. Data REST API" caption-side="top"}

For more information, see [Extracting metrics from a Sysdig instance (DATA API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-metrics_api).

For more information about the Sysdig Meric Query API, see [Data APIs](https://sysdig.gitbooks.io/sysdig-cloud-api/content/rest_api/data.html){: external}.



## Downtime REST API
{: #rest_apis_downtime}

Use this API to manage downtime events.
{: note}

| Action                             | REST API Method  | API_URL                                        | 
|------------------------------------|------------------|------------------------------------------------|
| Fetch an active downtime event     | `GET`            | `<ENDPOINT>/api/downtimes`                     |
| Schedule a downtime event          | `POST`           | `<ENDPOINT>/api/downtimes`                     |
| Remove a scheduled downtime event  | `DELETE`         | `<ENDPOINT>/api/downtimes/<DOWNTIME_EVENT_ID>` |
{: caption="Table 3. Downtime REST API" caption-side="top"}



## Notifications REST API
{: #rest_apis_notifications}

Use this API to manage notification channels.
{: note}

| Action                                  | REST API Method  | API_URL                                        | 
|-----------------------------------------|------------------|------------------------------------------------|
| Create a notification channel           | `POST`           | `<ENDPOINT>/api/notificationChannels`                 |
| Update a notification channel           | `PUT`            | `<ENDPOINT>/api/notificationChannels/<NOTIFICATION_CHANNEL_ID>`  |
| Delete a notification channel           | `DELETE`         | `<ENDPOINT>/api/notificationChannels/<NOTIFICATION_CHANNEL_ID>`  |
| Fetch a specific notification channel   | `GET`            | `<ENDPOINT>/api/notificationChannels/<NOTIFICATION_CHANNEL_ID>`  |
| Fetch all user notification channels    | `GET`            | `<ENDPOINT>/api/notificationChannels`                 |
{: caption="Table 4. Notifications REST API" caption-side="top"}

For more information, see [Managing notification channels (Notifications REST API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-notifications_api).






