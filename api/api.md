---

copyright:
  years:  2018, 2019, 2020
lastupdated: "2020-05-13"

keywords: Sysdig, IBM Cloud, monitoring, api

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

# Using Sysdig APIs

[Before you start, see Working With API Tokens](/docs/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)

**Sysdig documentation**
- [Sysdig REST API Conventions](https://docs.sysdig.com/en/sysdig-rest-api-conventions.html)

## Prerequisites for Using the API
{: #prerequisites}

- The Sysdig endpoint, `<SYSDIG-ENDPOINT>`, is the Sysdig domain used to view the UI. Ex: us-south.monitoring.test.cloud.ibm.com
    - [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_sysdig)
- The recommended authentication method is IAM; to use it you will need an API key and an IBM Cloud Monitoring with Sysdig instance

## Working with cURL
{: #curl-guide}

```shell
curl -X <METHOD> <SYSDIG_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```

An example being:
```shell
curl -X GET \
  https://us-south.monitoring.cloud.ibm.com/api/v2/dashboards \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json'
```

* [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_sysdig)

**Headers for IAM Tokens (Recommended)**:
```shell
-H "Authorization: Bearer $AUTH_TOKEN"
-H "IBMInstanceID: $GUID"
```
* `AUTH_TOKEN=$(ibmcloud iam oauth-tokens | awk '{print $4}')`
* `GUID=$(ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid')`

**Headers for Sysdig Token**:
```shell
-H "Authorization: Bearer $SYSDIG_TOKEN"
```
* `SYSDIG_TOKEN` can be found in the Sysdig dashboard settings under Sysdig Monitor API

## Python Client 
{: #python-client}

Sysdig's [Python Client](https://github.com/draios/python-sdc-client) is preferred for programmatic operations due to its ease of use and vendor support.

### Install Using pip
{: #install-pip}

```shell
# sddclient version must be at least 0.9.0
pip install sdcclient
```

Then from your application, reference the pip package via the import from `sdcclient`:

```python
from sdcclient import IbmAuthHelper, SdMonitorClient
```

### Install From GitHub
{: #install-github}

1. Make a folder for client usage and enter it
```shell
mkdir python-client && cd python-client
```

2. Clone the repository
```shell
git clone https://github.com/draios/python-sdc-client.git
```

3. Create a Python script and `ls` should show the following:
```shell
touch script.py
```

4. Confirm the contents of the folder:
```shell
ls
# python-sdc-client/ script.py
```

5. Import the cloned package into your Python script:
```python
import sys
sys.path.append("python-sdc-client")
from sdcclient import IbmAuthHelper, SdMonitorClient
```

### Authenticate using IAM
{: #iam-auth}

To use IBM Cloud IAM authentication with the Python client you will need the Sysdig endpoint, an API key, and the GUID from your IBM Cloud Monitoring with Sysdig instance.

```python
from sdcclient import IbmAuthHelper, SdMonitorClient

URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)
# You can now use sdclient to perform actions that will be authenticated using IAM
```

- `GUID` can be found using `ibmcloud resource service-instance <NAME>`

## cURL/Python Working Examples

- [Dashboard API Operations](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-dashboard-api-operations)
- [Alerting API Operations](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alerting-api-operations)
- [Notification API Operations](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-notification-api-operations)
- [Metric Query API Operations](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-metric-query-api-operations)
- [Downtimes API Operations](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-downtimes-api-operations)
