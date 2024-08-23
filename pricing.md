---

copyright:
  years:  2018, 2024
lastupdated: "2024-08-23"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Pricing
{: #pricing_plans}

This topic includes information about pricing for the {{site.data.keyword.mon_full_notm}}. You can also review the sample scenarios to learn more about the costs of a  {{site.data.keyword.mon_short}} instance.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} pricing is based on hourly consumption. You are billed monthly based on the number of connected agents and the agent deployment mode, the number of custom metric time series, extra number of containers per agent and additional API calls above 1M. There are two agent modes: agent for orchestrated environments, and agent for non-orchestrated environments.

All other {{site.data.keyword.mon_full_notm}} functionality, including dashboards, panels, and alerts, are included in the base service price and pricing does not vary.

The costs that are provided in this topic are guidelines and do not represent actual costs. They represent a starting point for estimates of costs that would be incurred in environments with a similar configuration. Actual costs can vary by geography. The prices that are used are based on actual prices as of April 1, 2023 and it is possible they can change.
{: important}




## Before you begin
{: #pricing_prereqs}

Read this section to understand concepts and costs that are associated with the {{site.data.keyword.mon_short}} service.

- [Service plans](/docs/monitoring?topic=monitoring-service_plans).

- [Time-series](/docs/monitoring?topic=monitoring-about-timeseries).

- [Sources of custom metrics](/docs/monitoring?topic=monitoring-about-collect-metrics).

- [Collecting metrics by infrastructure](/docs/monitoring?topic=monitoring-collect-metrics-by-host).


## Consumption charges
{: #billing_usage_metrics}

In your monthly usage charges, consumption is measured hourly and your bill breaks down into the following concepts:
​
| Metric              | Description |
| ------------------- | -------------- |
| `NODE_HOURS`        | Tracks the number of agents that are running in an agent for orchestrated environments.  \n \n This does not include the agents tracked by `LITE_NODE_HOURS`  \n  \n For example, if you have 1 agent connected continuously, that agent will be billed 720 `NODE_HOURS` at the end of the month.|
| `TIME_SERIES_HOURS` | Reflects the total number of custom metrics time series you are sending to {{site.data.keyword.mon_full_notm}} during a 1 hour time window. This is an aggregation of all time series from agents and other metrics sources. Platform metrics, Prometheus remote write, metric streaming and custom metrics collected with the agent (Prometheus, JMX or StatsD) contribute to `TIME_SERIES_HOURS`.  \n  \n Only custom metrics are counted for `TIME_SERIES_HOURS`. Default infrastructure metrics (such as host, container, program, or Kubernetes state) and CPU, memory, disk, and network are included in the agent price and do not contribute to `TIME_SERIES_HOURS`.   |
| `LITE_NODE_HOURS` | Tracks the number of agents that are monitoring non-containerized infrastructures such as VMs or bare metal servers, and are using the agent for non-orchestrated environments.  |
| `API_CALL_HOURS` | Represents how many calls are being made to the API per month. All instances include 1M API calls. |
| `CONTAINER_HOURS` | Represents how many containers are monitored across all hosts that are being monitored by agents.  |
{: caption="Table 2. Billing usage metrics" caption-side="bottom"}

To monitor how the {{site.data.keyword.mon_full_notm}} service is used and the costs associated to its usage, see [Viewing your usage](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).


All metrics that start with `sysdig_*` and `kube_*` are collected automatically by an agent and are included in the agent price.
{: note}



## Service plans
{: #pricing__service_plans}

The following service plans are available when you provision an instance of the {{site.data.keyword.mon_full_notm}} service:

### Lite plan
{: #lite_plan}

You can provision a {{site.data.keyword.mon_short}} instance with the `Lite` service plan to try out the {{site.data.keyword.mon_short}} service for free for 30 days.

After 30 days you must upgrade the instance to a graduated tier plan to continue working with the {{site.data.keyword.mon_short}} service or delete it.
{: note}


### Graduated tier plan
{: #graduated_tier}


The *graduated tier* service plan is billed based on the number of hosts that you monitor, the agent mode that is configured per host, the number of containers, the number of API calls, and the number of time series collected.

The following table outlines the cost per host by agent mode and what is included in the price:

| Agent mode          | Cost per host | Default infrastructure metrics (CPU, memory, disk, and network) | Includes up to 1K time-series (Prometheus, JMX, appchecks, StatsD) | Monitoring of 50 containers | 1M API calls |
|-------|------|-------|-------|-------|-------|
| Agent for non-orchestrated environments  | $9.36   | ![Checkmark icon](/images/checkmark-icon.svg) | | | |
| Agent for orchestrated environments   | $37   | ![Checkmark icon](/images/checkmark-icon.svg) |![Checkmark icon](/images/checkmark-icon.svg) |![Checkmark icon](/images/checkmark-icon.svg) |![Checkmark icon](/images/checkmark-icon.svg) |
{: caption="Table 4. Cost per host and agent mode" caption-side="top"}

For hosts running an agent for non-orchestrated environments or for hosts running an agent for orchestrated environments that exceed the base tier allotment for Prometheus, JMX, appchecks, and Statsd metrics, additional prices apply:

- Time series are priced according to the following tiers:

    - **Tier 1**: The price per time-series is 0.09 USD for up to 100K time-series per month.

    - **Tier 2**: The price per time-series is 0.05 USD for 100K to 1M time-series per month.

    - **Tier 3**: The price per time-series is 0.03 USD for 1M to 10M time-series per month.

    - **Tier 4**: The price per time-series is 0.02 USD for more than 10M time-series per month.

- Containers are priced as follows: 5.38 USD per 10 containers per month.

- API calls are priced as follows: The price for API calls is 0.01 USD per 1000 API calls per month.

Each measure is priced independently when there is an overage.
{: note}


Platform metrics are an additional source of time-series. They are priced based on the tiers.
{: important}

A host can be a container, a virtual machine, a bare metal, or any metrics source where you install a monitoring agent.

Data is collected and retained per the standard guidelines across all plans. For more information see [data collection](/docs/monitoring?topic=monitoring-mng-data#data-collection) and [data retention](/docs/monitoring?topic=monitoring-mng-data#data_storage_retention).

Prometheus remote write cost is based on metric ingestion. The price is calculated the same as for metrics collected using the agent with {{site.data.keyword.mon_full_notm}}.



### Graduated Tier - Sysdig Secure + Monitor
{: #graduated_secure}

{{site.data.content.combined-plan-deprecated}}

The *Graduated Tier - Sysdig Secure + Monitor* service plan includes both {{site.data.keyword.mon_full_notm}} and [{{site.data.keyword.sysdigsecure_full_notm}} functionality.](/docs/workload-protection).

The *Graduated Tier - Sysdig Secure + Monitor* service plan is billed based on the number of hosts that you monitor, the number of containers, the number of API calls, and the number of time series collected.

The following table outlines the cost per host by agent mode and what is included in the price:

| Agent mode | Cost per host | Default infrastructure metrics (CPU, memory, disk, and network) | Includes up to 1K time-series (Prometheus, JMX, appchecks, StatsD) | Monitoring of 50 containers | 1M API calls | Secure features |
|-------|------|-------|-------|-------|-------|-------|
| Agent for orchestrated environments  | $94  | ![Checkmark icon](/images/checkmark-icon.svg) |![Checkmark icon](/images/checkmark-icon.svg) |![Checkmark icon](/images/checkmark-icon.svg) |![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) |
{: caption="Table 5. Cost per host for Graduated Tier - Sysdig Secure and Monitor service plan" caption-side="top"}

For hosts running an agent for orchestrated environments that exceed the base tier allotment for Prometheus, JMX, appchecks, and Statsd metrics, additional prices apply:

- Time series are priced according to the following tiers:

    - **Tier 1**: The price per time-series is 0.09 USD for up to 100K time-series per month.

    - **Tier 2**: The price per time-series is 0.05 USD for 100K to 1M time-series per month.

    - **Tier 3**: The price per time-series is 0.03 USD for 1M to 10M time-series per month.

    - **Tier 4**: The price per time-series is 0.02 USD for more than 10M time-series per month.

- Containers are priced as follows: 5.38 USD per 10 containers per month.

- API calls are priced as follows: The price for API calls is 0.01 USD per 1000 API calls per month.

Each measure is priced independently when there is an overage.
{: note}

Platform metrics are an additional source of time-series. They are priced based on the tiers.
{: important}

A host can be a container, a virtual machine, a bare metal, or any metrics source where you install a monitoring agent.

Data is collected and retained per the standard guidelines across all plans. For more information see [data collection](/docs/monitoring?topic=monitoring-mng-data#data-collection) and [data retention](/docs/monitoring?topic=monitoring-mng-data#data_storage_retention).

Prometheus remote write cost is based on metric ingestion. The price is calculated the same as for metrics collected using the agent with {{site.data.keyword.mon_full_notm}}.



### Calculating time series pricing units
{: #pricing_unit_definitions}

Pricing units are comprised of *time-series*.

A *time-series* is a series of data-points ordered by time. It is a unique combination of a metric name and label key-value pairs. For example: `website_failedRequest |region='Asia', customer_ID='abc'`.

The same metric name can produce multiple *time-series* when the metric and label values differ.

For example, the following are 4 unique time series:

```text
metric_name{datacenter=”dc-1”, zone=”zone1”} 23
metric_name{datacenter=”dc-2”, zone=”zone1”} 34
metric_name{datacenter=”dc-3”, zone=”zone2”} 43
metric_name{datacenter=”dc-4”, zone=”zone2”} 23
```
{: screen}

A *data-point* is the value generated for a *time-series* at a given point in time.  For example: `[timestamp]|website_failedRequests:20|region='Asia', customer_ID='abc'`.

The number of *time-series* you are ingesting from the different sources are measured hourly and contribute to `TIME_SERIES_HOURS` pricing concept.

### Checking the metrics that are collected per agent
{: #pricing_agent_metrics}

In {{site.data.keyword.mon_full_notm}}, you can monitor your monitoring agent by using the dashboard template **monitoring agent Health & Status** that is available in the dashboard templates available out-of-the-box. In this dashboard, you can see the number of monitoring agents that are deployed and connected to the instance, check the version of the monitoring agents, and find out how many metrics per host the agent is collecting.

In this dashboard, the panel **TimeSeries Usage** provides the number of time-series that are collected from each category (Prometheus, JMX, StatsD, Prometheus Remote Write and Platform Metrics). This panel uses the query `sum(sysdig_ts_usage)by(metric_category)` that you can also run in PromQL Explorer, in your dashboards or for alerts.

In case you need to investigate which applications or services are contributing more to the Prometheus time-series, you can use the metric `scrape_series_added`. This metric represents the number of time series scraped and ingested from the monitoring agent via Prometheus and includes several labels to facilitate the analysis such as `kube_cluster_name`, `kube_namespace_name`, `kube_workload_name` or `container_name`.

The following query represents the number of time series ingested from the monitoring agent via Prometheus grouped by cluster, namespace, workloads and container so you can identify those applications that are contributing more time series:

```text
sum(scrape_series_added)by(kube_cluster_name, kube_namespace_name, kube_workload_name, container_name)
```
{: codeblock}

## Pricing considerations when monitoring Windows systems
{: #win_price}

Windows monitoring is charged by the number of *time-series* that are generated. The number of *time-series* depends on the number of collectors and resources your Windows system has.
​
The following table estimates the number of *time-series* generated when the default collectors are installed on a Windows system.
​
| Collector | Description | Estimate number of Time Series |
|---|---|---|
| `cpu` | CPU Usage |15 *time-series* per vCPU |
| `cs` | "Computer System" metrics (system properties, number of CPUs/total memory) | 3 |
| `logical_disk` | Logical disks, disk I/O | 14 *time-series* per disk partition |
| `os` | OS metrics (memory, processes, users) | 13 |
| `system` | System calls | 6 |
| `net` | Network interface I/O | 12 *time-series* per network adapter |
{: caption="Table 1. Time-series estimates for Windows systems based on default collector installation" caption-side="bottom"}

For example, if you have one Windows server with 2 vCPUs, 2 logical disks and 1 network adapter you can anticipate 92 *time-series*.
​
```text
15 * 2 + 3 + 14 * 2 + 13 + 6 + 12 * 1 = 92
```
{: screen}

With the cost per *time-series* of 0.09 USD for each *time-series* you would expect your cost to be 8.28 USD per month.
​
```text
92 * 0.09 USD = 8.28 USD
```
{: screen}

Other collectors that generate *time-series* include:

| Collector | Description | Estimate number of Time Series |
|---|---|---|
| `mssql` | SQL Server Performance Objects metrics | approximately 500 *time-series* per instance and approximately 100 *time-series* per database |
| `memory` | Memory usage metrics | 32 |
| `ad` | Active Directory Domain Services | 14 *time-series* per disk partition |
| `process` | Per-process metrics | 21 *time-series* per process. (This metric has high cardinality. One process can have subprocesses with multiple `process_id` values.) You can filter [processes](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.process.md){: external} |
| `service` | Service state metrics | 26 *time-series* per service. (This metric has high cardinality. Windows has a lot of services by default.) You can filter [services](https://github.com/prometheus-community/windows_exporter/blob/master/docs/collector.service.md){: external} |
{: caption="Table 2. Time-series estimates for Windows systems for additional collectors" caption-side="bottom"}

## Billing samples
{: #billing_example}

### Billing sample 1: Basic usage
{: #pricing_example1}


Consider the following example where you have the following configuration:
* 1 Kubernetes cluster with 3 worker nodes running agents for orchestrated environments
    * Host-1 generates 1200 custom metrics time-series
    * Host-2 generates 1000 custom metrics time-series
    * Host-3 generates 1500 custom metrics time-series

The billing calculation for the month is calculated as follows:

* *Base cost per host*

    The base price per host per month is 37 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, and StatsD metrics).

    For 3 hosts, the total monthly base cost is **111 USD**.

    ```text
    3 * 37 USD = 111 USD
    ```
    {: screen}

* *Additional time-series cost*

    Each host has a 1000 time-series allotment that are included in the base cost per host of 37 USD. If you have 3 hosts, you have 3000 time-series included. The remaining time-series are priced based on the tiers. The following shows the calculation of the 700 additional time-series.

    ```text
    1200 + 1000 + 1500 - ( 3*1000 ) = 700
    ```
    {: screen}

    The result from adding the time series per host minus the allotment defines the tier that is applied for pricing.

    700 additional time-series corresponds to tier 1. The price per host is 0.09 USD for up to 100K time-series per month.

    ```text
    700 * 0.09 USD = 63 USD
    ```
    {: screen}

    The total cost for additional time-series is **63 USD**.

The total monitoring cost per month is **174 USD**.

```text
111 USD + 63 USD = 174 USD
```
{: screen}

### Billing sample 2: Unused time-series allotment
{: #pricing_example2}


Consider the following example where you have the following configuration:
* 2 Kubernetes or OpenShift clusters with a total of 5 worker nodes running agents for orchestrated environments
    * Host-1 generates 2000 custom metrics time-series
    * Host-2 generates 100 custom metrics time-series
    * Host-3 generates 500 custom metrics time-series
    * Host-4 generates 100 custom metrics time-series
    * Host-5 generates 200 custom metrics time-series

The billing calculation for the month is calculated as follows:

* *Base cost per host*

    The price per host per month is 37 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, and StatsD metrics) and 50 containers.

    For 5 hosts, the total base cost is **185 USD**.

    ```text
    5 * 37 USD = 185 USD
    ```
    {: screen}

* *Additional time-series cost*

    Each host has a 1000 time-series allotment. The remaining time-series are priced based on the tiers.

    ```text
    2000 + 100 + 500 + 100 + 200 - ( 5*1000 ) = -1100
    ```
    {: screen}

    The result from adding the time series per host minus the allotment defines the tier that is applied for pricing.

    You have 1100 more time-series available per your configuration.

    The total cost for additional time-series is **0 USD**.

The total monitoring cost per month is **187 USD**.

```text
187 USD + 0 USD + 0 USD + 0 USD = 187 USD
```
{: screen}


### Billing sample 3: Platform metrics only
{: #pricing_example3}

Consider the following example where you have the following configuration for platform metrics:
* Event-stream generates 50 time-series per month
* IBM Cloud Databases generates 60 time-series per month
* 30k API calls

The billing calculation for the month is calculated as follows:

* *Additional time-series cost*

    Since there are no agents running in this instance, there is no time-series allotment.  All platform metrics time-series are priced based on the tiers. The following shows the total time-series for the configuration.

    ```text
    50 + 60 = 110
    ```
    {: screen}

    For tier 1, the price per time-series is 0.09 USD (Tier 1) for up to 100K time-series per month.

    ```text
    110 * 0.09 USD = 9.90 USD
    ```
    {: screen}

* *Additional API calls*

    1M API calls are included with the instance each month.

    The price for additional API calls is 0.01 USD per 1000 API calls.

    ```text
    0.03M - 1M = -970k
    0 * 0.01 USD/1k = 0 USD
    ```
    {: screen}

    The total cost for additional API calls is **0 USD**.

The total monitoring cost per month is **9.90 USD**.

```text
9.90 USD + 0 USD = 9.90 USD
```
{: screen}

Since there were no agents running in this example, the base price and additional containers costs were not applicable to this example.
{: note}

### Billing sample 4: Host allotment and platform metrics combined
{: #pricing_example4}

The following configuration demonstrates billing for a combination of host time-series allotment as well as platform metrics.

Consider the following example where you have the following configuration:
* 3 hosts running agents for orchestrated environments
    * Host-1 generates 1000 custom metrics time-series
    * Host-2 generates 850 custom metrics time-series
    * Host-3 generates 800 custom metrics time-series
* Cloud Foundry generates 200 time-series per month
* Event Streams generates 200 time-series per month
* IBM Cloud Databases generates 100 time-series per month
* 100 containers
* 300k API calls


The billing calculation for the month would look like:


* *Base cost per host*

    The price per host per month is 37 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, and StatsD metrics) and 50 containers.

    For 3 hosts, the total cost is **111 USD**.

    ```text
    3 * 37 USD = 111 USD
    ```
    {: screen}

* *Additional time-series cost*

    Each host has a 1000 time-series allotment. The remaining time-series are priced based on the tiers. In this case, 150 time-series.

    ```text
    1000 + 850 + 800 + 200 + 200 + 100 - ( 3*1000 ) = 150
    ```
    {: screen}

    The result from adding the time series per host, plus the platform metrics minus the allotment defines the tier that is applied for pricing.

    Notice that since the *Base cost per host* time-series allotment was not completely used by the agents, 350 of the 500 platform metrics time-series were covered by the base tier. Only the additional 150 platform metrics time-series (`500 - 350 = 150`)have an additional cost.

    ```text
    150 * 0.09 USD (Tier-1) = 13.50 USD
    ```
    {: screen}

    The total cost for time-series is **13.50 USD**.


The total monitoring cost per month is **124.50 USD**.

```text
111 USD + 13.50 USD = 124.50 USD
```
{: screen}


### Billing sample 5: Basic usage for Virtual Machine or Bare Metal servers running an agent for non-orchestrated environments
{: #pricing_example5}


Consider the following example where you have the following configuration:
* 3 hosts running an agent for non-orchestrated environments
    * Host-1 generates 50 custom metrics time-series
    * Host-2 generates 100 custom metrics time-series
    * Host-3 generates 100 custom metrics time-series

The billing calculation for the month is calculated as follows:

* *Base cost per host*

    The base price per host per month is 9.36 USD.

    For 3 hosts, the total base cost is **27 USD**.

    ```text
    3 * 9.36 USD = 28.08 USD
    ```
    {: screen}

* *Time-series cost*

    Time-series are priced based on the tiers. In this scenario you require 250 additional time-series.

    ```text
    50 + 100 + 100  = 250
    ```
    {: screen}

    The result from adding the time series per host defines the tier that is applied for pricing.

    250 time-series corresponds to tier 1. The price per host is 0.08 USD for up to 100K time-series per month.

    ```text
    250 * 0.09 USD = 22.50 USD
    ```
    {: screen}

    The total cost for additional time-series is **22.50 USD**.

The total monitoring cost per month is **50.58 USD**.

```text
28.08 USD + 22.50 USD = 50.58 USD
```
{: screen}
