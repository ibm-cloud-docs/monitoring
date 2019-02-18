---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Customizing the Sysdig agent to control data
{: #customize_agent}

By default, the Sysdig agent collects data from a range of platforms and applications. You can edit the agent config file to change its default behavior, and include or exclude data. You can customize the Sysdig agent configuration file to include custom metrics such as JMX, StatsD, and Prometheus. You also can filter out metrics, event data, and containers.
{:shortdesc}

## Customizing the Kubernetes Sysdig agent
{: #kube}

The Kubernetes Sysdig agent uses two configuration files that specify what data to collect automatically:

| File name                        | Actions           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modify log level. |
| `sysdig-agent-configmap.yaml`    | Block ports. </br>Include or exclude metric data. </br>Add or remove events. </br>Filter out containers. |
{: caption="Table 1. Kubernetes Sysdig agent configuration files" caption-side="top"} 

To edit a Kubernetes Sysdig agent, you might need to edit the *sysdig-agent-configmap.yaml*, the *sysdig-agent-daemonset-v2.yaml*, or both.

There are two methods that you can use to modify a configuration file:
* Method 1: Modify the file directly on the cluster where the agent is running. For more information, see [Editing the Kubernetes Sysdig agent configuration by using kubectl edit](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_edit_kube_agent_method1).
* Method 2: Modify the file locally and apply the changes to the cluster. For more information, see [Editing the Kubernetes Sysdig agent configuration by using kubectl apply](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_edit_kube_agent_method2).

You can add tags to the data that is collected by the agent. 
* Use these tags to help you manage the data that you monitor. 

    * Use labels to group infrastructure resources into logical hierarchies, filter out data, and split aggregated data into segments. 
    
    * Customize how data is aggregated when you configure a graph or create an alert for a metric. 
    
    * Set the scope of a dashboard, a panel, or an alert to filter out data points. 
    
    * Restrict access to data by managing users' data access through teams. 
    
    * For more information on how to manage data, see [Managing data](/docs/services/Monitoring-with-Sysdig/manage.html#manage).

* For information on how to add tags, see [Adding more tags to data collected from a Kubernetes Sysdig agent](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_add_tags). 


**You can customize what data is collected by the Sysdig agent.** 

When you exclude events, metrics, and containers, consider the following information:
* You can reduce agent and backend load.
* You only collect data from containers that you want to monitor.
* You can control costs by reporting on important containers, and filtering out unnecessary or not critical containers.
* You can configure the Kubernetes events that you want to monitor. For more information, see [Collecting a set of Kubernetes events](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_collect_events).

The following list outlines actions that you can perform to control the data that is collected by the Sysdig agent:
* [Disabling collection of events](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_disable_events)
* [Including and excluding metrics](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_inc_exc_metrics)
* [Filtering kubernetes objects and containers from which data is collected](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_filter_data)
* [Blocking ports](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_block_ports)
* [Filtering Kubernetes events by severity](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_filterby_severity)

You can customize the type of log and the entries that are collected too. For more information. see [Changing the log level](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_log_level).

You can also log the list of metrics fir which the agent reports data. For more information, see [Logging into a file what metrics are included or excluded](/docs/services/Monitoring-with-Sysdig/change_kube_agent.html#change_kube_agent_log_metrics).

The Sysdig agent generates log entries in */opt/draios/logs/draios.log*. 
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.
* Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*
* The default log level is *info*, where an entry is created for each aggregated metrics transmission to the backend servers, once per second, in addition to entries for any warnings and errors.

The following table lists some common scenarios and the value that you must set in each one of them:

| Use cases                                     | Log section entry           |
|-----------------------------------------------|-----------------------------|
| Troubleshoot agent behavior                   | `file_priority: debug`      |
| Reduce container console output               | `console_priority: warning` |
| Filtering events by severity                  | `event_priority: warning`   |
| Verify what metrics are included or excluded  | `metrics_excess_log: true`  |

## Container Sysdig agent
{: #container}


The following list outlines actions that you can perform to control the data that is collected by the Sysdig agent:
* [Disabling collection of events](/docs/services/Monitoring-with-Sysdig/change_container_agent.html#change_container_agent_disable_events)
* [Including and excluding metrics](/docs/services/Monitoring-with-Sysdig/change_container_agent.html#change_container_agent_inc_exc_metrics)
* [Filtering containers from which data is collected](/docs/services/Monitoring-with-Sysdig/change_container_agent.html#change_container_agent_collect_docker_events)
* [Blocking ports](/docs/services/Monitoring-with-Sysdig/change_container_agent.html#change_container_agent_block_ports)
* [Filtering events by severity](/docs/services/Monitoring-with-Sysdig/change_container_agent.html#change_container_agent_filterby_severity)

You can customize the type of log and the entries that are collected too. For more information. see [Changing the log level](/docs/services/Monitoring-with-Sysdig/change_container_agent.html#change_container_agent_log_level).



## Linux Sysdig agent
{: #linux}

The Linux Sysdig agent uses two configuration files that specify what data to collect automatically:

| File                   | Description                                                     | Location                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Main configuration file </br>**Note:****Do not edit this file.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Configuration file that you edit to customize the Sysdig agent. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Table 1. Sysdig agent configuration files" caption-side="top"} 

You can edit the *dragent.yaml* file to customize the data that is collected. Changes take effect immediately after you save the file. The agent detects the change and automatically restarts. You can find the frequency and the files that a Sysdig agent checks in the *dragent.default.yaml* file. For more information, see [Editing the dragent yaml file](/docs/services/Monitoring-with-Sysdig/change_agent.html#change_linux_agent_edit_agent).

For example, a *dragent.default.yaml* includes the following information:

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

The following list outlines actions that you can perform to control the data that is collected by the Sysdig agent:
* [Including and excluding metrics](/docs/services/Monitoring-with-Sysdig/change_agent.html#change_linux_agent_inc_exc_metrics)
* [Blocking ports](/docs/services/Monitoring-with-Sysdig/change_agent.html#change_linux_agent_block_ports)

You can customize the type of log and the entries that are collected too. For more information. see [Changing the log level](/docs/services/Monitoring-with-Sysdig/change_agent.html#change_linux_agent_log_level).


