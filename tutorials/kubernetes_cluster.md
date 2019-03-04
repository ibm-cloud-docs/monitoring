---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

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

Use this tutorial to learn how to configure a cluster to forward metrics to the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.cloud_notm}}.
{:shortdesc}

You can use the IBM Cloud Monitoring with Sysdig service to monitor Kubernetes clusters.

To configure a cluster to forward metrics, you must install an agent onto each worker node in your Kubernetes cluster using a DaemonSet. The Sysdig agent uses an access key (token) to authenticate with the IBM Cloud Monitoring with Sysdig instance. The Sysdig agent acts as a data collector. It automatically collects metrics such as *worker CPU* and worker memory*, *HTTP traffic into and out of your containers*, and several pieces of common infrastructure software. In addition, the agent can collect custom application metrics using either a Prometheus-compatible scraper or a statsd facade. 

You view metrics via Sysdig's web-based user interface.

![Components overview on the {{site.data.keyword.cloud_notm}}](../images/kube.png "Components overview on the {{site.data.keyword.cloud_notm}}")



## Before you begin
{: #kubernetes_cluster_prereqs}

To complete the steps in this getting tutorial, instructions are  provided to provision an instance of the IBM Cloud Monitoring with Sysdig in the US-South region. You can use an exiting cluster or a new **cluster version 1.10**. The cluster can be available in a different region.  

Read about IBM Cloud Monitoring with Sysdig. For more information, see [About](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Use a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}.

Your {{site.data.keyword.IBM_notm}}ID must have assigned IAM policies for each of the following resources: 

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **Default**           |  Resource group            | Viewer  | us-south  | This policy is required to allow the user to see service instances in the Default resource group.    |
| IBM Cloud Monitoring with Sysdig service |  Resource group            | Editor  | us-south  | This policy is required to allow the user to provision and administer the IBM Cloud Monitoring with Sysdig service in the Default resource group.   |
| Kubernetes cluster instance          |  Resource                 | Editor  | us-south  | This policy is required to configure the secret and the Sysdig agent in the Kubernetes cluster. |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"} 

For more information about the {{site.data.keyword.containerlong}} IAM roles, see [User access permissions](/docs/containers?topic=containers-access_reference#access_reference).

Install the {{site.data.keyword.cloud_notm}} CLI and the Kubernetes CLI plugin. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Step1: Provision an IBM Cloud Monitoring with Sysdig instance
{: #kubernetes_cluster_step1}

To provision an instance of IBM Cloud Monitoring with Sysdig through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

    Click [{{site.data.keyword.cloud_notm}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window} to launch the {{site.data.keyword.cloud_notm}} dashboard.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **IBM Cloud Monitoring with Sysdig** tile. The *Observability* dashboard opens.

5. Select **Create instance**. 

6. Enter a name for the service instance.

7. Select the **Default** resource group. 

    By default, the **Default** resource group is set.

8. Select the **Trial** service plan. 

    By default, the **Trial** plan is set.

    For more information about other service plans, see [Pricing plans](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. To provision the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.cloud_notm}} resource group where you are logged in, click **Create**.

After you provision an instance, the *Observability* dashboard opens. 


**Note:** To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Step2: Configure your Kubernetes cluster to send metrics to your instance
{: #kubernetes_cluster_step2}

To configure your Kubernetes cluster to send metrics to your IBM Cloud Monitoring with Sysdig instance, you must install a Sysdig agent pod on each node of your cluster. The Sysdig agent is installed via a DaemonSet which ensures an instance of the agent is running on every worker node. The Sysdig agent collects metrics from the pod where it is installed, and forwards the data to your instance.

**Note:** In order to provide the full suite of system metrics, the Sysdig agent needs to have a privileged status.

To configure your Kubernetes cluster to forward metrics to your IBM Cloud Monitoring with Sysdig instance, complete the following steps from the command line:

1. Open a terminal. Then, log in to the {{site.data.keyword.cloud_notm}}. Run the following command and follow the prompts:

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

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

3. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

4. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

5. Deploy the Sysdig agent. Run the following command:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

6. Verify that the Sysdig agent is created successfully and its status. Run the following command:

    ```
    kubectl get pods
    ```
    {: codeblock}



## Step3: Launch the Sysdig web UI
{: #kubernetes_cluster_step3}

Complete the following steps to launch the web UI:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

    Click [{{site.data.keyword.cloud_notm}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window} to launch the {{site.data.keyword.cloud_notm}} dashboard.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. 

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select your instance. Then, click **View Sysdig**.

If the Sysdig agent is configured successfully, the *EXPLORE* view opens.

However, if the Sysdig agent is not installed successfully, points to the wrong ingestion endpoint, or the access key is incorrect, the page that opens informs you about what to do next.

You can only have one Web UI session open per browser.
{: tip}


## Step 4: Monitor your cluster
{: #kubernetes_cluster_step4}

You can monitor your cluster in the **EXPLORE** view that is available through the Web UI. This view is the starting point to troubleshoot and monitor your infrastructure. It is the default homepage of the Web UI for users.

In the section *Host and containers*, you can see the list of workers in your cluster that are forwarding metrics to the monitoring instance. Each worker entry represents a group of related infrastructure objects for that worker.

Click **Host and containers** ![Host and containers](../images/switch_hosts.png) to switch data sources. Then, select a worker. The data that is displayed corresponds to the worker that you have selected.

If you click ** Back to Explore Table**, the *Explore table* is displayed. Each column shows a different metric. You can configure each metric individually. You can change the order of the columns. Notice that when you make changes to the order of existing columns, the change is persistent across different groupings while you are logged in. If you add or remove a column the change is persistent. You can also configure colors to highlight values and improve readability.

For example, to configure color-coding for a column, complete the following steps:

1. Select a column. Hover the mouse over the column title. Then, select the pencil icon.
2. Toggle the bar to enable color-coding.
3. Set values for the different thresholds.

If you select a worker, a default dashboard is displayed. Click on the ![switch dashboard](images/switch_dashboards_1.png) and explore the different default dashboards and metrics. Notice that you can only select metrics and dashboards that are relevant to the selected worker.


## Next steps
{: #kubernetes_cluster_next_steps}

Create a custom dashboard. For more information, see [Working with dashboards](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

You can also learn about alerts. For more information, see [Working with alerts](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 





