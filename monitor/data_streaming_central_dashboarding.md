---
copyright:
  years:  2018, 2026
lastupdated: "2026-06-29"

keywords:

subcollection: monitoring
---

{{site.data.keyword.attribute-definition-list}}

# Centralizing metrics to another {{site.data.keyword.mon_full_notm}} instance
{: #data-streaming-central-dashboarding}

You can use {{site.data.keyword.mon_full}} to push a set of selected metrics to a different {{site.data.keyword.mon_full_notm}} instances.
{: shortdesc}

You will need to configure:

- The metrics to export within a defined scope. The metric names and scope are specified in PromQL format.

- The granularity of the data.

  For example, 10 seconds (10s) or 1 minute (1m). The recommended aggregation is 1m.

- The target {{site.data.keyword.mon_full_notm}} instance defining the Prometheus Remote Write URL of the  {{site.data.keyword.mon_full_notm}} region and the  {{site.data.keyword.mon_full_notm}} token.

This functionality is only configurable using the API.

## Prerequisites
{: #data-streaming-central-dashboarding-prereqs}

Check the following prerequisites before managing streaming:

- You need at least 2 {{site.data.keyword.mon_full_notm}} instances.
  - One instance will be the target for centralizing your metrics.
  - The other instances you will configure the streaming to the central instances.
- You need Admin permissions in the source {{site.data.keyword.mon_full_notm}} instances to be able to create metric streaming.
- You need to [get the Monitor API token](/docs/monitoring?topic=monitoring-api_monitoring_token) of the target instance.

## Managing streaming by using the API
{: #data-streaming-central-dashboarding-api}

Complete the following steps to manage streaming using the API.

### List the streaming configurations
{: #data-streaming-central-dashboarding-api-1}

Use this method to get the details for all the existing streaming configurations.

```text
curl --request GET https://<ENDPOINT>/api/v1/dataStream/configs
 -H "content-type: application/json"
 -H "Authorization: <TOKEN>"
```
{: pre}

Where

- `<ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Monitoring REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`
- `<TOKEN>` API token that you use to authenticate with the {{site.data.keyword.mon_short}} service. You must include `Bearer` with the token. For more information, see [Working with {{site.data.keyword.mon_short}} API tokens](/docs/monitoring?topic=monitoring-api_monitoring_token).

The response will be similar to the following:

```text
{"dataStreamConfigs":[{"uuid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx","enabled":true,"name":"Streaming metrics - demo","type":"prws"}]}
```
{: codeblock}

### Getting the details for a streaming configuration
{: #data-streaming-central-dashboarding-api-2}

Use this method to get the details for one streaming configuration.

```text
curl --request GET https://<ENDPOINT>/api/v1/dataStream/configs/<STREAMING_CONFIG_ID>
 -H "content-type: application/json"
 -H "Authorization: <TOKEN>"
```
{: pre}

Where

- `<ENDPOINT>` represents the endpoint that is targetted by the REST API call. For more information, see [Monitoring REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`
- `<TOKEN>` API token that you use to authenticate with the {{site.data.keyword.mon_short}} service. You must include `Bearer` with the token. For more information, see [Working with {{site.data.keyword.mon_short}} API tokens](/docs/monitoring?topic=monitoring-api_monitoring_token).
- `<STREAMING_CONFIG_ID>` represents the UUID of the streaming configuration for which you want to get details.

The response will be similar to the following:

```json
{
  "dataStreamConfig": {
    "uuid": "6b9a1b73-0aa2-42e8-a75c-5932ade194d6",
    "enabled": true,
    "name": "event stream",
    "emitterType": "prws",
    "emitterProperties": {
      "url": "https://ingest.prws.us-south.monitoring.cloud.ibm.com/prometheus/remote/write",
      "bearer_token": "authentication token"
    }
  },
  "dataStreamRules": [
    {
      "uuid": "17811423-ab0b-44d0-be34-f78dd3438fa1",
      "enabled": true,
      "metrics": ["sysdig_host_cpu_used_percent"],
      "additionalLabels": {
        "custom_label_1": "label_value_1",
        "custom_label_2": "label_value_2"
      },
      "keepLabels": [
        "kube_deployment_status_replicas_available",
        "kube_daemonset_status_number_ready"
      ],
      "aggregation": "max",
      "aggregationSec": 60,
      "scope": "kube_cluster_name != 'my-cluster'",
      "dataStreamConfigUuid": "6b9a1b73-0aa2-42e8-a75c-5932ade194d6"
    }
  ]
}
```
{: codeblock}

### Creating a streaming configuration
{: #data-streaming-central-dashboarding-api-3}

Use this method to configure one streaming configuration that forwards a set of metrics to a different {{site.data.keyword.mon_full_notm}} instance.

```text
curl --request POST https://<ENDPOINT>/api/v1/dataStream/configs
 -H "content-type: application/json"
 -H "Authorization: <TOKEN>"
 -d @streaming-config.json
```
{: pre}

Where

- `<ENDPOINT>` represents the endpoint that is targetted by the REST API call. For more information, see [Monitoring REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`
- `<TOKEN>` API token that you use to authenticate with the {{site.data.keyword.mon_short}} service. You must include `Bearer` with the token. For more information, see [Working with {{site.data.keyword.mon_short}} API tokens](/docs/monitoring?topic=monitoring-api_monitoring_token).

A sample `streaming-config.json` file is similar to the following:

```json
{
  "dataStreamConfig": {
    "uuid": "6b9a1b73-0aa2-42e8-a75c-5932ade194d6",
    "enabled": true,
    "name": "event stream",
    "emitterType": "prws",
    "emitterProperties": {
      "url": "https://ingest.prws.us-south.monitoring.cloud.ibm.com/prometheus/remote/write",
      "bearer_token": "authentication token"
    }
  },
  "dataStreamRules": [
    {
      "uuid": "17811423-ab0b-44d0-be34-f78dd3438fa1",
      "enabled": true,
      "metrics": ["sysdig_host_cpu_used_percent"],
      "additionalLabels": {
        "custom_label_1": "label_value_1",
        "custom_label_2": "label_value_2"
      },
      "keepLabels": [
        "kube_deployment_status_replicas_available",
        "kube_daemonset_status_number_ready"
      ],
      "aggregation": "max",
      "aggregationSec": 60,
      "scope": "kube_cluster_name != 'my-cluster'",
      "dataStreamConfigUuid": "6b9a1b73-0aa2-42e8-a75c-5932ade194d6"
    }
  ]
}
```
{: codeblock}

Where:

- `emitterType`: This needs to be `prws`. Sending to Kafka (using `kafka`) is also supported.
- `emittedProperties`: Configure the [Remote Write endpoint](/docs/monitoring?topic=monitoring-prometheus_remote_write#prometheus_remote_write_endpoints) for the region and the [Monitoring API Token](/docs/monitoring?topic=monitoring-api_monitoring_token) where you have your target{{site.data.keyword.mon_full_notm}} instance.
- `dataStreamRules.metrics`: Configure the list of metrics to stream.
- `dataStreamRules.additionalLabels`: Configure a list of labels that will be attached to all emitted time-series.
- `dataStreamRules.keepLabels`: Any label that is part of the product that you want to include when sending the metrics to the central target {{site.data.keyword.mon_full_notm}} instance. {{site.data.keyword.mon_full_notm}} does not send all labels part of the metrics to reduce the load.
- `dataStreamRules.scope`: Define the scope of the time-series to emit.
- `dataStreamRules.aggregation`: Specify `avg`, `max`, `min` or `sum` to select which aggregation you want to do in the 1 minute aggregation of your time-series.

### Updating a streaming configuration
{: #data-streaming-central-dashboarding-api-4}

You need to update a streaming configuration in the following siuations:

- The API key to authenticate with {{site.data.keyword.mon_full_notm}} is rotated, compromissed, or needs changing.
- When you want to change the metrics that you stream, by either adding new metrics or removing metrics.
- When you need to change the scope.
- When you need to enable or disable data streaming for the configuration.

Use this method to update one streaming configuration that forwards a set of metrics to another {{site.data.keyword.mon_full_notm}} instance.

```text
curl --request PUT https://<ENDPOINT>/api/v1/dataStream/configs/<STREAMING_CONFIG_ID>
 -H "content-type: application/json"
 -H "Authorization: <TOKEN>"
 -d @streaming-config.json
```
{: pre}

Where

- `<ENDPOINT>` represents the endpoint that is targetted by the REST API call. For more information, see [Monitoring REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`
- `<TOKEN>` API token that you use to authenticate with the {{site.data.keyword.mon_short}} service. You must include `Bearer` with the token. For more information, see [Working with {{site.data.keyword.mon_short}} API tokens](/docs/monitoring?topic=monitoring-api_monitoring_token).
- `<STREAMING_CONFIG_ID>` represents the UUID of the streaming configuration.

A sample `streaming-config.json` file is similar to the following:

```json
{
  "dataStreamConfig": {
    "uuid": "6b9a1b73-0aa2-42e8-a75c-5932ade194d6",
    "enabled": true,
    "name": "event stream",
    "emitterType": "prws",
    "emitterProperties": {
      "url": "https://ingest.prws.us-south.monitoring.cloud.ibm.com/prometheus/remote/write",
      "bearer_token": "authentication token"
    }
  },
  "dataStreamRules": [
    {
      "uuid": "17811423-ab0b-44d0-be34-f78dd3438fa1",
      "enabled": true,
      "metrics": ["sysdig_host_cpu_used_percent"],
      "additionalLabels": {
        "custom_label_1": "label_value_1",
        "custom_label_2": "label_value_2",
        "custom_label_3": "label_value_3"
      },
      "keepLabels": [
        "kube_deployment_status_replicas_available",
        "kube_daemonset_status_number_ready"
      ],
      "aggregation": "max",
      "aggregationSec": 60,
      "scope": "kube_cluster_name != 'my-cluster'",
      "dataStreamConfigUuid": "6b9a1b73-0aa2-42e8-a75c-5932ade194d6"
    }
  ]
}
```
{: codeblock}

### Deleting a streaming configuration
{: #data-streaming-central-dashboarding-api-5}

Use this method to delete one streaming configuration that forwards a set of metrics to a central {{site.data.keyword.mon_full_notm}} instance.

```text
curl --request DELETE https://<ENDPOINT>/api/v1/dataStream/configs/<STREAMING_CONFIG_ID>
 -H "content-type: application/json"
 -H "Authorization: <TOKEN>"
```
{: pre}

Where

- `<ENDPOINT>` represents the endpoint that is targetted by the REST API call. For more information, see [Monitoring REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`
- `<TOKEN>` API token that you use to authenticate with the {{site.data.keyword.mon_short}} service. You must include `Bearer` with the token. For more information, see [Working with {{site.data.keyword.mon_short}} API tokens](/docs/monitoring?topic=monitoring-api_monitoring_token).
- `<STREAMING_CONFIG_ID>` represents the UUID of the streaming configuration.
