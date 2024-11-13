---

copyright:
  years:  2018, 2024
lastupdated: "2024-11-13"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Frequently Asked Questions
{: #faq}

Frequently asked questions about {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Where can I find the list of Cloud services that generate metrics?
{: #faq_1}
{: faq}

You can find information about the services that generate metrics in the following documentation topic: [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).


## Are you seeing errors when there are no problems?
{: #faq_2}
{: faq}

Are you observing monitoring agent connection errors or receiving uptime alerts reporting an host is down when there are no problems?

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

## Can {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.sysdigsecure_full_notm}} be used together?
{: #faq_4}
{: faq}

The {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.sysdigsecure_full_notm}} services can be configured so operational performance monitoring and security vulnerability monitoring data can be obtained from a single monitoring agent running in your orchestrated and non-orchestrated environment.

You need to consider the following when connecting the two services:

* You can connect only one {{site.data.keyword.mon_full_notm}} instance to one {{site.data.keyword.sysdigsecure_full_notm}} instance.

* The connected {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.sysdigsecure_full_notm}} instances must be in the same account and region.

* Once connected, a single monitoring agent will provide data to both {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.sysdigsecure_full_notm}} connected instances.

* Once connected, the only way to disconnect the service instances is to delete either the {{site.data.keyword.mon_full_notm}} or {{site.data.keyword.sysdigsecure_full_notm}} service instance.

To provision connected services, see [Provisioning an instance](/docs/monitoring?topic=monitoring-provision#provision_ui).
