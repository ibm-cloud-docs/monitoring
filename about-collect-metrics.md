---

copyright:
  years:  2018, 2025
lastupdated: "2025-02-27"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# Collecting metrics
{: #about-collect-metrics}

You can collect metrics from a number of platforms, orchestrators, and a wide range of applications such as Prometheus, JMX, StatsD, Kubernetes, and other application stacks, that are available in the {{site.data.keyword.cloud}}, outside the {{site.data.keyword.cloud_notm}}, or on-prem. You can also add more metrics by creating custom metrics and adding integrations.
{: shortdesc}


## Metrics and labels
{: #about-collect-metrics-1}

A metric is a quantitative measure that has one or more labels to define its characteristics.

Use metrics to analyze statistically data that has numerical values.
{: note}

A metric is represented by time series. A time-series is a unique combination of a metric name and label key-value pairs. For example: `website_failedRequest |region='Asia', customer_ID='abc'`. A data-point is the value generated for a time-series at a given point in time.

Labels are classified as infrastructure labels and metric descriptor labels. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels.

You can use labels to identify and differentiate characteristics of a metric, for example,
* You can group infrastructure objects into logical hierarchies.
* You can filter out data.
* You can split aggregated data into segments.




## Collecting default metrics by using the {{site.data.keyword.mon_short}} agent
{: #about-collect-metrics-2}

When you configure a {{site.data.keyword.mon_short}} agent, data for default metrics is automatically collected. These metrics include metadata that you can use to label, segment, and display metrics when you monitor them. You do not need additional instrumentation or configuration in your hosts to obtain metrics that are collected automatically by the agent to gain insight into what is happening in them.

To monitor your infrastructure, network, and applications with the {{site.data.keyword.mon_full}} service, you can deploy {{site.data.keyword.mon_short}} agents on supported hosts. The host determines the agent type that you can deploy. The agent type determines the metrics that are collected automatically for that host.


To start collecting default metrics, you must configure a {{site.data.keyword.mon_short}} agent per environment that you want to monitor.

The {{site.data.keyword.mon_short}} agent automatically collects the following types of system metrics per host:

- `System hosts metrics` provide information about CPU, memory, and storage usage metrics, that you can use to analyze the performance and resource utilization of all your processes.

- `File and File System metrics` provide information about files and file system that you can use to analyze file interactions that occur in your system. For example, you can find information about your open files, bytes going in and out, or the percentage of usage of a given file system.

- `Process metrics` provide information about the processes that run in your servers. For example, you can use these metrics to  explore the number of processes, or get client or server information.

- `Network metrics` provide information about the network. They offer insight to the connections that are established between your applications, containers, and servers. For example, you can find information about the bytes that are being sent or received, or the number of HTTP requests, connections, and latency. In addition, for SQL or MongoDB, the agent collects additional information when it is configured in troubleshooting mode.

In addition, the {{site.data.keyword.mon_short}} agent automatically collects the following types of metrics per Kubernetes or {{site.data.keyword.redhat_openshift_notm}} cluster:

- `State metrics`: Kube state metrics report on the health and state of the various objects that run inside Kubernetes components, such as deployments, nodes and pods. To see the list of metrics that are collected by default, see [Kubernetes State](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/sysdig-legacy-format/kubernetes/kubernetes-state/){: external}.

- `Resource usage metrics`: Resource usage metrics reports on the health and state of CPU and memory for workers (nodes) and pods that are running in the cluster. The data can be analyzed by namespace, by worker, by pod, by workload object such as deployments, daemonSets, and more.


### Agent for non-orchestrated environments
{: #agent-modes-ov-light}

By default, this agent collects core infrastructure and network time series that you can use to monitor the host.

For a list of collected metrics, see [Metrics Available for non-orchestrated environments](https://docs.sysdig.com/en/docs/installation/sysdig-agent/agent-configuration/configure-agent-modes/metrics-available-in-monitor-light/).

### Agent for orchestrated environments
{: #agent-modes-ov-full}

By default, this agent collects the same metrics as the agent for non-orchestrated environments and also Kubernetes state and resource usage metrics.

For a list of collected metrics, see [Metrics Available for orchestrated environments](https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/metrics/metrics-library/prometheus-format/).



## Collecting custom metrics by using the {{site.data.keyword.mon_short}} agent
{: #about-collect-metrics-3}

The {{site.data.keyword.mon_short}} agent includes components that collect metrics via Syscall, StatsD, JMX, and Promscrape.

- The agent extracts information directly from the kernel through server system calls. System calls provide information about the processes that are running, memory allocation, network connections, access to the filesystem, resource usage, and more.

- The agent includes a lightweight Prometheus server known as *Promscrape*. You can configure the agent to collect Prometheus metrics and send them to a {{site.data.keyword.mon_short}} instance for storage and processing.

You must configure the {{site.data.keyword.mon_short}} agent by using Prometheus syntax to configure the `scrape_config` settings and define the targets, instances and jobs.
- Promscrape is based on the open-source Prometheus server.
- Different {{site.data.keyword.mon_short}} agent versions include different levels of support for collection of Prometheus metrics For example, {{site.data.keyword.mon_short}} agent v10.5.0 and above, includes Promscrape v2 and supports Prometheus native service discovery. For more information on the {{site.data.keyword.mon_short}} agent, see [{{site.data.keyword.mon_short}} agent release notes](https://docs.sysdig.com/en/docs/release-notes/sysdig-agent-release-notes/).
- For more information about Promscrape versions, see [Migrating from Promscrape V1 to V2](https://docs.sysdig.com/en/docs/sysdig-monitor/integrations/working-with-integrations/custom-integrations/collect-prometheus-metrics/migrating-from-promscrape-v1-to-v2/){: external}.

## Collecting custom metrics by using Prometheus remote write
{: #about-collect-metrics-4}

You can configure Prometheus remote write to collect metrics from environments where a {{site.data.keyword.mon_short}} agent is not available and send them to a {{site.data.keyword.mon_short}} instance.

You can collect metrics from:
- An existing Prometheus server.
- Ephemeral or batch jobs that may not exist long enough to be scraped by a {{site.data.keyword.mon_short}} agent.
- Windows hosts and other operating systems where the {{site.data.keyword.mon_short}} agent is not available
- Non-x86 based architectures, typically seen on IoT environments or Edge computing.
- Non-containerized workloads, such as NGNIX, custom applications, RabbitMQ, and others.

![Prometheus remote write option](/images/prometheus_rw.svg "Prometheus remote write"){: caption="Prometheus remote write" caption-side="bottom"}

You can monitor the metrics that are collected by using Prometheus remote write through the {{site.data.keyword.mon_short}} web UI. You can also use PromQL to query the data by using the standard Prometheus query language.

For more information, see [Collecting metrics by using Prometheus remote write](/docs/monitoring?topic=monitoring-prometheus_remote_write).

## Collecting custom metrics by using Prometheus exporters
{: #about-collect-metrics-5}

You can use Prometheus exporters to collect metrics from hosts, services, or apps which do not natively expose Prometheus-formatted metrics. You can monitor these metrics through a {{site.data.keyword.mon_short}} instance.
{: shortdesc}

There are different sources for Prometheus exporters:
- Official exporters are available in [the official Prometheus GitHub organization](https://github.com/prometheus){: external} and are lable **official**.
- Sysdig curates and maintains [an integrations library](https://docs.sysdig.com/en/docs/sysdig-monitor/integrations/integration-library/){: external}. The integrations library is an enterprise resource catalog where you can find supported {{site.data.keyword.mon_short}} integrations for Kubernetes platforms and cloud-native services.

You can collect metrics from different sources such as:
- Hosts for which a {{site.data.keyword.mon_short}} agent is not available such as Windows systems or VMware ESXi-Host systems.
- Hosts for which a {{site.data.keyword.mon_short}} agent is available, but you need to collect other types of metrics such as IPMI sensor metrics or hardware and kernel-relaed metrics.
- Services like MySQL database

![Prometheus integration with {{site.data.keyword.mon_short}}](/exporters/images/prometheus.svg "Prometheus integration with {{site.data.keyword.mon_short}}"){: caption="Prometheus integration with {{site.data.keyword.mon_short}}" caption-side="bottom"}

For more information, see [Collecting metrics by using Prometheus exporters](/docs/monitoring?topic=monitoring-prometheus-exporters).

## Collecting Platform metrics from {{site.data.keyword.cloud_notm}} services
{: #about-collect-metrics-6}

Platform metrics are metrics that are exposed by enabled-monitoring services and the platform in {{site.data.keyword.cloud_notm}}.

You can configure 1 instance only of the {{site.data.keyword.mon_full_notm}} service per region to collect *platform metrics* in that location.

To monitor platform metrics for a service instance, provision the {{site.data.keyword.mon_full_notm}} instance in the same region where the {{site.data.keyword.cloud_notm}} service instance that you want to monitor is provisioned.

For more information, see [Working with platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_working).
