---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, teams

subcollection: Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Working with teams
{: #teams}

You can use teams to add another dimension of control on the data that is available through a Sysdig instance.
{:shortdesc} 

In the world of microservices, it is becoming harder to track down valuable metrics and ensure that no sensitive data is exposed. Teams fixes this by allowing admins to configure who exactly can see metrics from specific resources. A team can be created for a single service instance and an instance can have many teams. It specifies what resources are visible with fine grain control. Teams also allow you to customize the user experience of the dashboard. Once a team is created, an admin can add a user to it through {{site.data.keyword.iamlong}} (IAM).

## Pre-reqs
{: #teams_prereqs}

* An administrator or a manager of an {{site.data.keyword.mon_full_notm}} instance must switch to the *Monitor Operations* team before he can create teams and manage existing teams.
* You must have provisioned an instance of the {{site.data.keyword.mon_full_notm}} service.

## Creating a team
{: #teams_create}

Complete the following steps to create a team:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, select **Monitor Operations**. Then, choose **Settings**.

3. Select **Teams**. The list of existing teams is displayed.

4. Click **Add Team**. The team configuration page is displayed.

5. Configure the team details. 

    * Choose a color.

    * Enter the name of the team

    * [Optional] Enter a description for this team.

    * [Optional] Set the **Default team** parameter if you want this team to become the default team for new users.

    * Set the **Default Entry Point** to specify the view in the web UI that opens every time a user logs in. Valid entrypoints are: *Explore* view, *Dashboards* view, *Events* view, *Alerts* view, and *Settings* view. By default, the *Explore* view is set.

6. Configure the team scope. 

    * [Optional] Set **Scope by** to specify the level of data that members of the team have access to. Valid values are *host* and *container*. If the parameter is set to *Host*, members can see all Host-level and Container-level information. If the parameter is set to *Container*, members can see only Container-level information.

    * Set the **Scope** to limit what data users can see. You can set one or more conditions by specifying expressions for metrics. By default, the scope is set to *everywhere*.
	
    * [Optional] Enable or disable **Sysdig captures**. Check this box to allow this team to take Sysdig Captures. Capture files will only be visible to members of this team. **Note:** Captures include detailed information from every container on a host, regardless of the team’s scope.

    * [Optional] Enable or disable **Infrastructure Events**. Check this box to allow members to view all custom infrastructure events from every user and Sysdig agent. When is not checked, users can see infrastructure events that are sent specifically to this team. 

6. Add members to the team. Click **Assign user**. Search for a user and add it.



## Changing the scope of a team
{: #teams_scope}

To change the scope of the data that is visible to members of a team, complete the following steps: 

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, select **Monitor Operations**. Then, choose **Settings**.

3. Select **Teams**. The list of existing teams is displayed.

4. Identify the team and select it. The details of the team are displayed.

5. Change configuration details in the *Visibility* section.

6. Click **Save**. 


## Deleting a team
{: #teams_delete}

The default team, **Monitor Operations**, cannot be deleted. 

Complete the following steps to delete a team:

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. From the *Selector* button in the navigation bar, select **Monitor Operations**. Then, choose **Settings**.

3. Select **Teams**. The list of existing teams is displayed.

4. Identify the team that you want to delete and select it. The details of the team are displayed.

5. Click **Delete team**.

**Note:** When you delete a team, users that only belong to this team will be moved to the default team.


## Granting users permissions to work in a team
{: #teams_assign}

To add a user to a team, consider the following information:
1. You must have **manager** permissions in the Sysdig instance where the team is available.
2. You must define a team level IAM policy for the user.

When the policy is defined, the user is added to the list of users that have access to work with resources configured for a team.

[Learn more on how to grant a user permissions to manage all teams in a Sysdig instance](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_manage_events#admin_account_opt4).

[Learn more on how to grant a user permissions to view data for a team in a Sysdig instance](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_view_events#user_opt4).

