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

You are trying to create a [capture file](/docs/services/Monitoring-with-Sysdig/captures.html#captures) for a host to analyze what happens in that host during a time frame. 

Description of the troubleshooting entry symptom.
{: tsSymptoms}

In the *Captures* section of the web UI, you get an error when you try to create a capture file for a host.

Description of the troubleshooting entry cause.
{: tsCauses}

The Sysdig agent that runs on the host has the feature **sysdig_capture_enabled** set to *false*.

Description of the troubleshooting entry resolution.
{: tsResolve}

Enable the **sysdig_capture_enabled** feature in the Sysdig agent that runs on the host.

