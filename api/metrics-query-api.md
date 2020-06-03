---

copyright:
  years:  2018, 2019, 2020
lastupdated: "2020-05-13"

keywords: Sysdig, IBM Cloud, monitoring, query, api

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

# Metric Query API Operations

## Working with cURL
{: #curl-guide}

```shell
curl -X <METHOD> <SYSDIG_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```

An example being:
```shell
curl -X POST \
  https://us-south.monitoring.test.cloud.ibm.com/api/data \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @metrics.json
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

To fetch metrics through API, use Sysdig's [Data APIs](https://sysdig.gitbooks.io/sysdig-cloud-api/content/rest_api/data.html) or Python sdc_client.

## Using Python client

```python

from sdcclient import IbmAuthHelper, SdMonitorClient

URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# You just need to specify the ID for keys, and ID with aggregation for values
metrics = [
    {"id": "cpu.used.percent", "aggregations": {"time": "timeAvg", "group": "avg"}}
]

# Data filter or None if you want to see "everything"
filter = None

# Time window:
#   - for "from A to B": start is equal to A, end is equal to B (expressed in seconds)
#   - for "last X seconds": start is equal to -X, end is equal to 0
start = -600
end = 0

# Sampling time:
#   - for time series: sampling is equal to the "width" of each data point (expressed in seconds)
#   - for aggregated data (similar to bar charts, pie charts, tables, etc.): sampling is equal to 0
sampling = 60

# Load data
ok, res = sdclient.get_data(metrics, start, end, sampling, filter=filter)
if ok:
    print(res)
```

Python examples can be found at:
    [Example 1](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_simple.py), [Example 2](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_advanced.py), and [Example 3](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_datasource.py).

## Using curl

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| POST | `api/data` | metrics.json |

Template metrics.json:

[Please refer this link](https://sysdig.gitbooks.io/sysdig-cloud-api/content/rest_api/data.html) for more details on usage of the below syntax.

```json
{
  "start": "Number: seconds",
  "end": "Number: seconds",
  "last": "Number: last available seconds",
  "metrics": [
    {
      "id": "<>",
      "aggregations": {}
    }
  ],
  "sampling": "Number: <10|60|600|3600|86400>",
  "dataSourceType": "<host|container>",
  "filter": "<>",
  "paging": {
    "from": "Number",
    "to": "Number"
  }
}
```

### Metrics dictionary

Metrics dictionary can contain all current default metrics supported by Sysdig.
For more details on metrics dictionary [please refer this link](https://docs.sysdig.com/en/metrics-dictionary.html).

Sysdig Monitor allows us to adjust the aggregation settings. [For more details refer this link](https://docs.sysdig.com/en/data-aggregation.html).

## Examples

### Retrieve platform metrics

This example is fetching platform metrics from Cloud Foundry!
"I want the instance ID, app container age, and number of bytes my app is using"
"I want the metrics only for us-south"
"I want metrics for the last 24 hours"

**Template metrics.json:**

```json
{
  "metrics": [
    {
      "id": "ibm_resource"
    },
    {
      "id": "ibm_cloudfoundry_app_container_age",
      "aggregations": {"group": "max", "time": "max"}
    },
    {
      "id": "ibm_cloudfoundry_app_memory_bytes_used",
      "aggregations": {"group": "avg", "time": "avg"}
    }
  ],
  "filter": "ibm_location = \"us-south\"",
  "sampling": 86400,
  "last": 86400
}
```

**Result for the above API call:**

```json
{
  "data": [
    {
      "d": [
        "73a9d202-7e97-45b2-a107-3b1528856be3",
        316660942465643,
        18809015.575
      ],
      "t": 1587772800
    }
  ],
  "end": 1587772800,
  "start": 1587686400
}
```

### CPU by Host with start, end, and, sampling

**Template metrics.json:**

```json
{
  "start":"1555404790",
  "end":"1555404850",
  "sampling": 10,
  "metrics": [
    {
      "id": "host.hostName"
    },
    {
      "id": "cpu.used.percent",
      "aggregations": {"time": "avg"}
    }
  ],
  "dataSourceType": "host"
}
```

**Result for the above API call:**

```json
{
  "data": [
    {
      "d": [
        "j-rhel71.fyre.ibm.com",
        3.621
      ],
      "t": 1555404800
    },
    {
      "d": [
        "j-rhel71.fyre.ibm.com",
        3.597
      ],
      "t": 1555404810
    },
    {
      "d": [
        "j-rhel71.fyre.ibm.com",
        3.993
      ],
      "t": 1555404820
    },
    {
      "d": [
        "j-rhel71.fyre.ibm.com",
        3.145
      ],
      "t": 1555404830
    },
    {
      "d": [
        "j-rhel71.fyre.ibm.com",
        4.09
      ],
      "t": 1555404840
    },
    {
      "d": [
        "j-rhel71.fyre.ibm.com",
        5.057
      ],
      "t": 1555404850
    }
  ],
  "end": 1555404850,
  "start": 1555404790
}
```
