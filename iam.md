---

copyright:
  years:  2018, 2019
lastupdated: "2019-09-09"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

To manage access or assign new access for users by using access groups, you must be the account owner, administrator or editor on all Identity and Access enabled services in the account, or the assigned administrator or editor for the IAM Access Groups Service. 

Choose any of the following actions to manage access groups in the {{site.data.keyword.cloud_notm}}:

* [Creating an access group](/docs/iam?topic=iam-groups#create_ag).
* [Assigning access to a group](/docs/iam?topic=iam-groups#access_ag).


## Managing access by assigning policies directly to users
{: #iam_users}

To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance. 

Choose any of the following actions to manage IAM policies in the {{site.data.keyword.cloud_notm}}:

* To modify the permissions of a user, see [Editing existing access](/docs/iam?topic=iam-iammanidaccser#edit_existing).
* To grant permissions to a user, see [Assign new access](/docs/iam?topic=iam-iammanidaccser#assign_new_access).
* To revoke permissions, see [Removing access](/docs/iam?topic=iam-iammanidaccser#removing_access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/iam?topic=iam-iammanidaccser#review_your_access).


## {{site.data.keyword.cloud_notm}} platform roles
{: #iam_platform}

Use the following table to identify the platform role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following platform actions:


| Platform actions                                                        | Administrator                                     | Editor | Operator | Viewer  |
|-------------------------------------------------------------------------|:-------------------------------------------------:|:-------:|:--------:|:------:|
| `Grant other account members access to work with the service`           | ![Checkmark icon](../../icons/checkmark-icon.svg) |         |          |        |
| `Provision a service instance`                                          | ![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg)         |          |        |
| `Delete a service instance`                                             | ![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg)         |          |        |
| `Create a service ID`                                                   | ![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg)         |          |        |
| `View details of a service instance`                                    | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)    | ![Checkmark icon](../../icons/checkmark-icon.svg)      | ![Checkmark icon](../../icons/checkmark-icon.svg)    |
| `View service instances in the Observability Monitoring dashboard`      | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)    | ![Checkmark icon](../../icons/checkmark-icon.svg)      | ![Checkmark icon](../../icons/checkmark-icon.svg)    |
{: caption="Table 1. IAM user roles and actions" caption-side="top"}



## {{site.data.keyword.cloud_notm}} service roles
{: #iam_svcroles}

Use the following table to identify the service role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following actions:

| Actions                                          | Manager                            | Writer                         | Reader |
|--------------------------------------------------|:----------------------------------:|:------------------------------:|:------:|
| `Reset the Sysdig access key`                    | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |   |
| `Create, configure, and delete teams`            | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |   |
| `Configure and remove notifications channels`    | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |   |
| `Configure and remove Sysdig agents`             | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |   |
| `Create, delete, and edit content in the Sysdig web UI`                    | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg) | |
| `Create and delete alerts`                                                 | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg) | |
| `Create and delete captures`                                               | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg) | |  
| `View metrics, dashboards, alerts, events, and captures through the Sysdig Web UI`      | ![Checkmark icon](../../icons/checkmark-icon.svg)      | ![Checkmark icon](../../icons/checkmark-icon.svg)                    | ![Checkmark icon](../../icons/checkmark-icon.svg)    | 
{: caption="Table 2. Sysdig roles and actions" caption-side="top"}


## Policy that is required to be able to see the Sysdig instance in the {{site.data.keyword.cloud_notm}}
{: #iam_policies_cloud}

Use the following table to identify the platform role that you must grant a user in the {{site.data.keyword.cloud_notm}} to see the Sysdig instance in the {{site.data.keyword.cloud_notm}}:

 DevOps role               | Platform scope  | Platform role  | Service role      | Team scope   | See Sysdig instance in {{site.data.keyword.cloud_notm}}  |
|--------------------------|-----------------|----------------|-------------------|--------------|-------------------------------------------|
| `Service administrator`  | `All instances` | `Administrator`|                   |              | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Sysdig instance manager`| `Instance`      | `Editor`       |                   |              | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Sysdig instance writer` | `Instance`      | `Viewer`       |                   |              | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Team writer`            | `Instance`      | `Viewer`       |                   |              | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Instance viewer (user)` | `Instance`      | `Viewer`       |                   |              | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Team viewer (user)`     | `Instance`      | `Viewer`       |                   |              | ![Checkmark icon](../../icons/checkmark-icon.svg) | 
{: caption="Table 3. Roles and actions" caption-side="top"}

An instance viewer is a user that can see dashboards, alerts, and notifications in a Sysdig instance for all teams.
An instance writer is a user that can see and manage dashboards, alerts, and notifications in a Sysdig instance for all teams.  


## Policy that is required to work with data through the Sysdig UI or API
{: #iam_policies}

Use the following table to identify the platform role and the service role that you must grant a user in the {{site.data.keyword.cloud_notm}} to work in the Sysdig UI or to make REST API calls:

**Every user must have 1 policy defined that specifies if that user can work in the Sysdig UI, and can make REST API calls.** 
{: important}

* The **platform scope** controls the number of instances to which the policy apply. 
* The **platform role** determines if the user can see Sysdig instances in the {{site.data.keyword.cloud_notm}}. 
* The **service role** determines the permissions a user have to work Sysdig.
* The **team scope** determines whether the policy applies to a team or not. *When you define this policy, ensure that a team is not selected.*


| DevOps role              | Platform scope  | Platform role  | Service role      | Team scope   | Launch Sysdig UI and make REST API calls |
|--------------------------|-----------------|----------------|-------------------|--------------|-------------------------------------------|
| `Service administrator`  | `All instances` | `Administrator`| `Manager`         | `(*)`        | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Sysdig instance manager`| `Instance`      | `Editor`       | `Manager`         | `(**)`       | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Sysdig instance writer` | `Instance`      | `Viewer`       | `Writer`          | `(**)`       | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Instance viewer (user)` | `Instance`      | `Viewer`       | `Reader`          | `(**)`       | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 3. Roles and actions" caption-side="top"}

`(*)`The user gets permissions to manage all teams across all Sysdig instances.
`(**)` The user gets permissions to work across all teams in 1 Sysdig instance.


To configure a policy for a user or service ID, see [Granting permissions to launch the Sysdig UI or to make REST API calls](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_grant).



## Policy that is required to grant permissions to work in a team in a Sysdig instance
{: #iam_policies_team}

**Every user that must work in a team must have this policy defined.** 

You cannot combine the policy to work with Sysdig with the policy to work in a team. 
{: important}

A user that needs to work in a team requires the following policies:
* 1 policy with a platform role to allow the user to see Sysdig instances in the {{site.data.keyword.cloud_notm}}, and a service role that determines the permissions of that user to work in a Sysdig instance. 

    You cannot assign the manager service role to a user when you configure the policy that is required to work with data through the Sysdig UI or API.
    {: important}

    To define this policy, see [Granting permissions to launch the Sysdig UI or to make REST API calls](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_grant).

* 1 policy to grant permissions to work in a team.

Use the following table to identify the service role that you must grant a user in the {{site.data.keyword.cloud_notm}} to work in a Sysdig team:

| DevOps role              | Platform scope  | Platform role  | Service role      | Team scope   | Launch Sysdig UI and make REST API calls |
|--------------------------|-----------------|----------------|-------------------|--------------|-------------------------------------------|
| `Team writer`            | `Instance`      |                | `Writer`          | `Team`       | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| `Team viewer`            | `Instance`      |                | `Reader`          | `Team`       | ![Checkmark icon](../../icons/checkmark-icon.svg) | 
{: caption="Table 4. Roles and actions" caption-side="top"}

Team viewer is a user that can see dashboards, alerts, and notifications in a Sysdig instance, and is limited to analyze data that is available thorugh dashboards for the team the user belongs to.
Team writer is a user that can see and manage dashboards, alerts, and notifications in a Sysdig instance, and is limited to data that is available for the team it belongs to.  Add link to roles table.

To configure a policy for a user or service ID, see [Granting permissions to work in a team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_grant_team).


