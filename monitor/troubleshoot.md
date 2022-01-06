---

copyright:
  years:  2018, 2022
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, troubleshooting

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting for {{site.data.keyword.mon_full_notm}}
{: #troubleshoot}

Learn more about some general problems that you might encounter when you use the {{site.data.keyword.mon_full_notm}} service. In many cases, you can recover from these problems by following a few easy steps.
{: shortdesc}

## Are you getting an error when you create a capture?
{: #troubleshoot-entry-1}

You are failing to create a [capture file](/docs/monitoring?topic=monitoring-captures#captures) for a host in your infrastructure. 

In the *Captures* section of the web UI, you get an error when you try to create a capture file for a host.
{: tsSymptoms}

The monitoring agent that runs on the host has the feature **sysdig_capture_enabled** set to *false*.
{: tsCauses}

Enable the **sysdig_capture_enabled** feature in the monitoring agent that runs on the host.
{: tsResolve}


## Is the status of your capture file set to *requested* and does not change to status *uploaded*?
{: #troubleshoot-entry-2}

The status of a [capture file](/docs/monitoring?topic=monitoring-captures#captures) is set to *requested* and does not change to status *uploaded*. You are waiting for the capture file to be available for analysis.

In the *Captures* section of the web UI, the status of the capture file for a host does not change to *uploaded*.
{: tsSymptoms}

The host has the TCP port 6443 disabled.
{: tsCauses}


Check that port 6443 is opened. For more information, see [Managing network traffic](/docs/monitoring?topic=monitoring-service-connection)
{: tsResolve}


## Are you seeing errors when there are no problems? 
{: #troubleshoot-entry-3}

Are you observing monitoring agent connection errors or receiving uptime alerts reporting an host is down when there are no problems?

{{site.data.keyword.mon_full_notm}} has identified an issue with a subset of agent versions:
- monitoring agent 10.3.0
- monitoring agent 10.3.1
- monitoring agent 10.4.0
- monitoring agent 10.4.1 

Where connectivity between your infrastructure and the {{site.data.keyword.mon_full_notm}} hosted service may fail. For more information, see [Release Notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html).

If you are experiencing connectivity issues, complete the following steps:

1. Check the version of the monitoring agent.

    You can view the dashboard template **monitoring agent Health & Status** that is available in **Host Infrastructure** to check the version of your monitoring agents.

2. [Upgrade your monitoring agent](/docs/monitoring?topic=monitoring-upgrade_agent) to version 10.5 as soon as possible to ensure a reliable flow of metrics and data into our systems.


## Are you getting access denied when running API calls?
{: #troubleshoot-entry-4}

When the authorization method that is allowed in a {{site.data.keyword.mon_full_notm}} instance is set to `IAM_ONLY`, you can get the following response `{"errors":[{"reason":"Not enough privileges to complete the action","message":"Access is denied"}]}`. 

First, [check the instance authorization methods that are allowed](/docs/monitoring?topic=monitoring-iam_instance_auth#iam_instance_auth_step1).

Then, review [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam) and [Token headers](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-sysdig) before you retry the request.

