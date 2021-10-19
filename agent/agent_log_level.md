---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, monitoring agent, log level

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the log level of a monitoring agent
{: #agent_log_level}

The log level determines the type and amount of logging of an agent. You can configure the log level by adding parameters and log level arguments.
{: shortdesc}

The monitoring agent writes log entries into the `draios.log` file. 
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.
* The log files are located in the directory `/opt/draios/logs/`. 

By default, when you deploy a monitoring agent, the log level is set to `info`.
{: note}

Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

You can configure the level of detail that is written by a monitoring agent to its log file:

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

### Linux monitoring agent
{: #agent_log_level_check_linux}

To get the log level of a Linux monitoring agent, run the following command from a terminal:

```text
more /opt/draios/etc/statsite.ini | grep log_level
```
{: pre}

For example, you can get the following result:

```text
# more /opt/draios/etc/statsite.ini | grep log_level
log_level = INFO
```
{: screen}


### Docker monitoring agent
{: #agent_log_level_check_docker}


To get the log level of a docker monitoring agent, run the following command:

```text
docker exec -ti sysdig-agent  more /opt/draios/etc/statsite.ini | grep log_level
```
{: pre}

For example, you can get the following result:

```text
# docker exec -ti sysdig-agent  more /opt/draios/etc/statsite.ini | grep log_level
log_level = INFO
```
{: screen}


### Kubernetes monitoring agent
{: #agent_log_level_check_kube}

To get the log level of a Kubernetes monitoring agent, complete the following steps:

1. Set up the cluster environment. Run the following command:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Get the agent log level. Run the following command:

    ```text
    kubectl describe daemonset sysdig-agent -n ibm-observe | grep file_priority
    ```
    {: pre}

    If the command does not return any value, the log level is set to the default value `info`.



## Configuring the log level
{: #agent_log_level_configure}

The log level determines the type and amount of logging of an agent. You can configure the log level by adding parameters and log level arguments.

### Linux monitoring agent
{: #agent_log_level_configure_linux}

To configure the log level, you must customize the **log** section in the `/opt/draios/etc/dragent.yaml` file. 

By default, a `dragent.yaml` file includes the following information:

```text
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

```text
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

```text
service dragent restart
```
{: pre}



### Docker monitoring agent
{: #agent_log_level_configure_docker}


To change the log level of a docker monitoring agent, complete the following steps:

1. Open a shell in the running container:

    ```text
    docker exec –it sysdig-agent /bin/bash
    ```
    {: pre}

2. Copy to your local machine the `dragent.yaml` file:

    ```text
    docker cp sysdig-agent:/opt/draios/etc/dragent.yaml <local directory>/dragent.yaml
    ```
    {: pre}

3. Modify the configuration file. Include information about the log level and the console log level that you want to set. Add the following section if it is not included:

    ```yaml
    log:
      file_priority: error
      console_priority: warning
    ```
    {: codeblock}

    The *file_priority* controls the log level. Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

    The *console_priority* controls the console output. Valid console log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

    The following configuration sample shows a log level set to *error*, and a console log level set to *warning*:

    ```yaml
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

    ```text
    docker cp <local directory>/dragent.yaml sysdig-agent:/opt/draios/etc/dragent.yaml
    ```
    {: pre}

5. Restart the agent. Run the following command:

    ```text
    docker restart sysdig-agent
    ```
    {: pre}

6. Verify the level have been set. Run the following commands:

    ```text
    docker exec -ti sysdig-agent  more /opt/draios/etc/statsite.ini | grep log_level
    ```
    {: pre}

    You should see the log level that you specified in the `dragent.yaml` file.




### Kubernetes monitoring agent
{: #agent_log_level_configure_kube}

Complete the following steps to change the log level of a Kubernetes monitoring agent:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Modify the agent's DaemonSet file. Include information about the log level and the console log level that you want to set.

    Run the following command to edit the config map:

    ```text
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Then, add or modify the log entries:

    ```yaml
    log:
      file_priority: error
      console_priority: warning
    ```
    {: codeblock}

    The *file_priority* controls the log level. Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

    The *console_priority* controls the console output. Valid console log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*. 

    The following configuration sample shows a log level set to *debug*, and a console log level set to *error*:

    ```yaml
    ...
    spec:
      revisionHistoryLimit: 10
      selector:
        matchLabels:
          app: sysdig-agent
      template:
        metadata:
          creationTimestamp: null
          labels:
             app: sysdig-agent
        spec:
          containers:
          - image: icr.io/ext/sysdig/agent:latest
            imagePullPolicy: Always
            name: sysdig-agent
            env:
            - name: ADDITIONAL_CONF
              value: "log:\n  file_priority: debug\n  console_priority: error"
            readinessProbe:
    ...
    ```
    {: codeblock}

The log level changes are applied when you save the changes. 


If you have changed previously the log level, the DaemonSet section looks like:

```yaml
...
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: sysdig-agent
    spec:
      containers:
      - env:
        - name: ADDITIONAL_CONF
          value: |-
            log:
              file_priority: debug
              console_priority: error
        image: icr.io/ext/sysdig/agent:latest
        imagePullPolicy: Always
...
```
{: codeblock}

Note, you can also download the configmap by running: `kubectl get daemonset sysdig-agent -o yaml -n ibm-observe > sysdig-agent-ds.yaml`. To apply the changes, you can run `kubectl apply -f sysdig-agent-ds.yaml -n ibm-observe`.
{: note}


