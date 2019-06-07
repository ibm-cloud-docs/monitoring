---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

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

Different pricing plans are available for an {{site.data.keyword.mon_full_notm}} instance.
{:shortdesc}
 

| Plans            | Tier         | Data collection  |
|------------------|--------------|------------------|
| `Trial`          |              | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node for 30 days only. |
| `Graduated tier` | `Basic`      | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node. |
| `Graduated tier` | `Pro`        | Data is collected for a maximum of 50 containers per node or for 500 custom metrics per node. |
| `Graduated tier` | `Advanced`   | Data is collected for a maximum of 110 containers per node or for 3000 custom metrics per node. |
{: caption="Table 1. List of service plans" caption-side="top"} 


**Note:** A node can be a host, a container, a virtual machine, a bare metal, or any metrics source where you install a Sysdig agent.

When the number of containers per node or the number of metrics goes above the graduated tier plan's threshold limit over a period of time, automatic tier detection is applied. An alert notification is triggered following your billing usage notification configuration if you enable the following alert **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

You can request a **custom price quote** for anything beyond the upper bound of the *Advanced graduated tier paid pricing plan* by opening a ticket with [IBM Cloud Support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window}.
{: tip}

Data is collected and retained per the standard guidelines across all plans. For more information see [data collection](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection) and [data retention](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention).


## Checking your usage
{: #pricing_usage}

To monitor how the {{site.data.keyword.mon_full_notm}} service is used and the costs associated to its usage, see [Viewing your usage](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).



## Enabling the alert that notifies on a tier change
{: #pricing_alert}

To be notified when there is a tier change, you must enable the following alert: **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

Complete the following steps to enable an alert:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
2. Create a notification channel. For more information, see [Configuring a notification channel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create). 
3. Click **ALERTS** to navigate to the *Alerts* section.
2. Search for **[IBM]: Usage Tier Change**.
3. Edit the alert to add the notification channel.
4. Click **Save**.



## How is the service plan alert generated?
{: #pricing_how}

To be notified when there is a tier change, you must enable the following alert: **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

**Note:** When you enable this alert, you must specify the notification channels where you want to be notified.

The usage is calculated as the average of the number of nodes and metrics sampled every 10 seconds over the previous hour. Small, short-lived fluctuations are not included. The difference between the previous and the current usage happens once an hour.

The thresholds defined are set in the following way:

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [21, 50]
    Advanced = [51, 100]
  }
  metricDensity {
    Basic = [0, 200]
    Pro = [201, 500]
    Advanced = [501, 1000]
}
```
{: screen}

The alert notification is generated as follows:
1. Every hour, if the number of containers per node in a tier increases, a custom event is generated.
2. The alert condition checks for any custom events that inform about changes in the number of containers per node. If it finds an event where the number of containers in a tier increases from the last time the usage was calculated, it sends a notification.

The frequency of the alert is once every hour. For a fluctuating node, the frequency of the alert is at most every two hours.

Notice that the alert is only generated if a node moves from *Basic* tier to *Pro* tier or to *Advanced* tier. 



### Examples
{: #pricing_examples}

**Sample 1** 

If the average container count is the following: 

| Hour     | Number of containers | Description                                                                   | Is an alert generated? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 18                   | Tier is set to **Basic**.                                                     | No                     |
| 11:00    | 21                   | Number of containers is above *Basic* tier. Tier moves to **Pro**.            | Yes                    |
| 12:00    | 19                   | Number of containers is below *Basic* tier. Tier moves back to **Basic**.     | No                    |
| 13:00    | 20                   | No tier change. Tier is set to **Basic**.                                     | No                     |
{: caption="Table 2. Sample 1" caption-side="top"} 


**Sample2**

If the average container count is the following: 

| Hour     | Number of containers | Description                                                                   | Is an alert generated? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Tier is set to **Basic**.                                                     | No                     |
| 11:00    | 19                   | Tier is set to **Basic**.                                                     | No                     |
| 12:00    | 20                   | Tier is set to **Basic**.                                                     | No                    |
| 13:00    | 21                   | Number of containers is above *Basic* tier. Tier moves to **Pro**.            | Yes                     |
{: caption="Table 3. Sample 2" caption-side="top"}


**Sample3**

If the average container count is the following: 

| Hour     | Number of containers | Description                                                                   | Is an alert generated? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Tier is set to **Basic**.                                                     | No                     |
| 11:00    | 20                   | Tier is set to **Basic**.                                                     | No                    |
| 12:00    | 21                   | Tier is set to **Basic**.                                                     | Yes                    |
| 13:00    | 20                   | Number of containers is back to *Basic* tier. Tier moves to **Pro**.          | No                     |
{: caption="Table 3. Sample 3" caption-side="top"}



