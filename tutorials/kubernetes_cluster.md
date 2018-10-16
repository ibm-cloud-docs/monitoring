---

copyright:
  years: 2018
lastupdated: "2018-08-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Analyze logs in Kibana for an app that is deployed in a Kubernetes cluster
{: #kubernetes_cluster}
Use this tutoral to learn how to configure a cluster to forward logs to the {{site.data.keyword.loganalysisshort}} service in the {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Objectives
{: #objectives}

1. Configure logging configurations in a cluster. 
2. Search and analyze container logs for an app that is deployed in a Kubernetes cluster in the {{site.data.keyword.Bluemix_notm}}.

This tutorial walks through the steps that are required to get the following end to end scenario working in the {{site.data.keyword.Bluemix_notm}}: Provisioning a cluster, configuring the cluster to send logs to the {{site.data.keyword.loganalysisshort}} service in the {{site.data.keyword.Bluemix_notm}}, deploying an app in the cluster, and using Kibana to view and filter container logs for that cluster.


**Note:** To complete this tutorial, you must complete the prerequisites and the tutorials that are linked from the different steps.


## Prerequisites
{: #prereq}

1. Be a member or an owner of an {{site.data.keyword.Bluemix_notm}} account with permissions to create Kubernetes standard clusters, deploy apps into clusters, and query the logs in {{site.data.keyword.Bluemix_notm}} for advanced analysis in Kibana.

    Your user ID for the {{site.data.keyword.Bluemix_notm}} must have the following policies assigned:
    
    * An IAM policy for the {{site.data.keyword.containershort}} with *editor*, *operator* or *administrator* permissions.
    * A CF role for the space where the {{site.data.keyword.loganalysisshort}} service is provisioned with *developer* permissions.
    
    For more information, see [Assign an IAM policy to a user through the IBM Cloud UI](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account) and [Granting a user permissions to view space logs by using the IBM Cloud UI](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_space).

2. Have a terminal session from where you can manage the Kubernetes cluster and deploy apps from the command line. The examples in this tutorial are given for an Ubuntu Linux system.

3. Install the CLIs to work with the {{site.data.keyword.containershort}} and the {{site.data.keyword.loganalysisshort}} in your Ubuntu system.

    * Install the {{site.data.keyword.Bluemix_notm}} CLI. Install the {{site.data.keyword.containershort}} CLI to create and manage your Kubernetes clusters in {{site.data.keyword.containershort}}, and to deploy containerized apps to your cluster. For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview).
    
    * Install the {{site.data.keyword.loganalysisshort}} CLI. For more information, see [Configuring the Log Analysis CLI (IBM Cloud plugin)](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli_cloud.html#config_log_collection_cli).
    
4. Have access to a space named **dev** in your account in the US South region. 

    Logs available in the cluster will be configured to be forwarded to the space domain that is associated with this space. 
    
    In this space, you will provision the {{site.data.keyword.loganalysisshort}} service.
    
    You must have **developer** permissions in this space so that you can provision the {{site.data.keyword.loganalysisshort}} service.
    
    In the tutorial, the name of the organization used is **MyOrg**.

    
 

## Step 1: Provision a Kubernetes cluster
{: #step1}

Complete the following steps:

1. Create a standard Kubernetes cluster.

   For more information, see [Creating clusters](/docs/containers/cs_tutorials.html#cs_cluster_tutorial).

2. Set up the cluster context in a terminal. After the context is set, you can manage the Kubernetes cluster and deploy the application in the Kubernetes cluster.

    Log in to the region, organization, and space in the {{site.data.keyword.Bluemix_notm}} that is associated with the cluster that you created. For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

	Initialize the {{site.data.keyword.containershort}} service plug-in.

	```
	ibmcloud cs init
	```
	{: codeblock}

    Set your terminal context to your cluster.
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    The output of running this command provides the command that you must run in your terminal to set the path to your configuration file. For example:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Copy and paste the command to set the environment variable in your terminal, and then press **Enter**.



## Step 2: Configure your cluster to forward logs automatically to the {{site.data.keyword.loganalysisshort}} service
{: #step2}

When the app is deployed, logs are collected automatically by the {{site.data.keyword.containershort}}. However, logs are not automatically forwarded to the {{site.data.keyword.loganalysisshort}} service. You must create 1 or more logging configurations in your cluster that define:

* Where logs are to be forwarded. You can forward logs to the account domain or to a space domain.
* What logs are forwarded to the {{site.data.keyword.loganalysisshort}} service for analysis.


Before you define logging configurations, check your current logging configuration definitions in the cluster. Run the following command:

```
$ ibmcloud cs logging-config-get ClusterName
```
{: codeblock}

where *ClusterName* is the name of your cluster.

For example, the logging configurations that are defined for the cluster *mycluster* are the following: 

```
$ ibmcloud cs logging-config-get mycluster
Retrieving cluster mycluster logging configurations...
OK
Id                                     Source       Namespace   Host                                Port   Org            Space   Protocol   Paths   
13ded2c0-83f5-4cc5-8de7-1e34e1287f34   worker       -           ingest.logging.ng.bluemix.net       9091   Demo_Org       dev     ibm        /var/log/syslog,/var/log/auth.log   
ae249c04-a3a9-4c29-a890-22d8da7bd1b2   container    *           ingest.logging.ng.bluemix.net       9091   Demo_Org.      dev     ibm        -   
31739fc1-42e2-4b66-ac57-6a32091c257a   ingress      -           ingest.logging.ng.bluemix.net       9091   Demo_Org.      dev     ibm        /var/log/alb/ids/*.log,/var/log/alb/ids/*.err,/var/log/alb/customerlogs/*.log,/var/log/alb/customerlogs/*.err   
6b8cfe89-4959-448d-898b-c3b0584eca71   kubernetes   -           ingest-eu-fra.logging.bluemix.net   9091   Demo_Org.      dev     ibm        /var/log/kubelet.log,/var/log/kube-proxy.log   

```
{: screen}

To see the list of log sources for which you can define a logging configuration, see [Log sources](/docs/services/CloudLogAnalysis/containers/containers_kubernetes.html#log_sources).


### Configure your cluster to forward stderr and stdout logs to the {{site.data.keyword.loganalysisshort}} service
{: #containerstd}


Complete the following steps to send stdout and stderr logs to a space domain, where the organization name is *MyOrg* and the space name is *dev* in the US South region:

1. Check that your user ID has permissions to add a cluster configuration. Only users with an IAM policy for the {{site.data.keyword.containershort}} with permissions to manage clusters can enable this feature. Any of the following roles is required: *Administrator*, *Operator*

    To check that your user ID has an IAM policy assigned to manage clusters, complete the following steps:
    
    1. Log in to the {{site.data.keyword.Bluemix_notm}} console. Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window} After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

    2. From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
    3. Select the userID, and verify that the user ID has a policy for the {{site.data.keyword.containershort}}.

    If you need permissions, contact the account owner or an account administrator. Only the account owner or users with permissions to assign policies can perform this step.

2. Create a cluster logging configuration. Run the following command to send *stdout* and *stderr* log files to the {{site.data.keyword.loganalysisshort}} service:

    ```
    ibmcloud cs logging-config-create ClusterName --logsource container --namespace '*' --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
    ```
    {: codeblock}

    where 

    * *ClusterName* is the name of the cluster.
    * *EndPoint* is the URL to the logging service in the region where the {{site.data.keyword.loganalysisshort}} service is provisioned. For a list of endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls).
    * *OrgName* is the name of the organization where the space is available.
    * *SpaceName* is the name of the space where the {{site.data.keyword.loganalysisshort}} service is provisioned.


For example, to create a logging configuration that forwards stdout and stderr logs to the space dev in the US South region, run the following command:

```
ibmcloud cs logging-config-create mycluster --logsource container --type ibm --namespace '*' --type ibm --hostname ingest.logging.ng.bluemix.net --port 9091 --org MyOrg --space dev 
```
{: screen}




### Configure your cluster to forward worker logs to the {{site.data.keyword.loganalysisshort}} service
{: #workerlogs }

Complete the following steps to send worker logs to a space domain, where the organization name is *MyOrg* and the space name is *dev* in the US South region:

1. Check that your user ID has permissions to add a cluster configuration. Only users with an IAM policy for the {{site.data.keyword.containershort}} with permissions to manage clusters can enable this feature. Any of the following roles is required: *Administrator*, *Operator*

    To check that your user ID has an IAM policy assigned to manage clusters, complete the following steps:
    
    1. Log in to the {{site.data.keyword.Bluemix_notm}} console. Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window} After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

    2. From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
    3. Select the userID, and verify that the user ID has a policy for the {{site.data.keyword.containershort}}.

    If you need permissions, contact the account owner or an account administrator. Only the account owner or users with permissions to assign policies can perform this step.

2. Create a cluster logging configuration. Run the following command to send */var/log/syslog* and */var/log/auth.log* log files to the {{site.data.keyword.loganalysisshort}} service:

    ```
    ibmcloud cs logging-config-create ClusterName --logsource worker --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
    ```
    {: codeblock}

    where 

    * *ClusterName* is the name of the cluster.
    * *EndPoint* is the URL to the logging service in the region where the {{site.data.keyword.loganalysisshort}} service is provisioned. For a list of endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls).
    * *OrgName* is the name of the organization where the space is available.
    * *SpaceName* is the name of the space where the {{site.data.keyword.loganalysisshort}} service is provisioned.

    
For example, to create a logging configuration that forwards worker logs to the space domain in the US South region, run the following command:

```
ibmcloud cs logging-config-create mycluster --logsource worker  --type ibm --hostname ingest.logging.ng.bluemix.net --port 9091 --org MyOrg --space dev 
```
{: screen}



## Step 3: Grant your user permissions to see logs in a space domain
{: #step3}

To grant a user permissions to view logs in a space, you must assign that user a Cloud Foundry role that describes the actions that this user can do with the {{site.data.keyword.loganalysisshort}} service in the space. 

Complete the following steps to grant a user permissions to work with the {{site.data.keyword.loganalysisshort}} service:

1. Log in to the {{site.data.keyword.Bluemix_notm}} console.

    Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage > Account > Users**. 

    The *Users* window displays a list of users with their email addresses for the currently selected account.
	
3. If the user is a member of the account, select the user name from the list, or click **Manage user** from the *Actions* menu.

    If the user is not a member of the account, see [Inviting users](/docs/iam/iamuserinv.html#iamuserinv).

4. Select **Cloud Foundry access**, then select the organization.

    The list of spaces available in that organization are listed.

5. Choose the space. Then, from the menu action, select **Edit space role**.

    If you cannot see the space for US South, create the space before you proceed.

6. Select *developer*.

    You can select 1 or more roles. 
    
    Valid roles are: *Manager*, *Developer*, and *Auditor*
	
7. Click **Save role**.


## Step 4: Grant the {{site.data.keyword.containershort_notm}} key owner permissions
{: #step4}

For cluster logs to be forwarded to a space, the {{site.data.keyword.containershort_notm}} key owner must have the following permissions:

* IAM policy for the {{site.data.keyword.loganalysisshort}} service with *Administrator* permissions.
* Cloud Foundry (CF) permissions in the organization and space where logs are to be forwarded. The container key owner needs *orgManager* role for the organization, and *SpaceManager* and *Developer* for the space.

Complete the following steps:

1. Identify the user in the account that is the {{site.data.keyword.containershort}} key owner. From a terminal, run the following command:

    ```
    ibmcloud cs api-key-info ClusterName
    ```
    {: codeblock}
    
    where *ClusterName* is the name of the cluster.

2. Verify that the user that is identified as the {{site.data.keyword.containershort}} key owner has the *orgManager* role for the organization, and *SpaceManager* and *Developer* for the space.

    Log in to the {{site.data.keyword.Bluemix_notm}} console. Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window} After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

    From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
    Select the ID of the user, and verify that the user has the *orgManager* role for the organization, and *SpaceManager* and *Developer* for the space.

    If the user does not have the correct permissions, grant the user the following permissions: *orgManager* role for the organization, and *SpaceManager* and *Developer* for the space. For more information, see [Granting a user permissions to view space logs by using the IBM Cloud UI](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_space).
    
3. Verify that the user that is identified as the {{site.data.keyword.containershort}} key owner has an IAM policy for the {{site.data.keyword.loganalysisshort}} service with *Administrator* permissions.

    From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
    Select the ID of the user, and verify that the user has the IAM policy set. 

    If the user does not have tge IAM policy, see [Assign an IAM policy to a user through the IBM Cloud UI](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).

4. Refresh the logging configuration. Run the following command:
    
    ```
    ibmcloud cs logging-config-refresh ClusterName
    ```
    {: codeblock}
        
    where *ClusterName* is the name of the cluster.
	



## Step 5: Deploy a sample app in the Kubernetes cluster to generate content in stdout
{: #step5}

Deploy and run a sample app in the Kubernetes cluster. Complete the steps in the following tutorial to deploy the sample app: [Lesson 1: Deploying single instance apps to Kubernetes clusters](/docs/containers/cs_tutorials_apps.html#cs_apps_tutorial_lesson1).

The app is a Hello World Node.js app:

```
var express = require('express')
var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

In this sample app, when you test your app in a browser, the app writes to stdout the following message: `Sample app is listening on port 8080.`






## Step 6: View log data in Kibana
{: #step6}

Complete the following steps:

1. Launch Kibana in a browser. 

    For more information on how to launch Kibana, see [Navigating to Kibana from a web browser](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).

    To analyze log data for a cluster, you must access Kibana in the cloud Public region where the cluster is created. 
    
    For example, in the US South region, enter the following URL to launch Kibana:
	
	```
	https://logging.ng.bluemix.net/ 
	```
	{: codeblock}
	
    Kibana opens.
    
    **NOTE:** Verify that you launch Kibana in the region where you are forwarding your cluster logs. For information on the URLs per region, see [Logging endpoints](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#urls_kibana).
    	
2. To view log data that is available in the space domain, complete the following steps:

    1. In Kibana, click your user ID. The view to set the space opens.
    
    2. Select the account where the space is available. 
    
    3. Select the following domain: **space**
    
    4. Select the organization *MyOrg* where the space is available.
    
    5. Select the space *dev*.
    
    
3. In the **Discover** page, look at the events that are displayed. 
        
    In the *Available fields* section, you can see the list of fields that you can use to define new queries or filter the entries listed in the table that is displayed on the page.
    
    The following table lists some of the fields that you can use to define new search queries when analyzing application logs. The table also includes sample values that correspond to the event that is generated by the sample app:
 
    <table>
              <caption>Table 2. Common fields for container logs </caption>
               <tr>
                <th align="center">Field</th>
                <th align="center">Description</th>
                <th align="center">Example</th>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>The value of this field corresponds to the {{site.data.keyword.Bluemix_notm}} region where the log entry is collected.</td>
                <td>us-south</td>
              </tr>
			  <tr>
                <td>*ibm-containers.account_id_str*</td>
                <td>Account ID</td>
                <td></td>
              </tr>
			  <tr>
                <td>*ibm-containers.cluster_id_str*</td>
                <td>Cluster ID.</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.cluster_name_str*</td>
                <td>Cluster ID</td>
                <td></td>
              </tr>
			  <tr>
                <td>*kubernetes.namespace_name_str*</td>
                <td>Namespace name</td>
                <td>*default* is the default value.</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>Container name</td>
                <td>hello-world-deployment</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>Label fields are optional. You can have 0 or more labels. Each label starts with the prefix `kubernetes.labels.` followed by the *label_name*. </td>
                <td>In the sample app, you can see 2 labels: <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*stream_str*</td>
                <td>Type of log.</td>
                <td>*stdout*, *stderr*</td>
              </tr>
        </table>
     
For more information about other search fields that are relevant to Kubernetes clusters, see [Searching logs](/docs/services/CloudLogAnalysis/containers/containers_kubernetes.html#log_search).


## Step 7: Filter data by Kubernetes cluster name in Kibana
{: #step7}
    
In the table that is displayed in the *Discovery* page, you can see all the entries that are available for analysis. The entries that are listed correspond to the search query that is displayed in the *Search* bar. Use an asterisk (*) to display all entries within the period of time that is configured for the page.
    
For example, to filter the data by Kubernetes cluster name, modify the *Search* bar query. Add a filter based on the custom field *kubernetes.cluster_name_str*:
    
1. In the **Available fields** section, select the field *kubernetes.cluster_name_str*. A subset of available values for the field is displayed.    
    
2. Select the value that corresponds to the cluster for which you want to analyze logs. 
    
    After you select the value, a filter is added to the *Search bar* and the table displays only entries that match the criteria you just selected.     
   

**Note:** 

If you cannot see your cluster name, add a filter for any cluster name. Then, select the filter's edit symbol.    
    
The following query displays:
    
```
	{
        "query": {
          "match": {
            "kubernetes.cluster_name_str": {
              "query": "cluster1",
              "type": "phrase"
            }
          }
        }
      }
```
{: screen}

Replace the name of the cluster (*cluster1*) with the name of the cluster *mycluster* for which you want to view log data.
        
If you cannot see any data, try changing the time filter. For more information, see [Setting a time filter](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).

For more information, see [Filtering logs in Kibana](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).


## {{site.data.keyword.containershort_notm}} Reference material
{: reference}

CLI commands:

* [ibmcloud cs api-key-info](/docs/containers/cs_cli_reference.html#cs_api_key_info)
* [ibmcloud cs logging-config-create](/docs/containers/cs_cli_reference.html#cs_logging_create)
* [ibmcloud cs logging-config-get](/docs/containers/cs_cli_reference.html#cs_logging_get)
* [ibmcloud cs logging-config-update](/docs/containers/cs_cli_reference.html#cs_logging_update)
* [ibmcloud cs logging-config-rm](/docs/containers/cs_cli_reference.html#cs_logging_rm)
* [ibmcloud cs logging-config-refresh](/docs/containers/cs_cli_reference.html#cs_logging_refresh)

