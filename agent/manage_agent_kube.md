---

copyright:
  years:  2018, 2023
lastupdated: "2023-07-06"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Managing the Kubernetes {{site.data.keyword.mon_short}} agent
{: #manage_agent_kube}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you must configure a monitoring agent in each environment that you want to monitor. The monitoring agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{: shortdesc}

You can associate one or more tags to each monitoring agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}

## Prereqs
{: #manage_agent_kube_prereqs}

- Check the topic [Tune Agent](https://docs.sysdig.com/en/docs/installation/configuration/sysdig-agent/tune-agent/){: external}

- [Get information about Kubernetes monitoring agent images](/docs/monitoring?topic=monitoring-monitoring_agent_image).

- [Install the {{site.data.keyword.cloud_notm}} CLI and plug-ins](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps):

    * {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)

    * {{site.data.keyword.containerlong_notm}} plug-in (`ibmcloud ks`)

    * {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)

    * {{site.data.keyword.containerlong_notm}} observability plug-in (`ibmcloud ob`)

- [Install the Kubernetes CLI (kubectl)](/docs/containers?topic=containers-cs_cli_install#kubectl)

    Make sure that the `kubectl` version is compatible with your cluster version. If the `kubectl` version is not compatible, you can get an error such as `kubectl create clusterrolebinding failed!`. You can use `kubectl version --short` to check versions of your cluster and your `kubectl` client.

- If you plan to run the {{site.data.keyword.mon_short}} service, Secure with the node analyzer, or both, check your cluster flavor. You need a minimum `b3c.4x16` flavor for node analyzer to run.

    If you have a cluster with a `free` plan, you do not have sufficient CPU to run the {{site.data.keyword.mon_short}} agent.
    {: note}

## IAM permissions
{: #manage_agent_kube_iam}

You must have a minimum of `Viewer` and `Manager` IAM permissions assigned for the Kubernetes cluster to complete this step.
{: note}

## Deploying a monitoring agent
{: #manage_agent_kube_deploy}

Complete the following steps to configure a monitoring agent on a Kubernetes cluster:

1. Obtain the access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Set up the cluster environment.

    Run the following command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Deploy the monitoring agent. Choose one of the following commands:

    Option 1: Monitor only

    ```text
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a MONITORING_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false' -sn 'MONITORING_INSTANCE_NAME'
    ```
    {: pre}

    Option 2: Monitor and {{site.data.keyword.sysdigsecure_short}}

    ```text
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a MONITORING_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false' --nodeanalyzer --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector --api_endpoint <API-ENDPOINT>
    ```
    {: pre}

    Where

    * `MONITORING_ACCESS_KEY` is the ingestion key for the instance.

    * `COLLECTOR_ENDPOINT` is the public or private ingestion URL for the region where the {{site.data.keyword.mon_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

    * `TAG_DATA` are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example: *role:serviceX,location:us-south*.

    * `MONITORING_INSTANCE_NAME` is the name of the {{site.data.keyword.mon_short}} instance where you can monitor your cluster. This information is available as a label: `sysdig-instance`.

        Use the command `kubectl describe ds sysdig-agent -n ibm-observe` to see the label and identify the instance where you can monitor the cluster.
        {: tip}

    * Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

    * Add `--imageanalyzer --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector`, if you have the service plan that includes the **Secure** component, and images hosted in the {{site.data.keyword.registryshort_notm}}.  This will install the image analyzer **{{site.data.keyword.sysdigsecure_short}}** component only.

    * Add `--nodeanalyzer --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector --API_ENDPOINT <API-ENDPOINT>`, if you have the service plan that includes the **{{site.data.keyword.sysdigsecure_short}}** component, and images hosted in the {{site.data.keyword.registryshort_notm}}.  This will install the **{{site.data.keyword.sysdigsecure_short}}** components: image-analyzer, host-analyzer, and benchmark runner. The `API_ENDPOINT` is needed by the benchmark runner. The `COLLECTOR_ENDPOINT` is needed by the image analyzer.

    To get help about the different options, you can run `curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -h`.
    {: tip}

    For example, to deploy the agent for an instance located in London (`eu-gb`), you can run:

    ```text
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a xxxxxxxx -c ingest.eu-gb.monitoring.cloud.ibm.com -t classic -ac 'sysdig_capture_enabled: false' --nodeanalyzer --analysismanager https://ingest.eu-gb.monitoring.cloud.ibm.com/internal/scanning/scanning-analysis-collector --api_endpoint eu-gb.monitoring.cloud.ibm.com -sn 'my-monitoring-instance'
    ```
    {: screen}

If you get the error `ERROR: default-icr-io or all-icr-io secret doesn't exist in the default namespace`, run the following command `ibmcloud ks cluster pull-secret apply --cluster CLUSTER_ID` before you try to deploy the agent again.



## Updating a Kubernetes agent
{: #manage_agent_kube_update}

By default, the monitoring agent has a `RollingUpdate` update strategy.

```yaml
updateStrategy:
    rollingUpdate:
      maxUnavailable: 1
    type: RollingUpdate
```
{: codeblock}

When you update the agent's DaemonSet template, old DaemonSet pods are killed, and new DaemonSet pods are created automatically.

The image that is used to create the new pods is the one that is specified in the DaemonSet template. By default, the monitoring agent's image pull policy is configured to always so that it pulls the latest image. The `imagePullPolicy` of the container is set to `Always`.

```yaml
containers:
    - image: icr.io/ext/sysdig/agent
      imagePullPolicy: Always
      name: sysdig-agent
```
{: codeblock}

Complete the following steps to update a monitoring agent with a `RollingUpdate` update strategy:

1. Set up the cluster environment. Run the following command:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. List the DaemonSets that are running in the `ibm-observe` namespace, and verify that the monitoring agent is running in this namespace:

    ```text
    kubectl get daemonsets -n ibm-observe
    ```
    {: pre}

    Verify the monitoring agent is running.

3. Check the DaemonSet update strategy:

    ```text
    kubectl get ds/sysdig-agent -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}' -n ibm-observe
    ```
    {: pre}

    Verify that is set to `RollingUpdate`.

4. Check the image version that is deployed:

    ```text
    kubectl describe ds sysdig-agent -n ibm-observe | grep Image
    ```
    {: pre}

5. Update the image that is configured in the DaemonSet template to the monitoring agent image that you want to use:

    ```text
    kubectl set image ds/sysdig-agent sysdig-agent=icr.io/ext/sysdig/agent:IMAGE_VERSION -n ibm-observe
    ```
    {: pre}

    Where `IMAGE_VERSION` is the version of the agent that you want to deploy. To see the the agent versions that are available, see [monitoring agent Release Notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html){: external}.

    For example, to update the agent to version `10.5.1`, you can run the following command:

    ```text
    kubectl set image ds/sysdig-agent sysdig-agent=icr.io/ext/sysdig/agent:10.5.1 -n ibm-observe
    ```
    {: pre}

    This step will initiate the update request.

6. Check the update completes.

    ```text
    kubectl rollout status ds/sysdig-agent -n ibm-observe
    ```
    {: pre}


## Removing a monitoring agent
{: #manage_agent_kube_remove}

Complete the following steps to remove a monitoring agent from a Kubernetes cluster:

1. Obtain the access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Set up the cluster environment.

    If the cluster runs in the {{site.data.keyword.containerlong_notm}}, run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```text
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

4. Remove the monitoring agent.

    ```text
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a MONITORING_ACCESS_KEY -c COLLECTOR_ENDPOINT -r
    ```
    {: pre}

    Where

    * MONITORING_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).
