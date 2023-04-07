---

copyright:
  years:  2021, 2023
lastupdated: "2021-05-07"

keywords: IBM Cloud, monitoring, openshift, analyze metrics

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring an OpenShift cluster
{: #openshift_cluster}

Use this tutorial to learn how to configure an {{site.data.keyword.openshiftshort}} cluster to forward metrics to the {{site.data.keyword.mon_full}} service.
{: shortdesc}

To configure a cluster to forward metrics, you must install a monitoring agent onto each worker node in your Kubernetes cluster by using a [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external}. The monitoring agent uses an access key (token) to authenticate with the {{site.data.keyword.mon_full_notm}} instance. The monitoring agent acts as a data collector. It automatically collects metrics such as *worker node CPU* and *worker node memory* usage, *HTTP traffic into and out of your containers*, and data about several infrastructure components. In addition, the agent can collect custom application metrics by using either a Prometheus-compatible scraper or a StatsD facade.

You view metrics using the web-based user interface.

![Components overview on the {{site.data.keyword.cloud_notm}}](images/openshift.png "Components overview on the {{site.data.keyword.cloud_notm}}"){: caption="Components overview" caption-side="bottom"}

## Objectives
{: #openshift_cluster_objectives}

In this tutorial, you configure metrics for your {{site.data.keyword.openshiftshort}} cluster. In particular, you:
*  Provision an {{site.data.keyword.mon_full_notm}} instance.
*  Configure the monitoring agent in your cluster to send metrics.
*  Use the monitoring UI to analyze your cluster metrics.


## Before you begin
{: #openshift_cluster_prereqs}

1. [Read about {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

2. Have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://cloud.ibm.com/login){: external}.

3. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

4. [Create a cluster](/docs/openshift?topic=openshift-clusters) or use an existing {{site.data.keyword.openshiftshort}} cluster.
    *  The cluster must run Kubernetes version 1.9 or later.
    *  The cluster can be in any [{{site.data.keyword.containerlong_notm}} region](/docs/containers?topic=containers-regions-and-zones#regions-and-zones).

5. Make sure that your user ID is assigned the following {{site.data.keyword.iamlong}} policies:

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **default**           |  Resource group            | Viewer  | us-south  | This policy is required to allow the user to see service instances in the Default resource group.    |
| {{site.data.keyword.mon_full_notm}} service |  Resource group            | Editor  | us-south  | This policy is required to allow the user to provision and administer the {{site.data.keyword.mon_full_notm}} service in the default resource group.   |
| Kubernetes cluster instance          |  Resource                 | Editor  | us-south  | This policy is required to configure the secret and the monitoring agent in the {{site.data.keyword.openshiftshort}} cluster. |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"}

For more information about the {{site.data.keyword.containerlong}} IAM roles, see [User access permissions](/docs/containers?topic=containers-access_reference#access_reference).


## Step 1. Provision an {{site.data.keyword.mon_full_notm}} instance
{: #openshift_provision}

In this getting started tutorial, instructions are provided to provision an instance of the {{site.data.keyword.mon_full_notm}} in the `us-south` region. For more information about supported regions, see [Regions](/docs/monitoring?topic=monitoring-endpoints).

To provision an instance of {{site.data.keyword.mon_full_notm}}, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile.

5. For **Select a location** select `Dallas (us-south)`,

6. Select the **Lite** service plan.

    By default, the **Lite** plan is set.

    For more information about other service plans, see [Pricing plans](/docs/monitoring?topic=monitoring-pricing_plans#pricing_plans).

7. Enter a **Service name** for the service instance.

8. Select the **default** resource group.

    You can provision the instance in any resource group where you have permissions to create resources.

    By default, the **default** resource group is set.


9. Click **Create**.

    After you provision an instance, the *Observability* dashboard opens and shows details for your **Monitoring** instances.


To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/monitoring?topic=monitoring-provision#provision_cli).
{: note}


## Step 2. Configure your {{site.data.keyword.openshiftshort}} cluster to send metrics to your instance
{: #openshift_configure}

To configure your {{site.data.keyword.openshiftshort}} cluster to send metrics to your {{site.data.keyword.mon_full_notm}} instance, you must install a monitoring agent pod on each node of your cluster. The monitoring agent is installed using a DaemonSet which ensures an instance of the agent is running on every worker node. The monitoring agent collects metrics from the pod where it is installed, and forwards the data to your instance.

In order to provide the full suite of system metrics, the monitoring agent needs to have a privileged status.
{: note}

To configure your {{site.data.keyword.openshiftshort}} cluster to forward metrics to your {{site.data.keyword.mon_full_notm}} instance, complete the following steps from the command-line.

### Set the cluster context and log in to the cluster
{: #login_oscluster}

Complete the following steps:

1. Open a terminal to log in to {{site.data.keyword.cloud_notm}}.

   ```text
   ibmcloud login -a cloud.ibm.com
   ```
   {: pre}

   Select the account where you provisioned the {{site.data.keyword.mon_full_notm}} instance.

2. List the clusters to find out in which region and resource group the cluster is available.

    ```text
    ibmcloud oc clusters
    ```
    {: pre}

3. Set the resource group and region.

    ```text
    ibmcloud target -g RESOURCE_GROUP -r REGION
    ```
    {: pre}

    Where

    `RESOURCE_GROUP` is the name of the resource group where the cluster is available, for example, `default`.

    `REGION` is the region where the cluster is available, for example, `us-south`.

4. Set the cluster context in your session.

    ```text
    ibmcloud oc cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}

5. Log in to the cluster. Choose a method to login to an OpenShift cluster. [Learn more about the methods to login](/docs/openshift?topic=openshift-access_cluster).

### Install the {{site.data.keyword.mon_full_notm}} agent in your cluster
{: #install_os_agent}

1. Run the following command for your public or private endpoint.

   Private endpoints

   ```text
   curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a <MONITORING_ACCESS_KEY> -c ingest.private.us-south.monitoring.cloud.ibm.com -ac 'sysdig_capture_enabled: false' --openshift
   ```
   {: pre}

   Public endpoints

   ```text
   curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a <MONITORING_ACCESS_KEY> -c ingest.us-south.monitoring.cloud.ibm.com -ac 'sysdig_capture_enabled: false' --openshift
   ```
   {: pre}

   Where MONITORING_ACCESS_KEY is the ingestion key for the instance.

   By default the slim agent is installed.  The slim agent reduces the possible are of attack for potential vulnerabilities and, as a result, is more secure.  If installing the full agent is desired, add the `-af` option to the `curl` command.
   {: note}


2. Verify that the monitoring agent is created successfully and its status. Run the following command:

    ```text
    oc get pods -n ibm-observe
    ```
    {: codeblock}

    The deployment is successful when you see one or more `sysdig-agent` pods. The number of `sysdig-agent` pods equals the number of worker nodes in your cluster. All pods must be in a `Running` state.


## Step 3. Launch the monitoring UI
{: #openshift_launch_ui}

To launch the monitoring UI through the {{site.data.keyword.cloud_notm}} console, complete the following steps.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. From the menu ![Menu icon](../../../icons/icon_hamburger.svg), select **Observability**.

3. Select **Monitoring**. The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Find your instance and click **Open dashboard**.

    * **First time**: Because you already installed the monitoring agent, you can skip through the installation wizard, get started, and complete the onboarding.

    * **Subsequent times**: The **Explore** view opens.


If the monitoring agent is not installed successfully, points to the wrong ingestion endpoint, or the access key is incorrect, a page opens that tells you what to do next.

For example, if the monitoring agent is not installed successfully, you cannot skip through the installation wizard. You might see a message similar to the following:

```text
Waiting for the first node to connect... Go ahead and follow the instructions below.
```
{: screen}

You can try the following actions:
*  Verify that you are using the `ingest` [endpoint](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion), and not the  endpoint.
*  Verify that the [access key](/docs/monitoring?topic=monitoring-access_key) is correct.
*  Follow any additional instructions and repeat the steps in this tutorial.


## Step 4. Monitor your cluster
{: #openshift_monitor_cluster}

You can monitor your cluster in the **Explore** view that is available through the monitoring UI. This view is the default homepage and your starting point to troubleshoot and monitor your cluster infrastructure and resources.

In the section *Host and containers*, you can see the *Explore table*, a list of workers in your cluster that are forwarding metrics to the monitoring instance. Each worker entry represents a group of related infrastructure objects for that worker.

Click **Host and containers** ![Host and containers](../images/switch_hosts.png) to switch data sources. Then, select a worker. The data that is displayed corresponds to the worker that you have selected. If you click **Back to Explore Table**, the *Explore table* is displayed.

### Customizing the Explore table
{: #openshift_explore_table}

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
{: #openshift_customize_dashboards}

To view more details about a particular worker node, click on the infrastructure entry and the *Overview by Host* dashboard opens in the table. You can explore different dashboards and metrics by clicking on the ![switch dashboard](../images/switch_dashboards_1.png) icon. Notice that you can only select metrics and dashboards that are relevant to the selected worker node.

To return to the full *Explore table*, click the **X (Back to Explore Table)** button.


## Next steps
{: #openshift_cluster_next_steps}

Create a custom dashboard. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards#dashboards).

You can also learn about alerts. For more information, see [Working with alerts](/docs/monitoring?topic=monitoring-monitoring#monitoring_alerts).
