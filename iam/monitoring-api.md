---

copyright:
  years: 2018, 2021
lastupdated: "2021-03-19"

keywords: monitoring, sysdig, api

subcollection: Monitoring-with-Sysdig

content-type: api-docs

title: Monitoring with Sysdig API Reference

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:generic: .ph data-hd-programlang='generic'}
{:java: .ph data-hd-programlang='java'}
{:ruby: .ph data-hd-programlang='ruby'}
{:c#: .ph data-hd-programlang='c#'}
{:objectc: .ph data-hd-programlang='Objective C'}
{:python: .ph data-hd-programlang='python'}
{:node: .ph data-hd-programlang='node'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}
{:curl: .ph data-hd-programlang='curl'}
{:node: .ph data-hd-programlang='node'}
{:middle: .ph data-hd-position='middle'}
{:right: .ph data-hd-position='right'}

# Introduction

{{site.data.keyword.mon_full}} is a cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. In architectures that are focused on container and microservices, you can use *Sysdig Secure* to protect, monitor, and enhance forensic analysis of your pipeline and runtime components. For details about using {{site.data.keyword.mon_full_notm}}, see the {{site.data.keyword.cloud_notm}} [docs](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started#getting-started).

You can use the {{site.data.keyword.mon_short}} API to manage dashboards, alerts, and teams. For more information, see the following documentation:
- [Managing dashboards by using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-dashboard_python)
- [Managing alerts by using the Alerts API](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alert_api)
- [Managing alerts by using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alert_python)

You can use any of the following methods to manage the {{site.data.keyword.mon_short}} service:
- Python Client: You can use the Python client to manage the {{site.data.keyword.mon_short}} service. The client is also known as the sdcclient. For more information, see [Using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client).
- cURL: You can use cURL, a command line tool, from a terminal to manage the {{site.data.keyword.mon_short}} service by using URL syntax. For more information, see [Using cURL](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl).


## Curl example
{: curl}
{: right}

Use the following syntax from a terminal to run a cURL command:

```shell
curl -X <METHOD> <ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```
{: pre}

Where

* `<METHOD>` indicates the type of REST API call that you want to make.
* `<ENDPOINT>` indicates the endpoint where the monitoring instance is available. For more information, see [Monitoring endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_sysdig). For example, the endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com`
* `<API_URL>` For more information about API URLs, see [Monitoring REST APIs](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-rest_apis).
* `HEADERS` add additional information such as information to authenticate with the {{site.data.keyword.mon_full_notm}} service.
* `DATA` allows you to pass additional information that might be required.

## Python example
{: python}
{: right}

The code examples on this tab use the client library that is provided for Python.

```python
import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <ENDPOINT_URL> <API_KEY> <INSTANCE_GUID>' % sys.argv[0])
   print('ENDPOINT_URL: IBM Cloud endpoint URL (e.g. https://us-south.monitoring.cloud.ibm.com')
   print('API_KEY: IBM Cloud IAM API key. This key is used to retrieve an IAM access token.')
   print('INSTANCE_GUID: GUID of an IBM Cloud Monitoring with Sysdig instance.')
   sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]


# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)
```


# Endpoint URL

You can use public and private endpoints. To find out about the available endpoints, see [REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api).

The endpoint for the {{site.data.keyword.mon_full_notm}} API is in the format: `https://{DomainName}.monitoring.cloud.ibm.com/api` For example, the API endpoint for Dallas is: `https://us-south.monitoring.cloud.ibm.com/api` 


## Curl endpoint request
{: curl}
{: right}

Example request to a Dallas endpoint:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/api/alerts/<ALERT_ID> -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json"
```

Replace `<ALERT_ID>`, `AUTH_TOKEN`, `GUID` and `TEAM_ID` in this example with the values for your particular API call.


## Python endpoint request
{: python}
{: right}

Example request to a Dallas endpoint

```python
import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <ENDPOINT_URL> <API_KEY> <INSTANCE_GUID>' % sys.argv[0])
   print('ENDPOINT_URL: IBM Cloud endpoint URL (e.g. https://us-south.monitoring.cloud.ibm.com')
   print('API_KEY: IBM Cloud IAM API key. This key is used to retrieve an IAM access token.')
   print('INSTANCE_GUID: GUID of an IBM Cloud Monitoring with Sysdig instance.')
   sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]


# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)
```


# Authentication

Access to {{site.data.keyword.mon_full_notm}} is controlled by using {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM), which provides a unified approach to managing user identities and access control across your {{site.data.keyword.cloud_notm}} services and applications.

This API requires {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} (IAM) authentication. You must pass an IAM token in the Authorization header of the request. You can retrieve your IAM access token, which is prefixed with `Bearer`, by running the [ibmcloud iam oauth-tokens](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_oauth_tokens) command. You must also set the Account header to the unique ID for your {{site.data.keyword.cloud_notm}} account. You can retrieve your Account ID by running the [ibmcloud account show](/docs/cli?topic=cloud-cli-ibmcloud_commands_account#ibmcloud_account_show) command.

To call each method, you must be assigned a role that includes the required IAM actions. Each method lists the associated action. For more information about IAM actions and how they map to roles, see [Managing access for {{site.datatm.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-iam).
12qw

### Authentication when using cURL

In a cURL command, add the following headers to authenticate with the {{site.data.keyword.mon_full_notm}} service by using an IAM token:

```shell
-H "Authorization: $AUTH_TOKEN"
-H "IBMInstanceID: $GUID"
-H "TeamID: $TEAM_ID"
```
{: codeblock}

Where

* `IBMInstanceID` indicates the GUID of the {{site.data.keyword.mon_full_notm}} instance that you want to target with the cURL command. 

    To get the GUID of the monitoring instance, run the following command: `ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid'`

* `Authorization` indicates the IAM token that is used to authenticate with the {{site.data.keyword.mon_full_notm}} service instance.

    To get the IAM `AUTH_TOKEN` token, run the following command: `ibmcloud iam oauth-tokens | awk '{print $4}'`
    
    For more information, see [Getting the IAM API token](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-api_token#api_iam_token_get). 

* `TeamID` indicates the GUID of a team.

    To get the GUID, see [Getting the ID of a team](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-team_id).

### Authentication when using Python

To use {{site.data.keyword.cloud_notm}} IAM authentication with the Python client, you must specify an endpoint, an API key, and the GUID from your {{site.data.keyword.mon_full_notm}} instance.
{: note}

Complete the following steps from a terminal:

1. Get the GUID of your {{site.data.keyword.mon_full_notm}} instance. Run the following command:

    ```
    ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid'
    ```
    {: pre}

2. Get the API key. Run the following command to generate a user API key:

    ```
    ibmcloud iam api-key-create KEY_NAME
    ```
    {: pre}

3. Get the [endpoint](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_sysdig) for the region where the monitoring instance is available. 

4. Add the following entries to your Python script:

    ```python
    from sdcclient import IbmAuthHelper, SdMonitorClient

    URL = <ENDPOINT>
    # For example: URL = 'https://us-south.monitoring.cloud.ibm.com'

    APIKEY = <IAM_APIKEY>

    GUID = <GUID>

    ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
    sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)
    ```
    {: codeblock}

    Where

    `<ENDPOINT>` must be replaced with the endpoint where the monitoring instance is available. 

    `<IAM_APIKEY>` must be replaced with a valid IAM API key. [Learn more](/docs/account?topic=account-userapikey).

    `<GUID>` must be replaced with the GUID of the monitoring instance that you obtain in the previous step. 


You can now use the **sdclient** to perform actions that will be authenticated by using IAM.


If you get the error `400 Client Error: Bad Request for url: https://iam.cloud.ibm.com/identity/token`, check the API key. The value that you are passing is not valid.
{: note}

# Auditing

You can monitor API activity within your account by using the {{site.data.keyword.at_full_notm}} service. Whenever an API method is called, an event is generated that you can then track and audit from within {{site.data.keyword.at_short}}. The specific event type is listed for each individual method. 
For more information about how to track {{site.data.keyword.mon_full_notm}} activity, see [Auditing the events for {{site.datatm.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-at_events).


# Error handling

The {{site.data.keyword.mon_full_notm}} service uses standard HTTP response codes to indicate whether a method completed successfully. 
- A `200` response always indicates success. 
- A `400` type response indicates a failure. 
- A `500` type response usually indicates an internal system error.

| HTTP Error Code | Description           |
|-----------------|-----------------------|
| `200`           | Success               |
| `201`           | Success </br>E.g. Dashboard successfully created |
| `400`           | Bad Request           |
| `401`           | Unauthorized          |
| `403`           | Forbidden             |
| `404`           | Not Found </br>E.g. Dashboard V3 not active            |
| `422`           | Validation error, reason stated in the response body |
| `500`           | Internal Server Error |



