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


# Getting started with IBM Cloud Monitoring with Sysdig
{: #getting-started}

IBM Cloud Monitoring with Sysdig is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.Bluemix}} architecture. Use it to get visibility into the performance and health of your applications, services, and platform. IBM Cloud Monitoring with Sysdig is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}

The following figure shows the components overview for the IBM Cloud Monitoring with Sysdig service that is running on {{site.data.keyword.Bluemix_notm}}:

![IBM Cloud Monitoring with Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}](images/components.png "IBM Cloud Monitoring with Sysdig component overview on the {{site.data.keyword.Bluemix_notm}}")

IBM Cloud Monitoring with Sysdig offers administrators, DevOps teams, and developers advanced monitoring features to monitor and troubleshoot, including alerting and customizable dashboards. 

### Features
{: #features}

**Accelerate the diagnosis and resolution of performance incidents.**

By using IBM Cloud Monitoring with Sysdig, Developers and DevOps teams monitor and troubleshoot performance issues in real-time, identify the source of errors, and eliminate problems. IBM Cloud Monitoring with Sysdig offers deep visibility into your system, applications and services, service-oriented views for each one, and pre-defined metrics that you can use to determine potential threats or problems.

**Get critical insight from dynamic service–level monitoring and automatic correlation of data.**
 
IBM Cloud Monitoring with Sysdig collects metrics from multiple sources into a centralize location. Per source (host), you can deploy an agent that dynamically discovers the different resources in your environment and collects their pre-defined and custom metrics. Customize dashboards to visualize your environment.

**Mitigate the impact of abnormal situations with proactive notifications.**

Define alerts to reduce the impact on your day to day operations and accelerate your reaction and response time to anomalies, downtime, and performance degradation. 

**Control costs by customizing what cloud sources to manage through IBM Cloud Monitoring with Sysdig.**

Control the cost of your monitoring infrastructure in the {{site.data.keyword.Bluemix_notm}} by configuring the metric sources for which you want to monitor their performance. 


## Before you begin
{: #prereqs}

You must have a user ID that is a member or an owner of an {{site.data.keyword.Bluemix_notm}} account. To get an {{site.data.keyword.Bluemix_notm}} user ID, go to: [Registration ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/registration/){:new_window}.

The service is currently available in US South. Complete any getting started steps in the US-South region.

## Step1: Provision an instance of the IBM Cloud Monitoring with Sysdig service
{: #step1}

To add monitoring features with IBM Cloud Monitoring with Sysdig in the {{site.data.keyword.Bluemix_notm}}, you must provision an instance of the IBM Cloud Monitoring with Sysdig service.

Before you provision an instance, consider the following information:

* Your data is sent to a third party.
* The account owner can create, view, and delete an instance of a service in the {{site.data.keyword.Bluemix_notm}}, and can grant permissions to other users to work with the IBM Cloud Monitoring with Sysdig service.
* Other {{site.data.keyword.Bluemix_notm}} users with `administrator` or `editor` permissions can manage the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix_notm}}. These users must also have platform permissions to create resources within the context of the resource group where they plan to provision the instance.

You provision an instance within the context of a resource group. A resource group lets you organize your services for access control and billing purposes. You can provision the IBM Cloud Monitoring with Sysdig instance in the *default* resource group or in a custom resource group.

When you provision an instance, you automatically get an ingestion key, known as the *Sysdig access key*.

To provision an instance of through the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.Bluemix_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **IBM Cloud Monitoring with Sysdig** tile.

5. Select a service plan. By default, the **Lite** plan is set.

    For more information about the service plans, see [Service plans](/docs/services/Monitoring-with-Sysdig/pricing.html#pricing_plans).

6. Select a resource group. By default, the **default** one is set.

7. Click **Create** to provision an instance.

The service UI opens.

**Note:** To provision an instance of Sysdig through the CLI, see [Provisioning Sysdig through the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/Monitoring-with-Sysdig/provision.html#provision_cli).


## Step2: Configure a Sysdig agent
{: #step2}

After you provision an instance, you must configure a Sysdig agent for each metric source that you want to monitor. A metric source is a cloud resource that you want to monitor and control its performance and health. For example, a metric source can be a Kubernetes cluster.  

The Sysdig agent automatically collects and reports on pre-defined metrics. You use the *Sysdig access key* to configure the Sysdig agent that is responsible for collecting and forwarding metric data to your instance. For more information, see [Working with access keys](/docs/services/Monitoring-with-Sysdig/access_key.html#access_key).

You can configure a Sysdig agent for any of the following environments:

* Kubernetes, GKE, and OpenShift.
* Docker containers or for non-containerized services.
* Mesos, Marathon, and DCOS.
* Linux installations.

For example, to configure your Kubernetes cluster to send metrics to your Sysdig instance, you must install a `sysdig-agent` pod on each node of your cluster. The Sysdig agent reads log files from the pod where it is installed, and forwards the log data to your Sysdig instance.

Complete one of the following tutorials to learn how to deploy a Sysdig agent:

| Resource                |	Tutorial                        | Environment                | Scenario   |
|-------------------------|---------------------------------|----------------------------|------------|
| Containers running on the {{site.data.keyword.containershort}} |[Analyze metrics for an app that is deployed in a Kubernetes cluster](docs/services/Monitoring-with-Sysdig/tutorials/kubernetes_cluster.html#kubernetes_cluster) | {{site.data.keyword.Bluemix_notm}} Public | ![{{site.data.keyword.containershort}} and IBM Cloud Monitoring with Sysdig](images/kube.png "{{site.data.keyword.containershort}} and IBM Cloud Monitoring with Sysdig") |
|Linux Ubuntu/Debian | [Analyze metrics for an Ubuntu server]() | On-premises | ![Ubuntu and IBM Cloud Monitoring with Sysdig](images/kube.png "Ubuntu and IBM Cloud Monitoring with Sysdig") |
{: caption="Table 1. Tutorials to get started working with IBM Cloud Monitoring with Sysdig" caption-side="top"} 

For more information, see [Configuring a Sysdig agent](/docs/services/Monitoring-with-Sysdig/config_agent.html#config_agent) and [Removing a Sysdig agent](/docs/services/Monitoring-with-Sysdig/remove_agent.html#remove_agent).

After the Sysdig agent is deployed, collection and forwarding of metrics to the instance is automatic. The Sysdig agent automatically collects and reports on pre-defined metrics. You can also configure which metrics to monitor in an environment.

## Step 3: Launch the web UI
{: #step3}

You launch the web UI within the context of the Sysdig instance, from the {{site.data.keyword.Bluemix_notm}} UI. 

Complete the following steps to launch the Sysdig web UI:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. 

    The list of monitoring instances that are available on {{site.data.keyword.Bluemix_notm}} is displayed.

4. Select one instance. Then, click **View Sysdig**.

The IBM Cloud Monitoring with Sysdig Web UI opens. By default, the *Explore* tab is displayed.


## Step 4: Monitor your environment
{: #step4}

In the *Explore* tab, you can monitor data by using default metrics and default dashboards. You can use labels to define new infrastructure groups that you can then use to aggregate data differently and monitor your environment. You can also use custom dashboards that you define through the *Dashboard* tab. In the *Dashboards* tab, you can monitor data by using any of the default dashboards or by creating new ones. 

For more information, see [Monitoring your environment](/docs/services/Monitoring-with-Sysdig/monitoring.html#monitoring)

## Step 5: Manage data
{: #step5}

You can use labels to group infrastructure resources into logical hierarchies, filter out data, and split aggregated data into segments. You can customize how data is aggregated when you configure a graph or create an alert for a metric. You can set the scope of a dashboard, a panel, or an alert to filter out data points. 

For more information, see [Managing data](/docs/services/Monitoring-with-Sysdig/manage.html#manage).

## Step 6: Manage user access
{: #step6}

Every user that accesses the IBM Cloud Monitoring with Sysdig service in your account must be assigned an access policy with an IAM user role defined. The policy determines what actions the user can perform within the context of the service or instance you select. The allowable actions are customized and defined as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. For more information, see [Managing user access in the {{site.data.keyword.Bluemix_notm}}](/docs/services/Monitoring-with-Sysdig/iam.html#iam).




