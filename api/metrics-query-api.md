---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-17"

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

# Extracting metrics from a Sysdig instance (DATA API)
{: #metrics-query-api}

You can extract metrics from an {{site.data.keyword.mon_full_notm}} instance through REST API operations that you can run by using a Python client or by using a cURL command.
{:shortdesc}

For more information about the Sysdig Meric Query API, see [Data APIs ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdig.gitbooks.io/sysdig-cloud-api/content/rest_api/data.html){:new_window}.


## Get metrics by using a Python client
{: #metrics-query-api-python}

To learn how to use the Python client, see [Using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client).

The following code shows the structure of a Python script that you can use to retrieve metrics from a Sysdig instance:


```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <SYSDIG-ENDPOINT> 
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client 
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Specify the ID for keys, and ID with aggregation for values
metrics = [
    {"id": "cpu.used.percent", "aggregations": {"time": "timeAvg", "group": "avg"}}
]

# Add a data filter or set to None if you want to see "everything"
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
{: codeblock}


You must include the following information: `<SYSDIG-ENDPOINT>`, `<IAM_APIKEY>`, and `<GUID>` These data is required to authenticate the request with the monitoring instance. To get the monitoring instance information, see [Authenticate your user or service ID by using IAM](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-python-client#python-client-iam-auth).


For Python examples, see any of the following examples:
* [Example 1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_simple.py){:new_window}: This  sample script  shows how to get data by creating a request that has no filter and no segmentation.
* [Example 2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_advanced.py){:new_window}: This sample script shows how to get data by creating a request that has a filter and segmentation.
* [Example 3 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_datasource.py){:new_window}: This sample script shows how to get data by creating a request where you specify the datasource.



## Get metrics by using cURL
{: #metrics-query-api-curl}

You can use the following [cURL command](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl) to create an alert:

```shell
curl -X POST <SYSDIG_REST_API_ENDPOINT>/data -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" [-d DATA]
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).

* You can pass data to extract metrics by using `-d`. 

    You can name the file `metrics.json`.
    

The following sample shows a sample `metrics.json` template:

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
{: codeblock}



## Metrics dictionary
{: #metrics-query-dictionary}

To see the pre-defefined metrics by Sysdig, see [Metrics dictionary ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.sysdig.com/en/metrics-dictionary.html){:new_window}.

To see the pre-defined metrics that are defined by {{site.data.keyword.cloud_notm}} services that are Sysdig-enabled, see [Cloud services](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-cloud_services). 


## Data aggregation
{: #metrics-query-aggregation}


To learn about data aggregation, see [Data Aggregation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.sysdig.com/en/data-aggregation.html){:new_window}.



## Sample: Extract platform metrics
{: #metrics-query-api-samples-platform}


This example shows how to extract platform metrics from Cloud Foundry in *us-south*.


```shell
curl -X POST https://us-south.monitoring.cloud.ibm.com/api/data -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" [-d DATA]
```
{: codeblock}


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
