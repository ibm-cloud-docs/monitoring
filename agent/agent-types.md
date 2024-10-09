---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Choosing an agent type by infrastructure
{: #agent-types}

To monitor your infrastructure, network, and applications with the {{site.data.keyword.mon_full}} service, you can deploy {{site.data.keyword.mon_short}} agents on supported hosts.
{: shortdesc}

## About agent types
{: #agent-types-ov}

You configure an agent by choosing an agent type.

The type of the agent determines the metrics that are collected automatically for a host. You can choose from an agent for orchestrated environments or an agent for non-orchestrated environments. For more information, see [Collecting default metrics by using the {{site.data.keyword.mon_short}} agent](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-2).

If you have connected an instance of {{site.data.keyword.sysdigsecure_full_notm}} to your {{site.data.keyword.mon_full_notm}} instance, the agent will provide data to both services without having to configure two separate agents. For more information about connecting the services, see [Can {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.sysdigsecure_full_notm}} be used together?](/docs/monitoring?topic=monitoring-faq#faq_4)
{: note}

## Choosing metric collection method by infrastructure
{: #agent-types-by-host}

The following table shows the options that you can choose to monitor a host by type of infratsructure:


| Type                         | Infrastructure       | Non-Orchestrated environments | Orchestrated environments |
|------------------------------|----------------------|------------------|-----------------|
| Orchestrated environment     | Kubernetes clusters  |  | Supported |
| Orchestrated environment     | OpenShift clusters   |  | Supported |
| Non-Orchestrated environment | Virtual Machines (VM)  | Supported | Supported |
| Non-Orchestrated environment | Bare metal servers | Supported | Supported |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) | Supported | Supported |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) on VPC | Supported | Supported |
| Non-Orchestrated environment | Linux based Virtual Machines (VM) on VMware | Supported | Supported |
{: caption="Mode by infrastructure" caption-side="top"}

You can configure an agent on hosts in the {{site.data.keyword.cloud_notm}}, on-prem, and in other clouds.
{: note}

​
