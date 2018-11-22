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
 

| Plans            | Tier         | Data collection  |
|------------------|--------------|------------------|
| `Trial`          |              | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node for 30 days only. |
| `Graduated tier` | `Basic`      | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node. |
| `Graduated tier` | `Pro`        | Data is collected for a maximum of 50 containers per node or for 500 custom metrics per node. |
| `Graduated tier` | `Advanced`   | Data is collected for a maximum of 110 containers per node or for 1000 custom metrics per node. |
{: caption="Table 1. List of service plans" caption-side="top"} 

When the number of containers per node or the number of metrics goes above the graduated tier plan's threshold limit over a period of time, automatic tier detection is applied. An alert notification is triggered following your billing usage notification configuration if you enable the following alert **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

You can request a **custom price quote** for anything beyond the upper bound of the *Advanced graduated tier paid pricing plan* by opening a ticket with [IBM Cloud Support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window}.
{: tip}

Data is collected and retained per the standard guidelines across all plans. For more information see [data collection and retention](/docs/services/Monitoring-with-Sysdig/overview.html#data).


## Checking your usage
{: #usage}

To monitor how the IBM Cloud Monitoring with Sysdig service is used and the costs associated to its usage, see [Viewing your usage](/docs/billing-usage/viewing_usage.html#viewingusage).


## Enabling the alert that notifies on a tier change
{: #alert}

To be notified when there is a tier change, you must enable the following alert: **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

The alert notification is generated in a two step process:

1. Every hour, if the number of hosts in a tier has increased, a custom event is generated.

2. When the alert condition is checked, if the custom event 

The next minute when the alert checks run, if the above highlighted alert is enabled, it checks for any of those custom events and sends a notification to the specified notification channel.

The event/alert is generated only if the number of hosts in a tier increases from the last time the usage was calculated.

There are two parts to the alert frequency:

Because the usage calculation is the average of the number of containers/metrics sampled every 10s over the previous hour, small, short-lived fluctuations are smoothed out.

Because the usage calculation and thus the difference between the previous and the current usage happens once an hour, the most frequent you can expect to be alerted is once every hour (and this only happens if a host is moving from Basic, to Pro, to Advanced). For a fluctuating host, it would be at most every two hours.

Examples:

If the average container count for hour 1 is 21, and for hour 2 is 19, and for hour 3 is 20; you can expect to see an alert for hour 1 and hour 3, but not for hour 2.

If the average container count for hour 1 is 19, for hour 2 is 20, and for hour 3 is 21; you can expect to see an alert for hour 1, and hour 2, but not for hour 3.

If the average container count for hour 1 is 20, for hour 2 is 21, and for hour 3 is 20; you can expect to see an alert for hour 1, but not hour 2 or hour 3.
Complete the following steps to enable an alert:

1. Create a notification channel https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/206503956/Notifications+Management
2. View alerts and search for “[IBM]: Usage Tier Change” alert
3. Edit the alert to use the notification channel from 1)
4. Save the alert and enable it (edited)
