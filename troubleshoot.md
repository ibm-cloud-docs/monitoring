---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

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

# Troubleshooting for IBM Cloud Monitoring with Sysdig
{: #troubleshoot}

General problems with using IBM Cloud Monitoring with Sysdig might include xxx or xxx. In many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}

## Are you getting an error creating a capture?
{: #troubleshoot-entry-1}

You are failing to create a [capture file](/docs/services/Monitoring-with-Sysdig/captures.html#captures) for a host in your infrastructure. 

In the *Captures* section of the web UI, you get an error when you try to create a capture file for a host.
{: tsSymptoms}

The Sysdig agent that runs on the host has the feature **sysdig_capture_enabled** set to *false*.
{: tsCauses}

Enable the **sysdig_capture_enabled** feature in the Sysdig agent that runs on the host.
{: tsResolve}


## Is the status of your capture file set to *requested* and does not change to status *uploaded*?
{: #troubleshoot-entry-2}

The status of a [capture file](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures) is set to *requested* and does not change to status *uploaded*. You are waiting for the capture file to be available for analysis.

In the *Captures* section of the web UI, you the status of the capture file for a host does not change to *uploaded*.
{: tsSymptoms}

The host has the TCP port 6443 disabled.
{: tsCauses}


Check that port 6443 is opened. For more information, see [Managing network traffic](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send)
{: tsResolve}


