---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, api token

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


# Working with API tokens
{: #api_token}

Use the API token to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the Sysdig REST API to automate routine tasks and monitor notifications. 
{:shortdesc}

Consider the following information for each instance of the {{site.data.keyword.mon_full_notm}} service:

* There is an API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.


## Getting the Sysdig API token
{: #api_token_get}


Complete the following steps to get the token:

1. From the *Selector* button in the navigation bar, choose **Settings**
2. From the *Sysdig Monitor API* section, copy the **Sysdig Monitor API Token**.

## Resetting the Sysdig API token
{: #api_token_reset}

Complete the following steps to get the token:

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. In the *Sysdig Monitor API* section, click **Reset Token** to reset the API token.
