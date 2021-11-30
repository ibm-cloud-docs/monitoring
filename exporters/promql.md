---

copyright:
  years:  2018, 2021
lastupdated: "2021-04-14"

keywords: IBM Cloud, monitoring, panels

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Using PromQL
{: #promql}

Use the Prometheus Query Language (PromQL) to select and aggregate time-series metric data for Prometheus.
{: shortdesc}

For more information about PromQL, see the [open-source documentation](https://prometheus.io/docs/prometheus/latest/querying/basics/){: external}.

## Creating a PromQL query
{: #promql-query}

Create a PromQL query for a metric in an existing dashboard.
{: shortdesc}

1. From the [Monitoring dashboard](https://cloud.ibm.com/observe/monitoring){: external}, click **Open dashboard** for your service instance.
2. From **Dashboards**, select the dashboard that contains the metrics that you want to query.
3. For one panel in the dashboard, click the _edit_ icon.
4. Select the **PromQL** query type.
5. In the query form, enter _Display_ data, such as the query name and the timeseries name.
6. Enter your PromQL _Query_, such as `avg(avg_over_time(host_cpu_used_percent[$__interval])) by(kubernetes_cluster_name)`. Specify the following fields in your query:
    * Metric: Specify the metric that you want to query, such as `host_cpu_used_percent`. Note: The generated values on the table are the latest metric.
    * Time range: Specify a time range or time interval, such as `5m`. To use the time range that is selected in the UI, specify `$__range`. To use the time interval that is based on the time range that is selected in the UI, specify `$__interval`. The `$__range` and `$__interval` variables in this query automatically update as the time range is changed in the UI. For more information, see [Applying dashboard scopes to PromQL queries](#promql-scope).
    * Segmentation: Choose a value to segment the aggregated PromQL data, such as `kubernetes_cluster_name`.
7. Click **Run Query**.
8. Fine tune the results by configuring any additional _Options_, such as the units in which the data is returned and how the data is displayed.

## Applying dashboard scopes
{: #promql-scope}

To scope a panel built from a PromQL query, you must use a scope variable within the query.
{: shortdesc}

Two pre-defined variables exist for time-based scopes that you can specify in the query. These variables are automatically update as the time range for the dashed is changed in the UI.
* `$__range`: Represents the time frame that is selected in the dashboard UI. For example, you might use this variable to calculate an average for the selected time frame.
* `$__interval`: Represents the interval that is based on the time range that is selected in the dashboard UI. For example, you might use this variable to adapt the time range for different operations, such as the rate or average over time.

For example, say you use the following query to return the CPU used percent for all the hosts:

```text
avg_over_time(host_cpu_used_percent[$__interval])
```
{: codeblock}

This query uses the `$__interval` variable, which scopes data to the dynamic time interval based on the time range that is selected in the dashboard UI.

You can also specify your own variables in the query to scope its output. For example, to further scope the previous query to a specific label such as `hostname`, you must first [define a scope variable at the dashboard level](https://docs.sysdig.com/en/about-the-dashboard-ui.html#UUID-7a55e06a-7e2a-8dcb-7dd3-6d7eb39c9784_section-idm23184387629055){: external}. Then, you can specify that variable in the query:

```text
avg_over_time(host_cpu_used_percent{host_name=$hostname}[$__interval])
```
{: codeblock}

## Using labels
{: #promql-labels}

When you run PromQL queries, the data is returned with a minimum set of labels. To add more labels, such as a cluster name, use a vector matching operation.
{: shortdesc}

<!-- Prometheus returns [information metrics](https://docs.sysdig.com/en/mapping-between-classic-metrics-and-promql-metrics.html){: external} that have a value of 1 with several labels. -->

Prometheus returns information metrics that have a value of 1 with several labels. Joining the labels of an information metric with a non-information metric can provide useful insights, such as the value of a metric across an application. You can use a vector matching operation, which is similar to an SQL join, to add the information labels to your metric data.

### Example: Filtering an application metric by cluster
{: #promql-labels-ex-1}

In this example, a metric that is returned by an application is filtered by cluster. The PromQL aggregates a value of that metric for a cluster by having only one cluster selected in the scope.
{: shortdesc}

```text
sum (myapp_metric * on (container_id) kube_pod_container_info{cluster=$cluster})
```
{: codeblock}

This query:
* Filters the `kube_pod_container_info` information metric for only a specific cluster (`$cluster`, which is set as a dashboard variable) based on the `cluster` label and for a specific timeseries.
* Matches the `myapp_metric` non-information metric to the filtered `kube_pod_container_info` information metric when the `container_id` label has the same value. The values are multiplied, but because the information metric has a value of 1, the result is unchanged. The cluster label is added to the resulting data.
* Aggregates the timeseries of value `myapp_metric` by using the `sum` function, and returns the result.

### Example: Filtering average CPU used by account and region
{: #promql-labels-ex-2}

In this example, the average CPU used (percent) is calculated for a specific {{site.data.keyword.cloud_notm}} account and region.
{: shortdesc}

```text
avg by(region,account_id) (host_cpu_used_percent * on (host_mac) group_left(region,account_id) sysdig_cloud_provider_info{account_id=~$account, region=~$region})
```
{: codeblock}

This query:
* Filters the `sysdig_cloud_provider_info` information metric for only a specific region (`$region`) and account (`$account`) that are set as dashboard variables based on the `region` and `account_id` labels.
* Matches the `host_cpu_used_percent` non-information metric to the filtered `sysdig_cloud_provider_info` information metric when the `host_mac` label has the same value. The values are multiplied, but because the information metric has a value of 1, the result is unchanged. The region and account labels are added to the resulting data.
* Calculates the average of the new metrics by account and region.

## cURL sample to extract latest metric
{: #promql-latest-metric}

To get the latest value of a metric, specify only the metric name. The most recent value that was generated no more than 5 minutes ago is returned.

For instance, to get the latest value of `host_cpu_used_percent`:

```shell
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

