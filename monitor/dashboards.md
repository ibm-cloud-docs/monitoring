---

copyright:
  years:  2018, 2023
lastupdated: "2023-10-23"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}



# Working with dashboards
{: #dashboards}

Use dashboards to monitor your infrastructure, applications, and services. You can use pre-defined dashboards. You can also create custom dashboards through the Web UI or programmatically. You can backup and restore dashboards by using Python scripts.
{: shortdesc}

A **dashboard** shows groups of metrics that report on the health, performance, and state of your infrastructure, applications, and services for a single host or a group of hosts. Dashboards offer a specialized insight into network data, application data, topology, services, hosts, and containers.

In the **Dashboards** section of the Web UI, dashboards are organized into groups:
* *Recently Viewed* are dashboards that the user has recently used.
* *My Favorites* are dashboards the user has flagged to be included in this view.
* *My Dashboards* are dashboards that are created by the user who is currently logged in.  An icon indicates if the dashboard is shared with other team members.
* *Shared By My Team* are dashboards that are created by other users, and shared with the current user.

You can copy and share dashboards through the Web UI.

In the **Explore** section allows you to review specific metrics for your environment.  This section also provides support for PromQL queries.

You can run scripts to complete any of the following actions programmatically:
* Save existing dashboards to a local file.
* Create new dashboards that are identical to the dashboards that you save.
* Restore dashboards.



## Pre-defined dashboards
{: #dashboards_predefined}

Pre-defined dashboards are designed around various supported applications, network topologies, infrastructure layouts, and services.

Pre-defined dashboards include a series of panels that are already configured.

For more information on pre-defined dashboards, see [Dashboard Library](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/dashboard-templates/){: external}.

## Creating custom dashboards in the Web UI
{: #dashboards_create}

When you create a custom dashboard, you can start from a template such as a pre-defined dashboard, or choose a blank dashboard. A dashboard includes panels that are configured to display specific data in different formats. You also set how data is aggregated. The **scope** defines what data is used for aggregation and displayed. You can set the scope at a dashboard level, or override for individual panels within the dashboard.

Complete the following steps to create a custom dashboard:

1. Navigate to the **Dashboards** section in the Web UI

2. You can create a dashboard using a template or by creating a dashboard manually.

    * To create a dashboard using a template:

        1. Click **Dashboard Manager**.

        2. Click **Dashboard Library**.

        3. Click the template you want to use to create your dashboard.

        4. Click **Copy to My Dashboards**.

        5. Name your dashboard.

        6. Click **Create and Open**

    * To create a dashboard without a template:

        1. Click **+ New Dashboard**. The *New Dashboard* page opens.

        2. Modify your dashboard as desired.

        3. Click **Save**.

        4. Click *New Dashboard* to rename your dashboard.  Click the check mark to save your name change.

3. Set the dashboard scope. Click the *Pencil* icon ![Pencil icon](../images/pencil.png). The select the desired scope. By default, **Entire infrastructure** is selected.

    1. Select the scope.

    2. Click **Save**.

4. Configure panels. Repeat this step for any of the panels in the dashboard that you want to modify.

    1. Identify the panel that you want to modify.

    2. Select **Edit Panel**. This is the *Pencil* icon ![Pencil icon](../images/pencil.png).

    3. Change the visualization if needed.

    4. Change the query used to select the data.

    5. For **Number** and **Gauge** chart types you can set the panel color based on metric thresholds. Click **Thresholds**. Set values for the different thresholds.  

       For **Timechart** set the axes and legend for the chart.

    6. For **Panel** specify the name of the panel and an optional description.

    7. Change the scope of the panel. Click the *Pencil* icon ![Pencil icon](../images/pencil.png). Then, change the scope. If you need to restore the dashboard scope to the panel, delete the custom scope.  Click **Apply**.

    8. Click **Save**.

## Changing the scope
{: #dashboards_scope}

Instead of changing the scope of a pre-defined dashboard, copy the dashboard and change the scope in the copied dashboard.
{: tip}

Complete the following steps to change the scope of a dashboard:

1. Navigate to the **Dashboards** section in the Web UI, and select a dashboard.

2. Click the *Pencil* icon ![Pencil icon](../images/pencil.png) to **Edit Dashboard Scope** to change default scope.

3. Select the scope.

    <!--
    4. Optionally, click **Override the custom panel scopes** to override the scope for all panels which currently have a custom scope defined.

    This action cannot be undone.
    {: note}

    To reset the dashboard scope to the entire infrastructure, or to update an existing dashboard's scope to the entire infrastructure, select **Everywhere**.
    {: tip} -->

4. Click **Save**.



## Copying a dashboard
{: #dashboards_copy}

When you copy a dashboard, you create a duplicate of an existing dashboard.

The following table outlines the different actions and user permissions that are required for users to copy a dashboard:

| Action     |	Who can copy     |	Dashboard instance	   | Who can view the dashboard     | Who can edit the dashboard  |
|------------|-------------------|-------------------------|--------------------------------|-----------------------------|
| Copy to current Team    |	Users in the team with editor permissions | New dashboard instance  | Team members with viewing permissions	 | Users in the team with editor permissions |
| Copy to another Team    | Users in the team with editor permissions in both teams | New dashboard instance  | If the original dashboard is not shared, only the user who copies the dashboard has access.  \n If the original dashboard is shared, all team members of the team has access. | If the original dashboard is not shared, only the user who copies the dashboard.  \n If the original dashboard is shared, all team members of the team with editor permissions. |
{: caption="Table 2. Information about users and dashboards related to copying dashboards" caption-side="top"}

Complete the following steps to copy a dashboard in the Web UI:

1. Navigate to the *Dashboards* section in the Web UI.
2. Select a dashboard in the panel.
3. Click the **Action icon** ![three dots icon](/images/actions.png), and select **Duplicate Dashboard**.
4. Enter a name for the dashboard.
5. Click **Copy and Open**.


## Deleting a dashboard
{: #dashboards_delete}

Complete the following steps to delete a dashboard in the Web UI:

1. Navigate to the *Dashboards* section in the Web UI.
2. Select the dashboard in the panel.
3. Click the **Actions icon** ![three dots icon](/images/actions.png), and select **Delete**.
4. Confirm deletion by clicking **Delete Dashboard**.


## Sharing a dashboard
{: #dashboards_share}

You can share dashboards between users in a team, and externally, by configuring a public URL for the dashboard.

The following table outlines the different actions and user permissions that are required for users to share or work with a shared dashboard:

| Action      |	Who can share        |	Dashboard instance	       | Who can view the dashboard        | Who can edit the dashboard  |
|-------------|-------------------|-----------------------------|------------------------------------|-----------------------------|
| Share with current Team |	Dashboard creator         |	Share same dashboard instance   | Team members with viewing permissions  | Team members with editing permissions   |
| Share publicly as URL	  | Any Edit User of the team |	Share same dashboard instance   | Anyone     | No one                      |
{: caption="Table 3. Information about users and dashboards related to sharing dashboards" caption-side="top"}


Complete the following steps to share a dashboard in the Web UI:

1. Navigate to the *Dashboards* section in the Web UI.
2. Select the dashboard in the panel.
3. Click **Actions icon** ![three dots icon](/images/actions.png), and select **Dashboard Settings**.
4. Choose how you want to share the dashboard:

    * For **Share with** select how the dashboard will be shared.
        * **Not Shared** indicates the dashboard will not be shared with other users
        * **All My Teams** indicates the dashboard will be shared with all your team members.  You can specify whether other team members can only view the dashboard, or collaborate and make changes to the dashboard.
        * **Select Teams** indicates the dashboard will only be shared with members of the teams you select.  You can specify whether other team members can only view the dashboard, or collaborate and make changes to the dashboard.  If you add a team and want to remove that team's permissions to the dashboard, click the **X** next to the team member permissions line.

    * Toggle the **Public Dashboard** slider to reveal the custom public URL.

5. Click **Save**.

Share a dashboard externally to allow external users to view the dashboard metrics, while restricting access to changing panels and configurations.
{: tip}
