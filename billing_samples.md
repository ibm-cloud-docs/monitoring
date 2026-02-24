---

copyright:
  years:  2018, 2026
lastupdated: "2026-02-24"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Billing samples
{: #billing_example}

This topic includes billing examples for {{site.data.keyword.mon_full_notm}}. 
{: shortdesc}


## Billing sample 1: Basic usage
{: #pricing_example1}


Consider the following example where you have the following configuration:
* 1 Kubernetes cluster with 3 worker nodes running agents for orchestrated environments
    * Host-1 generates 1200 custom metrics time-series
    * Host-2 generates 1000 custom metrics time-series
    * Host-3 generates 1500 custom metrics time-series

The billing calculation for the month is calculated as follows:

* *Base cost per host*

    The base price per host per month is 35.05 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, and StatsD metrics).

    For 3 hosts, the total monthly base cost is **111 USD**.

    ```text
    3 * 35.05 USD = 105.15 USD
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
    700 * 0.072 USD = 50.40 USD
    ```
    {: screen}

    The total cost for additional time-series is **50.40 USD**.

The total monitoring cost per month is **155.55 USD**.

```text
105.15 USD + 50.40 USD = 155.55 USD
```
{: screen}

## Billing sample 2: Unused time-series allotment
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

    The price per host per month is 30.05 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, and StatsD metrics) and 50 containers.

    For 5 hosts, the total base cost is **150.25 USD**.

    ```text
    5 * 30.05 USD = 150.25 USD
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

The total monitoring cost per month is **150.25 USD**.

```text
150.25 USD + 0 USD + 0 USD + 0 USD = 150.25 USD
```
{: screen}


## Billing sample 3: Platform metrics only
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
    110 * 0.072 USD = 7.92 USD
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

The total monitoring cost per month is **7.92 USD**.

```text
7.92 USD + 0 USD = 7.92 USD
```
{: screen}

Since there were no agents running in this example, the base price and additional containers costs were not applicable to this example.
{: note}

## Billing sample 4: Host allotment and platform metrics combined
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

    The price per host per month is 30.05 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, and StatsD metrics) and 50 containers.

    For 3 hosts, the total cost is **90.15 USD**.

    ```text
    3 * 30.05 USD = 90.15 USD
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
    150 * 0.072 USD (Tier-1) = 10.80 USD
    ```
    {: screen}

    The total cost for time-series is **10.80 USD**.


The total monitoring cost per month is **124.50 USD**.

```text
90.15 USD + 10.80 USD = 100.95 USD
```
{: screen}


## Billing sample 5: Basic usage for Virtual Machine or Bare Metal servers running an agent for non-orchestrated environments
{: #pricing_example5}


Consider the following example where you have the following configuration:
* 3 hosts running an agent for non-orchestrated environments
    * Host-1 generates 50 custom metrics time-series
    * Host-2 generates 100 custom metrics time-series
    * Host-3 generates 100 custom metrics time-series

The billing calculation for the month is calculated as follows:

* *Base cost per host*

    The base price per host per month is 10.07 USD.

    For 3 hosts, the total base cost is **30.21 USD**.

    ```text
    3 * 10.07 USD = 30.21 USD
    ```
    {: screen}

* *Time-series cost*

    Time-series are priced based on the tiers. In this scenario you require 250 additional time-series.

    ```text
    50 + 100 + 100  = 250
    ```
    {: screen}

    The result from adding the time series per host defines the tier that is applied for pricing.

    250 time-series corresponds to tier 1. The price per host is 0.09 USD for up to 100K time-series per month.

    ```text
    250 * 0.072 USD = 18.00 USD
    ```
    {: screen}

    The total cost for additional time-series is **18.00 USD**.

The total monitoring cost per month is **48.31 USD**.

```text
30.21 USD + 18.00 USD = 48.31 USD
```
{: screen}
