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

## Alerting REST API
{: #rest_apis_alerts}

| Action                     | REST API Method  | API_URL                             | 
|----------------------------|------------------|-------------------------------------|
| Create an alert            | `POST`           | `<ENDPOINT>/api/alerts`             |
| Update an alert            | `PUT`            | `<ENDPOINT>/api/alerts/<ALERT_ID>`  |
| Delete an alert            | `DELETE`         | `<ENDPOINT>/api/alerts/<ALERT_ID>`  |
| Fetch a specific alert     | `GET`            | `<ENDPOINT>/api/alerts/<ALERT_ID>`  |
| Fetch all user alerts      | `GET`            | `<ENDPOINT>/api/alerts`             |
{: caption="Table 1. Alerting REST API" caption-side="top"}

For more information, see [Alerting by using REST API operations]().






