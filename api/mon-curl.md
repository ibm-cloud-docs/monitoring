---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-12"

keywords: Sysdig, IBM Cloud, monitoring, alerting, api, curl

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


# Using cURL to call the Sysdig API
{: #mon-curl}

You can use cURL from a terminal to make API calls to the {{site.data.keyword.mon_full_notm}} service.
{:shortdesc}

Use the following command from a terminal, to run a cURL command:

```shell
curl -X <METHOD> <SYSDIG_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```
{: pre}

Where

* `<METHOD>`
* `<SYSDIG-ENDPOINT>` must be replaced with the endpoint where the monitoring instance is available. For more inforamtion, see [Sysdig endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_sysdig). For example, the endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com`
* `<API_URL>`
* `HEADERS` 
* `DATA` 



## Headers for IAM Tokens (Recommended)
{: #mon-curl-headers-iam}


```shell
-H "Authorization: Bearer $AUTH_TOKEN"
-H "IBMInstanceID: $GUID"
```

* `AUTH_TOKEN=$(ibmcloud iam oauth-tokens | awk '{print $4}')`
* `GUID=$(ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid')`

## Headers for Sysdig Token
{: #mon-curl-headers-sysdig}


```shell
-H "Authorization: Bearer $SYSDIG_TOKEN"
```
* `SYSDIG_TOKEN` can be found in the Sysdig dashboard settings under Sysdig Monitor API


## Samples
{: #mon-curl-samples}

### Create an alert
{: #mon-curl-samples-alert}

For example, to create an alert where the alert definition and notification channel is defined through a JSON file, you can run the following command:

```shell
curl -X POST \
  https://us-south.monitoring.cloud.ibm.com/api/alerts \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @alert.json
```
{: screen}

### Create a dashboard
{: #mon-curl-samples-dashboard}

```shell
curl -X POST \
  https://us-south.monitoring.cloud.ibm.com/api/v2/dashboards \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @dashboard.json
```
{: screen}

### Get information on a downtime event
{: #mon-curl-samples-downtime-event}

```shell
curl -X POST \
  https://us-south.monitoring.cloud.ibm.com/api/downtimes \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @downtimes.json
```
{: screen}

### Create an alert
{: #mon-curl-samples-alert}

```shell
curl -X POST \
  https://us-south.monitoring.cloud.ibm.com/api/data \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @metrics.json
```
{: screen}


### List notification channels
{: #mon-curl-samples-alert}

```shell
curl -X POST \
  https://us-south.monitoring.cloud.ibm.com/api/notificationChannels \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @notification.json
```
{: screen}



