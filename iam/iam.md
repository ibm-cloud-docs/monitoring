---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-24"

keywords: Sysdig, IBM Cloud, monitoring, iam

subcollection: Monitoring-with-Sysdig

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

 
# Controlling access through IAM
{: #iam}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.cloud_notm}}. You grant permissions through policies that you define on the {{site.data.keyword.mon_full_notm}} service in the account.
{:shortdesc}

**Users in an account must be assigned a platform role to manage instances, and to launch the Sysdig UI from the {{site.data.keyword.cloud_notm}}. In addition, users must have a service role that defines the permissions to work with {{site.data.keyword.mon_full_notm}}.** 
{: important}

The policy determines what actions the user can perform within the context of the service or instance you select. The allowable actions are customized and defined as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

*Policies* enable access to be granted at different levels. Some of the options include the following: 

* Access to all IAM-enabled services in your account
* Access across all instances of the service in a single region in your account
* Access to an individual service instance in your account
* Access to all instances of the service within the context of a resource group
* Access to all instances of the service in a single region within the context of a resource group
* Access to all IAM-enabled services within the context of a resource group

*Roles* define the actions that a user or serviceID can run. There are different types of roles in the {{site.data.keyword.cloud_notm}}:
* *Platform management roles* enable users to perform tasks on service resources at the platform level, for example assign user access for the service, create or delete service IDs, create instances, assign policies for your service to other users, and bind instances to applications.
* *Service access roles* enable users to be assigned varying levels of permission for calling the service's API or running actions in the Sysdig UI.

To organize a set of users and service IDs into a single entity that makes it easy for you to manage IAM permissions, use **access groups**. You can assign a single policy to the group instead of assigning the same access multiple times per individual user or service ID.
{: tip}


## Managing access by using access groups
{: #iam_groups}

To manage access groups, you must be the account owner, administrator or editor on all Identity and Access enabled services in the account, or the assigned administrator or editor for the IAM Access Groups Service. 
{: note}

Choose any of the following actions to manage access groups in the {{site.data.keyword.cloud_notm}}:

* [Creating an access group](/docs/account?topic=account-groups#create_ag).
* [Assigning access to a group](/docs/account?topic=account-groups#access_ag).


## Managing access by assigning policies directly to users
{: #iam_users}

To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance. 

Choose any of the following actions to manage IAM policies in the {{site.data.keyword.cloud_notm}}:

* To grant permissions to a user, see [Assigning access](/docs/account?topic=account-assign-access-resources#assign_new_access).
* To revoke permissions, see [Removing access](/docs/account?topic=account-assign-access-resources#removing_access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/account?topic=account-assign-access-resources#review_your_access).


## {{site.data.keyword.cloud_notm}} platform roles
{: #iam_platform}

You must grant users a platform role to allow them to view and manage the {{site.data.keyword.mon_full_notm}} service in your account. 
- You can grant permissions to work with all the instances in the {{site.data.keyword.cloud_notm}} account. 
- You can restrict access to individual instances.

Use the following table to identify the platform role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following platform actions:

| Platform actions                                                        | Administrator                                     | Editor | Operator | Viewer  |
|-------------------------------------------------------------------------|:-------------------------------------------------:|:-------:|:--------:|:------:|
| `Grant other account members access to work with the service`           | ![Checkmark icon](../images/checkmark-icon.svg) |         |          |        |
| `Provision a service instance`                                          | ![Checkmark icon](../images/checkmark-icon.svg) |![Checkmark icon](../images/checkmark-icon.svg)         |          |        |
| `Delete a service instance`                                             | ![Checkmark icon](../images/checkmark-icon.svg) |![Checkmark icon](../images/checkmark-icon.svg)         |          |        |
| `Create a service ID`                                                   | ![Checkmark icon](../images/checkmark-icon.svg) |![Checkmark icon](../images/checkmark-icon.svg)         |          |        |
| `View details of a service instance`                                    | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)    | ![Checkmark icon](../images/checkmark-icon.svg)      | ![Checkmark icon](../images/checkmark-icon.svg)    |
| `View service instances in the Observability Monitoring dashboard`      | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)    | ![Checkmark icon](../images/checkmark-icon.svg)      | ![Checkmark icon](../images/checkmark-icon.svg)    |
{: caption="Table 1. IAM user roles and actions" caption-side="top"}


A user with an **administrator** role automatically gets the service **manager** role permissions.
{: note}



## {{site.data.keyword.cloud_notm}} service roles
{: #iam_svcroles}

Use the following table to identify the service role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following actions:

| Actions                                       | Manager                                           | Writer                         | Reader |
|-----------------------------------------------|---------------------------------------------------|--------------------------------|--------|
| `Reset the Sysdig access key`                    | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Create, configure, and delete teams`            | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Configure and remove notifications channels`    | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Configure and remove Sysdig agents`             | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Create, delete, and edit content in the Sysdig web UI`| ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Create and delete dashboards`                   | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Create and delete alerts`                       | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Create and delete events`                   | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | | 
| `Create and delete captures`                     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | | 
| `Modify the scope of dashboards/panels`        | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `View metrics, dashboards, alerts, events, and captures`  | ![Checkmark icon](../images/checkmark-icon.svg)      | ![Checkmark icon](../images/checkmark-icon.svg)                    | ![Checkmark icon](../images/checkmark-icon.svg)    | 
{: caption="Table 2. Service roles and actions" caption-side="top"}


## IAM actions
{: #iam_actions}

Use the following table to identify the IAM actions that are assigned to the platform and service roles for the {{site.data.keyword.mon_full_notm}} service:

| Role type         | Role              | IAM actions |
|-------------------|-------------------|--------------|
| Platform          | `adminsitrator`   | `sysdig-monitor.launch.admin` </br>`sysdig-monitor.launch.user` </br>`sysdig-monitor.launch.viewer` |
| Service           | `manager`         | `sysdig-monitor.launch.admin` </br>`sysdig-monitor.launch.user` </br>`sysdig-monitor.launch.viewer` |
| Service           | `writer`          | `sysdig-monitor.launch.user` </br>`sysdig-monitor.launch.viewer` |
| Service           | `reader`          | `sysdig-monitor.launch.viewer` |
{: caption="Table 3. IAM actions assigned to platform and service roles" caption-side="top"}



## Permissions to view and manage data within the scope of a team
{: #iam_policies_team}

In a {{site.data.keyword.mon_short}} instance, you can define 1 or more teams. A team provides an isolated workspace for a user or group of users to have access to metrics for a defined scope.

A {{site.data.keyword.mon_short}} instance includes the following teams:
- Monitor operations 
- Secure operations

By default, users are granted access to the `monitor operations` team or to the team that is configured as the default one by an administrator of the instance. An admin of the service can configure more teams, and change the default team. 

For a user to work within the context of a team, you must grant the user a policy for the {{site.data.keyword.mon_full_notm}} service. The policy specifies the team and the service permissions that the user has to work with the data in scope for that team.

To grant a user access to 1 or more teams, an administrator must grant the user a policy for each team that the user needs access to.

For example, a user that needs to work in a team requires the following policies:
* 1 policy with a platform role **viewer** to allow the user to see instances in the {{site.data.keyword.cloud_notm}}.
* 1 policy to grant the user access to 1 team. The service role determines the permissions of that user to work with data that is in scope of the team.

To configure a policy for a user or service ID, see [Granting permissions to work in a team](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-iam_grant_team).


## How do I know which access policies are set for me?
{: #iam_accesspolicy}

You can see which access policies are set for you in the [{{site.data.keyword.cloud_notm}} UI](https://cloud.ibm.com/){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.
4. Click the **Access groups** tab to see the access groups where you are a member. Check the policies for each group.



