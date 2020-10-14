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

# Configuring the log level of a Sysdig agent
{: #agent_log_level}

The log level determines the type and amount of logging of an agent. You can configure the log level by adding parameters and log level arguments.
{:shortdesc}

The Sysdig agent writes log entries into the `draios.log` file. 
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.
* The log files are located in the directory `/opt/draios/logs/`. 

By default, when you deploy a Sysdig agent, the log level is set to `info`.
{: note}

Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

You can configure the level of detail that is written by a Sysdig agent to its log file:

| Log level       | Detail                               |
|-----------------|--------------------------------------|
| `none`          | No errors are reported.              |
| `info`          | Reports an entry for each aggregated metrics transmission to the backend servers, once per second. </br>Reports entries for any warnings and errors. |
| `error`         | Reports error logs only.             |
| `trace`         | Reports all logs that are available. |
{: caption="Table 1. Log levels" caption-side="top"} 

* To get the least number of log entries, set the log level to *error*.
* To get the full set of available logs, set the log level to *trace*. 

You should set the log level to *info*, *debug*, or *trace* to troubleshoot agent-related issues.
{: tip}


The following table lists the locations of the Sysdig agent's logs per type of agent:

| Agent Type                                                    | Agent configuration file                  |
|---------------------------------------------------------------|-------------------------------------------|
| Sysdig agent as a service in a Linux system                   | `/opt/draios/logs/draios.log`             |
| Sysdig agent as a Docker container in a Linux system          | `/opt/draios/logs/draios.log`             |
| Sysdig agent as a pod in a standard Kubernetes environment    | `sysdig-agent-configmap.yaml`             |
| Sysdig agent as a pod in an Openshift Kubernetes environment  | `sysdig-agent-configmap.yaml`             |
{: caption="Table 2. Log locations per type of agent" caption-side="top"} 


For example, consider the following use cases and the log section that you can configure to indicate the data that you want to log for an agent:

| Use cases                                     | Log section entry           |
|-----------------------------------------------|-----------------------------|
| Troubleshoot agent behavior                   | `file_priority: debug`      |
| Reduce container console output               | `console_priority: warning` |
| Filtering events by severity                  | `event_priority: warning`   |
| Verify what metrics are included or excluded  | `metrics_excess_log: true`  |
{: caption="Table 2. Log section entries" caption-side="top"} 


## Checking the log level of an agent
{: #agent_log_level_check}

### Linux Sysdig agent
{: #agent_log_level_check_linux}

To get the log level of a Linux Sysdig agent, run the following command from a terminal:

```
more /opt/draios/etc/statsite.ini | grep log_level
```
{: pre}

For example, you can get the following result:

```
# more /opt/draios/etc/statsite.ini | grep log_level
log_level = INFO
```
{: screen}


### Docker Sysdig agent
{: #agent_log_level_check_docker}


To get the log level of a docker Sysdig agent, run the following command:

```
docker exec -ti sysdig-agent  more /opt/draios/etc/statsite.ini | grep log_level
```
{: pre}

For example, you can get the following result:

```
# docker exec -ti sysdig-agent  more /opt/draios/etc/statsite.ini | grep log_level
log_level = INFO
```
{: screen}


### Kubernetes Sysdig agent
{: #agent_log_level_check_kube}





## Configuring the log level
{: #agent_log_level_configure}

The log level determines the type and amount of logging of an agent. You can configure the log level by adding parameters and log level arguments.




### Linux Sysdig agent
{: #agent_log_level_configure_linux}

To configure the log level, you must customize the **log** section in the `/opt/draios/etc/dragent.yaml` file. 

By default, a `dragent.yaml` file includes the following information:

```
customerid: xxxxxxxxxxxxxxxxx
collector: ingest.us-south.monitoring.cloud.ibm.com
collector_port: 6443
ssl: true
sysdig_capture_enabled: false
```
{: codeblock}

To configure a log level, you must edit the file and add information about the log. 
- To set the log level, you must set **file_priority**. 
- Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

The following configuration sample shows a log level set to *error*:

```
customerid: xxxxxxxxxxxxxxxxx
collector: ingest.us-south.monitoring.cloud.ibm.com
collector_port: 6443
ssl: true
sysdig_capture_enabled: false
log:
  file_priority: error
```
{: codeblock}

After you edit the dragent.yaml file, you must restart the agent to activate the changes. Run the following command:

```
service dragent restart
```
{: pre}



### Docker Sysdig agent
{: #agent_log_level_configure_docker}


To change the log level of a docker Sysdig agent, complete the following steps:

1. Open a shell in the running container:

    ```
    docker exec –it sysdig-agent /bin/bash
    ```
    {: pre}

2. Copy to your local machine the `dragent.yaml` file:

    ```
    docker cp sysdig-agent:/opt/draios/etc/dragent.yaml <local directory>/dragent.yaml
    ```
    {: pre}

3. Modify the configuration file. Include information about the log level and the console log level that you want to set. Add the following section if it is not included:

    ```
    log:
      file_priority: error
      console_priority: warning
    ```
    {: codeblock}

    The *file_priority* controls the log level. Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

    The *console_priority* controls the console output. Valid console log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

    The following configuration sample shows a log level set to *error*, and a console log level set to *warning*:

    ```
    customerid: xxxxxxxxxxxxxxxx
    tags: location:us-east
    collector: ingest.us-east.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    sysdig_capture_enabled: false
    use_promscrape: true
    log:
      file_priority: error
      console_priority: warning
    ```
    {: codeblock}

4. Update the configuration file of the agent. Run the following command:

    ```
    docker cp <local directory>/dragent.yaml sysdig-agent:/opt/draios/etc/dragent.yaml
    ```
    {: pre}

5. Restart the agent. Run the following command:

    ```
    docker restart sysdig-agent
    ```
    {: pre}

6. Verify the levels have been set. Run the following commands:

    ```
     docker exec -ti sysdig-agent  more /opt/draios/etc/statsite.ini | grep log_level
    ```
    {: pre}

    You should see `log_level = ERROR`.




### Kubernetes Sysdig agent
{: #agent_log_level_configure_kube}




- name: ADDITIONAL_CONF #OPTIONAL pass additional parameters to the agent
  value: "log:\n file_priority: debug\n console_priority: error"

  
* The **file_priority** in the **log** section controls the type of log entries written to the file `/opt/draios/logs/draios.log`.
* The **console_priority** in the **log** section controls the type of log entries written to the container console output when running the containerized agent.
* The default log level is **info**, where a log entry is created for each aggregated metrics transmission to the backend servers, once per second, in addition to entries for any warnings and errors.
* Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*

Complete the following steps:

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

3. Make changes. Add the *metrics_filter* section or update the section.

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

4. Save the changes. 

Changes are applied automatically. 



### Filtering Kubernetes events by severity
{: #change_kube_agent_filterby_severity}

* The **event_priority** in the **log** section controls the type of events that are sent from the agent
* The default log level is *information*. This means that only information and higher severity events are transmitted.
* Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*. **Note**: The values are listed from high priority to low priority.
* Setting the level to `none` will block all event collection.


