---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, query, api

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Extracting metrics from a {{site.data.keyword.mon_short}} instance by using the Monitoring API
{: #metrics_api}

You can extract metrics from an {{site.data.keyword.mon_full_notm}} instance by using the {site.data.keyword.mon_short}} API.
{: shortdesc}


## Get metrics by using cURL
{: #metrics-api-curl}

You can use the following [cURL command](/docs/monitoring?topic=monitoring-mon-curl) to get metrics:

```text
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
{: #metrics-api-dictionary}

To see the pre-defefined metrics by Sysdig, see [Metrics dictionary](https://docs.sysdig.com/en/metrics-dictionary.html){: external}.

To see the pre-defined metrics that are defined by {{site.data.keyword.cloud_notm}} services that are Sysdig-enabled, see [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).


## Data aggregation
{: #metrics-api-aggregation}


To learn about data aggregation, see [Data Aggregation](https://docs.sysdig.com/en/data-aggregation.html){: external}.



## Sample: Extract platform metrics
{: #metrics-api-sample-platform}

This example shows how to extract platform metrics from Cloud Foundry in *us-south* for the last 24 hours.

```text
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
{: #metrics-api-sample-cpu}

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
{: #metrics-api-sample-prom}

To get the latest value of a metric, specify only the metric name. The most recent value that was generated no more than 5 minutes ago is returned.

For instance, to get the latest value of `host_cpu_used_percent`:

```text
curl <SYSDIG_REST_API_ENDPOINT>/prometheus/api/v1/query?query=sysdig_host_cpu_used_percent -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where

* `<SYSDIG_REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [Monitoring REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `SysdigTeamID` is optional. When you specify this header, you limit the request to the data and resources available for the team specified.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).


All dashboards support the full PromQL API. For more information about what’s possible with PromQL, see the [Prometheus documentation](https://www.prometheus.io/docs/prometheus/latest/querying/api/){: external}.
{: note}

## Sample: cURL sample to extract CPU data for a team
{: #metrics-api-sample-cpu-1}

This example shows how to extract CPU data that is available within the context of a team.

```text
curl -X POST https://us-south.monitoring.cloud.ibm.com/api/data -H "Authorization: Bearer $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: 30785" -H "content-type: application/json" -d @metrics.json
```
{: codeblock}

## Sample: Extract metric data from {{site.data.keyword.mon_short}} to {{site.data.keyword.messagehub}}
{: #sample-metrics-code}

You can use the following code example to extract metrics from your {{site.data.keyword.mon_short}} instance to {{site.data.keyword.messagehub}}.
{: shortdesc}

* Replace `<region>` with the region of your {{site.data.keyword.mon_short}} instance, such as `us-east`.
* Replace `<apikey>` with an {{site.data.keyword.cloud_notm}} [IAM API key token](/docs/monitoring?topic=monitoring-api_token).
* Replace `<instance_id>` with the ID of your {{site.data.keyword.mon_short}} instance.
* Replace the `metrics` field with the JSON array of metrics that you want to extract. The example metric is `cpu.cores.used`.

```text
from sdcclient import IbmAuthHelper, SdMonitorClient
endpoint = "https://<region>.monitoring.cloud.ibm.com"
apikey = "<apikey>"
instanceID = "<instance_id>"
ibm_headers = IbmAuthHelper.get_headers(endpoint, apikey, instanceID)
sdclient = SdMonitorClient(sdc_url=endpoint, custom_headers=ibm_headers)
metrics = [
    {
    "id": "cpu.cores.used",
    "aggregations": {
        "time": "avg",
        "group": "sum"
    }
    }
]
filter = None
start = -120
end = 0
sampling = 60
ok, res = sdclient.get_data(metrics, start, end, sampling, filter=filter, datasource_type = "container")
print(ok)
print(res)
return res
```
{: codeblock}

## Sample: Extract notifications from {{site.data.keyword.mon_short}} to {{site.data.keyword.messagehub}} with the {{site.data.keyword.messagehub}} REST API
{: #sample-extract-notifications}

1. [Create an {{site.data.keyword.messagehub}} instance](/docs/EventStreams?topic=EventStreams-getting_started).
    * From the pricing plans, select an **Enterprise Plan**.
    * If necessary, set up an [Authorization in IAM](https://cloud.ibm.com/iam/authorizations){: external} for {{site.data.keyword.messagehub}} to target a KMS provider such as {{site.data.keyword.keymanagementserviceshort}}, and refresh the page.
    * For the **Service Endpoint**, select an option with a **Private** network.
2. Wait a few minutes for your {{site.data.keyword.messagehub}} instance to provision.
3. In your {{site.data.keyword.messagehub}} instance, [create a topic](/docs/EventStreams?topic=EventStreams-getting_started#getting_started_steps), such as `kafka-java-console-sample-topic`.
4. Create a service key for credentials to your {{site.data.keyword.messagehub}} instance on the private cloud service endpoint.

    * `<name>`: Enter a name for the service key.
    * `<event_streams_instance>`: Replace with the name of your {{site.data.keyword.messagehub}} instance.

    ```text
    ibmcloud resource service-key-create <name> Writer --instance-name <event_streams_instance> --service-endpoint private
    ```
    {: pre}

5. In the output of the previous command, get the details that you need to make a REST call.
    * `api_key`
    * `kafka_http_url`

    Example output:

    ```text
    api_key:      123465123456123465123465123465123465
    kafka_http_url:           https://mh-<id>.private.us-south.messagehub.appdomain.cloud
    ```
    {: screen}

6. From the [{{site.data.keyword.mon_short}} dashboard](https://cloud.ibm.com/observe/monitoring){: external}, click **Open dashboard** for the {{site.data.keyword.mon_short}} instance that you want to use. 
7. Click **Get Started > Configure a notification channel > Configure Notification Channel**. The **Settings** page opens.
8. Click **+ Add Notification Channel** and select the **Webhook** option.
9. Configure the webhook notification channel. After you create the webhook notification channel, you must continue to set up authentication for the channel.
    * For **URL**, enter the `kafka_http_url` from the service key, and append the `/topics/<topic>/records` route to the URL. The `<topic>` is the name of the topic that you created in your {{site.data.keyword.messagehub}} instance.
    * For **Name**, enter a name for the webhook notification channel.
    * Leave the other fields at the default settings.
    * Click **Save** to create the channel.
10. [Get an IAM token](/docs/monitoring?topic=monitoring-api_token) to authenticate your requests to the {{site.data.keyword.mon_short}} API.
11. Curl the {{site.data.keyword.mon_short}} API to list the notification channels. 
    * Replace `<region>` with the region of your {{site.data.keyword.mon_short}} instance, such as `us-east`.
    * Replace `<token>` with the IAM token that you previously retrieved. 
    
    ```text
    curl ’https://<region>.monitoring.cloud.ibm.com/api/notificationChannels' --header ‘Authorization: Bearer <token>’ | jq 
    ```
    {: pre}

    In the output, note the `id` of the notification channel where the `options.url` field matches the **URL** that you previously created.

    ```json
     {
         "id": 123,
         "version": 6,
         ...
         "options": {
             "notifyOnOk": true,
             "url": "https://mh-<id>.private.us-south.messagehub.appdomain.cloud",
             "notifyOnResolve": true
         }
     },
    ```
    {: screen}

12. Curl the {{site.data.keyword.mon_short}} API to add the authentication header to the webhook notification channel.
    * Replace `<region>` with the region of your {{site.data.keyword.mon_short}} instance, such as `us-east`.
    * Replace `<id>` with the ID of the notification channel that you previously retrieved.
    * Replace `<token>` with the IAM token that you previously retrieved.

    ```text
    curl -X PUT ’https://<region>.monitoring.cloud.ibm.com/api/notificationChannels/<id>' \
    --header ‘Content-Type: application/json’ 
    --header ‘Authorization: Bearer <token>’ -d @/tmp/notification.json
    ```
    {: pre}

13. Curl the {{site.data.keyword.mon_short}} API again to confirm that the notification channel is updated with the authentication header. 
    * Replace `<region>` with the region of your {{site.data.keyword.mon_short}} instance, such as `us-east`.
    * Replace `<token>` with the IAM token that you previously retrieved. 
    
    ```text
    curl ’https://<region>.monitoring.cloud.ibm.com/api/notificationChannels' --header ‘Authorization: Bearer <token>’ | jq 
    ```
    {: pre}

    In the output, note the `additionalHeaders.X-Auth-Token` field is added to the notification channel.

    ```json
    {
    "notificationChannel":
        {
            "id": 123,
            ....
            "options": {
                "notifyOnOk": true,
                "url": "https://mh-<id>.private.us-south.messagehub.appdomain.cloud/topics/kafka-java-console-sample-topic/records",
                "notifyOnResolve": true,
                "additionalHeaders": {
                    "X-Auth-Token": "123456123456123456123456123465123456"
        ...
    ```
    {: screen}
    
14. [Set up an alert](/docs/monitoring?topic=monitoring-alerts) that uses the webhook notification channel that you created for {{site.data.keyword.messagehub}}. 

Now, when an alert is triggered from {{site.data.keyword.messagehub}}, you can review the details in your {{site.data.keyword.mon_short}} instance.
