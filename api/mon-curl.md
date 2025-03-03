---

copyright:
  years:  2018, 2025
lastupdated: "2025-03-03"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Using cURL
{: #mon-curl}

You can use cURL, a command line tool, from a terminal to manage the {{site.data.keyword.mon_full_notm}} service by using URL syntax.
{: shortdesc}


## cURL syntax
{: #mon-curl-tool}

Use the following syntax from a terminal to run a cURL command:

```text
curl -X <METHOD> <MONITORING_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```
{: pre}

Where

* `<METHOD>` indicates the type of REST API call that you want to make.
* `<MONITORING-ENDPOINT>` indicates the endpoint where the monitoring instance is available. For more inforamtion, see [{{site.data.keyword.mon_short}} endpoints](/docs/monitoring?topic=monitoring-endpoints). For example, the endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com`
* `<API_URL>` For more information about API URLs, see [REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api).
* `HEADERS` add additional information such as information to authenticate with the {{site.data.keyword.mon_full_notm}} service.
* `DATA` allows you to pass additional information that might be required.



### Headers for IAM Tokens
{: #mon-curl-headers-iam}

Use IAM tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use the {{site.data.keyword.mon_short}} REST API to automate routine tasks and monitor notifications.
{: important}

In a cURL command, add the following options to authenticate with the {{site.data.keyword.mon_full_notm}} service by using an IAM token:

```text
-H "Authorization: $AUTH_TOKEN"
-H "IBMInstanceID: $GUID"
-H "SysdigTeamID: $TEAM_ID"
```
{: codeblock}

Where

* `IBMInstanceID` indicates the GUID of the {{site.data.keyword.mon_full_notm}} instance that you want to target with the cURL command.

    To get the GUID of the monitoring instance, run the following command: `ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid'`

* `Authorization` indicates the IAM token that is used to authenticate with the {{site.data.keyword.mon_full_notm}} service instance.

    To get the IAM `AUTH_TOKEN` token, run the following command: `ibmcloud iam oauth-tokens | awk '{print $4}'`

    For more information, see [Getting the IAM API token](/docs/monitoring?topic=monitoring-api_token#api_iam_token_get).

* `SysdigTeamID` indicates the GUID of a team.

    To get the GUID, see [Getting the ID of a {{site.data.keyword.mon_short}} team](/docs/monitoring?topic=monitoring-team_id).


### Headers for {{site.data.keyword.mon_short}} Token
{: #mon-curl-headers-monitoring}

You can also use {{site.data.keyword.mon_short}} API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use the {{site.data.keyword.mon_short}} REST API to automate routine tasks and monitor notifications.

In a cURL command, add the following command option to authenticate with the {{site.data.keyword.mon_full_notm}} service by using a {{site.data.keyword.mon_short}} token:

```text
-H "Authorization: Bearer $SYSDIG_TOKEN"
```
{: codeblock}

To get the {{site.data.keyword.mon_short}} token, see [Getting the {{site.data.keyword.mon_short}} API token](/docs/monitoring?topic=monitoring-api_monitoring_token).



## Running a cURL API query
{: #mon-curl-query}

To run a cURL API query and authrnticat by using the IAM token, complete the following steps:

1. Set the IAM token.

    ```text
    AUTH_TOKEN=$(ibmcloud iam oauth-tokens | awk '{print $4}')
    ```
    {: codeblock}

2. Set the {{site.data.keyword.mon_full_notm}} instance GUID.

    ```text
    GUID=$(ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid')
    ```
    {: codeblock}

3. Run the cURL API query.

    ```text
    curl -X <METHOD> <MONITORING_ENDPOINT>/<API_URL> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "content-type: application/json"
    ```
    {: codeblock}


For example, to create an alert where the alert definition and notification channel is defined through a JSON file, you can run the following command:

```text
curl -X POST \
  https://us-south.monitoring.cloud.ibm.com/api/alerts \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @alert.json
```
{: screen}
