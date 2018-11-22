---

copyright:
  years: 2018
lastupdated: "2018-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Pricing plans
{: #pricing_plans}

Different pricing plans are available for an IBM Cloud Monitoring with Sysdig instance.
{:shortdesc}
 

| Plan             | Information  |
|------------------|--------------|
| `Trial`          | Data is collected for 30 days only. |
| `Graduated tier` | Data is collected for as long as you need. |
{: caption="Table 1. List of service plans" caption-side="top"} 

You can request a **custom price quote** for anything beyond the upper bound of the *Advanced graduated tier paid pricing plan* by opening a ticket with [IBM Cloud Support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window}.
{: tip}

Data is collected and retained per the standard guidelines across all plans. For more information see [data collection and retention](/docs/services/Monitoring-with-Sysdig/overview.html#data).

The average cost that has been estimated for using the IBM Cloud Monitoring with Sysdig service is between 5% and 10% of your overall compute cost. This estimation may be different depending on your architecture and usage of the IBM Cloud Monitoring with Sysdig service.



## Trial plan
{: #trial}

Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node for 30 days only.

## Graduated tier plan
{: #graduated}

There are different tiers in the graduated tier plan: 
* **Basic:** Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node.   
* **Pro:** Data is collected for a maximum of 50 containers per node or for 500 custom metrics per node. 
* **Advanced:** Data is collected for a maximum of 110 containers per node or for 1000 custom metrics per node.

When the number of containers per node or the number of metrics goes above the plan's threshold limit over a period of time, automatic tier detection is applied and an alert notification is triggered following your billing usage notification configuration.

**Note:** To be notified, you must enable the following alert **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

If you have enabled the alert **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**, an alert notification is triggered to inform you when you are switching from one tier to another based on your consumption.


## Checking your usage
{: #usage}

To monitor how the IBM Cloud Monitoring with Sysdig service is used and the costs associated to its usage, see [Viewing your usage](/docs/billing-usage/viewing_usage.html#viewingusage).


## Enabling the alert that notifies on a tier change
{: #alert}


Complete the following steps to enable an alert:

1. Create a notification channel https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/206503956/Notifications+Management
2. View alerts and search for “[IBM]: Usage Tier Change” alert
3. Edit the alert to use the notification channel from 1)
4. Save the alert and enable it (edited)
