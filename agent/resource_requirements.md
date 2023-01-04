---

copyright:
  years:  2022, 2023
lastupdated: "2022-10-06"

keywords: IBM Cloud, monitoring, monitoring agent, agent requirements

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Kubernetes resource requirements
{: #resource_requirements}

The resource requirements for the {{site.data.keyword.mon_full}} agent depend on the size and load of the monitored host. The greater the activity the greater the resource requirements.
{: shortdesc}

{{site.data.keyword.mon_short}} can consume between 5 KB to 20 KB of bandwidth. The following can affect the bandwidth required:

* The number of metrics

* The number of events

* The number of Kubernetes objects

* The enabled products and features

When data is collected you will see a spike in bandwidth usage while the file is being ingested.

You do not want to place bandwidth shaping or caps on the agent. Doing so can affect data sent to the collection service.
{: note}

In general, in larger clusters, the agent requires more memory. In servers with a larger number of cores the agent requires more CPU cores to monitor system calls. CPU cores are used on the host and Kubernetes nodes visible to the agent as proxies.

Consider the following environment definitions.

| Environment size | Description |
| -------------- | -------------- |
| Small | 8 or less CPU cores  \n 10 or less Kubernetes nodes |
| Medium | Between 9 and 32 CPU cores  \n Between 10 and 100 Kubernetes nodes |
| Large | More than 32 CPU cores  \n More than 100 Kubernetes nodes |
{: caption="Table 1. Example environment sizings" caption-side="bottom"}

The following recommendations can improve behavior instead of when you use default values. Your environment might require different resources depending on your requirements. The values should only be used for general information.
{: important}

| Cluster configuration | Small | Medium | Large |
| -------------- | -------------- | -------------- | ---- |
| Kubernetes CPU request | 1 | 3 | 5 |
| Kubernetes CPU limit | 1 | 3 | 5 |
| Kubernetes Memory Request | 1024 MB | 3072 MB | 6144 MB |
| Kubernetes Memory Limit | 1024 MB | 3072 MD | 6144 MB |
| Dragent Memory Watchdog | 512 MB | 1024 MB | 2048 MB |
| Cointerface Memory Watchdog | 512 MB | 2048 MB | 4096 MB |
{: caption="Table 2. Configuration considerations based on environment sizes" caption-side="bottom"}

The {{site.data.keyword.mon_short}} agent has its own memory watchdog to prevent runaway memory consumption on the host in case of memory leaks. The [agent configuration file](/docs/monitoring?topic=monitoring-change_kube_agent) can be modified to meet your environment needs.

By default the following is configured:

```yaml
watchdog:
  max_memory_usage_mb: 1024
  max_memory_usage_subprocesses:
    sdchecks: 128
    sdjagent: 256
    mountedfs_reader: 32
    statsite_forwarder: 32
    cointerface: 512
    promscrape: 640
```
{: codeblock}

The `max_memory_usage` value corresponds to the dragent process in the agent. All values are specified in MB. For example if you want to change the configuration to match the watchdog settings for a large environment you would specify the following:

```yaml
watchdog:
  max_memory_usage_mb: 2048
  max_memory_usage_subprocesses:
    sdchecks: 128
    sdjagent: 256
    mountedfs_reader: 32
    statsite_forwarder: 32
    cointerface: 4096
    promscrape: 640
```
{: codeblock}

The value for `promscape` depends on the amount of timeseries and label data to be scraped on a particular node. The cluster size does not affect `promscape` memory usage.
{: note}
