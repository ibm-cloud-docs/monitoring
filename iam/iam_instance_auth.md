---

copyright:
  years:  2018, 2022
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, api token

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the authentication method of a {{site.data.keyword.mon_short}} instance
{: #iam_instance_auth}

You can configure the authentication token that is allowed in a {{site.data.keyword.mon_short}} instance when you use Python scripts or the {{site.data.keyword.mon_short}} REST API to manage resources. By default, you can use an IAM token or a Monitor API token . However, you can restrict the {{site.data.keyword.mon_short}} instance to only allow IAM tokens.
{: shortdesc}


## Prereqs
{: #iam_instance_auth_prereqs}

Complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli). If the CLI is installed, continue with the next step.

2. Log in to the region and resource group in the {{site.data.keyword.cloud_notm}} where the {{site.data.keyword.mon_short}} instance is available. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Step 1. Get information on the {{site.data.keyword.mon_short}} instance
{: #iam_instance_auth_step1}

To get information about the {{site.data.keyword.mon_short}} instance, run the following command:

```text
ibmcloud resource service-instance MONITORING_INSTANCE_NAME --output JSON
```
{: pre}

The output includes a `parameters` section with the following information:

```json
"parameters": {
    "default_receiver": false,
    "external_api_auth": "IAM_ONLY"
}
```
{: codeblock}

The `external_api_auth` field indicates the types of tokens that are allowed to work with the {{site.data.keyword.mon_short}} instance.
- When the value is set to `IAM_ONLY`, you can only use IAM tokens to authenticate.
- When the value is set to `ANY`, you can use IAM tokens and Monitor API tokens to authenticate.

Check the `external_api_auth` to find out what tokens are allowed for authentication.

## Step 2. Reset the Monitor API token for each team
{: #iam_instance_auth_step2}

Complete this step if you are configuring your monitoring instance to authenticate with IAM tokens only.
{: note}

When you reset a Monitor API token , you disable the current Monitor API token that users might be using. There is 1 Monitor API token per team.

For each team in the {{site.data.keyword.mon_short}} instance, [Reset the Monitor API token](/docs/monitoring?topic=monitoring-api_monitoring_token#api_token_reset). 

## Step 3. Configure the {{site.data.keyword.mon_short}} instance to only allow IAM tokens 
{: #iam_instance_auth_step3}

Run the following command to update a {{site.data.keyword.mon_short}} instance so that only IAM tokens are allowed when you use Python scripts or the monitoring REST API to manage resources:

```text
ibmcloud resource service-instance-update NAME  -p '{"external_api_auth": "IAM_ONLY"}'
```
{: pre}

Where

`NAME` is the name of the {{site.data.keyword.mon_short}} instance.

`API_AUTH` is set to the authorization model that is enabled to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the monitoring REST API. By default, it is set to `ANY`. Valid values are: `ANY` and `IAM_ONLY`.

For example, to modify an instance, run the following command:

```text
ibmcloud resource service-instance-create monitoring-instance-01 -p '{"external_api_auth": "IAM_ONLY"}'
```
{: pre}






