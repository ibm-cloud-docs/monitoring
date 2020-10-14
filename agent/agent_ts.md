---

copyright:
  years:  2018, 2020
lastupdated: "2020-10-14"

keywords: Sysdig, IBM Cloud, monitoring, Sysdig agent, log level

subcollection: Monitoring-with-Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Troubleshooting problems with a Sysdig agent
{: #agent_ts}

You can view and analyze the Sysdig agent log file to troubleshoot problems. You can also monitor the agent through the Sysdig web UI.
{:shortdesc}



You should set the log level to *info*, *debug*, or *trace* to troubleshoot agent-related issues.
{: tip}


The following table lists the locations of the Sysdig agent's logs per type of agent:

| Agent Type                                                    | Agent configuration file                  |
|---------------------------------------------------------------|-------------------------------------------|
| Sysdig agent as a service in a Linux system                   | `/opt/draios/logs/draios.log`             |
| Sysdig agent as a Docker container in a Linux system          | `/opt/draios/logs/draios.log`             |
| Sysdig agent as a pod in a standard Kubernetes environment    | ``             |
| Sysdig agent as a pod in an Openshift Kubernetes environment  | `l`             |
{: caption="Table 2. Log locations per type of agent" caption-side="top"} 


For example, consider the following use cases and the log section that you can configure to indicate the data that you want to log for an agent:

| Use cases                                     | Log section entry           |
|-----------------------------------------------|-----------------------------|
| Troubleshoot agent behavior                   | `file_priority: debug`      |
| Reduce container console output               | `console_priority: warning` |
| Filtering events by severity                  | `event_priority: warning`   |
| Verify what metrics are included or excluded  | `metrics_excess_log: true`  |
{: caption="Table 2. Log section entries" caption-side="top"} 



When troubleshooting agent behavior, increase the logging to debug for full detail:

Container Console Logging
If you are running the containerized agent, you can also reduce container console output by adding the additional parameter console_priority:with the same arguments [ none | error | warning | info | debug | trace ]

log:
  console_priority: warning
Note that troubleshooting a host with less than the default 'info' level will be more difficult or not possible. You should revert to 'info' when you are done troubleshooting the agent.





You can also customize the type of log and the entries that are collected by configuring the Sysdig agent configuration file **/opt/draios/etc/dragent.yaml**. After you edit the file, you must restart the agent at the shell with `docker restart sysdig-agent` to activate the changes.



## Checking the status of an agent
{: #agent_log_level_status}

### Linux Sysdig agent
{: #agent_log_level_status_linux}

To check the status of an agent, run the following command:

```
service dragent status
```
{: pre}



### Docker Sysdig agent
{: #agent_log_level_status_docker}

To check the status of an agent, run the following command:

```
docker ps | grep sysdig-agent
```
{: pre}


### Kubernetes Sysdig agent
{: #agent_log_level_status_kube}





## Using a dashboard to monitor the agent


## Defining an alert to notify when an agent is down



### Filtering Kubernetes events by severity
{: #change_kube_agent_filterby_severity}

* The **event_priority** in the **log** section controls the type of events that are sent from the agent
* The default log level is *information*. This means that only information and higher severity events are transmitted.
* Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*. **Note**: The values are listed from high priority to low priority.
* Setting the level to `none` will block all event collection.


