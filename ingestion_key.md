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

## Creating a service ID through the {{site.data.keyword.Bluemix_notm}} UI
{: #create_serviceid}

To create a service ID, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg).

3. Identify the Sysdig instance, and click on it to open its UI.

4. Select **Service credentials** and click **New credential**.

5. Enter a name in the **Name** field, and select the **Manager** role. Then, click **Add**.

A key name entry is added.


## Getting the ingestion key through the {{site.data.keyword.Bluemix_notm}} UI
{: #ui}

To get the ingestion key for a Sysdig instance by using the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg).

3. Identify the Sysdig instance for which you want to get the ingestion key, and click on it to open its UI.

4. Select **Service credentials**.

5. Select a key name. Then, click **View credentials** to see the ingestion key. The value of the parameter **Sysdig Access Key** contains the ingestion key.



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
 
    The output from this command includes the field **Sysdig Access Key** that contains the ingestion key for the Sysdig instance.


## Changing the ingestion key
{: #change_key}

If the ingestion key is compromissed, you can open a support ticket to reset the password.

After you reset the value, you must create a new serviceID for the Sysdig instance in the {{site.data.keyword.Bluemix_notm}}, and update your Sysdig sources with the new ingestion key.

*****Check with Sysdig link to their docs where they document the process to reset the ingestion key.********

Anything else that we should add?????

