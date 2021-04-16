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

# Extracting metrics from a {{site.data.keyword.mon_short}} instance by using the Monitoring API
{: #metrics_api}

You can extract metrics from an {{site.data.keyword.mon_full_notm}} instance by using the {site.data.keyword.mon_short}} API.
{:shortdesc}


## Get metrics by using cURL
{: #metrics_api-curl}

You can use the following [cURL command](/docs/monitoring?topic=monitoring-mon-curl) to get metrics:

```shell
curl -X POST <SYSDIG_REST_API_ENDPOINT>/data -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json" -d DATA
```
{: codeblock}

Where

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Monitoring REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `SysdigTeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).

* You can pass the file `metrics.json` to extract metrics by using `-d`, for example, `-d @metrics.json`.




The following sample shows a template for the `metrics.json` file:

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
{: #metrics_api-dictionary}

To see the pre-defefined metrics by Sysdig, see [Metrics dictionary](https://docs.sysdig.com/en/metrics-dictionary.html){: external}.

To see the pre-defined metrics that are defined by {{site.data.keyword.cloud_notm}} services that are Sysdig-enabled, see [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).


## Data aggregation
{: #metrics_api-aggregation}


To learn about data aggregation, see [Data Aggregation](https://docs.sysdig.com/en/data-aggregation.html){: external}.



## Sample: Extract platform metrics
{: #metrics_api-sample-platform}

This example shows how to extract platform metrics from Cloud Foundry in *us-south* for the last 24 hours.

```shell
curl -X POST https://us-south.monitoring.cloud.ibm.com/api/data -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "content-type: application/json" -d @metrics.json
```
{: codeblock}


The following example of the `metrics.json` file shows how to configure the file to extract data by instance ID, app container age, and number of bytes the app is using:

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
{: codeblock}

The result for extracting data returns the following information:

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
{: screen}

## Sample: Extract CPU data
{: #metrics_api-sample-cpu}

This example shows how to extract CPU data by host with start, end, and, sampling limit.

The following example of the `metrics.json` file shows how to configure the file to extract CPU data:

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
{: codeblock}

The result for extracting data returns the following information:

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
{: screen}

## Sample: cURL sample to extract latest metric
{: #metrics_api-sample-prom}

To get the latest value of a metric, specify only the metric name. The most recent value that was generated no more than 5 minutes ago is returned.

For instance, to get the latest value of `host_cpu_used_percent`:
```
curl https://app.sysdigcloud.com/prometheus/api/v1/query?query=sysdig_host_cpu_used_percent
```
{: pre}

All dashboards support the full PromQL API. For more information about what’s possible with PromQL, see the [Prometheus documentation](https://www.prometheus.io/docs/prometheus/latest/querying/api/){:external}.
{: note}


## Sample: cURL sample to extract CPU data for a team
{: #metrics_api-sample-cpu-1}

This example shows how to extract CPU data that is avaialable within the context of a team.

```shell
curl -X POST https://us-south.monitoring.cloud.ibm.com/api/data -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: 30785" -H "content-type: application/json" -d @metrics.json
```
{: codeblock}
