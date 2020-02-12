---

copyright:
  years:  2018, 2020
lastupdated: "2020-02-12"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

subcollection: Sysdig

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


# Analyze metrics for an Ubuntu host
{: #ubuntu}

Use this tutorial to learn how to configure an Ubuntu host to forward metrics to the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}.
{:shortdesc}

To configure an Ubuntu server to forward metrics, you must install a Sysdig agent. The agent uses an access key (token) to authenticate with the {{site.data.keyword.mon_full_notm}} instance. The Sysdig agent acts as a data collector. It automatically collects metrics.

You view metrics via Sysdig's web-based user interface.

![Components overview on the {{site.data.keyword.cloud_notm}}](../images/ubuntu.png "Components overview on the {{site.data.keyword.cloud_notm}}")



## Before you begin
{: #ubuntu_prereqs}

Work in the US-South region. 

Read about {{site.data.keyword.mon_full_notm}}. For more information, see [About](/docs/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Use a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to [Registration ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}.

Your {{site.data.keyword.IBM_notm}}ID must have assigned IAM policies for each of the following resources: 

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **Default**           |  Resource group            | Viewer  | `Us-south`  | This policy is required to allow the user to see service instances in the Default resource group.    |
| {{site.data.keyword.mon_full_notm}} service |  Resource group            | Editor  | `Us-south`  | This policy is required to allow the user to provision and administer the {{site.data.keyword.mon_full_notm}} service in the Default resource group.   |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"} 

Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started).


## Step 1. Provision an {{site.data.keyword.mon_full_notm}} instance
{: #ubuntu_step1}

To provision an instance of {{site.data.keyword.mon_full_notm}} through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile. The *Observability* dashboard opens.

5. Select **Create instance**. 

6. Enter a name for the service instance.

7. Select the **Default** resource group. 

    By default, the **Default** resource group is set.

8. Select the **Lite** service plan. 

    By default, the **Lite** plan is set.

    For more information about other service plans, see [Pricing plans](/docs/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. To provision the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}} resource group where you are logged in, click **Create**.

After you provision an instance, the *Observability* dashboard opens. 


**Note:** To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Step 2. Configure your Ubuntu server to send metrics to your instance
{: #ubuntu_step2}

To configure your Ubuntu server to send metrics to your {{site.data.keyword.mon_full_notm}} instance, you must install a Sysdig agent. 

Complete the following steps from the command line:

1. Open a terminal. Then, log in to the {{site.data.keyword.cloud_notm}}. Run the following command and follow the prompts:

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    Select the account where the {{site.data.keyword.mon_full_notm}} instance is available.

2. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

3. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

4. Deploy the Sysdig agent. Run the following command:

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example, *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

If the Sysdig agent fails to install correctly, install the kernel headers manually. Choose a distribution and run the command for that distribution. Then, retry the deployment of the Sysdig agent.

* **For Debian and Ubuntu Linux distributions**, run the following command:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **For RHEL, CentOS, and Fedora Linux distributions**, run the following command:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## Step 3. Launch the Sysdig Web UI
{: #ubuntu_step3}

Complete the following steps to launch the web UI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. 

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select your instance. Then, click **View Sysdig**.

If the Sysdig agent is configured successfully, the *EXPLORE* view opens.

However, if the Sysdig agent is not installed successfully, points to the wrong ingestion endpoint, or the access key is incorrect, the page that opens informs you about what to do next.

You only can have one web UI session open per browser.
{: tip}


## Step 4. Monitor your Ubuntu server
{: #ubuntu_step4}

You can monitor your Ubuntu server in the **EXPLORE** view that is available through the Web UI. This view is the starting point to troubleshoot and monitor your infrastructure. It is the default homepage of the Web UI for users.

In the section *Host and containers*, you can find the entry for your Ubuntu server. Click **Host and containers** ![Host and containers](../images/switch_hosts.png) to switch data sources. Then, select your Ubuntu server. The data that is displayed corresponds to the Ubuntu server that you select.

For example, to configure color-coding for a column, complete the following steps:

1. Select a column. Hover the mouse over the column title. Then, select the pencil icon.
2. Toggle the bar to enable color-coding.
3. Set values for the different thresholds.



## Next steps
{: #ubuntu_next_steps}

Create a custom dashboard. For more information, see [Working with dashboards](/docs/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

You can also learn about alerts. For more information, see [Working with alerts](/docs/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 





