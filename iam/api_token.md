---

copyright:
  years:  2018, 2022
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, api token

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Working with IAM tokens
{: #api_token}

You can use IAM tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the monitoring REST API to automate routine tasks and monitor notifications. 
{: shortdesc}

## Getting an IAM API key through the {{site.data.keyword.cloud_notm}} UI
{: #api_iam_apikey_get}

An application programming interface key (API key) is a unique code that is passed in to an API to identify the calling application or user. [Learn more](/docs/account?topic=account-manapikey).
 
You can use a user API key or an API key that is associated with a service ID that you create.

* A user API key is associated with a user's identity, and each API key that is created by the user has the same access that the user is assigned. [Learn more](/docs/account?topic=account-userapikey).

    To view your API keys, go to **Manage** &gt; **Access (IAM)** &gt; **API keys**. 

    To create an API key, see [Creating an API key](/docs/account?topic=account-userapikey#create_user_key).

* API keys, that are associated with service IDs that you create, are used to connect an application inside or outside of {{site.data.keyword.cloud_notm}}
 to an {{site.data.keyword.cloud_notm}} service. [Learn more](/docs/account?topic=account-serviceidapikeys#serviceidapikeys).

    To view the API keys, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**. 

    Service ID API keys inherit all access that is assigned to the specific service ID.
    
    To create an API key, see [Creating an API key for a service ID](/docs/account?topic=account-serviceidapikeys#create_service_key).



## Getting an IAM API token programmatically
{: #api_iam_token_get}

Complete the following steps to get an IAM token:

1. From a terminal, log in to the {{site.data.keyword.cloud_notm}}.

2. Run the following command to get a token:

    ```text
    ibmcloud iam oauth-tokens | grep IAM | cut -d \: -f 2 | sed 's/^ *//'
    ```
    {: pre}


After you get the token, you can run API calls and use this token in the `Authorization` header. 

When you copy the token include the `Bearer` keyword: `Authorization: Bearer IAM_TOKEN`
{: note}

To get the token without the `Bearer` word, you can run the following command: `ibmcloud iam oauth-tokens | awk '{print $4}'`



