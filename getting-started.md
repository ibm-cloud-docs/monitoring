---

copyright:
  years:  2018, 2025
lastupdated: "2025-05-30"


keywords: monitoring

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with {{site.data.keyword.mon_full_notm}}
{: #getting-started}

{{site.data.keyword.mon_full}} is a cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
{: shortdesc}


## Before you begin
{: #getting-started-prereqs}

You must have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://cloud.ibm.com/login){: external}.

Check the regions where the service is available. [Learn more](/docs/monitoring?topic=monitoring-regions).

Read the *About* section:
- [{{site.data.keyword.mon_short}} topic](/docs/monitoring?topic=monitoring-about-monitor) to understand more about the {{site.data.keyword.mon_short}} service.
- [Collecting metrics](/docs/monitoring?topic=monitoring-about-collect-metrics) to understand more about how to collect metrics.

You can complete the getting started steps in any of the supported regions.


## Step 1. Manage user access
{: #getting-started-step1}

Every user that accesses the {{site.data.keyword.mon_full_notm}} service in your account must be assigned an access policy with an IAM user role defined. The policy determines what actions the user can perform within the context of the service or instance you select. The allowable actions are customized and defined as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. For more information, see [Managing user access in the {{site.data.keyword.cloud_notm}}](/docs/monitoring?topic=monitoring-iam#iam).

When a user is granted permissions in the {{site.data.keyword.cloud_notm}} to work with the {{site.data.keyword.mon_full_notm}} service, the user is automatically granted a service role. This role determines the actions that a user has permissions to run. For more information, see [Controlling access through IAM](/docs/monitoring?topic=monitoring-iam).

Before you can provision an instance, understand the following:
* The account owner can create, view, and delete an instance of a service in the {{site.data.keyword.cloud_notm}}, and can grant permissions to other users to work with the {{site.data.keyword.mon_full_notm}} service.
* You must have permissions to create resources in the *Default* resource group.
* Other {{site.data.keyword.cloud_notm}} users with `administrator` or `editor` permissions can manage the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}. These users must also have platform permissions to create resources within the context of the resource group where they plan to provision the instance.

To grant a user the administrator role for the service and to manage instances within a resource group in the account, the user must have an IAM policy for the {{site.data.keyword.mon_full_notm}} service with the platform role **Administrator** within the context of the resource group. Do the following to assign a user this role:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access within a resource group**.
4. Select a resource group.
5. If the user does not have a role already granted for the selected resource group, choose a role for the **Assign access to a resource group** field.

   Depending on the role that you select, the user can view the resource group on their dashboard, edit the resource group name, or manage user access to the group.

   You can select **No access**, if you want the user to only have access to the {{site.data.keyword.mon_full_notm}} service in the resource group.

6. Select **{{site.data.keyword.mon_full_notm}}**.
7. Select the platform role **Administrator**.
8. Click **Assign**.

## Step 2. Provision an instance of the {{site.data.keyword.mon_short}} service
{: #getting-started-step2}

To add monitoring features with {{site.data.keyword.mon_full_notm}} in the {{site.data.keyword.cloud_notm}}, you must provision an instance of the {{site.data.keyword.mon_full_notm}} service.

Instances are provisioned in the context of a resource group. A resource group organizes your services for access control and billing purposes. You can provision the {{site.data.keyword.mon_full_notm}} instance in the *default* resource group or in a custom resource group.



{{_include-segments/provision_ui.md}}

To provision an instance through the CLI, see [Provisioning a Monitoring instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/monitoring?topic=monitoring-provision#provision_cli).
{: tip}

## Step 3. Collect metrics
{: #getting-started-step3}


Next, configure your hosts to send metrics.

You can collect metrics from a number of platforms, orchestrators, and a wide range of applications such as Prometheus, JMX, StatsD, Kubernetes, and other application stacks, that are available in the {{site.data.keyword.cloud}}, outside the {{site.data.keyword.cloud_notm}}, or on-prem. You can also add more metrics by creating custom metrics and adding integrations. Learn more:
- [Collecting default metrics by using the Monitoring agent](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-2)
- [Collecting custom metrics by using the Monitoring agent](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-3)
- [Collecting custom metrics by using Prometheus remote write](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-4)
- [Collecting custom metrics by using Prometheus exporters](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-5)
- [Collecting Platform metrics from IBM Cloud services](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-6)

### Configure platform metrics
{: #getting-started-step3-1}

Platform metrics are metrics that are exposed by enabled-monitoring services and the platform in {{site.data.keyword.cloud_notm}}. You must configure an {{site.data.keyword.mon_full_notm}} instance in a region to monitor these metrics. [Learn more](/docs/monitoring?topic=monitoring-platform_metrics_enabling).

To see the list of enabled-monitoring services, see [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).

For example, to configure platform metrics in a region, complete the following steps:
1. From the{{site.data.keyword.cloud_notm}} dashboard, go to the menu icon ![menu icon](../../icons/icon_hamburger.svg) &gt; **Observability** to access the *Observability* dashboard.

2. Select **Monitoring** &gt; **Options** &gt; **Edit platform**.

3. Select a [region](/docs/monitoring?topic=monitoring-regions).

4. Choose the {{site.data.keyword.mon_short}} instance that will collect metrics from the enabled services on that location.

5. Click **Save**.

The main *Observability* page opens.

The instance that you configured to receive metrics shows the flag **Platform metrics**.


### Configure a monitoring agent
{: #getting-started-step3-2}

After you provision an instance, you can configure a monitoring agent for each host, where agents are supported, that you want to monitor. For example, a host can be a cloud resource that you want to monitor and control its performance and health such as a Kubernetes cluster. You might also monitor hosts outside the {{site.data.keyword.cloud_notm}}.

The monitoring agent automatically collects and reports on pre-defined metrics. You use the *access key* to configure the monitoring agent that is responsible for collecting and forwarding metric data to your instance. For more information, see [Working with access keys](/docs/monitoring?topic=monitoring-access_key#access_key).

You can configure a monitoring agent for different environments. For example, to configure your Kubernetes cluster to send metrics to your {{site.data.keyword.mon_full_notm}} instance, you must install a `monitoring-agent` pod on each node of your cluster. The monitoring agent collects data from the pod where it is installed, and forwards it to your {{site.data.keyword.mon_full_notm}} instance.

Complete one of the following tutorials to learn how to deploy a monitoring agent:

|	Tutorial                        |
|---------------------------------|
| [Monitoring a Linux VPC server instance](/docs/monitoring?topic=monitoring-ubuntu#ubuntu) |
| [Monitoring a Linux bare metal server](/docs/monitoring?topic=monitoring-baremetal_linux) |
| [Monitoring a Windows environment](/docs/monitoring?topic=monitoring-windows) |
| [Monitoring a Kubernetes cluster](/docs/monitoring?topic=monitoring-kubernetes_cluster) |
| [Monitoring a {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/monitoring?topic=monitoring-openshift_cluster) |
| [Monitoring VMware vCenter server deployments](/docs/monitoring?topic=monitoring-vmware-vcenter) |
{: caption="Tutorials to get started working with {{site.data.keyword.mon_full_notm}}" caption-side="top"}

After the monitoring agent is deployed, the monitoring agent automatically collects and reports on pre-defined and custom metrics.  These metrics are forwarded to the {{site.data.keyword.mon_full_notm}} instance.  You can configure which metrics are monitored in an environment.

If you have connected an instance of {{site.data.keyword.sysdigsecure_full_notm}} to your {{site.data.keyword.mon_full_notm}} instance, the agent will provide data to both services without having to configure two separate agents. 
{: note}

## Step 4. Launch the web UI
{: #getting-started-step4}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, and configure a monitoring agent for your node, you can view, monitor, and manage data through the service's web UI.

You launch the web UI within the context of the {{site.data.keyword.mon_full_notm}} instance, from the {{site.data.keyword.cloud_notm}} UI.

Complete the following steps to launch the monitoring UI:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

   Open the [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/login){: external}.

   After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**.

3. Select **Monitoring**.

    The list of available {{site.data.keyword.mon_full_notm}} instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select one instance. Then, click **Open dashboard**.

The {{site.data.keyword.mon_full_notm}} Web UI opens. By default, the *Overview* tab is displayed.

By default, users are automatically added as members of the **Monitor Operations** team that is predefined for each {{site.data.keyword.mon_short}} instance. Users have full permissions to see all the data in the web UI.

An administrator can restrict access to data by managing users in teams and controlling what data is visible. For example, to restrict users viewing permissions, an administrator can create a default team with limited scope and visibility. Then, manually assign users to other teams. For more information, see [Working with teams](/docs/monitoring?topic=monitoring-teams#teams).
{: note}


## Step 5. Next steps
{: #getting-started-step5}

- To monitor the usage and costs of your service, see [Viewing your usage](/docs/account?topic=account-viewingusage&interface=ui#viewingusage).

- Check [Getting started with {{site.data.keyword.sysdigsecure_full}}](/docs/workload-protection?topic=workload-protection-getting-started) and see how you can use it to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions and compliance from source to run.
