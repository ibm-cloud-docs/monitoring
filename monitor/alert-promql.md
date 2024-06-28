---

copyright:
  years:  2018, 2024
lastupdated: "2024-06-28"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# PromQL alerts
{: #alert-promql}

{{site.data.keyword.mon_full_notm}} lets you to use PromQL to monitor and alert on changes in your infrastructure.
{: shortdesc}

## Defining a PromQL alert
{: #alert-promql-config}

When you define a PromQL alert you will need to specify the following:

Condition
:   Enter a valid PromQL expression. Unlike Metric Alerts, PromQL queries only return time series that meet the specified condition. For example, if you enter `sysdig_host_cpu_used_percent > 80`, only the hosts with CPU usage above 80% will be included in the query results. If all hosts are below this threshold, the query will return a *Resolved* state, which is the same as *No Data* state.

    Users might be confused determining whether an alert has truly been resolved or if the metric has disappeared and silently failed. This is because the *No Data* state in Prometheus cannot be distinguised from a resolved state. There are [strategies](#alert-promql-nodata) for dealing with No Data in Prometheus.
    {: note}

Duration
:   The duration is how long an alert condition must remain true before triggering an alert. PromQL aerts have three states: `Resolved`, `Pending`, and `Firing`. If a duration of 10m is set, it means that the alert condition must be consistently satisfied for a continuous period of 10 minutes before transitioning into the `Firing` state. Alerts whose expression is satisfied but haven’t met the required duration are in a `Pending` state.

Alert Resolution Delay
:   The Alert Resolution Delay is the same as `keep_firing_for` in Prometheus. This setting enables the continuous firing of an alert occurrence for a user-defined duration even after the alert condition is no longer valid. Alerts that tend to have intervals of `no-data` in the underlying metric can be configured with Alert Resolution Delay to prevent unnecessary noise and false resolutions. If the alert condition is once again met before the Alert Resolution Delay has elapsed, the alert will continue to trigger without needing to satisfy the duration again.

## Range and Duration
{: #alert-promql-range}

The duration of an alert is the length of time a specific condition must persist before triggering the alert. It should not be confused with the range of an alert, which defines the time period over which the relevant metric data is evaluated.

Consider the following examples:

```text
  rules:
  - alert: highNetworkTraffic1
    expr: avg(rate(network_bytes_total[1h])) > 10000000
    for: 5m
  - alert: highNetworkTraffic2
    expr: avg(rate(network_bytes_total[5m])) > 10000000
    for: 1h
```
{: codeblock}

The `highNetworkTraffic1` alert examines the average network transmittance over the previous hour. If this average exceeds 10MB for a continuous duration of 5 minutes, the alert is triggered.

On the other hand, `highNetworkTraffic2` focuses on the average network transmittance over the past 5 minutes. If this average exceeds 10MB for the last hour, the alert is triggered.

While using a longer duration can help reduce noisy alerts, it also means that some alerts may meet the threshold momentarily without triggering. There is a trade-off between suppressing noisy alerts and potentially delaying notifications for certain conditions.

## The differences between PromQL and Metric alerts
{: #alert-promql-metric}

PromQL alerts query the same metrics as metric alerts. The difference between the two alert types is in the evaluation algorithm.

| Metric alerts | PromQL alerts | 
| -------------- | -------------- |
| Native `No Data` support | `No Data` state is the same as `Resolved` state |
| Multithreshold Support |	Must create two alerts for multiple thresholds |
| No Duration |	Duration creates an additional `Pending` alert state |
| Queries return all the time series by default |	Queries only return time series that satisfy the alert query |
{: caption="Table 1. Differences between PromQL and Metric alerts" caption-side="bottom"}

## Handling No Data and multiple thresholds
{: #alert-promql-nodata}

To see the benefits of identifying `No Data` scenarios and configuring multiple thresholds, you can switch from a PromQL alert to a Metric Alert.

To create a Metric Alert handling `No Data` and multiple thresholds:

1. Create a new Metric Alert.
2. Switch the alert creation mode from **Form** to **PromQL**.
3. Continue configuring a Metric Alert using PromQL.
4. Optionally add a warning threshold and notify on `No Data`.


## Importing Prometheus alert rules
{: #alert-promql-import}

You can import Prometheus rules. Click the **Upload Prometheus Rules** option and enter the rules in YAML format in the **Upload Prometheus Rules** YAML editor. Importing your Prometheus alert rules will convert them to PromQL alerts.

Each alert rule must include the following mandatory fields:

* `alert`
* `expr`
* `for`

## Example: Prometheus crash looping alert
{: #alert-promql-ex1}

This alert detects potential restart loops on the `prometheus`, `pushgateway` or `alertmanager` jobs.

```text
groups:
- name: crashlooping
  rules:
  - alert: PrometheusTooManyRestarts
    expr: changes(process_start_time_seconds{job=~"prometheus|pushgateway|alertmanager"}[10m]) > 2
    for: 0m
    labels:
      severity: warning
    annotations:
      summary: Prometheus too many restarts (instance {{ $labels.instance }})
      description: Prometheus has restarted more than twice in the last 15 minutes. It might be crashlooping.\n  VALUE = {{ $value }}\n
```
{: #codeblock}

## Example: HTTP error rate alert
{: #alert-promql-ex2}

In this example `NginxHighHttp5xxErrorRate` detects an HTTP error rate of 5% or higher.

`NginxLatencyHigh` monitors the p99 latency for 3 seconds or higher for all hosts and nodes.

To alert HTTP requests with status 5xx (> 5%) or high latency:

```text
groups:
- name: default
  rules:
  - alert: NginxHighHttp5xxErrorRate
    expr: sum(rate(nginx_http_requests_total{status=~"^5.."}[1m])) / sum(rate(nginx_http_requests_total[1m])) * 100 > 5
    for: 1m
    labels:
      severity: critical
    annotations:
      summary: Nginx high HTTP 5xx error rate (instance {{ $labels.instance }})
      description: Too many HTTP requests with status 5xx
  - alert: NginxLatencyHigh
    expr: histogram_quantile(0.99, sum(rate(nginx_http_request_duration_seconds_bucket[2m])) by (host, node)) > 3
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Nginx latency high (instance {{ $labels.instance }})
      description: Nginx p99 latency is higher than 3 seconds
```
{: codeblock}

