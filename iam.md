---

copyright:
  years:  2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

 
# Managing user access in the {{site.data.keyword.Bluemix_notm}}
{: #iam}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.Bluemix_notm}}. 
{:shortdesc}

**Every user that accesses the IBM Cloud Monitoring with Sysdig service in your account must be assigned an access policy with an IAM user role defined.** The policy determines what actions the user can perform within the context of the service or instance you select. The allowable actions are customized and defined as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

*Policies* enable access to be granted at different levels. Some of the options include the following: 

* Access to all IAM-enabled services in your account
* Access across all instances of the service in a single region in your account
* Access to an individual service instance in your account
* Access to all instances of the service within the context of a resource group
* Access to all instances of the service in a single region within the context of a resource group
* Access to all IAM-enabled services within the context of a resource group

*Roles* define the actions that a user or serviceID can run. There are different types of roles in the {{site.data.keyword.Bluemix_notm}}:
* *Platform management roles* enable users to perform tasks on service resources at the platform level, for example assign user access for the service, create or delete service IDs, create instances, assign policies for your service to other users, and bind instances to applications.
* *Service access roles* enable users to be assigned varying levels of permission for calling the service's API.

**To organize a set of users and service IDs into a single entity that makes it easy for you to manage IAM permissions, use **access groups*.** You can assign a single policy to the group instead of assigning the same access multiple times per individual user or service ID.
{: tip}


## Managing access by using access groups
{: #groups}

To manage access or assign new access for users by using access groups, you must be the account owner, administrator or editor on all Identity and Access enabled services in the account, or the assigned administrator or editor for the IAM Access Groups Service. 

Choose any of the following actions to manage access groups in the {{site.data.keyword.Bluemix_notm}}:

* [Creating an access group](/docs/iam/groups.html#creating-an-access-group).
* [Assigning access to a group](/docs/iam/groups.html#assigning-access-to-a-group).


## Managing access by assigning policies directly to users
{: #users}

To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance. 

Choose any of the following actions to manage IAM policies in the {{site.data.keyword.Bluemix_notm}}:

* To modify the permissions of a user, see [Editing existing access](/docs/iam/mngiam.html#editing-existing-access).
* To grant permissions to a user, see [Assign new access](/docs/iam/mngiam.html#assignaccess).
* To revoke permissions, see [Removing access](/docs/iam/mngiam.html#removing-access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/iam/mngiam.html#reviewing-your-assigned-access).



## {{site.data.keyword.Bluemix_notm}} platform roles
{: #platform}

Use the following table to identify the platform role that you can grant a user in the {{site.data.keyword.Bluemix_notm}} to run any of the following platform actions:

| Platform actions                                                        | {{site.data.keyword.Bluemix_notm}} Platform Roles    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `Grant other account members access to work with the service`           | Administrator                                        | 
| `Provision a service instance`                                          | Administrator </br>Editor                            | 
| `Delete a service instance`                                             | Administrator </br>Editor                            | 
| `Create a service ID`                                                   | Administrator </br>Editor                            |
| `View details of a service instance`                                    | Administrator </br>Editor </br>Operator </br>Viewer  | 
| `View service instances in the Observability Monitoring dashboard`      | Administrator </br>Editor </br>Operator </br>Viewer  | 
{: caption="Table 1. IAM user roles and actions" caption-side="top"}



## Sysdig roles
{: #sysdig_roles}

The following table outlines the Sysdig roles and actions per role:

| Actions                                                                    | Sysdig role                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Reset the Sysdig access key`                                              | Admin                                                |
| `Manage users`                                                             | Admin                                                |
| `Create, configure, and delete teams`                                      | Admin                                                |
| `Configure and remove notifications channels`                              | Admin                                                | 
| `Configure and remove Sysdig agents`                                       | Admin                                                |
| `Create, delete, and edit content in the Sysdig web UI`                    | Admin </br>User                                      |  
| `View metrics through the Sysdig Web UI`                                   | Admin </br>User                                      |  
| `Create and delete alerts`                                                 | Admin </br>User                                      | 
| `Create and delete captures`                                               | Admin </br>User                                      |   
{: caption="Table 2. Sysdig roles and actions" caption-side="top"}


## Mapping of Sysdig roles to {{site.data.keyword.Bluemix_notm}} roles
{: #sysdig}

Use the following table to see how an {{site.data.keyword.Bluemix_notm}} role maps to a Sysdig role:

| Type of role        | Role               | Sysdig role                | Description                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| Platform role       | Administrator      | Admin                      | Grants the user Sysdig admin privileges.   | 
| Service role        | Manager            | Admin                      | Grants the user Sysdig admin privileges.   | 
| Service role        | Writer             | User                       | Grants the user Sysdig user privileges.    |
| Service role        | Reader             |                            | No permissions are granted.                 |
{: caption="Table 3. Sysdig roles" caption-side="top"}


