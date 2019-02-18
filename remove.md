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

# Removing an instance
{: #remove}

You can remove an instance of the IBM Cloud Monitoring with Sysdig service from the {{site.data.keyword.Bluemix}} UI or through the command line.
{:shortdesc}

When you remove an instance from the {{site.data.keyword.Bluemix_notm}}, consider the following information to tidy up:

1. Write down the list of sources that forward metrics to the IBM Cloud Monitoring with Sysdig instance that you want to remove. You must remove the Sysdig agent from each source.
2. Remove permissions granted to users to work with the instance. 

    If you use an access group to manage access to the instance, you must remove the access group.

    If you use an access group to manage access to different service instances, you must remove the policies that grant permissions to the instance that you want to remove.
    
    If you have granted individual policies to users, you must gather the information of each user that has access, and remove one by one the policies that relate to the instance that you want to delete.


Then, delete the instance from the {{site.data.keyword.Bluemix_notm}} Dashboard.


## Removing an instance through the {{site.data.keyword.Bluemix_notm}} UI
{: #remove_ui}

To remove an instance of IBM Cloud Monitoring with Sysdig by using the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Select **Observability**. 

3. Select **Monitoring**. The list of the instances is displayed.

4. Select the instance that you want to delete.

5. From the *Action* menu, select **Remove**.


## Removing an instance through the CLI
{: #remove_cli}

To remove an instance of IBM Cloud Monitoring with Sysdig through the command line, complete the following steps:

1. [Pre-requisite] Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview).

   If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.Bluemix_notm}} where you want to provision the instance. Run the following command: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Set the resource group where the instance is provisioned. Run the following command: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    By default, the `default` resource group is set.

4. Remove the instance. Run the [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) command:

    ```
    ibmcloud resource service-instance-create NAME 
    ```
    {: codeblock}

    where NAME is the name of the instance

    For example, to remove an instance, run the following command:

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
