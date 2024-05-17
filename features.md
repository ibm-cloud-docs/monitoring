---

copyright:
  years:  2018, 2024
lastupdated: "2024-05-17"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# Features
{: #features}

You can use {{site.data.keyword.mon_full}} to monitor the performance and overall system health of your organization.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} enables monitoring of cloud, Kubernetes and VM infrastructure, applications and services, including managed service for Prometheus. Monitor multi-cloud environments in a single dashboard using agents running on other clouds.

* For Kubernetes, monitor status, health and performance of cluster, workloads and pods, prioritize issues with actionable insights from live logs and resources manifests with built-in remediation steps, and optimize resource utilization by understanding cluster capacity and right-sizing workloads.

* Centralize Prometheus monitoring with Remote Write for scale and long term retention, and extend monitoring to hundreds of applications and services using Prometheus exporters or custom metrics.

* Monitor {{site.data.keyword.cloud_notm}} platform services with built-in metrics and dashboards.

* Identify health and performance issues in bare metal hosts, {{site.data.keyword.cloud_notm}} VSIs or other VMs, such as VMware, along with support for zLinux and Windows environments.

* {{site.data.keyword.mon_full_notm}} provides a single operational solution for workloads deployed in a multicloud environment by deploying agents to the resources deployed outside {{site.data.keyword.cloud_notm}} and sending metrics back to the managed service.


## Monitor and troubleshoot hosts running in {{site.data.keyword.cloud_notm}}, outside {{site.data.keyword.cloud_notm}}, or on-prem
{: #features-1}

For orchestrated environments, you can monitor the status, the health, and the performance of clusters, workloads, and pods.

For non-orchestrated environments, you can identify health and performance issues in baremetal hosts, IBM Cloud VSIs or other VMs such as VMware.

You can also monitor zLinux and Windows environments.

- Optimize resource utilization by understanding the capacity of the host and sizing workloads accordingly.

- Reduce risk by leveraging flexible permission management with {{site.data.keyword.cloud_notm}} IAM and custom roles


## Monitor and troubleshoot {{site.data.keyword.cloud_notm}} services by monitoring Platform Metrics
{: #features-2}

- Collect built-in metrics for resources and services on {{site.data.keyword.cloud_notm}}.

- Benefit from seamless integration for more than 30 {{site.data.keyword.cloud_notm}} services with out-of-the-box dashboards and alerts.


## Centralize your Prometheus monitoring with Remote Write for scale and long term retention
{: #features-3}

- Extend monitoring to hundreds of applications and services by using Prometheus exporters or custom metrics.


## Accelerate the diagnosis and resolution of performance incidents
{: #features-4}

- {{site.data.keyword.mon_full_notm}} offers deep visibility into your infrastructure and applications with the ability to troubleshoot from service level all the way down to the system level. Pre-defined dashboards and alerts simplify identification of potential threats or problems. By using {{site.data.keyword.mon_full_notm}}, developers and DevOps teams monitor and troubleshoot performance issues in real-time, identify the source of errors, and eliminate problems.

- Use queries in dashboards and alerts with the form query UI or enriched metrics PromQL.


## Control the cost of your monitoring infrastructure
{: #features-5}

{{site.data.keyword.mon_full_notm}} includes functionality that help you control the cost of your monitoring infrastructure in the {{site.data.keyword.cloud_notm}}. You can configure the metric sources for which you want to monitor their performance.



## Get critical Kubernetes and container insights for dynamic microservice monitoring
{: #features-6}

{{site.data.keyword.mon_full_notm}} auto-discovers Kubernetes environments providing out-of-the-box dashboards and alerts for clusters, nodes, namespaces, services, deployments, pods and more. A single agent per node dynamically discovers all microservices and auto-collects metrics and events from various sources including Kubernetes, hosts, networks, containers, processes, applications and custom metrics like Prometheus, JMX, and StatsD.

## Mitigate the impact of abnormal situations with proactive notifications
{: #features-7}


{{site.data.keyword.mon_full_notm}} includes alerts and multi-channel notifications that you can use to reduce the impact on your day to day operations and accelerate your reaction and response time to anomalies, downtime, and performance degradation. Notification channels that you can easily configure such as *email*, *slack*, *PagerDuty*, or *Webhooks*.

## Identify software vulnerabilities
{: #features-8}

Use the {{site.data.keyword.sysdigsecure_full_notm}} service to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions and compliance from source to run.

An {{site.data.keyword.sysdigsecure_full_notm}} instance can be connected to an {{site.data.keyword.mon_full_notm}} instance allowing data to be provided to both services by a single agent.

For more information about {{site.data.keyword.sysdigsecure_full_notm}}, see the [{{site.data.keyword.sysdigsecure_full_notm}} documentation.](/docs/workload-protection)
