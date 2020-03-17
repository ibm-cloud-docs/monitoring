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

_Review the following example: https://cloud.ibm.com/docs/containers?topic=containers-service-arch. Review the System Architecture Guide: https://pages.github.ibm.com/CloudEngineering/system_architecture/services/multitenancy.html. Provide an architectural overview diagram identifying what runs within the IBM Service Account and what runs in the customer's account._

## {{site.data.keyword.mon_full_notm}} workload isolation
{: #workload-isolation}

_Document how customer workloads are isolated from each other by plan. Do customer workloads run within the customer account?  Are customer workloads isolated within Kubernetes namespaces? Do customer workloads run on dedicated compute? Check out the example from Kubernetes: https://cloud.ibm.com/docs/containers?topic=containers-service-arch#worker-components_
