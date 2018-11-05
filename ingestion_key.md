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

# Working with the ingestion key
{: #ingestion_key}

The ingestion key is a token that you must use to configure Sysdig agents to successfully forward data to your IBM Cloud Monitoring with Sysdig instance in {{site.data.keyword.Bluemix}}. To obtain the ingestion key, you must create a service ID for the Sysdig instance. 
{:shortdesc}


## Getting the ingestion key through the {{site.data.keyword.Bluemix_notm}} UI
{: #ibm_cloud_ui}

To get the ingestion key for an IBM Cloud Monitoring with Sysdig instance through the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. The IBM Cloud Monitoring with Sysdig dashboard opens. You can see the list of monitoirng instances that are available on {{site.data.keyword.Bluemix_notm}}.

3. Identify the instance for which you want to get the ingestion key, and click **View ingestion key**.

4. A pop up window opens where you can click **Show** to view the ingestion key.



## Getting the ingestion key through the CLI
{: #cli}

To get the ingestion key for a Sysdig instance through the command line, complete the following steps:

1. [Pre-requisite] Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview).

   If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.Bluemix_notm}} where the Sysdig instance is running. Run the following command: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Set the resource group where the Sysdig instance is running. Run the following command: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    By default, the `default` resource group is set.

4. Get the instance name. Run the following command: [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Get the name of the API key that is associated with the Sysdig instance. Run the [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) command:

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    where INSTANCE_NAME is the name of teh instance that you obtained in the previous step.

6. Get the ingestion key. Run the [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) command:

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    where APIKEY_NAME is the name of the API key.
 
    The output from this command includes the field **ingestion_key** that contains the ingestion key for the instance.


## Changing the ingestion key
{: #change_key}

If the ingestion key is compromissed, you can open a support ticket to reset the password.



## Reset the ingestion key 
{: #reset}

If the ingestion key is compromissed or you have a policy to renew it after a number of days, you can generate a new key and delete the old one.

To renew the ingestion key for an IBM Cloud Monitoring with Sysdig instance, complete the following steps:

1. Launch the IBM Log Analysis with LogDNA web UI. For more information, see [Launching the IBM Log Analysis with LogDNA Web UI](/docs/services/Log-Analysis-with-LogDNA/view_logs.html#step2).

2. Select the **Configuration** icon. Then select **Organization**. 

3. Select **API keys**.

    You can see the ingestion keys that have been created. 

4. Select **Generate Ingestion Key**.

    A new key is added to the list.

5. Delete the old ingestion key. Click **delete**.

**Note:** After you reset the ingestion key, you must update the ingestion key for any log sources that you have configured to forward logs to this IBM Log Analysis with LogDNA instance.
