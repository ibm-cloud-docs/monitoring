---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-24"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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
{:external: target="_blank" .external}


# Monitoring a Kubernetes cluster
{: #kubernetes_cluster}

Use this tutorial to learn how to configure an {{site.data.keyword.containerlong}} cluster to forward metrics to the {{site.data.keyword.mon_full}} service.
{:shortdesc}

To configure a cluster to forward metrics, you must install a monitoring agent onto each worker node in your Kubernetes cluster by using a [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external}. The monitoring agent uses an access key (token) to authenticate with the {{site.data.keyword.mon_full_notm}} instance. The monitoring agent acts as a data collector. It automatically collects metrics such as *worker node CPU* and *worker node memory* usage, *HTTP traffic into and out of your containers*, and data about several infrastructure components. In addition, the agent can collect custom application metrics by using either a Prometheus-compatible scraper or a StatsD facade. 

You view metrics via Sysdig's web-based user interface.

![Components overview on the {{site.data.keyword.cloud_notm}}](../images/kube.png "Components overview on the {{site.data.keyword.cloud_notm}}")

## Objectives
{: #kubernetes_cluster_objectives}

In this tutorial, you configure metrics with Sysdig in your {{site.data.keyword.containerlong}} cluster. In particular, you:
*  Provision an {{site.data.keyword.mon_full_notm}} instance.
*  Configure the monitoring agent in your cluster to sent metrics to Sysdig.
*  Use the monitoring UI to analyze your cluster metrics.


## Before you begin
{: #kubernetes_cluster_prereqs}

1. [Read about {{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started).

2. Have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://cloud.ibm.com/login){: external}.

3. [Install the {{site.data.keyword.cloud_notm}} CLI and the Kubernetes CLI plugin](/docs/cli?topic=cli-install-ibmcloud-cli).

4. [Create a cluster](/docs/containers?topic=containers-clusters#clusters) or use an existing {{site.data.keyword.containerlong_notm}} cluster.
    *  The cluster must run Kubernetes version 1.10 or above.
    *  The cluster does not have to be in the **Dallas** location, but can be in any [{{site.data.keyword.containerlong_notm}} region](/docs/containers?topic=containers-regions-and-zones#regions-and-zones).

5. Make sure that your user ID is assigned the following {{site.data.keyword.iamlong}} policies:

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **default**           |  Resource group            | Viewer  | Us-south  | This policy is required to allow the user to see service instances in the Default resource group.    |
| {{site.data.keyword.mon_full_notm}} service |  Resource group            | Editor  | Us-south  | This policy is required to allow the user to provision and administer the {{site.data.keyword.mon_full_notm}} service in the default resource group.   |
| Kubernetes cluster instance          |  Resource                 | Editor  | Us-south  | This policy is required to configure the secret and the monitoring agent in the Kubernetes cluster. |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"}

For more information about the {{site.data.keyword.containerlong}} IAM roles, see [User access permissions](/docs/containers?topic=containers-access_reference#access_reference).



## Step 1. Provision an {{site.data.keyword.mon_full_notm}} instance
{: #kubernetes_cluster_step1}

In this getting tutorial, instructions are provided to provision an instance of the {{site.data.keyword.mon_full_notm}} in the US-South region. For more information about supported regions, see [Regions](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints).

To provision an instance of {{site.data.keyword.mon_full_notm}} through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile. The *Observability* dashboard opens.

5. Select **Create instance**. 

6. Enter a name for the service instance.

7. Select the **default** resource group. 

    You can provision the instance in any resource group where you have permissions to create resources.

    By default, the **default** resource group is set.

8. Select the **Trial** service plan. 

    By default, the **Trial** plan is set.

    For more information about other service plans, see [Pricing plans](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-pricing_plans#pricing_plans).

9. Click **Create**.

    After you provision an instance, the *Observability* dashboard opens and shows details for your **Monitoring** instances. 


To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-provision#provision_cli).
{: note}


## Step 2. Configure your Kubernetes cluster to send metrics to your instance
{: #kubernetes_cluster_step2}

To configure your Kubernetes cluster to send metrics to your {{site.data.keyword.mon_full_notm}} instance, you must install a monitoring agent pod on each node of your cluster. The monitoring agent is installed via a DaemonSet which ensures an instance of the agent is running on every worker node. The monitoring agent collects metrics from the pod where it is installed, and forwards the data to your instance.

In order to provide the full suite of system metrics, the monitoring agent needs to have a privileged status.
{: note}

To configure your Kubernetes cluster to forward metrics to your {{site.data.keyword.mon_full_notm}} instance, complete the following steps from the command-line:

1. Open a terminal. Then, log in to the {{site.data.keyword.cloud_notm}}. Run the following command and follow the prompts:

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    Select the account where the cluster is available.

2. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable. Copy and paste the command that is displayed in your terminal to set the `KUBECONFIG` environment variable.

    Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.
    {: tip}

3. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

4. Obtain the ingestion URL from the [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

5. Deploy the monitoring agent. Run the following command:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: pre}

    Where

    * **SYSDIG_ACCESS_KEY** is the ingestion key for the instance that you previously retrieved.

    * **COLLECTOR_ENDPOINT** is the ingestion URL for the region where the monitoring instance is available that you previously retrieved.

    * **TAG_DATA** are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).

6. Verify that the monitoring agent is created successfully and its status. Run the following command:

    ```
    kubectl get pods -n ibm-observe
    ```
    {: codeblock}

    The deployment is successful when you see one or more `sysdig-agent` pods. The number of `sysdig-agent` pods equals the number of worker nodes in your cluster. All pods must be in a `Running` state.


## Step 3. Launch the monitoring UI
{: #kubernetes_cluster_step3}

To launch the monitoring UI through the {{site.data.keyword.cloud_notm}} console, complete the following steps.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. From the menu ![Menu icon](../../../icons/icon_hamburger.svg), select **Observability**. 

3. Select **Monitoring**. The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Find your instance and click **View Sysdig**.

    * **First time**: Because you already installed the monitoring agent, you can skip through the installation wizard, get started, and complete the onboarding.
    
    * **Subsequent times**: The **Explore** view opens.


If the monitoring agent is not installed successfully, points to the wrong ingestion endpoint, or the access key is incorrect, the page that opens informs you about what to do next.

For example, if the monitoring agent is not installed successfully, you cannot skip through the installation wizard., You might see a message similar to the following:
    
```
Waiting for the first node to connect... Go ahead and follow the instructions below.
```
{: screen}
    
You can try the following actions:
*  Verify that you are using the `ingest` [endpoint](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion), and not the Sysdig endpoint. 
*  Verify that the [access key](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key) is correct.
*  Follow any additional instructions and repeat the steps in this tutorial.



## Step 4. Monitor your cluster
{: #kubernetes_cluster_step4}

You can monitor your cluster in the **EXPLORE** view that is available through the monitoring UI. This view is the default homepage and your starting point to troubleshoot and monitor your cluster infrastructure and resources.

In the section *Host and containers*, you can see the you see the *Explore table*, a list of workers in your cluster that are forwarding metrics to the monitoring instance. Each worker entry represents a group of related infrastructure objects for that worker.

Click **Host and containers** ![Host and containers](../images/switch_hosts.png) to switch data sources. Then, select a worker. The data that is displayed corresponds to the worker that you have selected. If you click ** Back to Explore Table**, the *Explore table* is displayed. 

### Customizing the Explore table
{: #kubernetes_cluster_step4-1}

You can customize the *Explore table*. 

* Each column shows a different metric. 
* You can configure each metric individually. 
* You can change the order of the columns. 

    Notice that when you make changes to the order of existing columns, the change is persistent across different groupings while you are logged in. If you add or remove a column, the change is persistent. 

* You can also configure colors to highlight values and improve readability. 

For example, to configure color-coding for a column, complete the following steps:

1. Select a column. Hover the mouse over the column title. Then, select the pencil icon.
2. Toggle the bar to enable color-coding.
3. Set values for the different thresholds.


### Customizing dashboards
{: #kubernetes_cluster_step4-2}

To view more details about a particular worker node, click on the infrastructure entry and the *Overview by Host* dashboard opens in the table. You can explore different dashboards and metrics by clicking on the ![switch dashboard](../images/switch_dashboards_1.png) icon. Notice that you can only select metrics and dashboards that are relevant to the selected worker node.

To return to the full _Explore table_, click the **X (Back to Explore Table)** button.


For more information, check out the [Sysdig docs](https://docs.sysdig.com/en/sysdig-monitor.html){: externak}.



## Next steps
{: #kubernetes_cluster_next_steps}

Create a custom dashboard. For more information, see [Working with dashboards](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-dashboards#dashboards).

You can also learn about alerts. For more information, see [Working with alerts](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-monitoring#monitoring_alerts). 





