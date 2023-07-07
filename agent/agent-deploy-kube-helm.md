---

copyright:
  years:  2018, 2023
lastupdated: "2023-06-22"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Managing the {{site.data.keyword.mon_short}} agent in a Kubernetes cluster by using a HELM chart
{: #agent-deploy-kube-helm}


You can use a Helm chart to install, upgrade, and delete a {{site.data.keyword.mon_short}} agent on a Kubernetes cluster.
{: shortdesc}



## Before you begin
{: #agent-deploy-kube-helm-prereqs}

- Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

    [Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

- Check that you have access and permissions to deploy the {{site.data.keyword.mon_short}} agent on the cluster.

- Verify the `ibm-observe` namespace is available in your cluster. The agent is deployed in this namespace.

## Deploy an agent
{: #agent-deploy-kube-helm-deploy}

Complete the following steps to deploy an agent by using Helm:

### Step 1. Setup de Sysdig Helm repository
{: #agent-deploy-kube-helm-install-step1}

Add the {{site.data.keyword.mon_short}} Helm repository to your Helm instance.

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

3. Update the repos to retrieve the latest versions of all Helm charts.

    ```sh
    helm repo update
    ```
    {: pre}

4. List the Helm charts that are currently available for the Sysdig repo.

    ```sh
    helm search repo sysdig
    ```
    {: pre}

5. Verify the Helm chart `sysdig/sysdig-deploy` is listed.


If you get the following error:

```text
helm repo add sysdig https://charts.sysdig.com    --debug
Error: context deadline exceeded
helm.go:84: [debug] context deadline exceeded
```
{: screen}

Run the following command and try again.

```sh
rm $HOME/Library/Preferences/helm/repositories.lock
```
{: pre}



### Step 2. Create the values yaml file
{: #agent-deploy-kube-helm-install-step2}

Define a yaml file and include the values to deploy the {{site.data.keyword.mon_short}} agent and the {{site.data.keyword.sysdigsecure_short}} components that you plan to deploy. For example, name the file `agent-values-monitor-secure.yaml`.

The following yaml is a template that you can use to configure the {{site.data.keyword.mon_short}} agent and the {{site.data.keyword.sysdigsecure_short}} components. You can customize the file by removing or commenting with `#` the sections that are not required for your agent deployment.

```yaml
global:
  clusterConfig:
    name: CLUSTER_NAME
  sysdig:
    accessKey: MONITORING_INSTANCE_ACCESS_KEY
    secureAPIToken: SECURE_TOKEN
  kspm:
    deploy: true
agent:
  image:
    tag: AGENT_TAG
    registry: icr.io
  slim:
    enabled: true
    image:
      repository: ext/sysdig/agent-slim
    kmoduleImage:
      repository: ext/sysdig/agent-kmodule
  collectorSettings:
    collectorHost: INGESTION_ENDPOINT    # for example, ingest.eu-gb.monitoring.cloud.ibm.com
nodeAnalyzer:
  nodeAnalyzer:
    deploy: true
    apiEndpoint: API_ENDPOINT   # for example, eu-gb.monitoring.cloud.ibm.com
    benchmarkRunner:
      deploy: false
kspmCollector:
  apiEndpoint: API_ENDPOINT    # for example, eu-gb.monitoring.cloud.ibm.com
admissionController:
  enabled: true
  sysdig:
    url: WEB_UI_ENDPOINT    # for example, https://ingest.eu-gb.monitoring.cloud.ibm.com
  clusterName: CLUSTER_NAME
```
{: codeblock}

Where

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `MONITORING_INSTANCE_ACCESS_KEY` is the {{site.data.keyword.mon_short}} instance access key.
- `SECURE_TOKEN` is the Secure API token.
- `AGENT_TAG` is the version of the agent that you plan to deploy.
- `INGESTION_ENDPOINT` is the instance's ingestion endpoint.
- `API_ENDPOINT` is the intance's API endpoint.
- `WEB_UI_ENDPOINT` is the instance's web UI endpoint.


#### Sample of values yaml file to deploy the agent
{: #agent-deploy-kube-helm-install-step2-1}

For example, see the following sample of a values file that deploys the {{site.data.keyword.mon_short}} agent only:

```yaml
global:
  clusterConfig:
    name: mycluster-au-syd
  sysdig:
    accessKey: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    secureAPIToken: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  kspm:
    deploy: true
agent:
  image:
    registry: icr.io
  slim:
    enabled: true
    image:
      repository: ext/sysdig/agent-slim
    kmoduleImage:
      repository: ext/sysdig/agent-kmodule
  collectorSettings:
    collectorHost: ingest.au-syd.monitoring.cloud.ibm.com
```
{: screen}

#### Sample of values yaml file to deploy the agent and the Node Analyzer
{: #agent-deploy-kube-helm-install-step2-2}

For example, see the following sample of a values file that deploys the {{site.data.keyword.mon_short}} agent and the Node Analyzer component:

```yaml
global:
  clusterConfig:
    name: mycluster-au-syd
  sysdig:
    accessKey: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    secureAPIToken: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  kspm:
    deploy: true
agent:
  image:
    registry: icr.io
  slim:
    enabled: true
    image:
      repository: ext/sysdig/agent-slim
    kmoduleImage:
      repository: ext/sysdig/agent-kmodule
  collectorSettings:
    collectorHost: ingest.au-syd.monitoring.cloud.ibm.com
nodeAnalyzer:
  nodeAnalyzer:
    deploy: true
    apiEndpoint: API_ENDPOINT   # for example, eu-gb.monitoring.cloud.ibm.com
    benchmarkRunner:
      deploy: false
```
{: screen}


### Step 3. Install the helm chart
{: #agent-deploy-kube-helm-install-step3}

To deploy the agent, the {{site.data.keyword.sysdigsecure_short}} components, or both, you must install the `sysdig/sysdig-deploy` chart and use the variables yaml file that you configured in the previous step.

Run the following command to install the agent by using the helm chart:

```sh
helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
```
{: pre}


If you encounter the following error: `Error: INSTALLATION FAILED: Kubernetes cluster unreachable: xxxxxx failed to refresh token: oauth2: cannot fetch token: 400 Bad Request`, set your cluster context and try again.



## Update an agent
{: #agent-deploy-kube-helm-update}

To update the agent version by using Helm, complete the following steps:

1. Update the chart.

    ```sh
    helm repo update
    ```
    {: pre}

2. Find the values yaml file that you used to deploy the agent and modify the `agent.image.tag` with the version of the agent that you want to deploy.

3. Upgrade the agent.

    ```sh
    helm upgrade -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
    ```
    {: pre}



## Remove an agent
{: #agent-deploy-kube-helm-delete}

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

    In terms of Helm, `sysdig-agent` is the name of teh release.
    {: tip}


    If you forget to include the namespace in the command, you get the folloqing error: `Error: uninstall: Release not loaded: sysdig-agent: release: not found`.
