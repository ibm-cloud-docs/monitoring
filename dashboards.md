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


# Working with dashboards
{: #dashboards}

Use dashboards to monitor your infrastructure, applications, and services. You can use pre-defined dashboards. You can also create custom dashboards through the Web UI or programmatically. You can backup and restore dashboards by using Python scripts.
{:shortdesc}

A **dashboard** shows groups of metrics that report on the health, performance, and state of your infrastructure, applications, and services for a single host or a group of hosts. Dashboards offer a specialized insight into network data, application data, topology, services, hosts, and containers.

In the **DASHBOARDS** section of the Web UI, dashboards are organized into three main groups:

* *My Dashboards*: These are the dashboards that are created by the user who is currently logged in.
* *My Shared Dashboards*: These are the dashboards that are created by the user who is currently logged in, and that are shared with other users.
* *Dashboards Shared With Me*: These are the dashboards that are created by other users, and shared with the current user.

In the **EXPLORE** section of the Web UI, dashboards are organized into two groups:
* *Default dashboards*: These are the pre-defined dashboards.
* *My Dashboards*: These are the dashboards that are created by the user who is currently logged in.

You can copy and share dashboards through the Web UI. 

You can run scripts to complete any of the following actions programmatically:
* Save existing dashboards to a local file.
* Create new dashboards that are identical to the dashboards that you save.
* Restore dashboards.


## Pre-defined dashboards
{: #predefined}

Pre-defined dashboards are designed around various supported applications, network topologies, infrastructure layouts, and services. 

Pre-defined dashboards include a series of panels that are already configured.

The following table lists the different types of pre-defined dashboards:

| Type | Description | More information | 
|------|-------------|------------------|
| Applications | Dashboards that you can use to monitor your applications and infrastructure components.  | [Application dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#applications) |
| Host and containers | Dashboards that you can use to monitor resource utilization and system activity on your hosts and in your containers. | [Host and container dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#host_container) |
| Network | Dashboards that you can use to monitor your network connections and activity. | [Network dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#network) |
| Service | Dashboards that you can use to monitor the performance of your services, even if those services are deployed in orchestrated containers. | [Service dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#service) |
| Topology | Dashboards that you can use to monitor the logical dependencies of your application tiers and overlay metrics. | [Topology dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#topology) |
{: caption="Table 1. List of pre-defined dashboards" caption-side="top"} 



## Creating custom dashboards through the Web UI
{: #custom_ui}

When you create a custom dashboard, you can start from a template such as a pre-defined dashboard, or choose a blank dashboard. A dashboard includes panels that are configured to display specific data in a number of different formats. You also set how data is aggregated. The **scope** defines what data is used for aggregation and displayed. You can set the scope at a dashboard level, or override for individual panels. 

Complete the following steps to create a custom dashboard:

1. Navigate to the *DASHBOARD** section in the Web UI, and select **Add Dashboard**. The *Create a New Dashboard* page opens.

    1. Select a pre-defined dashboard or choose the *Blank Dashboard*. 

    2. Enter a name for your dashboard.

    3. Click **Create Dashboard**.

2. Set the dashboard scope. Click **Edit Scope** to change the default scope. By default, **Everywhere** is selected.
    
    1. Select the scope. 

    2. Optionally, click **Override the custom panel scopes** to override the scope for all panels which currently have a custom scope defined. **Note: This action cannot be undone.** 

    **Note:** To reset the dashboard scope to the entire infrastructure, or to update an existing dashboard's scope to the entire infrastructure, select **Everywhere**.

    3. Click **Save**.

3. Configure panels. Repeat this step for any of the panels in the dashboard that you want to modify.

    1. Identify the panel that you want to modify.

    2. Select **Edit Panel**. This is the pencil icon.
    
    3. Change the a chart type.

    4. Change the metric, and rate. Rate defines the type of aggregation that is done to the data.

    5. Change the scope of the panel. Click **Override Dashboard Scope**. Then, change the scope. If you need to restore the dashboard scope to the panel, select **Default to Dashboard Scope**.

    6. In the *Compare to* field, click **Configure**. Set the time range for the comparison.

    7. Set the panel background color based on metric thresholds. Click **Override Color Coding**, then, **Enable**. Set values for the different thresholds.

    8. Click **Save**.


## Changing the scope of a dashboard
{: #scope}

Instead of changing the scope of a pre-defined dashboard, copy the dashboard and change the scope in the copied dashboard.
{: tip}

Complete the following steps to change the scope of a dashboard:

1. Navigate to the *DASHBOARD** section in the Web UI, and select a dashboard.

2. Click **Edit Scope** to change the default scope. 

    By default, **Everywhere** is selected.
    
3. Select the scope. 

4. Optionally, click **Override the custom panel scopes** to override the scope for all panels which currently have a custom scope defined. 

    **Note: This action cannot be undone.** 

    To reset the dashboard scope to the entire infrastructure, or to update an existing dashboard's scope to the entire infrastructure, select **Everywhere**.
    {: tip}

5. Click **Save**.



## Copying a dashboard
{: #copy}

When you copy a dashboard, you create a duplicate.

The following table outlines the different actions and user permissions that are required for users to copy a dashboard:

| Action                  |	Who can copy                              |	Dashboard instance	    | Who can view the dashboard              | Who can edit the dashboard  |
|-------------------------|-------------------------------------------|-------------------------|----------------------------------------|-----------------------------|
| Copy to current Team    |	Users in the team with editor permissions | New dashboard instance  | Team members with viewing permissions	 | Users in the team with editor permissions |
| Copy to another Team    | Users in the team with editor permissions in both teams | New dashboard instance  | If the original dashboard is not shared, only the user who copies the dashboard has access. </br>If the original dashboard is shared, all team members of the team has access. | If the original dashboard is not shared, only the user who copies the dashboard. </br>If the original dashboard is shared, all team members of the team with editor permissions. |
{: caption="Table 2. Information about users and dashboards related to copying dashboards" caption-side="top"} 

Complete the following steps to copy a dashboard:

1. Navigate to the *DASHBOARDS* section in the Web UI.
2. Select the dashboard from the left hand panel.
3. Click **Settings** (three dots icon), and select **Copy dashboard**. 
4. Select where to copy the dashboard.

    1. Choose **Current Team** to copy the dashboard for the current team.
    
    2. Choose **Other Teams** to copy the dashboard to other teams. Select the teams where you want to copy the dashboard.

    3. Enter a name for the dashboard.

    4. Click **Send copy**.
    
    5. Check that the scope of the dashboard in the new team is updated based on the permissions of the destination team.

## Deleting a dashboard
{: #delete}

Complete the following steps to delete a dashboard:

1. Navigate to the *DASHBOARDS* section in the Web UI.
2. Select the dashboard from the left hand panel.
3. Click **Settings** (three dots icon), and select **Delete dashboard**. 
4. Confirm deletion by clicking **Yes, delete dashboard**.


## Sharing a dashboard
{: #share}

You can share dashboards between users in a team, and externally, by configuring a public URL for the dashboard.  

The following table outlines the different actions and user permissions that are required for users to share or work with a shared dashboard:

| Action                  |	Who can share             |	Dashboard instance	            | Who can view the dashboard             | Who can edit the dashboard  |
|-------------------------|---------------------------|---------------------------------|----------------------------------------|-----------------------------|
| Share with current Team |	Dashboard creator         |	Share same dashboard instance   | Team members with viewing permissions  | Team members with editing permissions   |
| Share publicly as URL	  | Any Edit User of the team |	Share same dashboard instance   | Anyone                                 | No one                      |
{: caption="Table 1. Information about users and dashboards related to sharing dashboards" caption-side="top"} 


Complete the following steps to share a dashboard:

1. Navigate to the *DASHBOARDS* section in the Web UI.
2. Select the dashboard from the left hand panel.
3. Click **Settings** (three dots icon), and select **Share**.
4. Choose how you want to share the dashboard:

    * Toggle the **Share with Team** slider to share the dashboard with the current team. The team where the dashboard is shared is displayed.

    * Toggle the **Share Public URL** slider to reveal the custom public URL.

5. Click **Close**.

Share a dashboard externally to allow external users to view the dashboard metrics, while restricting access to changing panels and configurations.
{: tip}


## Saving dashboards programmatically by using a Python Script
{: #save}

Complete the following steps to save dashboards locally:


The library and example scripts are available in the Sysdig GitHub repository: https://github.com/draios/python-sdc-client.
Download the Scripts

Save All Dashboards with a Python Script

To save the dashboards:

    In a terminal, access the virtual environment set up in Download the Scripts.

    Run the script, replacing API_TOKEN with the API token for the relevant user, and SAVED_DASHBOARDS.ZIP with the desired name of the zip file:

    The user API token can be found in the User Profile tab of the UI Settings page.
    (venv) $ sudo python examples/download_dashboards.py API_TOKEN SAVED_DASHBOARDS.ZIP
    Dashboard name: JVM, # Charts: 5
    Finished writing dashboard data in zip format to SAVED_DASHBOARDS.ZIP


## Restoring dashboards programmatically by using a Python Script
{: #restore}

You can restore a *.zip* file 

Restoring dashboards will not override the user's existing dashboards. Instead, new dashboards will be added to the list.


The restore script does not have to target the same account as the save script. This allows dashboards to be saved from one user, and restored to multiple users.

To restore dashboards from a .zip archive

    In a terminal, access the virtual environment set up in Download the Scripts.

    Run the script, replacing API_TOKEN with the API token for the relevant user, and SAVED_DASHBOARDS.ZIP with the correct zip file:
    (venv) $ sudo python examples/restore_dashboards.py API_TOKEN SAVED_DASHBOARDS.ZIP
    Dashboards pushed.
    (venv) user@server:~/python-sdc-client$


