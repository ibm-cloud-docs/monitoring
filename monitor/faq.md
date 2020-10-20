---

copyright:
  years:  2018, 2020
lastupdated: "2020-10-12"

keywords: Sysdig, IBM Cloud, monitoring,  faq

subcollection: Monitoring-with-Sysdig

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

You can find information about the services that generate metrics in the following documentation topic: [Cloud services](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-cloud_services).


## Are you noticing connection problems between your infrastructure and Sysdig’s hosted service?
{: #faq_2}
{: faq}

Sysdig has identified an issue with a subset of agent versions:
- Sysdig agent 10.3.0
- Sysdig agent 10.3.1
- Sysdig agent 10.4.0
- Sysdig agent 10.4.1 

Where connectivity between your infrastructure and Sysdig’s hosted service may fail.

You must upgrade all Sysdig agents to `10.5`. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-troubleshoot#troubleshoot-entry-3).



## How can I find out the metrics that are collected per agent?
{: #faq_3}
{: faq}

In Sysdig, you can monitor your Sysdig agent by using the dashboard template **Sysdig Agent Health & Status** that is available in **Host Infrastructure**. In this dashboard, you can see the number of Sysdig agents that are deployed and connected to the Sysdig instance, check the version of the Sysdig agents, and find out how many metrics per host the agent is collecting.



