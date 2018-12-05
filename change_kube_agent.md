---

copyright:
  years: 2018
lastupdated: "2018-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:download: .download}

# Customizing the Kubernetes Sysdig agent
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
* Method 2: Modify the file locally and apply the chages to the cluster.

## Editing the Kubernetes Sysdig agent configuration by using kubectl edit
{: #edit_kube_agent_method1}

Complete the following steps to edit a Kubernetes Sysdig agent configuration:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent
    ```
    {: codeblock}

    Make changes. **Note:** Refer to `vi` editor instructions to learn how to make changes.

    Save the changes. Changes are applied automatically. 

3. Edit the *sysdig-agent-daemonset-v2.yaml* file. 

    Run the following command: 

    ```
    kubectl edit daemonset sysdig-agent
    ```
    {: codeblock}

    Make changes. **Note:** Refer to `vi` editor instructions to learn how to make changes.

    Save the changes. Changes are applied automatically.

## Editing the Kubernetes Sysdig agent configuration by using kubectl apply
{: #edit_kube_agent_method2}

Use this method if you have the configuration yaml files stored and managed in a source control system.

Complete the following steps to edit a Kubernetes Sysdig agent configuration:

1. Get the latest copy of each file from the source controller. 

    To create a local file with the configuration that is deployed in a cluster, you can also run the command:
    
    ```
    kubectl get configmap sysdig-agent -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    or 
    
    ```
    kubectl get daemonset sysdig-agent -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
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
{: #tag}

Complete the following steps to add more tags to a Kubernetes Sysdig agent configuration that you have already deployed:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent
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
{: #kube}

{{site.data.keyword.mon_full_notm}} supports event integrations with Kubernetes. Sysdig agents automatically discover these services and collect event data from them. You can edit the agent config file to change its default behavior, and include or exclude event data. 

By default, only a limited set of events is collected. For more information about the events that are collceted by default, see [Kubernetes events ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}.

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

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent
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

Fior more information on how to work with custom events, see [Working with custom events ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


## Disabling collection of events
{: #disable}

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

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent
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




## Filtering Kubernetes events by severity
{: #severity}

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

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

2. Edit the *sysdig-agent-daemonset-v2.yaml* file. 

    Run the following command:

    ```
    kubectl edit daemonset sysdig-agent
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



## Including and excluding metrics
{: #params}

To filter custom metrics, you must customize the **metrics_filter** section in the *sysdig-agent-configmap.yaml* file. You can specify which metrics to include and which ones to filter out by configuring the **include** and **exclude** filtering parameters.

<p class="important">The filtering rule order is set as follows: the first rule that matches a metric is applied.</p>

Complete the following steps:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

2. Edit the *sysdig-agent-configmap.yaml* file. 

    Run the following command:

    ```
    kubectl edit configmap sysdig-agent
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

6. Save the changes. 

Changes are applied automatically. 



## Logging into a file what metrics are included or excluded
{:#log_metrics}

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

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

2. Edit the *sysdig-agent-daemonset-v2.yaml* file. 

    Run the following command:

    ```
    kubectl edit daemonset sysdig-agent
    ```
    {: codeblock}

3. Make changes. Add the *log* section or update the section.

    For example, to filter out low severity events (*notice*, *information*, *debug*), you must set the log section **event_priority** to *warning*:

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. Save the changes. 

Changes are applied automatically. 


## Containers
{:#containers}




