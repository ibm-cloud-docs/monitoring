---

copyright:
  years: 2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, customer responsibilities, IBM responsibilities, terms and conditions

subcollection: Monitoring-with-Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Understanding your responsibilities when using {{site.data.keyword.mon_full_notm}}
{: #shared-responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.mon_full_notm}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.mon_full_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

  
## Incident and operations management
{: #incident-and-ops}

You and {{site.data.keyword.IBM_notm}} share responsibilities for the set up and maintenance of your {{site.data.keyword.mon_full_notm}} service instance for monitoring your application and infrastructure workloads. You are responsible for incident and operations management of your application data.
{: note}

| Task              | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-------------------|-------------------------------------------------|-----------------------|
| `Monitor incidents`  | Provide notifications for planned maintenance, security bulletins, or unplanned outages. | Set preferences to [receive emails about platform notifications](/docs/overview?topic=overview-ui#email-prefsl). </br>Monitor the [IBM Cloud status page](https://{DomainName}/status?selected=announcement) for general announcements. |
| `Maintain {{site.data.keyword.cloud_notm}} high availability SLA`  | Operate the {{site.data.keyword.contdelivery_short}} service in accordance with the {{site.data.keyword.cloud_notm}} Public [Service Level Agreements (SLAs)](/docs/overview/terms-of-use?topic=overview-slas). |   |
| `Provide high availability capabilities` | Provide capabilities, such as {{site.data.keyword.IBM_notm}}-owned infrastructure in multizone regions (MZR), to meet local access and low latency requirements for each supported region.  | Use the list of [available regions](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints) to plan for and create new instances of the service. |
| `Monitor monitoring agents`   | Provide images and instructions for how to install monitoring agents in environments that you want to monitor, such as Kubernetes, Linux, Openshift. | Install and configure monitoring agents. </br>Monitor that the agents are running in your environment, for example, by using monitoring alerts. |
| `Deliver platform metrics`  | Deliver platform metrics for Sysdig-enabled services to the monitoring instance that collects platform metrics and is located in the region where the platform metrics are generated.  | Configure 1 monitoring instance per region to collect platform metrics in that region. |
{: caption="Table 1. Responsibilities for incident and operations" caption-side="top"}



## Change management
{: #change-management}

You and {{site.data.keyword.IBM_notm}} share responsibilities for keeping {{site.data.keyword.mon_full_notm}} service components at the latest version. You are responsible for change management of your monitoring agents, dashboards, and alert definitions.
{: note}

| Task                                                    | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|---------------------------------------------------------|-----------------------|--------|
| `Update the {{site.data.keyword.mon_full_notm}} service` | Provide regular updates to the service with new features, fixes for defects, and security fixes. |   |
| `Update the monitoring agent image that is hosted in {{site.data.keyword.cloud_notm}}` | Provide regular updates to the monitoring agent image with new features, fixes to defects, and security fixes. Document changes in the [Agent release notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html)  | Update the agent to keep it up to date as new versions are made available. |
| `Update default dashboards `                            | Update the default dashboards as requirements change. | Update custom dashboards and track changes by using your own change management process. |
| `Update pre-defined alert definitions`                  | Update the default alert definitions as requirements change. | Update custom alert definitions and track changes by using your own change management process. |
| `Track versions of custom dashboards, alerts, notifications, and teams`    |   | Use your own change management process to control versions of monitoring resources such as dashboards, alert definitions, teams, and notifications. | 
{: caption="Table 2. Responsibilities for change management" caption-side="top"}


## Identity and access management
{: #iam-responsibilities}

{{site.data.keyword.IBM_notm}} is responsible for the security and compliance of {{site.data.keyword.mon_full_notm}}. You are responsible for defining the {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) policies to control which users within your account have access to the monitoring data.
{: note}

| Task                           | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------|-------------------------------------------------|-----------------------|
| `Manage platform permissions`  | Allow administrators to control access to manage resources in the {{site.data.keyword.cloud_notm}}. | Grant, revoke, and manage access to service instances by using IAM. | 
| `Manage service permissions`   | Allow administrators to control access to work with the {{site.data.keyword.mon_full_notm}}. | Grant, revoke, and manage access to monitoring features by using IAM. |
| `Control monitoring data access` | Allow administrators to control access to metrics data and metadata through Sysdig teams. | Grant, revoke, and manage access to monitoring data by using IAM. |
{: caption="Table 3. Responsibilities for identity and access management" caption-side="top"}

[Learn more about controlling access through IAM](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-iam).


## Security and regulation compliance
{: #security-compliance}

{{site.data.keyword.IBM_notm}} is responsible for the security and compliance of {{site.data.keyword.mon_full_notm}}. You are responsible for ensuring that metrics, that contain regulated data, are not provided to the {{site.data.keyword.mon_full_notm}} service.
{: note}

| Task                                       | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------------------|-------------------------------------------------|-----------------------|
| `Meet security and compliance objectives`  | Maintain controls that are commensurate to supported industry compliance standards, such as SOC. | Ensure that regulated data is not provided to the {{site.data.keyword.mon_full_notm}} service. |
{: caption="Table 4. Responsibilities for security and regulation compliance" caption-side="top"}



## Disaster recovery
{: #disaster-recovery}

{{site.data.keyword.IBM_notm}} is responsible for the recovery of {{site.data.keyword.mon_full_notm}} components in case of disaster.
{: note}

| Task                                                            | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-----------------------------------------------------------------|-------------------------------------------------|-----------------------|
| `Service`         | Automatically recover and restart service components after any disaster event. |   |
| `Data`            |   |Extract and save data, dashboards definitions, and alert definitions if you cannot afford for it to be lost in the event of an un-recoverable event. | 
| `monitoring agent`    |   |  Recovery of the monitoring agents running in your environment should they be impacted by a disaster. |
{: caption="Table 5. Responsibilities for disaster recovery" caption-side="top"}

