---

copyright:
  years: 2018
lastupdated: "2018-11-21"

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

You are failing to create a [capture file](/docs/services/Monitoring-with-Sysdig/captures.html#captures) for a host in your infrastructure to analyze what is happening during a time frame. 

In the *Captures* section of the web UI, you get an error when you try to create a capture file for a host.
{: tsSymptoms}

* The host has the TCP port 6643 disabled.
* The Sysdig agent that runs on the host has the feature **sysdig_capture_enabled** set to *false*.
{: tsCauses}


1. Check that port 6643 is opened. For more information, see [Managing network traffic](/docs/services/Monitoring-with-Sysdig/network.html#send).
2. Enable the **sysdig_capture_enabled** feature in the Sysdig agent that runs on the host.
{: tsResolve}
