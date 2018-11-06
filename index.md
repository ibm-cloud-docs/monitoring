---

copyright:
  years: 2018
lastupdated: "2018-09-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Getting started with Sysdig
{: #getting-started}

Use Sysdig Monitoring to get visibility into the performance and health of the {{site.data.keyword.Bluemix}}. 
{:shortdesc}

IBM Cloud account owner grants IAM policy with platform admin role to a user. This user becomes and administrator of Sysdig in that region. He can provision Sysdig instances and can create a serviceID to obtain the ingestion key..
When the Sysdig instance is configured, the IBMid of this  user  gets the Sysdig admin priviledges automatically in Sysdig.
He can grant other user admin permissions on teh service, he can add other users to be able to see data in Sysdig WebUI.



## Before you begin
{: #prereqs}

You must have a user ID that is a member or an owner of an {{site.data.keyword.Bluemix_notm}} account. To get an {{site.data.keyword.Bluemix_notm}} user ID, go to: [Registration ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/registration/){:new_window}.

Read about Sysdig Monitor. For more information, see [Sysdig Monitor Documentation ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/overview){:new_window}.

Work in the US-South region.

## Step1: Provision an instance of the Sysdig Monitoring service
{: #step1}

To provision an instance of Sysdig through the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.Bluemix_notm}} opens.

3. To filter the list of services that is displayed, select the **Developer Tools** category.

4. Click the **Sysdig Monitoring** tile.

5. Select a service plan. By default, the **Lite** plan is set.

    For more information about the service plans, see [Service plans](/docs/services/.....).

6. Select a resource group. By default, the **default** one is set.

7. Click **Create** to provision an instance.

The service UI opens.

**Note:** To provision an instance of Sysdig through the CLI, see [Provisioning Sysdig through the {{site.data.keyword.Bluemix_notm}} CLI]().
## Step2: Obtain the ingestion key to access Sysdig
{: #step2}

To obtain the ingestion key, you must create a service ID. Complete the following steps rto create a service ID for your Sysdig instance:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg).

3. Identify the Sysdig instance, and click on it to open its UI.

4. Select **Service credentials** and click **New credential**.

5. Enter a name in the **Name** field, and select the **Manager** role. Then, click **Add**.

A key name entry is added.


## Step3: Configure your Kubernetes cluster to send logs to your Sysdig instance
{: #step3}

To configure your Kubernetes cluster to send metrics to your Sysdig instance, you must install a `sysdig-agent` pod on each node of your cluster. The Sysdig agent reads log files from the pod where it is installed, and forwards the log data to your Sysdig instance.

To configure your Kubernetes cluster to forward logs to your Sysdig instance, complete the following steps:

1. Add a secret to your Kubernetes cluster. The secret corresponds to the Sysdig ingestion key.

    Run the following command:

    ```
    kubectl create secret generic Sysdig-agent-key --from-literal=Sysdig-agent-key=YOUR_Sysdig_INGESTION_KEY
    ```
    {: pre}

2. Create the Sysdig agent DeamonSet in your Kubernetes cluster.

    Run the following command:

    ```
    kubectl create -f https://raw.githubusercontent.com/Sysdig/Sysdig-agent/master/Sysdig-agent-ds.yaml
    ```
    {: pre}



## Step 4: Launch the Sysdig Web UI
{: #step4}

You launch the Sysdig web UI within the context of the Sysdig instance, from the {{site.data.keyword.Bluemix_notm}} UI. 

Complete the following steps to launch the Sysdig web UI:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} Dashboard opens.

2. In the **Services** section, select the Sysdig instance.

3. In the **Manage** tab, click **Launch**.

The Sysdig Web UI opens. 


## Next steps
{: #next_steps}

Learn how to [monitor your infrastructure. [External link icon](../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/215744574/Explore){:new_window}!