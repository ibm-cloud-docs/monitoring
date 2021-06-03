---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, pricing

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


# Pricing
{: #pricing_plans}

This topic includes information about pricing for the {{site.data.keyword.mon_full_notm}}. You can also review the sample scenarios to learn more about the costs of a monitoring instance
{: shortdesc}

The following service plans are available:

| Plans                                      | Plan ID                                | Plan Name                   |
|--------------------------------------------|----------------------------------------|-----------------------------|
| `Lite`                                     | `367a3918-9efc-43c5-bef9-20553051b7af` | `lite`                      | 
| `Graduated tier`                           | `231bb072-1b2f-4d7e-ae9e-9574d382be32` | `graduated-tier`            |
| `Graduated Tier - Sysdig Secure + Monitor` | `35784193-e918-42d9-9598-4e842ed75192` | `graduated-tier-sysdig-secure-plus-monitor` |
{: caption="Table 1. Service plans" caption-side="top"} 

A `Lite` monitoring instance expires after 30 days.
{: note}

The costs that are provided in this topic are guidelines and do not represent actual costs. They represent a starting point for estimates of costs that would be incurred in environments with a similar configuration. Actual costs can vary by geography. The prices that are used are based on actual prices as of March 1, 2020 and it is possible they can change.
{: important}


| Plans            | Base tier | Tier 1 | Tier 2 | Tier 3 | Tier 4 |
|------------------|---------------------------------------------------|--------|--------|--------|
| `Lite`           | ![Checkmark icon](../../icons/checkmark-icon.svg) | | | | |
| `Graduated tier` | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Graduated Tier - Sysdig Secure + Monitor` | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 2. Time-series tiers per service plans" caption-side="top"} 


The *graduated tier* plan is billed based on the following measurements and pricing:

* **Base tier**: The price per host per month is 35 USD which includes host, Kubernetes and container metrics as well as up to 1K additional time-series (includes Prometheus, JMX, appchecks, StatsD and platform metrics) and 50 containers.
* **Additional time series**: If you exceed your base tier allotment for Prometheus, JMX, appchecks, Statsd and platform metrics, then the additional time series are priced according to the following tiers.
    * **Tier 1**: The price per time-series is 0.08 USD for up to 100K time-series per month, or 0.00011 USD time-series per hour.
    * **Tier 2**: The price per time-series is 0.05 USD for 100K to 1M time-series per month or 0.000069 USD time-series per hour.
    * **Tier 3**: The price per time-series is 0.03 USD for 1M to 10M time-series per month or 0.000042 USD time-series per hour.
    * **Tier 4**: The price per time-series is 0.02 USD for more than 10M time-series per month or 0.000028 USD time-series per hour.
* **Additional containers**: The price is 5 USD per 10 containers per month.
* **Additional API calls**: Your instance comes with an allotment of 1M API calls regardless of the number of agents.  The price for API calls in excess of this allotment is 0.01 USD per 1000 API calls per month.

Each measure is priced independently when there is an overage.
{: note}


Platform metrics are an additional source of time-series. They are priced based on the tiers.
{: important}

A host can be a container, a virtual machine, a bare metal, or any metrics source where you install a monitoring agent.

Data is collected and retained per the standard guidelines across all plans. For more information see [data collection](/docs/monitoring?topic=monitoring-mng-data#data-collection) and [data retention](/docs/monitoring?topic=monitoring-mng-data#data-storage_retention).


## Checking the metrics that are collected per agent
{: #pricing_agent_metrics}

In {{site.data.keyword.mon_full_notm}}, you can monitor your monitoring agent by using the dashboard template **monitoring agent Health & Status** that is available in **Host Infrastructure**. In this dashboard, you can see the number of monitoring agents that are deployed and connected to the instance, check the version of the monitoring agents, and find out how many metrics per host the agent is collecting.



## Checking your usage
{: #pricing_usage}

To monitor how the {{site.data.keyword.mon_full_notm}} service is used and the costs associated to its usage, see [Viewing your usage](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).



## Billing sample 1: Basic usage
{: #pricing_example1}


Consider the following example where you have the following configuration: 
* 3 hosts
    * Host-1 generates 1200 time-series
    * Host-2 generates 1000 time-series
    * Host-3 generates 1500 time-series
* 170 containers
* 1.2M API calls

The billing calculation for the month is calculated as follows:

* `Base cost per host`

    The base price per host per month is 35 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, StatsD and platform metrics) and 50 containers.

    For 3 hosts, the total base cost adds to **105 USD**.
  
    ```
    3 * 35 USD = 105 USD
    ```
    {: screen}

* `Additional time-series cost`

    Each host has a 1000 time-series allotment that are included in the base cost per host of 35 USD. If you have 3 hosts, you have included 3000 time-series. The remaining time-series are priced based on the tiers.
  
    ```
    1200 + 1000 + 1500 - ( 3*1000 ) = 700 additional time-series
    ```
    {: screen}
    
    The result from adding the time series per host minus the allotment defines the tier that is applied for pricing. 
    
    700 additional time-series corresponds to tier 1. The price per host is 0.08 USD for up to 100K time-series per month.
    
    ``` 
    700 additional time-series * 0.08 USD (Tier-1) = 56 USD
    ```
    {: screen}
    
    The total cost for additional time-series adds to **56 USD**.

* `Additional containers cost`

    Each host has a 50 containers allotment. The remaining containers are priced 5 USD per 10 containers per month.

    ```
    170 - (3x50) = 20 
    (20 additional containers/10) * 5 USD = 10 USD
    ```
    {: screen}

    The total cost for additional containers adds to **10 USD**.

* `Additional API calls`

    1M API calls are included with the instance each month.

    The price for additional API calls is 0.01 USD per 1000 API calls.
  
    ```
    1.2M - 1M = 200k 
    200k * 0.01 USD/1k = 2 USD
    ```
    {: screen}

    The total cost for additional API calls adds to **2 USD**.

The total monitoring cost per month adds to **173 USD**.

```
105 USD + 56 USD + 10 USD + 2 USD = 173 USD
```
{: screen}

## Billing sample 2: Unused time-series allotment
{: #pricing_example2}


Consider the following example where you have the following configuration: 
* 5 hosts
    * Host-1 generates 2000 time-series
    * Host-2 generates 100 time-series
    * Host-3 generates 500 time-series
    * Host-4 generates 100 time-series
    * Host-5 generates 200 time-series
* 100 containers
* 700k API calls

The billing calculation for the month is calculated as follows:

* `Base cost per host`

    The price per host per month is 35 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, StatsD and platform metrics) and 50 containers.

    For 5 hosts, the total base cost adds to **175 USD**.
  
    ```
    5 * 35 USD = 175 USD
    ```
    {: screen}

* `Additional time-series cost`

    Each host has a 1000 time-series allotment. The remaining time-series are priced based on the tiers.
  
    ```
    2000 + 100 + 500 + 100 + 200 - ( 5*1000 ) = -1100 
    ```
    {: screen}
    
    The result from adding the time series per host minus the allotment defines the tier that is applied for pricing. 
    
    You have 1100 more time-series available per your configuration.
    
    The total cost for additional time-series adds to **0 USD**.

* `Additional containers cost`

    Each host has a 50 containers allotment. The remaining containers are priced 5 USD per 10 containers per month.

    ```
    100 - 5x50 = -150
    ```
    {: screen}

    You have 150 more containers available per your configuration.

    The total additional cost for containers adds to **0 USD**.

* `Additional API calls`

    1M API calls are included with the instance each month.

    The price for additional API calls is 0.01 USD per 1000 API calls.
  
    ```
    700k - 1M = -300k
    ```
    {: screen}

    You have 300k more API calls available per your configuration.

    The total cost for additional API calls adds to **0 USD**.


The total monitoring cost per month adds to **175 USD**.

```
175 USD + 0 USD + 0 USD + 0 USD = 175 USD
```
{: screen}




## Billing sample 3: Platform metrics only
{: #pricing_example3}

Consider the following example where you have the following configuration for platform metrics: 
* Event-stream generates 50 time-series per month
* IBM Cloud Databases generates 60 time-series per month
* 30k API calls

The billing calculation for the month is calculated as follows:

* `Additional time-series cost`

    Since there are no agents running in this instance, there is no time-series allotment.  All platform metrics time-series are priced based on the tiers.

    ```
    50 + 60 = 110 time-series
    ```
    {: screen}

    For tier 1, the price per time-series is 0.08 USD for up to 100K time-series per month.

    ```
    110 * 0.08 USD (Tier-1) = 8.80 USD
    ```
    {: screen}

* `Additional API calls`

    1M API calls are included with the instance each month.

    The price for additional API calls is 0.01 USD per 1000 API calls.
  
    ```
    0.03M - 1M = -970k
    0 * 0.01 USD/1k = 0 USD
    ```
    {: screen}

    The total cost for additional API calls adds to **0 USD**.

The total monitoring cost per month adds to **8.80 USD**.

```
8.80 USD + 0 USD = 8.80 USD
```
{: screen}

Since there were no agents running in this example, the base price and additional containers costs were not applicable to this example.
{: note}

## Billing sample 4: Host allotment and platform metrics combined
{: #pricing_example4}

The following configuration demonstrates billing for a combination of host time-series allotment as well as platform metrics.

Consider the following example where you have the following configuration: 
* 3 hosts
    * Host-1 generates 1000 time-series
    * Host-2 generates 850 time-series
    * Host-3 generates 800 time-series
* Cloud Foundry generates 200 time-series per month
* Event Streams generates 200 time-series per month
* IBM Cloud Databases generates 100 time-series per month
* 100 containers
* 300k API calls


The billing calculation for the month would look like:


* `Base cost per host`

    The price per host per month is 35 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, StatsD and platform metrics) and 50 containers.

    For 3 hosts, the total cost adds to **105 USD**.
  
    ```
    3 * 35 USD = 105 USD
    ```
    {: screen}

* `Additional time-series cost`

    Each host has a 1000 time-series allotment. The remaining time-series are priced based on the tiers.
  
    ```
    1000 + 850 + 800 + 200 + 200 + 100 - ( 3*1000 ) = 150 time-series
    ```
    {: screen}

    The result from adding the time series per host, plus the platform metrics minus the allotment defines the tier that is applied for pricing.

    Notice that since the `Base cost per host` time-series allotment was not completely used by the agents, 350 of the 500 platform metrics time-series were covered by the base tier.
    
    ```
    150 additional time-series * 0.08 USD (Tier-1) = 12 USD
    ```
    {: screen}

    The total cost for time-series adds to **12 USD**.

* `Additional containers cost`

    Each host has a 50 containers allotment. The remaining containers are priced 5 USD per 10 containers per month.

    ```
    100 - 3x50 = -50 containers
    ```
    {: screen}

    You have 50 more containers available per your configuration.

    The total cost for containers adds to **0 USD**.

* `Additional API calls`

    1M API calls are included with the instance each month.

    The price for additional API calls is 0.01 USD per 1000 API calls.
  
    ```
    300k - 1M = -700k
    ```
    {: screen}

    You have 700k more API calls available per your configuration.

    The total cost for additional API calls adds to **0 USD**.


The total monitoring cost per month adds to **117 USD**.

```
105 USD + 12 USD + 0 USD + 0 USD = 117 USD
```
{: screen}



