---

copyright:
  years:  2018
lastupdated: "2018-09-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

 
# Managing user access with Identity and Access Management
{: #sysdig_iam}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.Bluemix_notm}}. 
{:shortdesc}

Every user that accesses the Sysdig service in your account must be assigned an access policy with an IAM user role defined. That policy determines what actions the user can perform within the context of the service or instance you select. The allowable actions are customized and defined by the {{site.data.keyword.Bluemix_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

Policies enable access to be granted at different levels. Some of the options include the following: 

* Access across all instances of the service in your account
* Access to an individual service instance in your account
* Access to a specific resource within an instance
* Access to all IAM-enabled services in your account

After you define the scope of the access policy, you assign a role. 

* You can assign platform roles to manage Sysdig instances in the {{site.data.keyword.Bluemix_notm}}, and to manage and monitor data through the Sysdig web UI.
* You can assign service roles to manage and monitor data through the Sysdig web UI.



## Configuring Sysdig admin priviledges for a user
{: #admin}

To grant Sysdig admin priviledges to a user, you can assign the user any of the following roles:

* `Administrator` platform role: Grant this role if the user is also an administrator for the Sysdig service in the {{site.data.keyword.Bluemix_notm}}.
* `Editor` platform role: Grant this role if the user must be able to provision or remove Sysdig instances in the {{site.data.keyword.Bluemix_notm}}.
* `Manager` service role:  Grant this role if the user should not be able to manage the Sysdig service in the {{site.data.keyword.Bluemix_notm}}.

To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance. 

Choose any of the following actions to manage a user's Sysdig admin priviledges:

* To edit modify the permissions of a user, see [Editing existing access](/docs/iam/mngiam.html#editing-existing-access).
* To grant permissions to a user, see [Assign new access](/docs/iam/mngiam.html#assignaccess).
* To revoke permissions, see [Removing access](/docs/iam/mngiam.html#removing-access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/iam/mngiam.html#reviewing-your-assigned-access).


## Configuring Sysdig user priviledges for a user
{: #user}

To grant Sysdig user priviledges to a user, you can assign a user the `Writer` service role.

Choose any of the following actions to manage a user's Sysdig user priviledges:

* To edit modify the permissions of a user, see [Editing existing access](/docs/iam/mngiam.html#editing-existing-access).
* To grant permissions to a user, see [Assign new access](/docs/iam/mngiam.html#assignaccess).
* To revoke permissions, see [Removing access](/docs/iam/mngiam.html#removing-access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/iam/mngiam.html#reviewing-your-assigned-access).
 


## Platform roles
{: #platform}

The following table details actions that are mapped to platform management roles in the {{site.data.keyword.Bluemix_notm}}. Platform management roles enable users to perform tasks on service resources at the platform level, for example assign user access for the service, create or delete service IDs, create instances, assign policies for your service to other users, and bind instances to applications.

| Platform management role | Description of actions              | Examples                                  |
|:-------------------------|:------------------------------------|-------------------------------------------|
| Viewer                   | View details of a service instance. | View information about a Sysdig instance. |
| Editor                   | All actions a viewer and operator can perform.    |                             |
| Operator                 | Create a service instance.          | Provision a Sysdig instance.              |
| Administrator            | Manage users and permissions. </br>Create service instances. </br>All actions a viewer, editor, and operator can perform. | Assign user access for the service. </br>Provision a Sysdig instance. |
{: caption="Table 1. IAM user roles and actions" caption-side="top"}

The following table maps Sysdig roles to Platform {{site.data.keyword.Bluemix_notm}} roles:

| Sysdig role                              |  {{site.data.keyword.Bluemix_notm}} role  |
|:-----------------------------------------|:------------------------------------------|
| Sysdig admin priviledges                 | Administrator </br>Editor |
{: caption="Table 2. Mapping of Sysdig roles to Platform {{site.data.keyword.Bluemix_notm}} roles" caption-side="top"}


## Service roles
{: #service}

Service access roles enable users to be assigned varying levels of permission for calling the service's API.

The following table details actions that are mapped to service access roles. Service access roles enable users access to Sysdig as well as the ability to call the Sysdig's API.

| Service access role | Description of actions                      | 
|:--------------------|:--------------------------------------------|
| Reader              | No permissions are granted.                 | 
| Writer              | Grants the user Sysdig user priviledges.    |
| Manager             | Grants the user Sysdig admin priviledges.   | 
{: caption="Table 3. IAM service access roles and actions" caption-side="top"}




