---

copyright:
  years:  2018, 2021
lastupdated: "2021-04-05"

keywords: IBM Cloud, monitoring, prometheus, exporters, promcat

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# Collecting metrics by using Prometheus remote write
{: #prometheus_remote_write}

You can use the built in Prometheus remote write feature to send metrics from environments where the {{site.data.keyword.mon_short}} agent coexists with Prometheus servers. Additionally, you can send metrics from environments where the {{site.data.keyword.mon_short}} agent cannot currently be installed.
{: shortdesc}

Use the {{site.data.keyword.mon_short}} agent in environments where an agent is available. However, use the Prometheus remote write feature to send metrics from ephemeral or batch jobs that may not exist long enough to be scraped by the agent.

Use the Prometheus remote write feature to send metrics from environments where the {{site.data.keyword.mon_short}} agent cannot currently be installed:
- Windows hosts and other operating systems
- Non x86 based architectures, typically seen on IoT environments or Edge computing

To collect metrics by using the Prometheus remote write feature, your {{site.data.keyword.mon_short}} instance requires the *Prom-Beacon service* enabled. For existing {{site.data.keyword.mon_full_notm}} instances, the Prom-Beacon service is enabled by default. Notice that for new instances, the feature is coming soon.

With the Prometheus remote write feature, you can either monitor metrics through the UI or you can use PromQL to query the data by using the standard Prometheus query language.

All communication between your Prometheus servers and {{site.data.keyword.mon_short}} instances must use the authorization header with the Monitor API token as Bearer Token.


## Configuring Prometheus remote write
{: #prometheus_remote_write_configure}

You can configure your Prometheus server to remote write to a {{site.data.keyword.mon_short}} instance. 

For Prometheus v2.25 and previous versions, you must configure the `remote_write` section in your `prometheus.yml` configuration file as follows:

```yaml
global:
  external_labels:
    [ <labelname>: <labelvalue> ... ]
remote_write:
- url: "https://<INGESTION_URL>/prometheus/remote/write"
  bearer_token: "<MONITOR_API_TOKEN>"
```
{: codeblock}

Where
- `<MONITOR_API_TOKEN>` contains the authorization token.
- `<INGESTION_URL>` indicates the ingestion endpoint. You must set this value to the ingestion endpoint for the region where the {{site.data.keyword.mon_short}} instance is available.


For Prometheus version 2.26 and later versions, you must configure the `remote_write` section in your `prometheus.yml` configuration file as follows:

```yaml
global:
  external_labels:
    [ <labelname>: <labelvalue> ... ]
remote_write:
- url: "https://<INGESTION_URL>/prometheus/remote/write"
  authorization:
    credentials: "<MONITOR_API_TOKEN>"
```
{: codeblock}

For example, you can configure the Prometheus server that runs in a Kubernetes cluster in different ways. Depending on how you installed it, you can choose any of the following options to configure the remote write feature in Prometheus to send metrics to an {{site.data.keyword.mon_full_notm}} instance:
- Configure a Prometheus server that is managed by Prometheus Operator 
- Configure a Prometheus server by using Helm
- Configure a Prometheus server through a Kubernetes ConfigMap
For more information, see [Collecting metrics from a Kubernetes cluster by using Prometheus remote write](/docs/monitoring?topic=monitoring-prometheus_remote_write).



## Managing metrics
{: #prometheus_remote_write_manage}

By default, when you configure your Prometheus server to remote write to a {{site.data.keyword.mon_short}} instance, all metrics are sent. These metrics are sent and include a `remote_write: true` label to easily identify them.

### Controling the metrics that are sent
{: #prometheus_remote_write_control}

You can manage and control the metrics that you collect and send to a {{site.data.keyword.mon_short}} instance. To select which series and labels to collect, and reduce the number of active series that are sent to the {{site.data.keyword.mon_short}} instance, you can set up relabel configurations by using the `write_relabel_configs` block within your `remote_write` section.

For example, to collect metrics from 1 namespace `my-namespace`, you can add the following:

```yaml
remote_write:
    - url: https://<INGESTION_URL>/prometheus/remote/write
      authorization:
        credentials_file: /etc/secrets/<SECRET_NAME>
      write_relabel_configs:
        - action: keep
          regex: my-namespace
          source_labels: 
          - namespace
```
{: codeblock}   

### Labeling metrics by Prometheus server
{: #prometheus_remote_write_label}

You can specify custom labels that are sent along with each time series that is collected by a Prometheus server by using the `external_labels` block within `global`. 

You can use these labels to filter and define the scope of the metrics that you monitor through dashboards in the {{site.data.keyword.mon_short}} UI.

For example, if you have 2 different Prometheus servers configured to remote write to a {{site.data.keyword.mon_short}} instance, you can include an external label to identify each server:

```yaml
# Prometheus server 1
global:
  external_labels:
    provider: prometheus1
remote_write:
- url: ...
```
{: codeblock}

```yaml
# Prometheus server 2
global:
  external_labels:
    provider: prometheus2
remote_write:
- url: ...
```
{: codeblock}



## Rate limits
{: #prometheus_remote_write_rate}

The following table lists the default rate limits per instance:

| Rate  | Limit | Info |
|-------|-------|-------|
| Parallel writes | 100 concurrent requests |
| Data points per minute (DPM) | 1 million | The number of data points that are sent depends on how often metrics are sent. For example, a scrape interval of 10s will submit more DPM than an interval of 60 seconds |
| Number of writes per minute | 10,000 |
{: caption="Table 1. Rate limits" caption-side="top"} 


## Ingestion endpoints
{: #prometheus_remote_write_endpoints}

The following table lists the public {{site.data.keyword.mon_short}} ingestion endpoints that you can configure to collect metrics via Prometheus Remote Write:
 
| Region                | Endpoint                            | 
|-----------------------|-------------------------------------|
| `US South`            | `https://ingest.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` |
| `EU-DE`               | `https://ingest.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| `EU-GB`               | `https://ingest.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| `JP-OSA`              | `https://ingest.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `JP-TOK`              | `https://ingest.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `US-EAST`             | `https://ingest.us-east.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| `AU-SYD`              | `https://ingest.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `CA TOR`              | `https://ingest.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `BR SAO`              | `https://ingest.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write`   |
{: caption="Table 2. Prometheus remote write public endpoints" caption-side="top"} 

The following table lists the private {{site.data.keyword.mon_short}} ingestion endpoints that you can configure to collect metrics via Prometheus Remote Write:
 
| Region                | Endpoint                            | 
|-----------------------|-------------------------------------|
| `US South`            | `https://ingest.private.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` |
| `EU-DE`               | `https://ingest.private.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| `EU-GB`               | `https://ingest.private.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| `JP-OSA`              | `https://ingest.private.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `JP-TOK`              | `https://ingest.private.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `US-EAST`             | `https://ingest.private.us-east.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| `AU-SYD`              | `https://ingest.private.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `CA TOR`              | `https://ingest.private.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| `BR SAO`              | `https://ingest.private.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write`   |
{: caption="Table 3. Prometheus remote write private endpoints" caption-side="top"} 

## Limitations 
{: #prometheus_remote_write_limitations}

The {{site.data.keyword.mon_full_notm}} Prometheus Remote Write feature has the following limitations:
- Metrics that are sent to an instance can be accessed in Explore, but they are not compatible with the scope tree.
- This feature is not supported with teams.
- Only labels that are collected at source can be used to filter metrics.
- The metadata of a metric is not sent via remote write.
- Metrics that have a name that ends with `_total`, `_sum`, or `_count` are stored as a counters, otherwise they are managed as gauge.
- You can set units in Dashboards manually.
- You cannot mix metrics with different sampling in a dashboard, for example, 10s and 1min. 

    Consider configuring the scrape interval to be 10s so that you can combine Prometheus Remote Write metrics with {{site.data.keyword.mon_short}} agent metrics.
    {: tip}


## Collecting metrics from a Kubernetes cluster by using Prometheus remote write
{: #prometheus_remote_write_kube}

You can use the Prometheus remote write feature to send metrics directly from a Kubernetes cluster to an {{site.data.keyword.mon_full_notm}} instance, in addition to metrics that are collected from the {{site.data.keyword.mon_short}} Kubernetes agent. The Kubernetes cluster can run in the {{site.data.keyword.cloud_notm}}, outside the {{site.data.keyword.cloud_notm}}, or on-prem.


### Before you begin
{: #prometheus_remote_write_kube_prereqs}

Complete the following steps:
1. Check that you have a Kubernetes cluster running and the kubectl CLI installed in your local environment.

2. Check that you have permissions to manage the cluster. You need administrator permissions to add secrets to the cluster and manage the Prometheus deployment.

3. Check that Prometheus in running in your cluster. 

    For example, you can run `kubectl get pods --all-namespaces`. Look for Prometheus and the namespace where the Prometheus server is running. 

4. Check that you have access to a {{site.data.keyword.mon_short}} instance.

5. If you use a firewall, check the firewall rules are opened for accessing the {{site.data.keyword.mon_short}} ingestion endpoint port TCP 443.


### Step 1. Create a Kubernetes Secret 
{: #prometheus_remote_write_kube_step1}

To avoid including sensitive information directly in the Prometheus ConfigMap, you must create a Kubernetes secret to store your instance's Monitor API Token that will be referenced in the Remote Write configuration.. For more information on how to get the token, see  [Monitor API token](/docs/monitoring?topic=monitoring-api_monitoring_token).

Run the following command to create the secret:

```text
kubectl create secret generic <SECRET_NAME> --from-literal=monitor-api-token="<MONITOR_API_TOKEN>" -n <PROMETHEUS_NAMESPACE>
```
{: pre}

Where

- `<SECRET_NAME>` is the name of the secret.
- `<MONITOR_API_TOKEN>` contains the [Monitor API token](/docs/monitoring?topic=monitoring-api_monitoring_token).
- `<PROMETHEUS_NAMESPACE>` is the namespace where you have Prometheus server running in your cluster.

For example, run the following command to create the secret `monitor-api-token` in the namespace `prometheus`. This command assumes Prometheus server is running in the `proemtheus` namespace:

```text
kubectl create secret generic monitor-api-token --from-literal=monitor-api-token="<MONITOR_API_TOKEN>" -n <PROMETHEUS_NAMESPACE>
```
{: pre}


### Step 2. Configure the Prometheus server remote write feature 
{: #prometheus_remote_write_kube_step2}

You can choose any of the following options to configure the Prometheus remote write feature to send metrics to an {{site.data.keyword.mon_full_notm}} instance:
- Configure the Prometheus server by updating the Kubernetes ConfigMap
- Configure the Prometheus server that is managed by Prometheus Operator 
- Configure the Prometheus server by using Helm

Choose one of the following methods to configure the Prometheus server remote write feature:
 
#### Prometheus config map
{: #prometheus_remote_write_kube_step2_1}

Complete the following steps to modify the Prometheus config map:

1. Configure your Prometheus deployment or statefulSet to mount the Kubernetes Secret that you have created in step 1.

    For example, get the name of the deployment by running the following command: 
    
    ```text
    kubectl get deployment -n <PROMETHEUS_NAMESPACE>
    ```
    {: pre}
    
    Configure a Prometheus deployment: 
    
    ```text
    kubectl edit deployment prometheus-deployment -n <PROMETHEUS_NAMESPACE>
    ```
    {: pre}

    Add the following sections to the deployment config file:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    ...
    spec:
    replicas: 1
    ...
    spec:
        containers:
        - name: prometheus-server
        args:
        ...
        volumeMounts:
        - name: secret-files
            mountPath: /etc/secrets
    volumes:
    - name: secret-files
        secret:
        secretName: <SECRET_NAME>
    ```
    {: codeblock}

2. Modify the Prometheus configMap to include the Prometheus `remote_write` block.

    Get the name of the configMap by running the following command: 
    
    ```text
    kubectl get cm -n <PROMETHEUS_NAMESPACE>
    ```
    {: pre}
    
    For Prometheus v2.25 and previous versions, follow these instructions:

    Edit the configMap:

    ```text
    kubectl edit cm <PROMETHEUS_CONFIG_MAP> -n <PROMETHEUS_NAMESPACE> 
    ```
    {: pre}

    Add the `remote_write` section:

    ```yaml
    prometheus.yml: |
        global:
            evaluation_interval: 1m
            scrape_interval: 1m
            scrape_timeout: 10s
        scrape_configs:
          - job_name: ...
        remote_write:
          - url: https://<INGESTION_URL>/prometheus/remote/write
            bearer_token_file: /etc/secrets/<SECRET_NAME>
    ```
    {: codeblock}

    Where

    `<SECRET_NAME>` is the name of the secret.

    `<INGESTION_URL>` indicates the ingestion endpoint. You must set this value to the ingestion endpoint for the region where the {{site.data.keyword.mon_short}} instance is available.

    For Prometheus version 2.26 and later versions, follow these instructions:

    Edit the configMap:

    ```text
    kubectl edit cm <PROMETHEUS_CONFIG_MAP> -n <PROMETHEUS_NAMESPACE> 
    ```
    {: codeblock}

    Add the `remote_write` section:

    ```yaml
    prometheus.yml: |
        global:
            evaluation_interval: 1m
            scrape_interval: 1m
            scrape_timeout: 10s
        scrape_configs:
          - job_name: ...
        remote_write:
        - url: https://<INGESTION_URL>/prometheus/remote/write
          authorization:
            credentials_file: /etc/secrets/<SECRET_NAME>
    ```
    {: codeblock}

    Where

    `<SECRET_NAME>` is the name of the secret.

    `<INGESTION_URL>` indicates the ingestion endpoint. You must set this value to the ingestion endpoint for the region where the {{site.data.keyword.mon_short}} instance is available.
    
3. Manage the metrics that you want to collect and send to the {{site.data.keyword.mon_short}} instance.

    To select which series and labels to collect, and reduce the number of active series that are sent to the {{site.data.keyword.mon_short}} instance, you can set up relabel configurations by using the `write_relabel_configs` block within your remote_write section.

    For example, to collect metrics from the namespace `my-namespace`, you can add the following:

    ```yaml
    remote_write:
        - url: https://<INGESTION_URL>/prometheus/remote/write
          authorization:
            credentials_file: /etc/secrets/<SECRET_NAME>
          write_relabel_configs:
            - action: keep
              regex: my-namespace
              source_labels: 
              - namespace
    ```
    {: codeblock}   

4. Restart your Prometheus server to reload the configuration.

    For example, you can delete the pod to force a restart.


#### Prometheus Operator
{: #prometheus_remote_write_kube_step2_2}

If you use the Prometheus Operator to configure and manage your Prometheus server, you can configure the Prometheus remote write feature by using the Prometheus Operator that offers Kubernetes native deployment and management of the Prometheus server and related monitoring components. 

Complete the following steps to configure the Prometheus remote write feature:
 
1. Modify your Prometheus instance to mount the secret and configure the Prometheus `remote_write` block. 

    Edit the `prometheus-prometheus.yml` file. If you have used the kube-prometheus GitHub repository, the `prometheus-prometheus.yml` file is located in the manifests directory. 
    
    Add the following entries:

    ```yaml
    ...
    volumeMounts:
    - mountPath: /etc/secrets
    name: bearer
    volumes:
    - name: bearer
    secret:
        secretName: <SECRET_NAME>
    remoteWrite:
    - url: "https://<INGESTION_URL>/prometheus/remote/write"
        bearerTokenFile: /etc/secrets/<SECRET_NAME>
    ```
    {: codeblock}

    Where

    `<SECRET_NAME>` is the name of the secret.

    `<INGESTION_URL>` indicates the ingestion endpoint. You must set this value to the ingestion endpoint for the region where the {{site.data.keyword.mon_short}} instance is available.

2. Apply the changes. Run the following command:

    ```text
    kubectl apply -f prometheus-prometheus.yaml -n <PROMETHEUS_NAMESPACE>
    ```
    {: pre}


The Prometheus Operator will restart the Prometheus StatefulSets.



#### Prometheus with Helm
{: #prometheus_remote_write_kube_step2_3}


For Prometheus v2.25 and previous versions, follow these instructions:

1. Configure the Helm Prometheus values file `values.yml` and include the `remote_write` block inside the `server` section:

    ```yaml
    ... server:
    extraSecretMounts:
    - name: secret-file
        mountPath: /etc/secrets/
        secretName: <SECRET_NAME>
    remoteWrite:
    - url: "https://<INGESTION_URL>/prometheus/remote/write"
        bearer_token_file: /tmp/bearer/<SECRET_NAME>
    ...
    ```
    {: codeblock}

    Where

    `<SECRET_NAME>` is the name of the secret.

    `<INGESTION_URL>` indicates the ingestion endpoint. You must set this value to the ingestion endpoint for the region where the {{site.data.keyword.mon_short}} instance is available.
    
2. Upgrade the Prometheus Helm release.

    ```text
    helm upgrade -f prometheus-values.yml <release name> prometheus-community/prometheus -n <PROMETHEUS_NAMESPACE>
    ```
    {: pre}

For Prometheus version 2.26 and later versions, follow these instructions:

1. Configure the Helm Prometheus values file `values.yml` and include the `remote_write` block inside the `server` section:

    ```yaml
    ... server:
    remoteWrite:
    - url: "https://<INGESTION_URL>/prometheus/remote/write"
      authorization:
        credentials_file: /etc/secrets/<SECRET_NAME>
    ...
    ```
    {: codeblock}

    Where

    `<SECRET_NAME>` is the name of the secret.

    `<INGESTION_URL>` indicates the ingestion endpoint. You must set this value to the ingestion endpoint for the region where the {{site.data.keyword.mon_short}} instance is available.
    
2. Upgrade the Prometheus Helm release.

    ```text
    helm upgrade -f prometheus-values.yml <release name> prometheus-community/prometheus -n <PROMETHEUS_NAMESPACE>
    ```
    {: pre}

### Step 3. Configure a dashboard to view metrics
{: #prometheus_remote_write_kube_step3}

Complete the following steps to check that you can monitor metrics that are collected by using the Prometheus remote write feature:

1. [Launch the {{site.data.keyword.mon_short}} web UI](/docs/monitoring?topic=monitoring-launch).

2. Navigate to the **Dashboards** section ![Dashboard icon](/images/dashboards.png "Dashboard icon"), and select **Add Dashboard** ![Add dashboard icon](/images/add.png "Add dashboard icon"). The *Create a New Dashboard* page opens.

3. Select **PromQL**.

    ![Dashboard page](/images/dashboard-page.png "Dashboard page")    

4. In the *Query* section, delete the default query and enter **container**, for example. The list of available metrics is displayed.

    ![Query](/images/query1.png "Query")  

5. Choose a metric and click **Run Query**. 

    ![Query](/images/query.png "Query")  

    You can see a metric that is collected by using the Prometheus remote write feature.

    ![Metric](/images/metric.png "<etrics")    

6. Click **Save** to create the panel that monitors the metric in the dashboard.


### Known issues
{: #prometheus_remote_write_kube_issues}

#### Prom-Beacon service not enabled
{: #prometheus_remote_write_kube_issue_1}

If you find the following log entry in the logs of the Prometheus server that is deployed in your cluster, your {{site.data.keyword.mon_short}} instance does not have the Prom-Beacon service enabled.

```text
ts=2021-05-05T13:32:16.975Z caller=dedupe.go:112 component=remote level=warn remote_name=2e147e url=https://ingest.us-south.monitoring.cloud.ibm.com/prometheus/remote/write msg="Failed to send batch, retrying" err="server returned HTTP status 503 Service Unavailable: {\"errors\":[{\"reason\":\"Customer settings error\",\"message\":\"Prom-Beacon service not enabled\"}]}"
```
{: screen}

To solve the problem, open a support ticket. You can [create](/docs/get-support?topic=get-support-open-case) and [manage](/docs/get-support?topic=get-support-managing-support-cases) a support case by using the [Support Center](https://dev.console.cloud.ibm.com/unifiedsupport/supportcenter){: external}.



