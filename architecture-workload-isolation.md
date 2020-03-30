---

copyright:
  years: 2020, 2020
lastupdated: "2020-03-16"

keywords: Sysdig, IBM Cloud, monitoring, security, connection

subcollection: Sysdig

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


# Learning about {{site.data.keyword.mon_full_notm}} architecture and workload isolation
{: #compute-isolation}

Review the following sample architecture for {{site.data.keyword.mon_full_notm}}, and learn more about different isolation levels so that you can choose the solution that best meets the requirements of the workloads that you want to run in the cloud.
{: shortdesc}



## {{site.data.keyword.mon_full_notm}} architecture
{: #architecture}

{{site.data.keyword.mon_full_notm}} is a highly available, multi-tenant, regional service that is available in {{site.data.keyword.cloud_notm}}. You can use it to monitor your applications, platform resources, and infrastructure.

![{{site.data.keyword.mon_full_notm}}](images/monitoring.svg "{{site.data.keyword.mon_full_notm}} high level architecture")



The agent lives on the hosts being monitored and collects the appropriate metrics and events.

### Backend Components (stateless)

The backend components connect with each other internally on port 9000.

| Component  | Description | Ports |
|------------|-------------|-------|
| `API Servers` | Provide a web and API interface to the Sysdig application. | `9000` |
| `Collectors`  | Agents connect here to deliver data to the Sysdig Monitor backend. | `9000` |
| `Workers`     | Process data aggregations and alerts. | `9000` |
{: caption="Table 3. Tasks grouping labels" caption-side="top"} 
	

### Cache Layer (stateful)

| Component  | Description | Ports |
|------------|-------------|-------|
| `Redis`    | An open-source (BSD licensed) data structure store used as an intra-service cache. | `6639` |
	


### Datastores (stateful)

| Component  | Description | Ports |
|------------|-------------|-------|
| `MySQL`    | Stores user credentials and environmental data | `3306` |
| `Elasticsearch` | Stores all events and metadata | `9200` |
| `Cassandra` | Stores all metrics | `9042` |

### Load Balancer Services

| Component  | Description | Ports |
|------------|-------------|-------|
| `lb-api service` | Load balancer for API server | `80` </br>`443` |
| `lb-collector service` | Load balancer for collector | `6443` </br>`6666` |



## {{site.data.keyword.mon_full_notm}} workload isolation
{: #workload-isolation}

A single instance of the {{site.data.keyword.mon_full_notm}} service and its underlying components serves multiple tenants, also known as user accounts.
* There is 1 instance of the {{site.data.keyword.mon_full_notm}} service per region that is responsible for running user workloads in the region.
* Each instance of the {{site.data.keyword.mon_full_notm}} service in a region is highly available. [Learn more](/docs/Monitoring-with-Sysdig?topic=Sysdig-ha-dr).
* The monitoring data that is collected and processed by the {{site.data.keyword.mon_full_notm}} service for an account is isolated and invisible to the other accounts, ensuring data security and privacy for all tenants. 
* Within an account, monitoring data is isolated per instance within a region. 
* The {{site.data.keyword.mon_full_notm}} service offers soft isolation for data storage. Each account has its own schema in each of the different data stores that are part of the {{site.data.keyword.mon_full_notm}} service.

You can use {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to control which users see, create, use, and manage resources in your account. [Learn more](/docs/Monitoring-with-Sysdig?topic=Sysdig-iam).
* To grant access to manage the {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}, you can assign platform roles that define users levels of access for completing platform management tasks and accessing account resources. 
* To grant access to manage the Sysdig monitoring instance and its resources, you can assign service roles that define users levels of access for viewing data and managing features such as dashboards, teams, and alerts.

Within a Sysdig instance, you can define teams to group users and control what data and resources are available for members of a team. 
* Adding users to a team is managed through IAM policies. [Learn more](/docs/Monitoring-with-Sysdig?topic=Sysdig-iam#iam_policies_team).
* User access to view, manage, and monitor data is granted through IAM policies.


