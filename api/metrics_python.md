---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, query, api

subcollection: monitoring

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

# Extracting metrics from an instance by using the {{site.data.keyword.mon_short}} Python client
{: #metrics_python}

You can extract metrics from an {{site.data.keyword.mon_full_notm}} instance through REST API operations that you can run by using a Python client or by using a cURL command.
{:shortdesc}


## Get metrics by using a Python client
{: #metrics_python-py}

To learn how to use the Python client, see [Using the Python client](/docs/monitoring?topic=monitoring-python-client).

The following code shows the structure of a Python script that you can use to retrieve metrics from a {{site.data.keyword.mon_short}} instance:


```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <MONITORING-ENDPOINT> 
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


You must include the following information: `<MONITORING-ENDPOINT>`, `<IAM_APIKEY>`, and `<GUID>` These data is required to authenticate the request with the monitoring instance. To get the monitoring instance information, see [Authenticate your user or service ID by using IAM](/docs/monitoring?topic=monitoring-python-client#python-client-iam-auth).



## Samples
{: #metrics_python-samples}

For Python examples, see any of the following examples:
* [Example 1](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_simple.py){: external}: This  sample script  shows how to get data by creating a request that has no filter and no segmentation.

* [Example 2](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_advanced.py){: external}: This sample script shows how to get data by creating a request that has a filter and segmentation.

* [Example 3](https://github.com/draios/python-sdc-client/blob/master/examples/get_data_datasource.py){: external}: This sample script shows how to get data by creating a request where you specify the datasource.




## Metrics dictionary
{: #metrics_python-dictionary}

To see the pre-defined metrics, see [Metrics dictionary](https://docs.sysdig.com/en/metrics-dictionary.html){: external}.

To see the pre-defined metrics that are defined by {{site.data.keyword.cloud_notm}} services that are enabled for Monitoring, see [Cloud services](/docs/monitoring?topic=monitoring-cloud_services). 


## Data aggregation
{: #metrics_python-aggregation}


To learn about data aggregation, see [Data Aggregation](https://docs.sysdig.com/en/data-aggregation.html){: external}.

