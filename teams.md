---

copyright:
  years:  2019
lastupdated: "2019-09-10"

keywords: Sysdig, IBM Cloud, monitoring, team, teams

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

# Working with Teams
{: .no_toc }

Teams allow you to add another dimension of control on top of platform and service access.

In the world of microservices it is becoming harder to track down valuable metrics and ensure that no sensitive data is exposed. Teams fixes this by allowing admins to configure who exactly can see metrics from specific resources. A team can be created for a single service instance and an instance can have many teams. It specifies what resources are visible with fine grain control. Teams also allow you to customize the user experience of the dashboard. Once a team is created an admin can add a user to it through the _Access (IAM)_ page.

NOTE: These instructions assume that you have provisioned a Sysdig service instance on IBM Cloud

## Creating a Team
{: #teams_create}

1. Enter your Sysdig dashboard

2. Navigate to the settings page and then the Teams tab

3. Press _Add team_

4. Configure the options following the chart below

5. Press _Save_

| Configuration | Required | Description |
|----------|----------|----------|
| Color | Yes | Assigns a color to the team to make them easier to identify quickly in a list | 
| Name | Yes | The name of the team as it will appear in the “Switch to” drop-down selector and other menus |
| Description | No | Longer description for the team |
| Default Team | No | If users are not assigned to any team, they will automatically be a part of this team if it's turned on |
| Default Entry Point | Yes | Defaults to the Explore page; choose an alternate entry if needed |
| Scope by | No | Determines the highest level the data to which team members will have visibility. If set for _Host_, Team members can see all Host-level and Container-level information. If set for _Container_, Team members can see only Container-level information |
| Scope | Yes | Further limits what data Team members can see by specifying tag/value expressions for metrics. The pull-down selector defaults to _is_, but can be changed to _is not_, _in_, _contains_, and etc. Complex policies can be created by clicking _Add another_ to create AND chains of several expressions.<br><br>NOTE: Making changes to the Scope settings can have a dramatic impact on what’s visualized in the Team’s Dashboards that are already configured, so you may want to carefully review these before/after your change |
| Additional Permissions | No | **Sysdig Capture** - Check this box to allow this team to take Sysdig Captures. Captures will only be visible to members of this team.<br>WARNING: Captures will include detailed information from every container on a host, regardless of the team’s Scope<br><br>**Infrastructure Events** - Check this box to allow this team to view ALL infrastructure events (from every user and agent. Otherwise, this team will only see infrastructure events sent specifically to this team |

<img src="images/team-configuration.png" alt="Team Configuration" width="800" />

## Editing a Team
{: #teams_edit}

1. You must have the _Manager_ service access role in IAM for the instance containing the team

2. Enter your Sysdig dashboard

3. Switch to the default team, Monitor Operations, by pressing on the user icon

4. Navigate to the settings page and then the Teams tab

5. Press the team you want to modify and follow the configuration chart above

6. Press _Save_

## Deleting a Team
{: #teams_delete}

1. You must have the _Manager_ service access role in IAM for the instance containing the team

2. Enter your Sysdig dashboard

3. You cannot delete the team that you're currently using

4. Navigate to the settings page and then the Teams tab

5. Press the team you want to modify

6. Press _Delete Team_

7. Think about the repercussions and then press _Yes, delete_

NOTE: When you delete a team, users that only belong to this team will be moved to the default team

## Assigning Users to Teams
{: #teams_assign}

1. Enter the [Access (IAM) page](https://test.cloud.ibm.com/iam/overview) and ensure you have sufficient privileges to modify the user

2. Enter the Users tab and press on the user you want to add to your team

3. Press the _Access policies_ tab

4. Press _Assign access_

5. Press _Assign access to resources_

6. Search for _IBM Cloud Monitoring with Sysdig_

7. Select your Service Instance

8. Select your team

9. Select your platform and service access roles

10. Press _Assign_

<img src="images/instance-policies.png" alt="Instance Policies" width="800" />
