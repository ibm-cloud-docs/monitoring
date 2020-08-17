---

copyright:
  years:  2018, 2020
lastupdated: "2020-07-09"

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


# Working with API tokens
{: #api_token}

You can use IAM tokens or Sysdig API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the Sysdig REST API to automate routine tasks and monitor notifications. 
{:shortdesc}

## Getting an IAM API key
{: #api_iam_apikey_get}

An application programming interface key (API key) is a unique code that is passed in to an API to identify the calling application or user. [Learn more](/docs/account?topic=account-manapikey).
 
You can use a user API key or an API key that is associated with a service ID that you create.

* A user API key is associated with a user's identity, and each API key that is created by the user has the same access that the user is assigned. [Learn more](/docs/account?topic=account-userapikey).

    To view your API keys, go to **Manage** &gt; **Access (IAM)** &gt; **API keys**. 

    To create an API key, see [Creating an API key](/docs/account?topic=account-userapikey#create_user_key).

* API keys, that are associated with service IDs that you create, are used to connect an application inside or outside of {{site.data.keyword.cloud_notm}}
 to an {{site.data.keyword.cloud_notm}} service. [Learn more](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys).

    To view the API keys, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**. 

    Service ID API keys inherit all access that is assigned to the specific service ID.
    
    To create an API key, see [Creating an API key for a service ID](/docs/account?topic=account-serviceidapikeys#create_service_key).



## Getting an IAM API token
{: #api_iam_token_get}

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

To get the token without the `Bearer` word, you can run the following command: `ibmcloud iam oauth-tokens | awk '{print $4}'`
{: tip}


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
