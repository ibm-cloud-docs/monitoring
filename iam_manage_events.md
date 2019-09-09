---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: Sysdig, IBM Cloud, monitoring, iam, access groups

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

 
# Granting administration permissions to a user or service ID
{: #iam_manage_events}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.cloud_notm}}. Complete the following steps to grant a user or service ID administration permissions to work with the {{site.data.keyword.mon_full_notm}} service:
{:shortdesc}


## Prerequisites
{: #iam_manage_events_prereq}

Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.mon_full_notm}} service. Contact the account administrator. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/iam?topic=iam-userroles).


## Step 1. Create an access group
{: #ime_step1}

Complete the following steps to create an access group:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Click **Create**.
3. Enter a name and optional description for your group, and click **Create**.

You can delete a group by selecting the **Remove group** option. When you remove a group from the account, you are removing all users and service IDs from the group and all access that is assigned to the group.
{: note}

To create an access group by using the CLI, you can use the [ibmcloud iam access-group-create](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_create) command.

```
ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
{: codeblock}




## Step 2. Add permissions to manage events
{: #ime_step2}

After you set up your group, you can assign a common access policy to the group. 

Any policy that you set for an access group applies to all entities, users, and service IDs, within the group. 
{: note}

You can assign the policy by using the UI or through the command line.

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

```
ibmcloud iam access-group-policy-create GROUP_NAME {-f, --file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```
{: codeblock}

When you define the policy, you need to select a platform role and a service role:
* Platform management roles cover a range of actions, including the ability to create and delete instances, manage aliases, bindings, and credentials, and manage access. The platform roles are administrator, editor, operator, viewer. Platform management roles also apply to account management services that enable users to invite users, manage service IDs, access policies, catalog entries, and track billing and usage depending on their assigned role on an account management service.
* Service access roles define a user or service’s ability to perform actions on a service instance. The service access roles are manager, writer, and reader.

To manage the {{site.data.keyword.mon_full_notm}} service, a user needs the following roles:
* Platform role: **Administrator** or **Editor**. 
* Service role: **Manager**. 
[Learn more](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam).

Complete the following steps to assign a policy to an access group through the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to. 
3. Click **Access policies**.
4. Click **Assign access**.
5. Choose to assign access by resources within a resource group, or by individual resources available within the account. For example, you can choose any of the following options to grant a user an administrator role to manage {{site.data.keyword.mon_full_notm}}:

### Option 1. Grant permissions on the service
{: #admin_account_opt1}

Complete the following steps to assign a user administrator role to the {{site.data.keyword.mon_full_notm}} service in the account: 

1. Select **Assign access to resources**.
2. In the *Services* section, select **{{site.data.keyword.mon_full_notm}}**.
3. Skip configuring a value in the *Service Instance* section.
4. Skip configuring a value in the *Sysdig Team* section.
5. Select a platform role.

    Select **Administrator** to allow the user to manage the service and user access to work with the service.

    Select **Editor** to allow the user to manage the service only.

6. Select the service role **Manager**.
7. Click **Assign**.

### Option 2. Grant permissions within the context of a resource group
{: #admin_account_opt2}

Complete the following steps to assign a user administrator role to the {{site.data.keyword.mon_full_notm}} service within the context of a resource group: 

1. Select **Assign access within a resource group**.
2. Select a resource group.
3. If the user does not have a role that is already granted for the selected resource group, choose a role for the **Assign access to a resource group** field. 

    Depending on the role that you select, the user can view the resource group on their dashboard, edit the resource group name, or manage user access to the group. 
    
    You can select **No access**, if you want the user to have access only to the {{site.data.keyword.mon_full_notm}} service in the resource group.

4. Select **{{site.data.keyword.mon_full_notm}}**.
5. Select a platform role.

    Select **Administrator** to allow the user to manage the service and user access to work with the service.

    Select **Editor** to allow the user to manage the service only.

6. Select the service role **Manager**.
7. Click **Assign**.

### Option 3. Grant permissions on a single instance
{: #admin_account_opt3}


Complete the following steps to assign a user administrator role on 1 instance of the {{site.data.keyword.mon_full_notm}} service: 

1. Select **Assign access to resources**.
2. Select **{{site.data.keyword.mon_full_notm}}**.
3. In the *Service Instance* section, select 1 instance.
4. In the *Sysdig Team* section, skip the section to grant permissions on all teams that are defined in Sysdig for that instance, or choose a team.

5. Select a platform role.

    Select **Administrator** to allow the user to manage the service and user access to work with the service.

    Select **Editor** to allow the user to manage the service only.
    
6. Select the service role **Manager**.
7. Click **Assign**.

### Option 4. Grant permissions to manage all teams in a Sysdig instance
{: #admin_account_opt4}

When you grant a user the **manager** role, the user gets permissions to manage all teams in a Sysdig instance. 
{: note}

Complete the following steps to assign a user administrator role to manage all teams in a Sydig instance: 

1. Select **Assign access to resources**.
2. Select **{{site.data.keyword.mon_full_notm}}**.
3. In the *Service Instance* section, select 1 instance.
4. In the *Sysdig Team* section, choose a team.

5. Select a platform role.

    Select **Administrator** to allow the user to manage the service and user access to work with the service.

    Select **Editor** to allow the user to manage the service only.
    
6. Select the service role **Manager** to grant the user permissions to manage all teams.
7. Click **Assign**.

## Step 3. Add a user or service ID to the access group
{: #ime_step3}

Continue to set up your group by adding users or service IDs.

### Add a user to the access group
{: #ime_step3_user}

Complete the following steps to add a user:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to. 
3. Click **Add users** on the **Users** tab.
4. Select the users that you want to add from the list, and click **Add to group**.


### Add a service ID to the access group
{: #ime_step3_svcid}

Complete the following steps to add a service ID:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to. 
3. Click the **Service IDs** tab, and click **Add service ID**.
4. Select the IDs that you want to add from the list, and click **Add to group**.




