---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-12"

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

For more information, see [Managing alerts (Alerts REST API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alerting-api).

For more information about the Sysdig Alerts API, see [Sysdig Cloud API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://app.sysdigcloud.com/apidocs/#!/Alerts/){:new_window}.



## Dashboards REST API
{: #rest_apis_dashboards}

Use this API to manage dashboards.
{: note}

| Action                      | REST API Method  | API_URL                                        | 
|-----------------------------|------------------|------------------------------------------------|
| Create a dashboard          | `POST`           | `<ENDPOINT>/api/v2/dashboards`                 |
| Update a dashboard          | `PUT`            | `<ENDPOINT>/api/v2/dashboards/<DASHBOARD_ID>`  |
| Delete a dashboard          | `DELETE`         | `<ENDPOINT>/api/v2/dashboards/<DASHBOARD_ID>`  |
| Fetch a specific dashboard  | `GET`            | `<ENDPOINT>/api/v2/dashboards/<DASHBOARD_ID>`  |
| Fetch all user dashboards   | `GET`            | `<ENDPOINT>/api/v2/dashboards`                 |
{: caption="Table 2. Dashboards REST API" caption-side="top"}

For more information, see [Managing dashboards (Dashboards REST API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-dashboard-api-operations).



## Data REST API
{: #rest_apis_data}

Use this API to extract data from a Sysdig instance.
{: note}

| Action                      | REST API Method  | API_URL                                        | 
|-----------------------------|------------------|------------------------------------------------|
| Extract metrics             | `POST`           | `<ENDPOINT>/api/data`                          |
{: caption="Table 4. Data REST API" caption-side="top"}

For more information, see [Extracting metrics from a Sysdig instance (DATA API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-metric-query-api-operations).

For more information about the Sysdig Meric Query API, see [Data APIs ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdig.gitbooks.io/sysdig-cloud-api/content/rest_api/data.html){:new_window}.



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

For more information, see [Managing downtime events (Downtime REST API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-downtimes-api-operations).





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
{: caption="Table 2. Notifications REST API" caption-side="top"}

For more information, see [Managing notification channels (Notifications REST API)](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-notification-api-operations).






