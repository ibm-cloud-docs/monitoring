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

# Navigating to the Web UI
{: #launch}

After you provision an instance of the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix}}, and configure a Sysdig agent for a metrics source, you can view, monitor, and manage metrics through the IBM Cloud Monitoring with Sysdig Web UI.
{:shortdesc}


## Step 1: Grant IAM policies to a user to view data 
{: #step1}

**Note:** You must be an adminsitrator of the IBM Cloud Monitoring with Sysdig service, an administrator of the IBM Cloud Monitoring with Sysdig instance, or have account IAM permissions to grant other users policies.

The following table lists the minimum policies that a user must have to be able to launch the IBM Cloud Monitoring with Sysdig Web UI, and view data:

| Service                        | Role                      | Permission granted                                                                            |
|--------------------------------|---------------------------|-----------------------------------------------------------------------------------------------|
| `IBM Cloud Monitoring with Sysdig` | Platform role: Viewer     | Allows the user to view the list of service instances in the Observability Logging dashboard. |
| `IBM Cloud Monitoring with Sysdig` | Service role: Writer      | Allows the user to launch the Web UI and view logs in the Web UI.                             |
{: caption="Table 1. IAM policies" caption-side="top"} 

For more information on how to configure these policies for a user, see [Granting permissions to a user to view metrics](/docs/services/Monitoring-with-Sysdig/iam_work.html#user_sysdig).


## Step 2: Launch the Web UI through the {{site.data.keyword.Bluemix_notm}} UI
{: #step2}

You launch the Web UI within the context of an IBM Cloud Monitoring with Sysdig instance, from the {{site.data.keyword.Bluemix_notm}} UI. 

Complete the following steps to launch the web UI:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. 

    The list of instances that are available on {{site.data.keyword.Bluemix_notm}} is displayed.

4. Select one instance. Then, click **View Sysdig**.

The Web UI opens.
