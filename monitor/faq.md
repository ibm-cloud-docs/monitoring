---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring,  faq

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
{:faq: data-hd-content-type='faq'}
{:external: target="_blank" .external}


# Frequently Asked Questions
{: #faq}

Frequently asked questions about {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Where can I find the list of Cloud services that generate metrics?
{: #faq_1}
{: faq}

You can find information about the services that generate metrics in the following documentation topic: [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).


## Are you observing monitoring agent connection errors or receiving uptime alerts reporting an host is down when there are no problems?
{: #faq_2}
{: faq}

{{site.data.keyword.mon_full_notm}} has identified an issue with a subset of agent versions:
- monitoring agent 10.3.0
- monitoring agent 10.3.1
- monitoring agent 10.4.0
- monitoring agent 10.4.1 

Where connectivity between your infrastructure and Monitoring's hosted service may fail.

You must upgrade all monitoring agents to `10.5`. [Learn more](/docs/monitoring?topic=monitoring-troubleshoot#troubleshoot-entry-3).



## How can I find out the metrics that are collected per agent?
{: #faq_3}
{: faq}

In {{site.data.keyword.mon_full_notm}}, you can monitor your monitoring agent by using the dashboard template **monitoring agent Health & Status** that is available in **Host Infrastructure**. In this dashboard, you can see the number of monitoring agents that are deployed and connected to the monitoring instance, check the version of the monitoring agents, and find out how many metrics per host the agent is collecting.



