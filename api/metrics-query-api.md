---

copyright:
  years:  2018, 2019
lastupdated: "2019-06-11"

keywords: Sysdig, IBM Cloud, monitoring, query, api

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

* [Sysdig endpoints](https://test.cloud.ibm.com/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_sysdig)

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

```json
{
  "start": <>,
  "end": <>,
  "metrics": [
    {
      "id": <>,
      "aggregations": <>,
      ...
    }
  ],
  "sampling": <>,
  "data": <>,
  "dataSourceType": <HOST/CONTAINER>,
  "last": <>,
  "filter": <>,
  "sampling": <>
}
```

Please refer this [link](https://sysdig.gitbooks.io/sysdig-cloud-api/content/rest_api/data.html) for more details on usage of the above syntax.

### Metrics dictionary

Metrics dictionary can contain all current default metrics supported by Sysdig.
For more details on metrics dictionary please refer this [link](https://docs.sysdig.com/en/metrics-dictionary.html).

Sysdig Monitor allows us to adjust the aggregation settings. For more details refer this [link](https://docs.sysdig.com/en/data-aggregation.html).

## Examples

### CPU by host

Template metrics.json:

```json
{
  "metrics": [
    {
      "id": "host.hostName"
    },
    {
      "id": "cpu.used.percent",
      "aggregations": {"group": "avg", "time": "avg"}
    }
  ],
  "dataSourceType": "host",
  "last": 600
}
```

- Here datasource type is `Host`

Result for the above API call:

```json
{
  "data": [
    {"d": ["jupiter-vm781", 52.062]},
    {"d": ["jupiter-vm853", 4.245]}
  ],
  "start": 1553071030,
  "end": 1553071630
}
```

### CPU by container

Template metrics.json:

```json
{
  "metrics": [
    {
      "id": "container.name"
    },
    {
      "id": "cpu.used.percent",
      "aggregations": {
        "group": "avg",
        "time": "avg"
      }
    }
  ],
  "dataSourceType": "container",
  "last": 600
}
```

- Here datasource type is `Container`

Result for the above API call:

```json
{
  "data": [
    {"d": ["sysdig-agent", 1.586]},
    {"d": ["Container_1", 0.905]},
    {"d": ["Container_2", 0.893]},
    {"d": ["Container_3", 0.892]},
    {"d": ["Container_4", 0.886]},
    {"d": ["Container_5", 0.885]},
    {"d": ["Container_6", 0.873]}
  ],
  "start": 1553074770,
  "end": 1553075370
}
```

### CPU by Host with start and end time

Template metrics.json:

```json
{
  "start": "1533078521",
  "end": "1553078521",
  "metrics": [
    {
      "id": "host.hostName"
    },
    {
      "id": "cpu.used.percent",
      "aggregations": {"group": "avg", "time": "avg"}
    }
  ],
  "dataSourceType": "host"
}
```

- Here `last` field is not required as we have used `start` and `end`

Result for the above API call:

```json
{
  "data": [
    {"d": ["jupiter-vm376", 38.453]},
    {"d": ["jupiter-vm853", 9.853]}
  ],
  "start": 1532995200, "end": 1553040000
}
```

### CPU by Host with start, end time and sampling

Template metrics.json:

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

- Here `sampling` field is to fetch sampled data for the given time period.
- Valid options for `sampling` are 10, 60, 600, 3600, 86400 seconds.

Result for the above API call:

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
