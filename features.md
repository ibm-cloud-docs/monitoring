---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-10"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# Features
{: #features}

You can use {{site.data.keyword.mon_full}} to monitor the performance and overall system health of your organization.
{: shortdesc}

By using the {{site.data.keyword.mon_short}} service, you can improve operational performance with out-of-the-box dashboards, alerts and prioritized insights into cloud-native applications and services. You can monitor hosts such as Kubernetes clusters, {{site.data.keyword.redhat_openshift_notm}} clusters, Virtual machines (VM) or VMware solutions. You can monitor hosts that run in {{site.data.keyword.cloud_notm}}, outside {{site.data.keyword.cloud_notm}}, or on-prem. You can also monitor your {{site.data.keyword.cloud_notm}} services and unify observability across {{site.data.keyword.cloud_notm}} and other hybrid or multi-cloud environments. In addition, you can simplify and scale your Prometheus monitoring as your infrastructure grows; the {{site.data.keyword.mon_short}} service includes a managed service for Prometheus.


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
