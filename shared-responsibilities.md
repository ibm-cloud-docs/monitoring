---

copyright:
  years: 2019
lastupdated: "2019-11-12"

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

# Understanding your responsibilities when using {{site.data.keyword.mon_full_tm}}
{: #your-id}
<!-- The title of your H1 should be Understanding your responsibilities with using _service-name_, where _service-name_ is the non-trademarked short version conref. -->

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.mon_full_tm}}. For a high-level view of the service types in {{site.data.keyword.Bluemix}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyboard.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.mon_full_notm}}. For the overall terms of use, see [{{site.data.keyword.Bluemix}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

  
## Incident and operations management
{: #incident-and-ops}

You and IBM share responsibilities for the set up and maintenance of your {{site.data.keyword.mon_full_notm}} service instance for monitoring your application and infrastructure workloads. You are responsible for incident and operations management of your application data.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Availability | Provide high availability capabilities, such as IBM-owned infrastructure in multizone regions, to meet local access and low latency requirements for each supported region.  | Use the list of [available regions](/docs/Monitoring-with-Sysdig?topic=Sysdig-endpoints) to plan for and create new instances of the service. |
| Sysdig agents | Provide images and instructions for how to install the Sysdig agents in environments to be monitoring ( ie. Kubernetes, Linux, Openshift ). | Install the Sysdig agents and monitor that the agents are running in your environment ( Sysdig alerts can help with this ) |
| Platform metrics | Deliver platform metrics for Sysdig-enabled services to your Sysdig instances in the region where the platform metrics are generated.  | Configure a monitoring instance for platform metrics in each region in order to receive platform metrics into your monitoring instance. |
| Incidents | Provide notifications for planned maintenance, security bulletins, or unplanned outages | Set preferences to [receive emails about platform notifications](/docs/overview?topic=overview-ui#email-prefsl), and monitor the [IBM Cloud status page](https://{DomainName}/status?selected=announcement) for general announcements.  |
{: caption="Table 1. Responsibilities for incident and operations" caption-side="top"}


## Change management
{: #change-management}

You and IBM share responsibilities for keeping {{site.data.keyword.mon_full_notm}} service components at the latest version. You are responsible for change management of your Sysdig agents and the dashboard and alert definitions.


| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Sysdig service | Provide regular updates to the service with new features and security fixes | |
| Sysdig agents | Provide regular updates to the agent with new features and security fixes and document changes in the [Agent release notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html)  | Install updates to the agent and keep them up to date as new versions are made available |
| Defining Dashboards and Alerts | Update the default dashboard and alert definitions as requirements change | You are responsible for updating your own dashboard and alert definitions and tracking changes to those dashboards via your own change management processes. |
{: caption="Table 2. Responsibilities for change management" caption-side="top"}


## Identity and access management
{: #iam-responsibilities}

IBM is responsible for the security and compliance of {{site.data.keyword.mon_full_notm}}. You are responsible for defining the IAM policies to control which users within your account have access to the monitoring data.


| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Sysdig service | Provide the ability to restrict access to resources | Depending on your needs, restrict access to resources and service functionality by using Cloud IAM access policies. For more information, see [Managing user access](https://cloud.ibm.com/docs/key-protect?topic=key-protect-manage-access). |
{: caption="Table 3. Responsibilities for identity and access management" caption-side="top"}

## Security and regulation compliance
{: #security-compliance}

IBM is responsible for the security and compliance of {{site.data.keyword.mon_full_notm}}. You are responsible for ensuring that metrics containing regulated data is not provided to the {{site.data.keyword.mon_full_notm}} service.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Compliance | Maintain controls that are commensurate to various industry compliance standards, such as SOC and ISO. | Ensure that regulated data is not provided to the {{site.data.keyword.mon_full_notm}} service |
{: caption="Table 4. Responsibilities for security and regulation compliance" caption-side="top"}

## Disaster recovery
{: #disaster-recovery}

IBM is responsible for the recovery of {{site.data.keyword.mon_full_notm}} components in case of disaster. You are responsible for the recovery of the Sysdig agents running in your environment should they be impacted by a disaster.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Sysdig service | Back up metric data and metadata in the region that the service operates in at least every 24 hrs, and automatically recover and restart service components after any disaster event. |  |
| Sysdig agents |  | Reinstalling or reconfiguring the Sysdig agents in the event of any disaster event impacting the agent runtime. |
{: caption="Table 5. Responsibilities for disaster recovery" caption-side="top"}
