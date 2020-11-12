---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

keywords: Sysdig, IBM Cloud, monitoring, Sysdig agent, event filters

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

# Including and excluding metrics
{: #agent_mng_metrics}

When you delete an {{site.data.keyword.mon_full_notm}} instance, or if you want to stop collecting metrics from a source, you must uninstall the Sysdig agent from sources where it was installed as a service. If you deployed a Sysdig agent as a container, you must run docker commands to remove the agent.
{:shortdesc}


## Including and excluding metrics
{: #change_linux_agent_mng_inc_exc_metrics}

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




## Including and excluding metrics
{: #params}  docker

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





### Logging into a file what metrics are included or excluded
{: #logging_including_metrics}

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
{: #change_kube_agent_mng_sample_configmap}

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

