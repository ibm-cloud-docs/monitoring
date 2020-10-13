---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

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
{: #agent_log_level}

You can view and analyze the Sysdig agent log file to troubleshoot problems. 
{:shortdesc}

By default, when you deploy a Sysdig agent, the log level is set to `info`. 

Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

You can configure the log level of a Sysdig agent to configure the level of detail that is written to the Sysdig agent log file.  
* Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*
* The *info* level reports an entry for each aggregated metrics transmission to the backend servers, once per second. It also reports entries for any warnings and errors.
* To get the least number of log entries, set the log level to *error*.
* To get the full set of available logs, set the log level to *trace*. 

You should set the log level to *info*, *debug*, or *trace* to troubleshoot agent-related issues.
{: tip}

The Sysdig agent writes log entries into the `draios.log` file. 
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.
* The log files are located in the directory `/opt/draios/logs/`. 




The Sysdig agent generates log entries in /opt/draios/logs/draios.log. The agent will rotate out the log file when it reaches 10MB in size, keeping the 10 most recent log files archived with a date-stamp appended to the filename.

The type and amount of logging can be changed by adding parameters and log level arguments shown below to the agent's user settings configuration file here:

/opt/draios/etc/dragent.yaml

After editing the dragent.yaml file, restart the agent at the shell with: service dragent restart to affect changes.

Note that dragent.yaml code can be written in both YAML and JSON. The examples below use YAML.


The following table lists the location of the Sysdig agent configuration file that sets the log level of an agent:

| Agent Type                                                    | Agent configuration file                  |
|---------------------------------------------------------------|-------------------------------------------|
| Sysdig agent as a service in a Linux system                   | `/opt/draios/logs/draios.log`             |
| Sysdig agent as a Docker container in a Linux system          | `/opt/draios/logs/draios.log`             |
| Sysdig agent as a pod in a standard Kubernetes environment    | `sysdig-agent-configmap.yaml`             |
| Sysdig agent as a pod in an Openshift Kubernetes environment  | `sysdig-agent-configmap.yaml`             |
{: caption="Table 1. Log configuration files" caption-side="top"} 



* You can customize the type of log and the entries that are collected by configuring the Sysdig agent configuration file **/opt/draios/etc/dragent.yaml**. After you edit the file, you must restart the agent at the shell with `docker restart sysdig-agent` to activate the changes.

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




## Changing the log level
{: #log_level}

To configure the log level, you must customize the **log** section in the *dragent.yaml* file. 




## Changing the log configurations
{: #change_kube_agent_log_configurations}

To configure the log configurations, you must customize the **log** section in the *sysdig-agent-configmap.yaml* file.

The Sysdig agent generates log entries in */opt/draios/logs/draios.log*. 
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.

The following table lists some common scenarios and the value that you must set in each one of them:

| Use cases                                     | Log section entry           | Default Value |
|-----------------------------------------------|-----------------------------|---------------|
| Troubleshoot agent behavior                   | `file_priority: debug`      | `info`        |
| Reduce container console output               | `console_priority: warning` | `info`        |
| Filtering events by severity                  | `event_priority: warning`   | `information` |
| Verify what metrics are included or excluded  | `metrics_excess_log: true`  | `false`       |
{: caption="Table 2. Log section entries" caption-side="top"} 

### Changing the log level
{: #change_kube_agent_log_level}

* The **file_priority** in the **log** section controls the type of log entries written to the file `/opt/draios/logs/draios.log`.
* The **console_priority** in the **log** section controls the type of log entries written to the container console output when running the containerized agent.
* The default log level is **info**, where a log entry is created for each aggregated metrics transmission to the backend servers, once per second, in addition to entries for any warnings and errors.
* Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*

### Filtering Kubernetes events by severity
{: #change_kube_agent_filterby_severity}

* The **event_priority** in the **log** section controls the type of events that are sent from the agent
* The default log level is *information*. This means that only information and higher severity events are transmitted.
* Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*. **Note**: The values are listed from high priority to low priority.
* Setting the level to `none` will block all event collection.


### Logging into a file what metrics are included or excluded
{: #change_kube_agent_log_metrics}

* Setting **metrics_excess_log** to **true** in the **log** section will enable logging of the custom metrics that are included or excluded.
* Metric logging is disabled by default.
* Logging occurs at INFO-level every 30 seconds and lasts for 10 seconds.
* The **metricsfile** setting is required to specify the location for the metrics to be written by the agent.  The `metricsfile.location` value is a relative path under the /opt/draios directory.  *Note:* The `metricsfile` entry is specified at the same level as `log`( not as a child in the yaml)
* Logging data is formatted as follows:

    ```
    +/-[type] [metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* is a symbol that indicates if the metric is included or excluded. Plus (*+*) indicates that a metric is included. Minus (*-*) indicates that a metric is excluded.  

    * *[type]* specifies the metric type, for example, *statsd*.

    * *[metric included/excluded]* indicates in a human readable way whether the metric is included or excluded.

    *  *metric.name* indicates the metric name.

    * *(filter: +/-[metric.filter])* provides information about any filters that are defined in the **metrics_filter** section in the *sysdig-agent-configmap.yaml* file.

A sample log entry looks as follows:

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}


Complete the following steps to configure the log settings:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file.

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *log* section or update the section and include the configurations that you wish to modify based on the descriptions above.

    For example:

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    metricsfile: { location : metrics }
    ```
    {: codeblock}

6. Save the changes. 

Changes are applied automatically. 




## Sample configmap yaml file
{: #change_kube_agent_sample_configmap}

```yaml
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:    
      kubernetes:
        node: 
          - Rebooted
    metrics_filter:
      - include: metricA.*
      - exclude: metricA.*
      - include: metricB.*
    use_container_filter: true
    container_filter:
      - exclude:
        kubernetes.namespace.name: kube-system
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    metricsfile: { location : metrics }
kind: ConfigMap
metadata:
  annotations:
...
```
{: codeblock}



