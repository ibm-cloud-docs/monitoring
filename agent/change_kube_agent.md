---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-24"

keywords: IBM Cloud, monitoring, customize, kubernetes agent

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Customizing Kubernetes monitoring agents
{: #change_kube_agent}

In {{site.data.keyword.mon_full_notm}}, you can customize the monitoring agent configuration to set a log level, block ports, include or exclude metric data, add or remove events, and filter out containers. 
{: shortdesc}

To customize a Kubernetes monitoring agent, you need to configure the `sysdig-agent-configmap.yaml` file.

There are two methods that you can use to modify a configuration file:
* Method 1: Modify the file directly on the cluster where the agent is running.
* Method 2: Modify the file locally and apply the changes to the cluster.

## Editing the Kubernetes monitoring agent configuration by using kubectl edit
{: #change_kube_agent_edit_kube_agent_method1}

Complete the following steps to edit a Kubernetes monitoring agent configuration:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Make changes. **Note:** Refer to `vi` editor instructions to learn how to make changes.

    Save the changes. Changes are applied automatically. 

## Editing the Kubernetes monitoring agent configuration by using kubectl apply
{: #change_kube_agent_edit_kube_agent_method2}

Use this method if you have the configuration yaml files stored and managed in a source control system.

Complete the following steps to edit a Kubernetes monitoring agent configuration:

1. Get the latest copy of each file from the source controller. 

    To create a local file with the configuration that is deployed in a cluster, you can also run the command:
    
    ```text
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
2. Edit the configuration.

3. Apply the changes by using the following commands:

    ```text
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
Running agents will automatically pick the new configuration after Kubernetes pushes the changes across all the nodes in the cluster.


## Adding more tags to data that is collected from a Kubernetes monitoring agent
{: #change_kube_agent_add_tags}

Complete the following steps to add more tags to a Kubernetes monitoring agent configuration that you have already deployed:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. **Note:** Refer to `vi` editor instructions to learn how to make changes.

    ```yaml
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. Save the changes. 

Changes are applied automatically. 

For the sample provided, you would get the tags **agent.tag.cluster_version** and **agent.tag.region**. You could use them to define alerts, customize scopes and more.



## Collecting a set of Kubernetes events
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} supports event integrations with Kubernetes. monitoring agents automatically discover these services and collect event data from them. You can edit the agent config file to change its default behavior, and include or exclude event data. 

By default, only a limited set of events is collected. For more information about the events that are collected by default, see [Kubernetes events](https://docs.sysdig.com/en/event-types.html){: external}.

To add or remove events, you must customize the *sysdig-agent-configmap.yaml* file and specify what events to include and which ones to filter out. **Note:** An entry in a section in *sysdig-agent-configmap.yaml* overrides the entire section in the default configuration.
{: tip}

To filter events from Kubernetes pods, complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *events* section or update the section.

    **Note:** Refer to `vi` editor instructions to learn how to make changes.

    For example, you might want to collect Kubernetes pod pulling events and filter out other pod events that are collected by default. You still want to collect default Kubernetes events for nodes and replicationControllers.

    ```yaml
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. Save the changes. 

Changes are applied automatically. 


Another example where you can see how to collect a subset of Kubernetes events: You only want to monitor pulling, pulled, and failed events for pods.

* Option 1: Define the sequence on entries as a bulleted list:

    ```yaml
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* Option 2: Define the sequence on entries in a bracketed single line:

    ```yaml
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

For more information on how to work with custom events, see [Working with custom events](https://docs.sysdig.com/en/event-types.html){: external}.


## Disabling collection of events
{: #change_kube_agent_disable_events}

To disable a monitoring agent from collecting Kubernetes events, you must modify the *sysdig-agent-configmap.yaml* file. Set the **Kubernetes** entry in the **events** section to *none*. 

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *events* section or update the section.

    ```yaml
    events:
      kubernetes: none
    ```
    {: codeblock}

4. Save the changes. 

Changes are applied automatically. 






## Including and excluding metrics
{: #change_kube_agent_inc_exc_metrics}

To filter custom metrics, you must customize the **metrics_filter** section in the *sysdig-agent-configmap.yaml* file. You can specify which metrics to include and which ones to filter out by configuring the **include** and **exclude** filtering parameters.

The filtering rule order is set as follows: the first rule that matches a metric is applied. Follow up rules for that metric are ignored.
{: important}

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *metrics_filter* section or update the section.

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

4. Save the changes. 

Changes are applied automatically. 




## Filtering kubernetes objects and containers from which data is collected
{: #change_kube_agent_filter_data}

A Kubernetes monitoring agent automatically collects metrics from *all containers* that it detects in a cluster, including Prometheus, StatsD, JMX, app-checks, and built-in metrics.
 
You can customize the monitoring agent to exclude containers from metrics collection. 

When you exclude containers, consider the following information:
* You reduce agent and backend load.
* You only collect data from containers that you want to monitor.
* You can control costs by reporting on important containers, and filtering out unnecessary or not critical containers.

To enable the feature where a monitoring agent filters containers, you must customize the *sysdig-agent-configmap.yaml* file. Set the **use_container_filter** entry in the **containers** section to *true*. **Note:** By default, this feature is turned off. Then, define the rules that include one or more conditions and that you want to apply.

The following table outlines the parameters that you can define to set the filtering rules in a cluster:

| Parameter                          | Condition                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | Container image name                           |
| `container.name`                   | Container name                                 |
| `container.label.*`                | Container label                                |
| `kubernetes.object.*`             | Kubernetes object. An object can be a pod, a namespace, etc.   |
| `kubernetes.object.annotation.*`  | Kubernetes object annotation                   |
| `kubernetes.object.label.*`       | Kubernetes object label                        |
| `all`                              | Default rule to specify all objects            |
{: caption="Table 1. Parameters to define conditions on containers" caption-side="top"} 

Consider the following information on how the monitoring agent applies the rules that you define in the **container_filter** section:
* You define conditions by configuring them with the **include** and **exclude** filtering parameters. 
* The first matching rule in the list determines if the container is included or excluded.
* The conditions consist of a key name and a value. If the given key for a container matches the value, the rule is applied.
* When a rule contains multiple conditions, `all the conditions` need to match for the rule to be applied.

Complete the following steps to filter out containers that a monitoring agent monitors in a cluster:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *use_container_filter* entry and *container_filter* section or update the the existing entries.

    For example, see the following extract of a config map:

    ```yaml
    # Enable the feature
    use_container_filter: true
    #
    # Include or exclude conditions
    container_filter:
      - include:
            container.image: appdomain/my-app-image
      - include:
            container.name: my-java-app
      - exclude:
            kubernetes.namespace.name: kube-system
    ```
    {: codeblock}

4. Save the changes. 

Changes are applied automatically. 


## Blocking ports
{: #change_kube_agent_block_ports}

To block network traffic and metrics from network ports, you must customize the **blacklisted_ports** section in the *sysdig-agent-configmap.yaml* file. You must list the ports from which you want to filter out any data.

Port 53 (DNS) is always in the blocklist and does not need to be specified in the **blacklisted_ports**. 
{: note}

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *metrics_filter* section or update the section.

    For example, the following sample shows how to set the *blacklisted_ports* section of a monitoring agent to exclude data coming from ports 6666 and 6379:

    ```yaml
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

4. Save the changes. 

Changes are applied automatically. 



## Changing the log configurations
{: #change_kube_agent_log_configurations}

To configure the log configurations, you must customize the **log** section in the *sysdig-agent-configmap.yaml* file.

The monitoring agent generates log entries in */opt/draios/logs/draios.log*. 
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

    ```yaml
    +/-[type] [metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* is a symbol that indicates if the metric is included or excluded. Plus (*+*) indicates that a metric is included. Minus (*-*) indicates that a metric is excluded.  

    * *[type]* specifies the metric type, for example, *statsd*.

    * *[metric included/excluded]* indicates in a human readable way whether the metric is included or excluded.

    *  *metric.name* indicates the metric name.

    * *(filter: +/-[metric.filter])* provides information about any filters that are defined in the **metrics_filter** section in the *sysdig-agent-configmap.yaml* file.

A sample log entry looks as follows:

```yaml
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}


Complete the following steps to configure the log settings:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Edit the *sysdig-agent-configmap.yaml* file.

    Run the following command:

    ```text
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *log* section or update the section and include the configurations that you wish to modify based on the prior descriptions.

    For example:

    ```yaml
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    metricsfile: { location : metrics }
    ```
    {: codeblock}

4. Save the changes. 

Changes are applied automatically. 




## Sample configmap yaml file
{: #change_kube_agent_sample_configmap}

```yaml
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
     
    ####
    # collector address
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
