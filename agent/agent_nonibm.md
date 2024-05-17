---

copyright:
  years:  2018, 2024
lastupdated: "2024-05-17"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Deploying the agent a Kubernetes or OpenShift cluster that is not part of {{site.data.keyword.cloud_notm}}
{: #agent-deploy-kube-helm}


In addition to its ability to run in {{site.data.keyword.cloud}}, the centralized monitoring that {{site.data.keyword.mon_full_notm}} provides can also be run in other clouds and on premises by using Helm charts to install the monitoring agent onto Kubernetes or OpenShift clusters.
{: shortdesc}

## Before you begin
{: #nonibm-deploy-kube-helm-prereqs}

- [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)](/docs/openshift?topic=openshift-openshift-cli#cs_cli_install_steps)

- Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

   Helm 3.6 or later is required.
   {: note}

   [Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

- Check that you have access and permissions to deploy the {{site.data.keyword.mon_full_notm}} agent on the cluster.

- Verify the `ibm-observe` namespace is available in your cluster. The agent is deployed in this namespace.

    You can run the following command to create the namespace: `kubectl create namespace ibm-observe`
    {: tip}

    If you are connecting a Kubernetes or OpenShift cluster with {{site.data.keyword.mon_full_notm}} and [{{site.data.keyword.sysdigsecure_full_notm}}](/docs/workload-protection?topic=workload-protection-about) see [Deploying the agent in an outside Kubernetes or OpenShift cluster in the {{site.data.keyword.sysdigsecure_full_notm}} documentation](https://cloud.ibm.com/docs/workload-protection?topic=workload-protection-deploy-wp-outside-cloud) and follow the instructions.
    {: tip}


## Deploy an agent
{: #nonibm-deploy-kube-helm-deploy}

Complete the following steps to deploy an agent by using Helm:

### Step 1. Setup the Sysdig Helm repository
{: #agent-deploy-kube-helm-install-step1}

Add the {{site.data.keyword.mon_full_notm}} Helm repository to your Helm instance.

Complete the following steps:

1. Set the cluster context.

    ```sh
    ibmcloud ks cluster config --cluster <CLUSTER_NAME>
    ```
    {: pre}

2.  Add the Helm repository.

    ```sh
    helm repo add sysdig https://charts.sysdig.com
    ```
    {: pre}

    If you get the following error:

    ```text
    helm repo add sysdig https://charts.sysdig.com    --debug
    Error: context deadline exceeded
    helm.go:84: [debug] context deadline exceeded
    ```
    {: screen}

    Run the following command and retry adding the Helm repository.

    ```sh
    rm $HOME/Library/Preferences/helm/repositories.lock
    ```
    {: pre}

3. Update the repos to retrieve the latest versions of all Helm charts.

    ```sh
    helm repo update
    ```
    {: pre}

4. List the Helm charts that are currently available for the `sysdig` repo.

    ```sh
    helm search repo sysdig
    ```
    {: pre}

5. Verify the Helm chart `sysdig/sysdig-deploy` is listed.

### Step 2. Create the values yaml file
{: #nonibm-deploy-kube-helm-install-step2}

Define a yaml file and include the values to deploy the {{site.data.keyword.mon_full_notm}} agent that you plan to deploy. For example, name the file `agent-values-monitor.yaml`.

The following yaml is a template that you can use to configure the {{site.data.keyword.mon_full_notm}} agent.

```yaml
global:
  clusterConfig:
    name: CLUSTER_NAME
  sysdig:
    accessKey: SERVICE_ACCESS_KEY
agent:
  collectorSettings:
    collectorHost: INGESTION_ENDPOINT
nodeAnalyzer:
  enabled: false
```
{: codeblock}

Where

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.mon_full_notm}} instance access key.
- `INGESTION_ENDPOINT` is the instance's ingestion endpoint. For example, `ingest.us-east.monitoring.cloud.ibm.com`

You can find [here](https://github.com/sysdiglabs/charts/tree/main/charts/sysdig-deploy){: external} all available options to configure the {{site.data.keyword.mon_full_notm}} agent.

### Step 3. Install the Helm chart
{: #agent-deploy-kube-helm-install-step3}

To deploy the agent you must install the `sysdig/sysdig-deploy` chart. You can install the chart by using a variables yaml file like the one that you configured in the previous step, or you can configure the variables directly.

Run the following command to install the agent by using the Helm chart and the variables `yaml` file:

```sh
helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor.yaml
```
{: pre}


If you are not using the Helm values file, you can run the following command to install the agent by using the Helm chart and setting the variables:

```sh
helm install sysdig-agent sysdig/sysdig-deploy --namespace ibm-observe --create-namespace\
    --set global.sysdig.accessKey=<SERVICE_ACCESS_KEY> \
    --set agent.collectorSettings.collectorHost=<INGESTION_ENDPOINT> \
    --set nodeAnalyzer.enabled=false \
    --set global.clusterConfig.name=<CLUSTER_NAME> 
```
{: pre}

Where

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.mon_full_notm}} instance access key.
- `INGESTION_ENDPOINT` is the instance's ingestion endpoint.


For example, for the `us-east` region, a sample Helm install is similar to the follows:

```sh
helm install sysdig-agent sysdig/sysdig-deploy --namespace ibm-observe \
    --set global.sysdig.accessKey=<ENTER_YOUR_ACCESS_KEY> \
    --set agent.collectorSettings.collectorHost=ingest.us-east.monitoring.cloud.ibm.com \
    --set nodeAnalyzer.enabled=false \
    --set global.clusterConfig.name=mycluster
```
{: pre}


If you encounter the following error: `Error: INSTALLATION FAILED: Kubernetes cluster unreachable: xxxxxx failed to refresh token: oauth2: cannot fetch token: 400 Bad Request`, set your cluster context and try again.

## Updating an agent
{: #nonibm-deploy-kube-helm-update}

To update the agent version by using Helm, complete the following steps:

1. Update the chart.

    ```sh
    helm repo update
    ```
    {: pre}

2. Upgrade the agent.

    ```sh
    helm upgrade -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor.yaml
    ```
    {: pre}

These steps install latest available version in your cluster.


## Removing an agent
{: #nonibm-deploy-kube-helm-delete}

To delete the agent by using Helm, you must uninstall the chart.

Complete the following steps:

1. List the charts that are installed.

    ```sh
    helm list -n ibm-observe
    ```
    {: pre}

    The output of the command lists charts as follows:

    ```text
    NAME        	NAMESPACE  	REVISION	UPDATED                             	STATUS  	CHART              	APP VERSION
    sysdig-agent	ibm-observe	1       	2023-03-24 15:02:58.408108 +0100 CET	deployed	sysdig-deploy-1.6.3
    ```
    {: screen}

2. Uninstall the chart.

    ```sh
    helm delete sysdig-agent  -n ibm-observe
    ```
    {: pre}

    In terms of Helm, `sysdig-agent` is the name of the release.
    {: tip}


    If you forget to include the namespace in the command, you get the following error: `Error: uninstall: Release not loaded: sysdig-agent: release: not found`.
