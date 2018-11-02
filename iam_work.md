---

copyright:
  years:  2018
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

 
# Managing user access with IAM
{: #iam_work}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.Bluemix_notm}}. 
{:shortdesc}


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
 

