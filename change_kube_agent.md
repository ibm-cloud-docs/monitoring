---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

subcollection: Sysdig

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

# Customizing Kubernetes Sysdig agents
{: #change_kube_agent}

In {{site.data.keyword.mon_full_notm}}, you can customize the Sysdig agent configuration to set a log level, block ports, include or exclude metric data, add or remove events, and filter out containers. 
{:shortdesc}

To customize a Kubernetes Sysdig agent, you might need to configure sections in any of the following files:

| File name                        | Actions       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modify log level. |
| `sysdig-agent-configmap.yaml`    | Block ports. </br>Include or exclude metric data. </br>Add or remove events. </br>Filter out containers. |
{: caption="Table 1. Kubernetes Sysdig agent configuration files" caption-side="top"} 

To edit a Kubernetes Sysdig agent, you might need to edit the *sysdig-agent-configmap.yaml*, the *sysdig-agent-daemonset-v2.yaml*, or both.
{: tip}

There are two methods that you can use to modify a configuration file:
* Method 1: Modify the file directly on the cluster where the agent is running.
* Method 2: Modify the file locally and apply the changes to the cluster.

## Editing the Kubernetes Sysdig agent configuration by using kubectl edit
{: #change_kube_agent_edit_kube_agent_method1}

Complete the following steps to edit a Kubernetes Sysdig agent configuration:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Make changes. **Note:** Refer to `vi` editor instructions to learn how to make changes.

    Save the changes. Changes are applied automatically. 

3. Edit the *sysdig-agent-daemonset-v2.yaml* file. 

    Run the following command: 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Make changes. **Note:** Refer to `vi` editor instructions to learn how to make changes.

    Save the changes. Changes are applied automatically.

## Editing the Kubernetes Sysdig agent configuration by using kubectl apply
{: #change_kube_agent_edit_kube_agent_method2}

Use this method if you have the configuration yaml files stored and managed in a source control system.

Complete the following steps to edit a Kubernetes Sysdig agent configuration:

1. Get the latest copy of each file from the source controller. 

    To create a local file with the configuration that is deployed in a cluster, you can also run the command:
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    or 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. Edit the configuration.

3. Apply the changes by using the following commands:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    or
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

Running agents will automatically pick the new configuration after Kubernetes pushes the changes across all the nodes in the cluster.


## Adding more tags to data collected from a Kubernetes Sysdig agent
{: #change_kube_agent_add_tags}

Complete the following steps to add more tags to a Kubernetes Sysdig agent configuration that you have already deployed:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. **Note:** Refer to `vi` editor instructions to learn how to make changes.

    ```
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

{{site.data.keyword.mon_full_notm}} supports event integrations with Kubernetes. Sysdig agents automatically discover these services and collect event data from them. You can edit the agent config file to change its default behavior, and include or exclude event data. 

By default, only a limited set of events is collected. For more information about the events that are collected by default, see [Kubernetes events ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}.

To add or remove events, you must customize the *sysdig-agent-configmap.yaml* file and specify what events to include and which ones to filter out. **Note:** An entry in a section in *sysdig-agent-configmap.yaml* overrides the entire section in the default configuration.
{: tip}

To filter events from Kubernetes pods, complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *events* section or update the section.

    **Note:** Refer to `vi` editor instructions to learn how to make changes.

    For example, you might want to collect Kubernetes pod pulling events and filter out other pod events that are collected by default. You still want to collect default Kubernetes events for nodes and replicationControllers.

    ```
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

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* Option 2: Define the sequence on entries in a bracketed single line:

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

For more information on how to work with custom events, see [Working with custom events ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


## Disabling collection of events
{: #change_kube_agent_disable_events}

To disable a Sysdig agent from collecting Kubernetes events, you must modify the *sysdig-agent-configmap.yaml* file. Set the **Kubernetes** entry in the **events** section to *none*. 

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *events* section or update the section.

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. Save the changes. 

Changes are applied automatically. 






## Including and excluding metrics
{: #change_kube_agent_inc_exc_metrics}

To filter custom metrics, you must customize the **metrics_filter** section in the *sysdig-agent-configmap.yaml* file. You can specify which metrics to include and which ones to filter out by configuring the **include** and **exclude** filtering parameters.

<p class="important">The filtering rule order is set as follows: the first rule that matches a metric is applied. Follow up rules for that metric are ignored.</p>

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

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




## Filtering kubernetes objects and containers from which data is collected
{: #change_kube_agent_filter_data}

A Kubernetes Sysdig agent automatically collects metrics from *all containers* that it detects in a cluster, including Prometheus, StatsD, JMX, app-checks, and built-in metrics.
 
You can customize the Sysdig agent to exclude containers from metrics collection. 

When you exclude containers, consider the following information:
* You reduce agent and backend load.
* You only collect data from containers that you want to monitor.
* You can control costs by reporting on important containers, and filtering out unnecessary or not critical containers.

To enable the feature where a Sysdig agent filters containers, you must customize the *sysdig-agent-configmap.yaml* file. Set the **use_container_filter** entry in the **containers** section to *true*. **Note:** By default, this feature is turned off. Then, define the rules that include one or more conditions and that you want to apply.

The following table outlines the parameters that you can define to set the filtering rules in a cluster:

| Parameter                          | Condition                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | Container image name                           |
| `container.name`                   | Container name                                 |
| `container.label.*`                | Container label                                |
| `kubernetes.<object>.*`            | Kubernetes object. An object can be a pod, a namespace, etc.   |
| `kubernetes.<object>.annotation.*` | Kubernetes object annotation                   |
| `kubernetes.<object>.label.*`      | Kubernetes object label                        |
| `all`                              | Default rule to specify all objects            |
{: caption="Table 2. Parameters to define conditions on containers" caption-side="top"} 

Consider the following information on how the Sysdig agent applies the rules that you define in the **container_filter** section:
* You define conditions by configuring them with the **include** and **exclude** filtering parameters. 
* The first matching rule in the list determines if the container is included or excluded.
* The conditions consist of a key name and a value. If the given key for a container matches the value, the rule is applied.
* When a rule contains multiple conditions, `all the conditions` need to match for the rule to be applied.
{: tip}


Complete the following steps to filter out containers that a Sysdig agent monitors in a cluster:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *metrics_filter* section or update the section.

    For example, see the following extract of a config map:

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. Save the changes. 

Changes are applied automatically. 


## Blocking ports
{: #change_kube_agent_block_ports}

To block network traffic and metrics from network ports, you must customize the **blacklisted_ports** section in the *sysdig-agent-configmap.yaml* file. You must list the ports from which you want to filter out any data.

**Note:** Port 53 (DNS) is always blacklisted. 

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *metrics_filter* section or update the section.

    For example, the following sample shows how to set the *blacklisted_ports* section of a Sysdig agent to exclude data coming from ports 6666 and 6379:

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. Save the changes. 

Changes are applied automatically. 



## Changing the log level
{: #change_kube_agent_log_level}

To configure the log level, you must customize the **log** section in the *sysdig-agent-daemonset-v2.yaml* file. 

The Sysdig agent generates log entries in */opt/draios/logs/draios.log*. 
* The log file rotates when it reaches 10MB in size.
* The 10 most recent log files are kept. The date-stamp that is appended to the filename is used to determine which files to keep.
* Valid log levels are: *none*, *error*, *warning*, *info*, *debug*, *trace*
* The default log level is *info*, where an entry is created for each aggregated metrics transmission to the backend servers, once per second, in addition to entries for any warnings and errors.
* You can customize the type of log and the entries that are collected by configuring the Sysdig agent configuration file **/opt/draios/etc/dragent.yaml**. After you edit the file, you must restart the agent at the shell with `service dragent restart` to activate the changes.

The following table lists some common scenarios and the value that you must set in each one of them:

| Use cases                                     | Log section entry           |
|-----------------------------------------------|-----------------------------|
| Troubleshoot agent behavior                   | `file_priority: debug`      |
| Reduce container console output               | `console_priority: warning` |
| Filtering events by severity                  | `event_priority: warning`   |
| Verify what metrics are included or excluded  | `metrics_excess_log: true`  |
{: caption="Table 2. Log section entries" caption-side="top"} 

Complete the following steps to configure the log level:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-daemonset-v2.yaml* file. 

    Run the following command:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *log* section or update the section.

    For example, to filter out low severity events (*notice*, *information*, *debug*), you must set the entry **metrics_excess_log** in the **log** section to *true*:

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. Save the changes. 

Changes are applied automatically. 


## Filtering Kubernetes events by severity
{: #change_kube_agent_filterby_severity}

To filter events by severity, you must modify the *sysdig-agent-daemonset-v2.yaml* file. Set the entry **event_priority** in the **log** section to *none*. 

The default log level is **information**. This means that only warning and higher severity events are transmitted.

Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*. **Note**: The values are listed from high priority to low priority.

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-daemonset-v2.yaml* file. 

    Run the following command:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *log* section or update the section.

    For example, to filter out low severity events (*notice*, *information*, *debug*), you must set the log section **event_priority** to *warning*:

    ```
    log:
      event_priority: warning
    ```
    {: codeblock}

6. Save the changes. 

Changes are applied automatically. 

## Logging into a file what metrics are included or excluded
{: #change_kube_agent_log_metrics}

To log into a file information about which custom metrics are included and which ones are excluded, you must customize the *sysdig-agent-daemonset-v2.yaml* file. Set the entry **metrics_excess_log** to **true** in the **log** section.

* Logging is disabled by default. 
* Logging occurs at INFO-level every 30 seconds and lasts for 10 seconds. 
* The log file is available in */opt/draios/logs/draios.log*.
* Logging data is formatted as follows:

    ```
    +/-[type] [metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* is a symbol that indicates if the metric is included or excluded. Plus (*+*) indicates that a metric is included. Minus (*-*) indicates that a metric is excluded. 

    * *[type]* specifies the metric type, for example, *statsd*.
    
    * *[metric included/excluded]* indicates in a human readable way whether the metric is included or excluded.

    *  *metric.name* indicates the metric name.

    * *(filter: +/-[metric.filter])* provides information about any filters that are defined in the **metrics_filter** section in the *sysdig-agent-daemonset-v2.yaml* file.

A sample entry looks as follows:

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Edit the *sysdig-agent-daemonset-v2.yaml* file. 

    Run the following command:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Make changes. Add the *log* section or update the section.

    For example, to filter out low severity events (*notice*, *information*, *debug*), you must set the entry **metrics_excess_log** in the **log** section to *true*:

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. Save the changes. 

Changes are applied automatically. 


## Sample configmap yaml file
{: #change_kube_agent_sample_configmap}

```
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
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## Sample daemonset yaml file
{: #change_kube_agent_sample_daemonset}

```
 Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

