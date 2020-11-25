---

copyright:
  years:  2018, 2020
lastupdated: "2020-02-12"

keywords: Sysdig, IBM Cloud, monitoring, sysdig rest api

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


# Working with the Sysdig REST API
{: #api}

Use the Sysdig REST API to automate routine tasks and monitor notifications.
{:shortdesc}



## Authenticating with the Sysdig API
{: #api_1}

You can use IAM tokens or Sysdig API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the Sysdig REST API to automate routine tasks and monitor notifications. For more information, see [Working With API Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-api_token#api_token_get).

When you use the Sysdig REST API from your custom scripts or programs, use an IAM token to authenticate with the {{site.data.keyword.mon_full_notm}} instance. 
{: tip}



## Working with the API
{: #api_2}

See the [official Sysdig REST API conventions](https://docs.sysdig.com/en/sysdig-rest-api-conventions.html) for general information on required headers and syntax.

For dashboard operations, see [Working with Dashboards](https://docs.sysdig.com/en/working-with-dashboards.html)

For saving and backing up dashboards, see [Save and Restore Dashboards](https://docs.sysdig.com/en/save-and-restore-dashboards-with-scripts.html)

