---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, ubuntu, analyze metrics

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


# Monitoring an Ubuntu Linux VPC server instance
{: #ubuntu}

Use this tutorial to learn how to configure an Ubuntu host to forward metrics to the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

To configure an Ubuntu server to forward metrics, you must install a monitoring agent. The agent uses an access key (token) to authenticate with the {{site.data.keyword.mon_full_notm}} instance. The monitoring agent acts as a data collector. It automatically collects metrics.

You then view the metrics using the web-based user interface.


## Before you begin
{: #ubuntu_prereqs}

[Read about {{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started).

Work in the `US South` region. 

Use a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} {{site.data.keyword.IBM_notm}}ID, go to [Create an account](https://cloud.ibm.com/login){: external}.

Your {{site.data.keyword.IBM_notm}}ID must have assigned IAM policies for each of the following resources: 

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **default**           |  Resource group            | Viewer  | `US South`  | This policy is required to allow the user to see service instances in the **default** resource group.    |
| {{site.data.keyword.mon_full_notm}} service |  Resource group            | Editor  | `US South`  | This policy is required to allow the user to provision and administer the {{site.data.keyword.mon_full_notm}} service in the **default** resource group.   |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"} 

The {{site.data.keyword.cloud_notm}} CLI must be installed. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

## Step 1. Provision an Ubuntu Linux VPC server instance
{: #ubuntu_step1}

If you have an existing Ubuntu Linux virtual server instance you want to monitor, you can skip this step.

1. If you don't have a virtual private cloud, [use the {{site.data.keyword.cloud_notm}} console to create VPC resources](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).

2. If you don't have an Ubuntu Linux virtual server instance, [create an Umbuntu Linux virtual server instance by using the UI and selecting **Ubuntu Linux** as the **Operating System**](https://cloud.ibm.com/docs/vpc?topic=vpc-creating-virtual-servers).

## Step 2. Provision an {{site.data.keyword.mon_full_notm}} instance
{: #ubuntu_step2}

To provision an instance of {{site.data.keyword.mon_full_notm}} through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

   After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Logging and Monitoring** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile. The *Observability* dashboard opens.

5. Select the **Create** tab. 

6. Select a region for the service instance.

7. Select the **Lite** service plan. 

   By default, the **Lite** plan is set.

   For more information about other service plans, see [Pricing](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-pricing_plans).

8. Enter a **Service name** for the service instance.

9. Select the **default** resource group. 

   By default, the **default** resource group is set.

10. (Optional) Specify any [tags](/docs/account?topic=account-tag) you want to use.

11. Select whether of not the service instance receives platform metrics for all service instances in the region.

12. To provision the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}} resource group where you are logged in, click **Create**.

After you provision an instance, the **Monitoring** dashboard opens. 

**Note:** To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-provision#provision_cli).

## Step 3. Configure your Ubuntu server to send metrics to your instance
{: #ubuntu_step3}

To configure your Ubuntu server to send metrics to your {{site.data.keyword.mon_full_notm}} instance, you must install a monitoring agent. 

Complete the following steps from a command line:

1. Open a terminal. Then, log in to the {{site.data.keyword.cloud_notm}}. Run the following command and follow the prompts:

   ```
   ibmcloud login -a cloud.ibm.com
   ```
   {: pre}

   Select the account and region where the {{site.data.keyword.mon_full_notm}} instance is available.

2. [Access your Ubuntu server](/docs/vpc?topic=vpc-vsi_is_connecting_linux).

3. Obtain the  access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

4. Obtain the ingestion URL. For more information, see [ collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

5. Deploy the monitoring agent. Run the following command:

   ```
   curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key <ACCESS_KEY> --collector <COLLECTOR_ENDPOINT> --collector_port 6443 --secure false --check_certificate false --tags <TAG_DATA> --additional_conf 'sysdig_capture_enabled: false'
   ```
   {: pre}

   Where

   * ACCESS_KEY is the [access key](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key) for the instance.

   * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.  To determine the endpoint, see [Collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

   * TAG_DATA are comma-separated tags that are formatted as `TAG_NAME:TAG_VALUE`. You can associate one or more tags to your monitoring agent. For example, `role:serviceX,location:us-south`. Later on, you can use these tags to identify metrics from the environment where the agent is running.

   * The `sysdig_capture_enabled` is set to *false* to disable the  capture feature. By default this is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).

   If the monitoring agent fails to install correctly, install the kernel headers manually. Choose a distribution and run the command for that distribution. Then, retry the deployment of the monitoring agent.

   * **For Debian and Ubuntu Linux distributions**, run the following command:

      ```
      apt-get -y install linux-headers-$(uname -r)
      ```
      {: pre}

   * **For RHEL, CentOS, and Fedora Linux distributions**, run the following command:

      ```
      yum -y install kernel-devel-$(uname -r)
      ```
      {: pre}


## Step 4. Launch the monitoring UI
{: #ubuntu_step4}

Complete the following steps to launch the web UI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

   After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. 

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select your instance. Then, click **View Sysdig**.

If the monitoring agent is configured successfully, the **Overview** view opens.

However, if the monitoring agent is not installed successfully, points to the wrong ingestion endpoint, or the access key is incorrect, the page that opens informs you about what to do next.

You only can have one web UI session open per instance per browser.
{: tip}

## Step 5. Monitor your Ubuntu server
{: #ubuntu_step5}

You can monitor your Ubuntu server in the **Overview** view that is available through the Web UI. This view is your starting point to troubleshoot and monitor your infrastructure. It is the default homepage of the Web UI.

In the section **Hosts & containers**, you can find the entry for your Ubuntu server. Click **Hosts & containers** ![Hosts & containers](../images/switch_hosts.png) to switch data sources. Then, select your Ubuntu server. The data that is displayed corresponds to the selected server.

To configure color-coding for a column, complete the following steps:

1. Select a column by hovering your mouse over the column title. Then, click the pencil icon.

2. Toggle **Enable** to enable color-coding.

3. Set values for the different thresholds.

## Next steps
{: #ubuntu_next_steps}

* Create a custom dashboard. For more information, see [Working with dashboards](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-dashboards#dashboards).

* Learn about alerts. For more information, see [Working with alerts](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-monitoring#monitoring_alerts). 

