---

copyright:
  years:  2018, 2021
lastupdated: "2021-01-20"

keywords: Sysdig, IBM Cloud, monitoring, api token

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
{:external: target="_blank" .external}


# Working with Sysdig tokens
{: #api_sysdig_token}

You can use Sysdig API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the Sysdig REST API to automate routine tasks and monitor notifications. 
{:shortdesc}


## Getting the Sysdig API token
{: #api_token_get}

Consider the following information for each instance of the {{site.data.keyword.mon_full_notm}} service:

* There is a Sysdig API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.

Complete the following steps to get the token:

1. From the *Selector* button in the navigation bar, choose **Settings**
2. From the *Sysdig Monitor API* section, copy the **Sysdig Monitor API Token**.

After you get the token, you can run API calls and use this token in the `Authorization` header. 

When you copy the token include the `Bearer` keyword: `Authorization: Bearer SYSDIG_TOKEN`
{: note}



## Resetting the Sysdig API token
{: #api_token_reset}

Complete the following steps to reset the token:

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. In the *Sysdig Monitor API* section, click **Reset Token** to reset the API token.


