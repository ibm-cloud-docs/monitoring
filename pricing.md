---

copyright:
  years:  2018, 2020
lastupdated: "2020-03-01"

keywords: Sysdig, IBM Cloud, monitoring, pricing

subcollection: Sysdig

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


# Pricing
{: #pricing_plans}

This topic includes information about pricing for the {{site.data.keyword.mon_full_notm}}. You can also review the sample scenarios to learn more about the costs of a Sysdig instance
{: shortdesc}

The costs that are provided in this topic are guidelines and do not represent actual costs. They represent a starting point for estimates of costs that would be incurred in environments with a similar configuration. Actual costs can vary by geography. The prices that are used are based on actual prices as of March 1, 2020 and it is possible they can change.
{: important}


| Plans            | Base tier | Tier 1 | Tier 2 | Tier 3 | Tier 4 |
|------------------|---------------------------------------------------|--------|--------|--------|--------|
| `Lite`           | ![Checkmark icon](../../icons/checkmark-icon.svg) | | | |
| `Graduated tier` | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 1. Time-series tiers per service plans" caption-side="top"} 


The *graduated tier* plan is billed based on the following prices:

* **Base tier**: The price per host per month is 35 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, StatsD), 50 containers and 1M API calls.
* **Tier 1**: The price per host is 0.08 USD for up to 100K time-series per month, or 0.00011 USD time-series per hour.
* **Tier 2**: The price per host is 0.05 USD for 100K to 1M time-series per month or 0.000069 USD time-series per hour.
* **Tier 3**: The price per host is 0.03 USD for 1M to 10M time-series per month or 0.000042 USD time-series per hour.
* **Tier 4**: The price per host is 0.02 USD for more than 10M time-series per month or 0.000028 USD time-series per hour.
* **Additional containers**: The price is 5 USD per 10 containers per month.
* **Additional API calls**: The price is 0.01 USD per 1000 API calls across all hosts per month.

Each measure is priced independently when there is an overage.
{: note}


There is no time-series allotment for platform metrics. These time-series are priced based on the tiers.
{: important}

**Note:** A host can be a container, a virtual machine, a bare metal, or any metrics source where you install a Sysdig agent.




Data is collected and retained per the standard guidelines across all plans. For more information see [data collection](/docs/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection) and [data retention](/docs/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention).


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

* `Cost per host`

    The price per host per month is 35 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, StatsD), 50 containers and 1M API calls.

    For 3 hosts, the total cost adds to **105 USD**.
  
    ```
    3 * 35 USD = 105 USD
    ```
    {: screen}

* `Time-series cost`

    Each host has a 1000 time-series allotment. The remaining time-series are priced based on the tiers.
  
    ```
    1200 + 1000 + 1500 - ( 3*1000 ) = 700 time-series
    ```
    {: screen}
    
    The result from adding the time series per host minus the allotment defines the tier that is applied for pricing. 
    
    700 time-series corresponf to tier 1. The price per host is 0.08 USD for up to 100K time-series per month.
    
    ``` 
    700 time-series * 0.08 USD (Tier-1) = 56 USD
    ```
    {: screen}
    
    The total cost for time-series adds to **56 USD**.

* `Containers cost`

    Each host has a 50 containers allotment. The remaining containers are priced 5 USD per 10 containers per month.

    ```
    170 - (3x50) = 20 
    (20 containers/10) * 5 USD = 10 USD
    ```
    {: screen}

    The total cost for containers adds to **10 USD**.

* `API calls`

    1M API calls are allowed across all hosts per month.

    The price is 0.01 USD per 1000 API calls across all hosts per month.
  
    ```
    1.2M - 1M = 200k 
    200k * 0.01 USD/1k = 2 USD
    ```
    {: screen}

    The total cost for API calls adds to **56 USD**.

The total amount adds to **173 USD**.

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

* `Cost per host`

    The price per host per month is 35 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, StatsD), 50 containers and 1M API calls.

    For 5 hosts, the total cost adds to **175 USD**.
  
    ```
    5 * 35 USD = 175 USD
    ```
    {: screen}

* `Time-series cost`

    Each host has a 1000 time-series allotment. The remaining time-series are priced based on the tiers.
  
    ```
    2000 + 100 + 500 + 100 + 200 - ( 5*1000 ) = -1100 
    ```
    {: screen}
    
    The result from adding the time series per host minus the allotment defines the tier that is applied for pricing. 
    
    You have 1100 more time-series available per your configuration.
    
    The total cost for time-series adds to **0 USD**.

* `Containers cost`

    Each host has a 50 containers allotment. The remaining containers are priced 5 USD per 10 containers per month.

    ```
    100 - 5x50 = -150
    ```
    {: screen}

    You have 150 more containers available per your configuration.

    The total cost for containers adds to **0 USD**.

* `API calls`

    1M API calls are allowed across all hosts per month.

    The price is 0.01 USD per 1000 API calls across all hosts per month.
  
    ```
    700k - 1M = -300k
    ```
    {: screen}

    You have 300 more API calls available per your configuration.

    The total cost for API calls adds to **0 USD**.


The total amount adds to **175 USD**.

```
175 USD + 0 USD + 0 USD + 0 USD = 175 USD
```
{: screen}




## Billing sample 3: Platform metrics only
{: #pricing_example3}

Consider the following example where you have the following configuration for platform metrics: 
* Event-stream generates 50 time-series per month
* IBM Cloud Databases generats 60 time-series per month

The billing calculation for the month is calculated as follows:
  
```
50 + 60 = 110 time-series
```
{: screen}

For tier 1, the price per host is 0.08 USD for up to 100K time-series per month.

```
110 * 0.08 USD (Tier-1) = 8.80 USD
```
{: screen}

The total amount adds to **8.80 USD**.



## Billing sample 4: Host allotment and platform metrics combined
{: #pricing_example4}

The following configuration demonstrates billing for a combination of host time-series allotment as well as platform metrics.

Consider the following example where you have the following configuration: 
* 3 hosts
* Host-1 generates 1000 time-series
* Host-2 generates 100 time-series
* Host-3 generates 500 time-series
* Cloud Foundry generates 200 time-series per month
* Event Streams generates 200 time-series per month
* IBM Cloud Databases generats 100 time-series per month
* 100 containers
* 300k API calls


The billing calculation for the month would look like:


* `Cost per host`

    The price per host per month is 35 USD which includes up to 1K time-series (includes Prometheus, JMX, appchecks, StatsD), 50 containers and 1M API calls.

    For 3 hosts, the total cost adds to **105 USD**.
  
    ```
    3 * 35 USD = 105 USD
    ```
    {: screen}

* `Time-series cost`

    Each host has a 1000 time-series allotment. The remaining time-series are priced based on the tiers.
  
    ```
    1000 + 100 + 500 + 200 + 200 + 100 - ( 3*1000 ) = -900 time-series
    ```
    {: screen}
    
    The result from adding the time series per host minus the allotment defines the tier that is applied for pricing. 

    Notice that there is no additional charge for the platform metrics in this case since the excess allotment from the agents can be used to cover the cost of the platform metrics.

    You have 900 more time-series available per your configuration.
    
    The total cost for time-series adds to **0 USD**.

* `Containers cost`

    Each host has a 50 containers allotment. The remaining containers are priced 5 USD per 10 containers per month.

    ```
    100 - 3x50 = -50 containers
    ```
    {: screen}

    You have 50 more containers available per your configuration.

    The total cost for containers adds to **0 USD**.

* `API calls`

    1M API calls are allowed across all hosts per month.

    The price is 0.01 USD per 1000 API calls across all hosts per month.
  
    ```
    300k - 1M = -700k
    ```
    {: screen}

    You have 700 more API calls available per your configuration.

    The total cost for API calls adds to **0 USD**.


The total amount adds to **105 USD**.

```
105 USD + 0 USD + 0 USD + 0 USD = 105 USD
```
{: screen}



