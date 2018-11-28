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

 
# Working with IAM policies and access groups
{: #iam_work}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.Bluemix_notm}}. 
{:shortdesc}

To grant Sysdig admin priviledges to a user, you can assign the user any of the following roles:

* `Administrator` platform role: Grant this role if the user is also an administrator for the Sysdig service in the {{site.data.keyword.Bluemix_notm}}.
* `Editor` platform role: Grant this role if the user must be able to provision or remove Sysdig instances in the {{site.data.keyword.Bluemix_notm}}.
* `Manager` service role:  Grant this role if the user should not be able to manage the Sysdig service in the {{site.data.keyword.Bluemix_notm}}.

To grant Sysdig user priviledges to a user, you can assign a user the `Writer` service role.

**Note:** To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance. 

As the **account owner** or as an **IBM Cloud Monitoring with Sysdig service administrator**, you must have permissions to run the following platform actions: 

* Grant other account members access to work with the service
* Provision a service instance
* Delete a service instance
* View details of a service instance
* Create a service ID

As a **Devops user**, you must have permissions to run the following platform actions: 

* Provision a service instance
* Delete a service instance
* View details of a service instance
* Create a service ID


## Granting permissions to a user to become an administrator of the service in the {{site.data.keyword.Bluemix_notm}} account
{: #admin_account}

To grant a user administrator role to manage the service in the account, the user must have an IAM policy for the IBM Cloud Monitoring with Sysdig service with the platform role **Administrator**. You must assign this user access to an individual resource in the account. 

Complete the following steps to assign a user administrator role to the IBM Cloud Monitoring with Sysdig service in the account: 

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access to resources**.
4. Select **IBM Cloud Monitoring with Sysdig**.
5. Select **All current regions**.
6. Select **All current service instances**.
7. Select the platform role **Administrator**.
8. Click Assign.


## Granting permissions to a user to become an administrator of the service within a resource group
{: #admin_rg}

To grant a user administrator role to manage instances within a resource group in the account, the user must have an IAM policy for the IBM Cloud Monitoring with Sysdig service with the platform role **Administrator** within the context of the resource group. 

Complete the following steps to assign a user administrator role to the IBM Cloud Monitoring with Sysdig service within the context of a resource group: 

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access within a resource group**.
4. Select a resource group.
5. If the user does not have a role already granted for the selected resource group, choose a role for the **Assign access to a resource group** field. 

    Depending on the role that you select, the user can view the resource group on their dashboard, edit the resource group name, or manage user access to the group. 
    
    You can select **No access**, if you want the user to only have access to the IBM Cloud Monitoring with Sysdig service in the resource group.

6. Select **IBM Cloud Monitoring with Sysdig**.
7. Select the platform role **Administrator**.
8. Click **Assign**.


## Granting permissions to a Devops user to manage the service in the {{site.data.keyword.Bluemix_notm}} account
{: #devops_account}

You need to have an IAM policy for the IBM Cloud Monitoring with Sysdig service with the platform role **Editor**.

Complete the following steps to assign a user editor role to the IBM Cloud Monitoring with Sysdig service in the account: 

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access to resources**.
4. Select **IBM Cloud Monitoring with Sysdig**.
5. Select **All service instances**.
6. Select the platform role **Editor**.
7. Click Assign.

## Granting permissions to a Devops user to manage an instance in the {{site.data.keyword.Bluemix_notm}} account
{: #devops_account_instance}

Complete the following steps to assign a user editor role on one instance of the IBM Cloud Monitoring with Sysdig service in the account: 

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access to resources**.
4. Select **IBM Cloud Monitoring with Sysdig**.
5. Select the instance.
6. Select the platform role **Editor**.
7. Click Assign.



## Granting permissions to a Devops user to manage the service within a resource group
{: #devops_rg}

You need an IAM policy for the IBM Cloud Monitoring with Sysdig service with the platform role **Editor**.

Complete the following steps to assign a user editor role to the IBM Cloud Monitoring with Sysdig service within the context of a resource group: 

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access within a resource group**.
4. Select a resource group.
5. If the user does not have a role already granted for the selected resource group, choose a role for the **Assign access to a resource group** field. 

    Depending on the role that you select, the user can view the resource group on their dashboard, edit the resource group name, or manage user access to the group. 
    
    You can select **No access**, if you want the user to only have access to the IBM Cloud Monitoring with Sysdig service in the resource group.

6. Select **IBM Cloud Monitoring with Sysdig**.
7. Select the platform role **Editor**.
8. Click **Assign**.

## Granting permissions to manage metrics and configure alerts in Sysdig
{: #admin_user_sysdig}

As an **admin user** in Sysdig, you must have permissions to run the following actions: 

* Add metric sources
* View metrics
* Search metrics
* Filter metrics
* Configure alerts

Therefore, you need the following policies:

* An IAM policy for the IBM Cloud Monitoring with Sysdig service with the platform role **Editor**. This policy allows you to view the service instance details through the command line and in the {{site.data.keyword.Bluemix_notm}} dashboard.
* An IAM policy for the IBM Cloud Monitoring with Sysdig service with the service role **Manager**. This policy allows you to monitor, filter and search metrics, and define alerts through the Sysdig web UI.

**Note:** As an administrator of the service, when you grant a user these policies, consider doing it within the context of a resource group. An IBM Cloud Monitoring with Sysdig instance is provisioned within the context of a resource group. Therefore, you should grant access permissions within the context of the resource group.


Complete the following steps to assign a user both policies for the IBM Cloud Monitoring with Sysdig service within the context of a resource group: 

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access within a resource group**.
4. Select a resource group.
5. If the user does not have a role already granted for the selected resource group, choose a role for the **Assign access to a resource group** field. 

    Depending on the role that you select, the user can view the resource group on their dashboard, edit the resource group name, or manage user access to the group. 
    
    You can select **No access**, if you want the user to only have access to the IBM Cloud Monitoring with Sysdig service in the resource group.

6. Select **IBM Cloud Monitoring with Sysdig**.
7. Select the platform role **Editor**.
8. Select the service role **Manager**.
8. Click **Assign**.

## Granting permissions to a user to view metrics in Sysdig
{: #user_sysdig}

As a **user**, **auditor**, or **developer**, you might need permissions to run the following actions: 

* View metrics
* Search metrics
* Filter metrics

Therefore, you need the following policies:

* An IAM policy for the IBM Cloud Monitoring with Sysdig service with the platform role **Viewer**. This policy allows you to view the service instance details through the command line and in the {{site.data.keyword.Bluemix_notm}} dashboard.
* An IAM policy for the IBM Cloud Monitoring with Sysdig service with the service role **Writer**. This policy allows you to view, filter and search metrics through the Sysdig web UI.

**Note:** As an administrator of the service, when you grant a user these policies, consider doing it within the context of a resource group. An IBM Cloud Monitoring with Sysdig instance is provisioned within the context of a resource group. Therefore, you should grant access permissions within the context of the resource group.

Complete the following steps to assign a user both policies for the IBM Cloud Monitoring with Sysdig service within the context of a resource group: 

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and then select **Users**.
2. From the row for the user that you want to assign access, select the **Actions** menu, and then click **Assign access**.
3. Select **Assign access within a resource group**.
4. Select a resource group.
5. If the user does not have a role already granted for the selected resource group, choose a role for the **Assign access to a resource group** field. 

    Depending on the role that you select, the user can view the resource group on their dashboard, edit the resource group name, or manage user access to the group. 
    
    You can select **No access**, if you want the user to only have access to the IBM Cloud Monitoring with Sysdig service in the resource group.

6. Select **IBM Cloud Monitoring with Sysdig**.
7. Select the platform role **Viewer**.
8. Select the service role **Writer**.
8. Click **Assign**.

