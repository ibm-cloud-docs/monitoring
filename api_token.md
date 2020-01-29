---

copyright:
  years:  2018, 2020
lastupdated: "2020-01-29"

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

You can use IAM tokens or Sysdig API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the Sysdig REST API to automate routine tasks and monitor notifications.
{:shortdesc}

## Getting the IAM API token
{: #api_iam_token_get}

The Sysdig APIs are fully integrated with {{site.data.keyword.IBM_notm}} IAM. 

Complete the following steps to get an IAM token:

1. From a terminal, log in to the {{site.data.keyword.cloud_notm}}.

2. Run the following command to get a token:

    ```
    ibmcloud iam oauth-tokens
    ```
    {: pre}


After you get the token, you can run API calls and use this token in the `Authorization` header. 

When you copy the token include the `Bearer` keyword: `Authorization: Bearer IAM_TOKEN`
{: note}


## Getting the Sysdig API token
{: #api_token_get}

Consider the following information for each instance of the {{site.data.keyword.mon_full_notm}} service:

* There is an API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.

Complete the following steps to get the token:

1. From the *Selector* button in the navigation bar, choose **Settings**
2. From the *Sysdig Monitor API* section, copy the **Sysdig Monitor API Token**.

After you get the token, you can run API calls and use this token in the `Authorization` header. 

When you copy the token include the `Bearer` keyword: `Authorization: Bearer SYSDIG_TOKEN`
{: note}



## Resetting the Sysdig API token
{: #api_token_reset}

Complete the following steps to get the token:

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. In the *Sysdig Monitor API* section, click **Reset Token** to reset the API token.
