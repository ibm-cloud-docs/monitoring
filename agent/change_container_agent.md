---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Customizing container monitoring agents
{: #change_agent}

In {{site.data.keyword.mon_full_notm}}, you can customize the monitoring agent configuration to set a log level, block ports, include or exclude metric data, add or remove events, and filter out containers.
{: shortdesc}




## Editing the dragent yaml file
{: #edit_agent}

The yaml file is located in */opt/draios/etc/*.

Complete the following steps to edit the file and apply the changes:

1. Access the *dragent.yaml* directly at `/opt/draios/etc/dragent.yaml`.
2. Edit the file. Use valid YAML syntax.
3. Restart the agent. Run the following command:

    ```text
    docker restart sysdig-agent
    ```
    {: codeblock}



## Blocking ports
{: #ports}

To block network traffic and metrics from network ports, you must customize the **blacklisted_ports** section in the *dragent.yaml* file. You must list the ports from which you want to filter out any data.

Port 53 (DNS) is always in the blocklist and does not need to be specified in the **blacklisted_ports**.
{: note}

For example, the following sample shows how to set the *blacklisted_ports* section of a monitoring agent to exclude data coming from ports 6666 and 6379:

```yaml
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## Collecting a set of Docker events
{: #docker}

{{site.data.keyword.mon_full_notm}} supports event integration with Docker. monitoring agents automatically discover Docker sources and collect event data from them. You can edit the agent config file to change its default behavior, and include or exclude event data.

By default, only a limited set of events is collected. The default settings configuration file */opt/draios/etc/dragent.default.yaml* includes the events that are collected. For more information about the events that are collected by default, see [Event Types](https://docs.sysdig.com/en/docs/sysdig-monitor/events/event-types/){: external}.

To add or remove events, you must customize the *dragent.yaml* file and specify what events to include and which ones to filter out. **Note:** An entry in a section in *dragent.yaml* overrides the entire section in the default configuration.
{: tip}

For example, to filter out Docker image events and collect only events for attach, commit, and copy actions, you must set the *docker* section as follows:

* Option 1: Define the sequence on entries as a bulleted list:

    ```yaml
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

    ```yaml
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## Disabling collection of events
{: #disable}

To disable a monitoring agent from collecting events, modify the *dragent.default.yaml* file. Set the **events** section to *none* in the *dragent.yaml* file.

For example, to filter out Docker events, you must set the *events* section in the *dragent.yaml* file as follows:

```yaml
events:
  docker: none
```
{: codeblock}



## Filtering events by severity
{: #filter_by_severity}

To filter events by severity, you can also change the log entry type for events in the *dragent.yaml* file.

The default log level is **information**. This means that only warning and higher severity events are transmitted.

Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*.

The values are listed from high priority to low priority.
{: note}

For example, to filter out low severity events (*notice*, *information*, *debug*), you must set the log section **event_priority** to *warning*:

```yaml
log:
  event_priority: warning
```
{: codeblock}


To block collection of events, you must set the log section **event_priority** to *none*:

```yaml
log:
  event_priority: none
```
{: codeblock}




## Including and excluding metrics
{: #params}

To filter custom metrics, you must customize the **metrics_filter** section in the *dragent.yaml* file. You can specify which metrics to include and which ones to filter out by configuring the **include** and **exclude** filtering parameters.

The filtering rule order is set as follows: the first rule that matches a metric is applied.
{: note}

For example, if the *metrics_filter* section of a monitoring agent looks as follows:

```yaml
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* You are configuring the monitoring agent to collect all data from metrics that start with *metricA*, *metricB*, and *haproxy.backend*.
* You are filtering out metrics that start with *metricC* and other metrics that start with *haproxy*.
* The entry `exclude: metricA.*` is ignored.


## Changing the log level
{: #log_level}

To configure the log level, you must customize the **log** section in the *dragent.yaml* file.

The monitoring agent generates log entries in */opt/draios/logs/draios.log*.
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.
* Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*
* The default log level is *info*, where an entry is created for each aggregated metrics transmission to the backend servers, once per second, in addition to entries for any warnings and errors.
* You can customize the type of log and the entries that are collected by configuring the monitoring agent configuration file **/opt/draios/etc/dragent.yaml**. After you edit the file, you must restart the agent at the shell with `docker restart sysdig-agent` to activate the changes.

| Use cases                                     | Log section entry           |
|-----------------------------------------------|-----------------------------|
| Troubleshoot agent behavior                   | `file_priority: debug`      |
| Reduce container console output               | `console_priority: warning` |
| Filtering events by severity                  | `event_priority: warning`   |
| Verify what metrics are included or excluded  | `metrics_excess_log: true`  |
{: caption="Log section entries" caption-side="top"}
