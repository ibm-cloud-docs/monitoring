---

copyright:
  years:  2018, 2019
lastupdated: "2019-07-21"

keywords: Sysdig, IBM Cloud, monitoring, sysdig rest api

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


# Managing the Sysdig REST API
{: #api}

Use the Sysdig REST API to automate routine tasks and monitor notifications.
{:shortdesc}

When you use the API from your custom scripts or programs, you must use a valid IBM IAM token to authenticate with the {{site.data.keyword.mon_full_notm}} instance. A Sysdig token may also be used, but IAM tokens are the recommended method.
{: tip}

## Authenticating with the Sysdig API
See [Working With API Tokens](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get) for information on the types of valid tokens and how to retrieve them.

## Working with the API
See the [official Sysdig REST API conventions](https://docs.sysdig.com/en/sysdig-rest-api-conventions.html) for general information on required headers and syntax.

For dashboard operations, see [Working with Dashboards](https://docs.sysdig.com/en/working-with-dashboards.html)

For saving and backing up dashboards, see [Save and Restore Dashboards](https://docs.sysdig.com/en/save-and-restore-dashboards-with-scripts.html)

