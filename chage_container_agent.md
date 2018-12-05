---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Customizing container Sysdig agents
{: #change_agent}

By default, the Sysdig agent collects data from a range of platforms and applications. You can edit the agent config file to change its default behavior, and include or exclude data. You can customize the Sysdig agent configuration file to include custom metrics such as JMX, StatsD, and Prometheus. You also can filter out metrics and containers.
{:shortdesc}


## Editing the dragent yaml file
{: #edit_agent}

The yaml file is loacated in */opt/draios/etc/*.

Complete the following steps to edit the file and apply the changes:

1. Access the *dragent.yaml* directly at `/opt/draios/etc/dragent.yaml`.
2. Edit the file. Use YAML systax.
3. Restart the agent. Run the following command:

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}


## Blocking ports
{: #ports}

To block network traffic and metrics from network ports, you must customize the **blacklisted_ports** section in the *dragent.yaml* file. You must list the ports from which you want to filter out any data.

**Note:** Port 53 (DNS) is always blacklisted. 

For example, the following sample shows how to set the *blacklisted_ports* section of a Sysdig agent to exclude data coming from ports 6666 and 6379:

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## Collecting a set of Docker events
{: #docker}

For example, to filter out Docker image events and collect only events for attach, commit, and copy actions, you must set the *docker* section as follows:

* Option 1: Define the sequence on entries as a bulleted list:

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* Option 2: Define the sequence on entries in a bracketed single line:

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## Disabling collection of events
{: #disable}

To disable a Sysdig agent from collecting events specified in a section of the *dragent.default.yaml*, set the event section to none in the *dragent.yaml* file.

For example, to filter out Docker events, you must set the *events* section in the *dragent.yaml* file as follows:

```
events:
  docker: none
```
{: codeblock}



## Filtering events by severity
{: #severity}

To filter events by severity, you can also change the log entry type for events in the *dragent.yaml* file. 

The default log level is **information**. This means that only warning and higher severity events are transmitted.

Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*. **Note**: The values are listed from high priority to low priority.

For example, to filter out low severity events (*notice*, *information*, *debug*), you must set the log section **event_priority** to *warning*:

```
log:
  event_priority: warning
```
{: codeblock}


To block collection of events, you must set the log section **event_priority** to *none*:

```
log:
  event_priority: none
```
{: codeblock}




## Including and excluding metrics
{: #params}

To filter custom metrics, you must customize the **metrics_filter** section in the *dragent.yaml* file. You can specify which metrics to include and which ones to filter out by configuring the **include** and **exclude** filtering parameters.

**Note:** The filtering rule order is set as follows: the first rule that matches a metric is applied.

For example, if the *metrics_filter* section of a Sysdig agent looks as follows:

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* You are configuring the Sysdig agent to collect all data from metrics that start with *metricA*, *metricB*, and *haproxy.backend*. 
* You are filtering out metrics that start with *metricC* and other metrics that start with *haproxy*. 
* The entry `exclude: metricA.*` is ignored.

To verify what metrics are enabled and disabled, see []().




## Filtering designated containers
{: #containers}

By default, a Sysdig agent will collect metrics from all containers it detects in an environment. However, as of agent version 0.86, it is possible to exclude designed containers from metrics collection. This can help reduce agent and backend load by not monitoring unnecessary containers, or-- if encountering backend limits for containers-- you can filter to ensure that the important containers are always reported on.

This feature affects the monitoring of all the processes/metrics within a container, including Prometheus, StatsD, JMX, app-checks, and built-in metrics.




## Agent auto-config
{: #auto_config}

Agent Auto-Config: Describes how to use the Sysdig REST APIs and Python client wrappers to auto-orchestrate changes to all agents in an environment, in the (rare) situation in which a standard orchestration tool such as Kubernetes, Chef, or Ansible is not being used. 



## Changing the log level
{: #log_level}

To configure the log level, you must customize the **log** section in the *dragent.yaml* file. 

The Sysdig agent generates log entries in */opt/draios/logs/draios.log*. 
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.
* Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*
* The default log level is *info*, where an entry is created for each aggregated metrics transmission to the backend servers, once per second, in addition to entries for any warnings and errors.
* You can customize the type of log and the entries that are collected by configuring the Sysdig agent configuration file **/opt/draios/etc/dragent.yaml**. After you edit the file, you must restart the agent at the shell with `service dragent restart` to activate the changes.

| Use cases                                     | Log section entry           |
|-----------------------------------------------|-----------------------------|
| Troubleshoot agent behavior                   | `file_priority: debug`      |
| Reduce container console output               | `console_priority: warning` |
| Filtering events by severity                  | `event_priority: warning`   |
| Verify what metrics are included or excluded  | `metrics_excess_log: true`  |
{: caption="Table 2. Log section entries" caption-side="top"} 


Note that troubleshooting a host with less than the default 'info' level will be more difficult or not possible. You should revert to 'info' when you are done troubleshooting the agent.  

A level of 'error' will generate the fewest log entries, a level of 'trace' will give the most, 'info' is the default if no entry exists.
Example in dragent.yaml 
customerid: 831f3-Your-Access-Key-9401
tags: local:sf,acct:eng,svc:websvr
log:
 file_priority: warning
 console_priority: info


OR 
customerid: 831f3-Your-Access-Key-9401
tags: local:sf,acct:eng,svc:websvr
log: { file_priority: debug, console_priority: debug }
Docker run command

If you are using the "ADDITIONAL_CONF" parameter to start a Docker containerized agent, you would specify this entry in the Docker run command:  
-e ADDITIONAL_CONF=“log:  { file_priority: error, console_priority: none }”
-e ADDITIONAL_CONF="log:\n  file_priority: error\n  console_priority: none"

