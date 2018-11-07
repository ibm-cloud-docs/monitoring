---

copyright:
  years: 2018
lastupdated: "2018-11-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Analyze metrics for an app that is deployed in a Kubernetes cluster
{: #kubernetes_cluster}
Use this tutorial to learn how to configure a cluster to forward metrics to the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

You can use the IBM Cloud Monitoring with Sysdig service to monitor Kubernetes clusters.

To configure a cluster to forward metrics, you must install an agent onto each worker node in your Kubernetes cluster using a DaemonSet. The Sysdig agent uses an access key (token) to authenticate with the IBM Cloud Monitoring with Sysdig instance. The Sysdig agent acts as a data collector. It automatically collects metrics such as *worker CPU* and worker memory*, *HTTP traffic into and out of your containers*, and several pieces of common infrastructure software. In addition, the agent can collect custom application metrics using either a Prometheus-compatible scraper or a statsd facade. 

You view metrics via Sysdig's web-based user interface.

![Components overview on the {{site.data.keyword.Bluemix_notm}}](../images/kube.png "Components overview on the {{site.data.keyword.Bluemix_notm}}")



## Before you begin
{: #prereqs}

Work in the US-South region. Both resources, the IBM Cloud Monitoring with Sysdig instance and the Kubernetes cluster must run in the same account.

Read about IBM Cloud Monitoring with Sysdig. For more information, see [About](/docs/services/Monitoring-with-Sysdig/overview.html#about).

Use a user ID that is a member or an owner of an {{site.data.keyword.Bluemix_notm}} account. To get an {{site.data.keyword.Bluemix_notm}} user ID, go to: [Registration ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/registration/){:new_window}.

Your {{site.data.keyword.IBM_notm}}ID must have assigned IAM policies for each of the following resources: 

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **Default**           |  Resource group            | Viewer  | us-south  | This policy is required to allow the user to see service instances in the Default resource group.    |
| IBM Cloud Monitoring with Sysdig service |  Resource group            | Editor  | us-south  | This policy is required to allow the user to provision and administer the IBM Cloud Monitoring with Sysdig service in the Default resource group.   |
| Kubernetes cluster instance          |  Resource                 | Editor  | us-south  | This policy is required to configure the secret and the Sysdig agent in the Kubernetes cluster. |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"} 

For more information about the {{site.data.keyword.containerlong}} IAM roles, see [User access permissions](/docs/containers/cs_access_reference.html#understanding).

Install the {{site.data.keyword.Bluemix_notm}} CLI. For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview).

Install the Kubernetes CLI plugin. For more information, see [Installing the CLI](/docs/containers/cs_cli_install.html#cs_cli_install).


## Step1: Provision an IBM Cloud Monitoring with Sysdig instance
{: #step1}

To provision an instance of IBM Cloud Monitoring with Sysdig through the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.Bluemix_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **IBM Cloud Monitoring with Sysdig** tile. The *Observability* dashboard opens.

5. Select **Create instance**. 

6. Enter a name for the service instance.

7. Select the **Default** resource group. 

    By default, the **Default** resource group is set.

8. Select the **Lite** service plan. 

    By default, the **Lite** plan is set.

    For more information about other service plans, see [Pricing plans](/docs/services/Monitoring-with-Sysdig/overview.html#pricing_plans).

9. To provision the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix_notm}} resource group where you are logged in, click **Create**.

After you provision an instance, the *Observability* dashboard opens. 


**Note:** To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/Monitoring-with-Sysdig/provision.html#provision_cli).


## Step2: Configure your Kubernetes cluster to send metrics to your instance
{: #step2}

To configure your Kubernetes cluster to send metrics to your IBM Cloud Monitoring with Sysdig instance, you must install a Sysdig agent pod on each node of your cluster. The Sysdig agent is installed via a DaemonSet which ensures an instance of the agent is running on every worker node. The Sysdig agent collects metrics from the pod where it is installed, and forwards the data to your instance.

**Note:** In order to provide the full suite of system metrics, the Sysdig agent needs to have a privileged status.

To configure your Kubernetes cluster to forward metrics to your IBM Cloud Monitoring with Sysdig instance, complete the following steps from the command line:

1. Open a terminal. Then, log in to the {{site.data.keyword.Bluemix_notm}}. Run the following command and follow the prompts:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    Select the account where you have provisioned the IBM Cloud Monitoring with Sysdig instance.

2. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

3. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/access_key.html#ibm_cloud_ui).

4. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

5. Deploy the Sysdig agent. Run the following command:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA

    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

6. Verify that the Sysdig agent is created successfully and its status. Run the following command:

    ```
    kubectl get pods
    ```
    {: codeblock}



## Step3: Launch the Sysdig Web UI
{: #step3}


## Step 4: View your metrics
{: step4}



## Next steps
{: #next_steps}







