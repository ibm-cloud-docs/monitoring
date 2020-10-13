---

copyright:
  years:  2018, 2020
lastupdated: "2020-10-12"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Monitoring-with-Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Troubleshooting for {{site.data.keyword.mon_full_notm}}
{: #troubleshoot}

Learn more about some general problems that you might encounter when you use the {{site.data.keyword.mon_full_notm}} service. In many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}

## Are you getting an error when you create a capture?
{: #troubleshoot-entry-1}

You are failing to create a [capture file](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures) for a host in your infrastructure. 

In the *Captures* section of the web UI, you get an error when you try to create a capture file for a host.
{: tsSymptoms}

The Sysdig agent that runs on the host has the feature **sysdig_capture_enabled** set to *false*.
{: tsCauses}

Enable the **sysdig_capture_enabled** feature in the Sysdig agent that runs on the host.
{: tsResolve}


## Is the status of your capture file set to *requested* and does not change to status *uploaded*?
{: #troubleshoot-entry-2}

The status of a [capture file](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures) is set to *requested* and does not change to status *uploaded*. You are waiting for the capture file to be available for analysis.

In the *Captures* section of the web UI, the status of the capture file for a host does not change to *uploaded*.
{: tsSymptoms}

The host has the TCP port 6443 disabled.
{: tsCauses}


Check that port 6443 is opened. For more information, see [Managing network traffic](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-service-connection)
{: tsResolve}


# Are you noticing connection problems between your infrastructure and Sysdig’s hosted service?
{: #troubleshoot-entry-3}

Sysdig has identified an issue with a subset of agent versions:
- Sysdig agent 10.3.0
- Sysdig agent 10.3.1
- Sysdig agent 10.4.0
- Sysdig agent 10.4.1 

Where connectivity between your infrastructure and Sysdig’s hosted service may fail. For more information, see [Sysdig Release Notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html).

If you are experiencing connectivity issues, complete the following steps:

1. Check the version of the Sysdig agent.

    You can view the dashboard template **Sysdig Agent Health & Status** that is available in **Host Infrastructure** to check the version of your Sysdig agents.

2. [Upgrade your Sysdig agent](https://docs.sysdig.com/en/agent-upgrade.html) to version 10.5 as soon as possible to ensure a reliable flow of metrics and data into our systems.



