---

copyright:
  years:  2018, 2024
lastupdated: "2024-09-25"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Granting permissions to work with the {{site.data.keyword.mon_short}} service
{: #iam_grant}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and consistently control access to all cloud resources in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Complete the following steps to grant a user or service ID permissions to work with the {{site.data.keyword.mon_full_notm}} service:

## Prerequisites
{: #iam_grant_sprereq}

Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.mon_full_notm}} service. The account owner can grant user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).


## Step 1. Create an access group
{: #iam_grant_step1}

Complete the following steps to create an access group:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Click **Create**.
3. Enter a name and optional description for your group, and click **Create**.

You can delete a group by selecting the **Remove group** option. When you remove a group from the account, you are removing all users and service IDs from the group and all access that is assigned to the group.
{: note}

To create an access group by using the CLI, you can use the [ibmcloud iam access-group-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_create) command.

```text
ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
{: pre}



## Step 2. Add permissions to view {{site.data.keyword.mon_short}} instances in the Observability UI
{: #iam_grant_step2}

After you set up your group, you can assign a common access policy to the group. You must add permissions to view {{site.data.keyword.mon_short}} instances in the Observability UI, to manage the instance in the {{site.data.keyword.cloud_notm}}, or both.

Any policy that you set for an access group applies to all entities, users, and service IDs, within the group.
{: note}

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}

You can assign the policy by using the UI or through the command line.

When you define the policy, you need to select a platform role. Platform management roles cover a range of actions, including the ability to create and delete instances, manage aliases, bindings, and credentials, and manage access. Valid platform roles are administrator, editor, operator, and viewer.


### Add permissions through the CLI
{: #iam_grant_step2_1}

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

```text
ibmcloud iam access-group-policy-create GROUP_NAME {-f, --file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```
{: codeblock}

Where valid `roles` are `Administrator`, `Editor`, `Operator`, and `Viewer`.

For example, you can run the following command to grant a user viewer permissions:

```text
ibmcloud iam access-group-policy-create my-access-group --roles Viewer --service-name my-monitoring-instance --service-instance 99999999-9999-9999-999999
```
{: pre}


### Add permissions through the UI
{: #iam_grant_step2_2}

Complete the following steps to assign a policy to an access group through the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Access policies**  &gt; **Assign access**  &gt; **Assign access to resources**.
4. Select **IAM services**.
5. In the section *What type of access do you want to assign?*, select **{{site.data.keyword.mon_full_notm}}**.
6. In the section *Which services do you want to assign access to?*, choose one of the following options:

    Select **All services** to define the scope of the policy to include all instances.

    Select **Services based on attributes** to refine the scope of the policy. Choose 1 of the following options:

    Option 1: The scope is set to a resource group. Select **Resource group** to choose 1 resource group and define the scope of the policy to include all instances that are associated with that resource group.

    Option 2: The scope is set to 1 instance in a resource group. Select **Resource group** to choose the resource group. Then select **Service Instance** to choose the instance within the resource group.

    Option 3: The scope is set to 1 instance. Select **Service Instance** to choose the instance.

    Do not specify a value in the *Sysdig Team* section.
    {: important}

7. Select a platform role.

    Select **administrator** to grant admin permissions for the service.

    Select **viewer** to grant permissions to view instances in the *Observability* UI.

    [Learn more about the roles that you need](/docs/monitoring?topic=monitoring-iam).

8. Click **Assign**.



## Step 3. Add permissions to work with data in the {{site.data.keyword.mon_short}} service
{: #iam_grant_step3}

Next, you must add a policy that grants the user permission to work with data in the {{site.data.keyword.mon_short}} service.

When you define the policy, you need to select a service role. Service access roles define a user's or service's ability to perform actions on a service instance. The service access roles are manager, writer, and reader.


### Add permissions through the CLI
{: #iam_grant_step3_1}

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

```text
ibmcloud iam access-group-policy-create GROUP_NAME {-f, --file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```
{: codeblock}

Where valid `roles` are `Reader`, `Writer`, and `Manager`.

For example, you can run the following command to grant a user reader permissions:

```text
ibmcloud iam access-group-policy-create my-access-group --roles Reader --service-name my-monitoring-instance --service-instance 99999999-9999-9999-999999
```
{: pre}


### Add permissions through the UI
{: #iam_grant_step3_2}

Complete the following steps to assign a policy to an access group through the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Access policies**  &gt; **Assign access**  &gt; **Assign access to resources**.
4. Select **IAM services**.
5. In the section *What type of access do you want to assign?*, select **{{site.data.keyword.mon_full_notm}}**.
6. In the section *Which services do you want to assign access to?*, choose one of the following options:

    Select **All services** to define the scope of the policy to include all instances.

    Select **Services based on attributes** to refine the scope of the policy. Choose 1 of the following options:

    Option 1: The scope is set to a resource group. Select **Resource group** to choose 1 resource group and define the scope of the policy to include all instances that are associated with that resource group.

    Option 2: The scope is set to 1 instance in a resource group. Select **Resource group** to choose the resource group. Then select **Service Instance** to choose the instance within the resource group.

    Option 3: The scope is set to 1 instance. Select **Service Instance** to choose the instance.

    Do not specify a value in the *Sysdig Team* section.
    {: important}

7. Select a service role.

    Select **manager** to grant admin permissions for the service.

    Select **reader** to grant permissions to view data only.

    [Learn more about the roles that you need](/docs/monitoring?topic=monitoring-iam).

8. Click **Assign**.


## Step 4. Add a user or service ID to the access group
{: #iam_grant_step4}

You can add users or service IDs to an existing group.

### Add a user to the access group
{: #iam_grant_step4_user}

Complete the following steps to add a user:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Add users** on the **Users** tab.
4. Select the users that you want to add from the list, and click **Add to group**.


### Add a service ID to the access group
{: #iam_grant_step4_svcid}

Complete the following steps to add a service ID:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click the **Service IDs** tab, and click **Add service ID**.
4. Select the IDs that you want to add from the list, and click **Add to group**.
