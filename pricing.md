---

copyright:
  years: 2018
lastupdated: "2018-11-05"

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
 

| Plan             | Description  |
|------------------|--------------|
| `Lite`           | Data is collected for up to 20 containers, and for a maximum of 200 custom metrics per node every 10secs. </br>The plan is free for 21 days only. </br>Lite plan services are deleted after 30 days of inactivity. |
| `Graduated tier` (*) | There are different tiers: </br>`Basic`: Data is collected for up to 20 containers per host, for a maximum of 200 custom metrics per node every 10secs. This plan is suitable for one core compute. </br>`Pro`: Data is collected for up to 50 containers or 500 custom metrics per node every 10 secs. This plan is suitable for 8-16 core computes. </br>`Advanced`: Data is collected for 50+ containers or up to 1000 custom metrics per node every 10 secs. This plan is suitable for more than 16 core computes. |
{: caption="Table 1. List of service plans" caption-side="top"} 


(*) **Note:** Based on your usage of average number of containers or number of custom metrics emitted by each node every 10 seconds, {{site.data.keyword.IBM_notm} will auto-compute the tier in which the mode fits. Ay any point in time, you could have some nodes in one tier and some in another. Alerts will be provided to inform you when you are switching from one tier to another based on your consumption.


**Note: ** For very high container density or metric volumes contact sales.  


Basic: 0-20 containers per host, 200 auto-detected app metrics, 200 custom metrics
Pro:  21-50 containers per host, 500 auto-detected app metrics, 500 custom metrics
Advanced: >50 containers per host, 1000 auto-detected app metrics, 1000 custom metrics, 
Note:
- For each plan, you get 10s granularity, and 15 months data retention.
- When the number of containers per host or the number of metrics goes above the plan's threshold over a period of time, automatic tier detection is applied and an alert notification is triggered following your billing usage notification configuration. 
- For very high container density or metric volumes, contact sales. (Can we add a link)