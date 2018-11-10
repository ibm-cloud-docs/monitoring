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


# Working with panels
{: #panels}

Use dashboards to monitor your infrastructure, applications, and services. You can use pre-defined dashboards. You can also create custom dashboards through the Web UI or programmatically. You can backup and restore dashboards by using Python scripts.
{:shortdesc}






## Changing the scope
{: #scope}

Instead of changing the scope of a pre-defined dashboard, copy the dashboard and change the scope in the copied dashboard.
{: tip}

Complete the following steps to change the scope of a dashboard:

1. Navigate to the *DASHBOARD** section in the Web UI. Select a dashboard. Then, identify the panel that display the metric for which you want to change the scope.

2. In the panel, click **Edit Scope** to change the default scope. 

    By default, **Everywhere** is selected.
    
3. Select the scope. 

4. Optionally, click **Override the custom panel scopes** to override the scope for all panels which currently have a custom scope defined. 

    **Note: This action cannot be undone.** 

    To reset the dashboard scope to the entire infrastructure, or to update an existing dashboard's scope to the entire infrastructure, select **Everywhere**.
    {: tip}

5. Click **Save**.