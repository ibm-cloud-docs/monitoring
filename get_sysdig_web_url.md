---

copyright:
  years:  2018, 2020
lastupdated: "2020-10-14"

keywords: Sysdig, IBM Cloud, monitoring, web UI

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

# Getting the Sysdig web UI URL
{: #get_sysdig_web_url}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you can monitor metrics through the {{site.data.keyword.mon_full_notm}} web UI. You can launch the Sysdig web UI from the {{site.data.keyword.cloud_notm}} UI.
{:shortdesc}

To get the Sysdig web UI URL, complete the following steps from a terminal:

1. [Pre-requisite] Installation of the {{site.data.keyword.cloud_notm}} CLI. [Learn more](/docs/cli?topic=cli-getting-started).

2. Log in to the location in the {{site.data.keyword.cloud_notm}} where the instance is provisioned. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where the instance is available. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Get the dashboard URL. Run the following command:

    ```
    ic resource service-instance INSTANCE_NAME --output JSON | grep dashboard_url
    ```
    {: codeblock}
    
Where *INSTANCE_NAME* is the name of the instance.

To get the name of the instances that are available in a resource group, you can run `ibmcloud resource service-instances`.
{: tip}

