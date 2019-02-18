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

# Navigating to the Web UI
{: #launch}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.Bluemix}}, and configure a Sysdig agent for a metrics source, you can view, monitor, and manage metrics through the {{site.data.keyword.mon_full_notm}} web UI.
{:shortdesc}


## Grant IAM policies to a user to view data 
{: #launch_step1}

**Note:** You must be an administrator of the {{site.data.keyword.mon_full_notm}} service, an administrator of the {{site.data.keyword.mon_full_notm}} instance, or have account IAM permissions to grant other users policies.

The following table lists the minimum policies that a user must have to be able to launch the {{site.data.keyword.mon_full_notm}} web UI, and view data:

| Service                        | Role                      | Permission granted     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | Platform role: Viewer     | Allows the user to view the list of service instances in the Observability Monitoring dashboard. |
| `{{site.data.keyword.mon_full_notm}}` | Service role: Writer      | Allows the user to launch the Web UI and view metrics in the Web UI.  |
{: caption="Table 1. IAM policies" caption-side="top"} 

For more information on how to configure these policies for a user, see [Granting permissions to a user to view metrics](/docs/services/Monitoring-with-Sysdig/iam_work.html#user_sysdig).


## Launch the web UI through the {{site.data.keyword.Bluemix_notm}} UI
{: #launch_step2}

You launch the Web UI within the context of an {{site.data.keyword.mon_full_notm}} instance, from the {{site.data.keyword.Bluemix_notm}} UI. 

Complete the following steps to launch the web UI:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.

    The {{site.data.keyword.Bluemix_notm}} dashboard can be found at: [http://cloud.ibm.com  ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://cloud.ibm.com ){:new_window}.

	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**. 

3. Select **Monitoring**. 

    The list of instances that are available on {{site.data.keyword.Bluemix_notm}} is displayed.

4. Select one instance. Then, click **View Sysdig**.

The Web UI opens.


