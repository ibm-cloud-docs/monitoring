---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Working with access keys
{: #access_key}

The **Access Key** is a token that you must use to configure Sysdig agents to successfully forward data to your IBM Cloud Monitoring with Sysdig instance in {{site.data.keyword.Bluemix}}.   
{:shortdesc}


## Getting the access key through the {{site.data.keyword.Bluemix_notm}} UI
{: #ibm_cloud_ui}

To get the access key for an IBM Cloud Monitoring with Sysdig instance through the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://cloud.ibm.com  ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://cloud.ibm.com ){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. The IBM Cloud Monitoring with Sysdig dashboard opens. You can see the list of monitoring instances that are available on {{site.data.keyword.Bluemix_notm}}.

3. Identify the instance for which you want to get the access key, and click **View access key**.

4. A pop up window opens where you can click **Show** to view the access key.



## Getting the access key through the CLI
{: #cli}

To get the access key for a Sysdig instance through the command line, complete the following steps:

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

6. Get the access key. Run the [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) command:

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    where APIKEY_NAME is the name of the API key.
 
    The output from this command includes the field **Sysdig Access Key** which contains the access key for the instance.


For example, the following command shows the output of a sample service ID:

```
$ ic resource service-key "IBM Cloud Monitoring with Sysdig-shg-key-admin"
Retrieving service key IBM Cloud Monitoring with Sysdig-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          IBM Cloud Monitoring with Sysdig-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## Resetting the access key 
{: #reset}

If the access key is compromised or you have a policy to renew it after a number of days, you can generate a new key and delete the old one.

To renew the access key for an IBM Cloud Monitoring with Sysdig instance, complete the following steps:

1. Launch the IBM Cloud Monitoring with Sysdig web UI. For more information, see [Navigating to the Web UI](/docs/services/Monitoring-with-Sysdig/launch.html#launch).

2. From the *Selector* button in the navigation bar, choose **Settings**.

2. In the *Password management* section, click **Reset your password**.

**Note:** After you reset the Sysdig access key, you must update the access key for any log sources that you have configured to forward metrics to this IBM Cloud Monitoring with Sysdig instance.
