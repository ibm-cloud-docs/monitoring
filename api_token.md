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

There are two types of tokens that can be used with the Sysdig API: IBM IAM tokens and Sysdig API tokens. IAM tokens are the recommended method for IBM users.

Use these API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the Sysdig REST API to automate routine tasks and monitor notifications.
{:shortdesc}

## Getting the IAM API token
The Sysdig APIs are fully integrated with IBM IAM. Complete the following steps to get the token:

1. Log into the ibmcloud CLI
2. `ibmcloud iam oauth-tokens` will produce the token
3. Use this token (along with the `Bearer` keyword) in the `Authorization` header when making API calls:
  ```
  'Authorization: Bearer IAM_TOKEN'
  ```
  {: codeblock}


## Getting the Sysdig API token
{: #api_token_get}

Consider the following information for each instance of the {{site.data.keyword.mon_full_notm}} service:

* There is an API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.

Complete the following steps to get the token:

1. From the *Selector* button in the navigation bar, choose **Settings**
2. From the *Sysdig Monitor API* section, copy the **Sysdig Monitor API Token**.
3. Use this token (along with the `Bearer` keyword) with the `Authorization` header:
  ```
  'Authorization: Bearer SYSDIG_TOKEN'
  ```
  {: codeblock}

## Resetting the Sysdig API token
{: #api_token_reset}

Complete the following steps to get the token:

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. In the *Sysdig Monitor API* section, click **Reset Token** to reset the API token.
