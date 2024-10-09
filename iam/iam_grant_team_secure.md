---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Granting permissions to view data within the context of a team in {{site.data.keyword.sysdigsecure_short}}
{: #iam_grant_team_secure}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and consistently control access to all cloud resources in the {{site.data.keyword.cloud_notm}}. Teams provide an isolated workspace in a {{site.data.keyword.mon_short}} {{site.data.keyword.sysdigsecure_short}} instance for a user or group of users to have access to metrics in a defined scope.
{: shortdesc}

IAM can map a combination of teams and roles so that a user only has access to a specific set of metrics and can take a defined set of actions within the product.
{: note}

Teams provide additional security by only allowing users to see metrics that are related to the infrastructure where their apps are deployed, as opposed to the entire infrastructure of the account. For example, in a Kubernetes cluster, you could grant a group of developers access to only see reports from scanned images from 1 `kubernestes.namespace` where their application is deployed.

In an {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} instance, you can define 1 or more teams. A team provides an isolated workspace for a user or group of users to have access to metrics with a defined scope.

An {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} instance includes the **Secure operations** teams.

By default, users are granted access to the `Secure operations` team or to the team that is configured as the default team by the instance administrator.

- An admin of the service can configure multiple teams, and change the default team.

- Each team has their own set of custom resources that they can use to monitor the data in scope for the team.

- Users in a team have access to the data that is included in the scope defined by the team administrator.

[Learn more about teams](/docs/monitoring?topic=monitoring-teams).

For a user to monitor data within the context of a team, you must grant the user a policy for the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} service. The policy specifies the team and the service permissions for the user so the user can work with the data in scope for that team.

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}

The following table shows the user roles that you can grant a user to work with the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} service:

| User role            | IAM service role |
|----------------------|------------------|
| `ROLE_USER`          | `reader`         |
| `ROLE_ADVANCED_USER` | `writer`         |
| `ROLE_ADMIN`         | `manager`        |
{: caption="List of user roles" caption-side="top"}


The following table shows the team roles that you can grant users to work within the context of a team in an {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} instance:

| Team role            | IAM service role | Team   |
|----------------------|------------------|--------|
| `ROLE_TEAM_READ`     | `reader`         | Custom team |
| `ROLE_TEAM_EDIT`     | `writer`         | Custom team |
| `ROLE_TEAM_ADMIN`    | `manager`        | Custom team |
| `ROLE_TEAM_SECURE_MANAGER`  | `manager` | `Secure operations`  |
{: caption="List of team roles" caption-side="top"}

You can define in the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} UI more teams to define different levels of access to data per team and set of users.

To grant a user access to 1 or more teams, an administrator must grant the user a policy for each team that the user needs access to. By using individual policies for each team, administrators can define different service access and permissions levels to work with data in the monitoring instance.

For example, a user that needs to work in a team requires the following policies:
* A policy with a platform role **viewer** to allow the user to see monitoring instances in the {{site.data.keyword.cloud_notm}}.
* A policy to grant the user access to 1 team. The service role determines the permissions of the user to work with data that is in scope for the team.

Complete the following steps to grant a user or service ID permissions to work with the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} service within the context of a team:


## Prerequisites
{: #iam_grant_team_secure_prereq}

Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} service. The account owner can grant user access to the account for the purposes of managing user access and managing account resources. [Learn more](/docs/account?topic=account-userroles).


## Step 1. Create an access group
{: #iam_grant_team_secure_step1}

Do the following to create an access group:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Click **Create**.
3. Enter a name and optional description for your group, and click **Create**.

You can delete a group by selecting the **Remove group** option. When you remove a group from the account, you are removing all users and service IDs from the group and all access that is assigned to the group.
{: note}

To create an access group by using the CLI, you can use the [ibmcloud iam access-group-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_create) command.

```text
ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
{: codeblock}




## Step 2. Add permissions to view {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} instances in the Observability UI
{: #iam_grant_team_secure_step2}

After you set up your group, you can assign a common access policy to the group. You must add permissions to view {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} instances in the Observability UI.

Any policy that you set for an access group applies to all entities, users, and service IDs within the group.
{: note}

You can assign the policy by using the UI or through the command line.

When you define the policy, you need to select a platform role. Platform management roles cover a range of actions, including the ability to create and delete instances, manage aliases, bindings, and credentials, and manage access. Valid platform roles are administrator, editor, operator, viewer.


### Add permissions through the CLI
{: #iam_grant_team_secure_step2_1}

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command with the **viewer** role.

```text
ibmcloud iam access-group-policy-create GROUP_NAME {-f, --file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```
{: codeblock}

For example, you can run the following command to grant a user viewer permissions:

```text
ibmcloud iam access-group-policy-create my-access-group --roles Viewer --service-name my-monitoring-instance --service-instance 99999999-9999-9999-999999
```
{: pre}


### Add permissions through the UI
{: #iam_grant_team_secure_step2_2}

Complete the following steps to assign a new policy to an access group through the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Access**  &gt; **Assign access** to create a policy.
4. In the **Service** section, select **{{site.data.keyword.sysdigsecure_full_notm}}**. Then, click **Next**.
5. In the **Resources** section, choose one of the following options:

    Select **All resources** to define the scope of the policy to include all instances.

    Select **Specific resources** to refine the scope of the policy. Then, configure 1 or more attributes: region, resource group, and service instance. Do not specify a value in the *Sysdig Team* section.

    Then, click **Next**.

6. Choose roles and actions to define the levels of access do you want to assign. You must choose a platform role and a service role.

    Select **viewer** to grant permissions to view instances in the *Observability* UI.

    [Learn more about the roles that you need](/docs/monitoring?topic=monitoring-iam).

7. Click **Review** &gt; **Add** &gt; **Assign**.





## Step 3. Add permissions to work in a team
{: #iam_grant_team_secure_step3}

Next, you must add a policy that grants the user permissions to work with data in the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} service within the context of a team.

When you define the policy, you need to select a service role. Service access roles define a user's or service’s ability to perform actions on a service instance. The service access roles are manager, writer, and reader.


### Add permissions through the CLI
{: #iam_grant_team_secure_step3_1}

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

```text
ibmcloud iam access-group-policy-create GROUP_NAME {-f, --file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```
{: codeblock}

Where valid roles are `Reader`, `Writer`, and `Manager`.

You must use a JSON file to create the team policy.
{: important}

For example, you can run the following command:

```text
ibmcloud iam access-group-policy-create accessGroupName accessGroupGUID --file policy.json
```
{: codeblock}

Where

* `accessGroupName` is the access group name.
* `accessGroupGUID` is the GUID of the access group.

You can run the command `ibmcloud iam access-groups` to get the list of names and corresponding GUIDs in the account.
{: tip}

And use the following JSON file.

```json
{
    "type": "access",
    "subjects": [
        {
            "attributes": [
                {
                    "name": "access_group_id",
                    "value": "AccessGroupGuid"
                }
            ]
        }
    ],
    "roles" : [
    {
            "role_id" : "crn:v1:bluemix:public:iam::::serviceRole:Reader"
    }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "accountGuid"
                },
                {
                    "name": "serviceName",
                    "value": "sysdig-monitor"
                },
                {
                    "name": "serviceInstance",
                    "value": "instanceGuid"
                },
                {
                    "name": "sysdigTeam",
                    "value": "sysdigTeamID"
                }
            ]
        }
    ]
}
```
{: codeblock}


### Add permissions through the UI
{: #iam_grant_team_secure_step3_2}

Complete the following steps to assign a policy to an access group through the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Access**  &gt; **Assign access** to create a policy.
4. In the **Service** section, select **{{site.data.keyword.sysdigsecure_full_notm}}**. Then, click **Next**.
5. In the **Resources** section, choose one of the following options:

    Select **All resources** to define the scope of the policy to include all instances.

    Select **Specific resources** to refine the scope of the policy. Then, configure the **Instance** and the **Sysdig Team** attribute.

    Then, click **Next**.

6. Choose roles and actions to define the levels of access do you want to assign. You must choose a platform role and a service role.

    Select **manager** to grant admin permissions for the service.

    Select **reader** to grant permissions to view data only.

    [Learn more about the roles that you need](/docs/monitoring?topic=monitoring-iam).

7. Click **Review** &gt; **Add** &gt; **Assign**.



## Step 4. Add a user or service ID to the access group
{: #iam_grant_team_secure_step4}

You can add users or service IDs to an existing access group.

### Add a user to the access group
{: #iam_grant_team_secure_step4_user}

Complete the following steps to add a user:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Add users** on the **Users** tab.
4. Select the users that you want to add from the list, and click **Add to group**.


### Add a service ID to the access group
{: #iam_grant_team_secure_step4_svcid}

Complete the following steps to add a service ID:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click the **Service IDs** tab, and click **Add service ID**.
4. Select the IDs that you want to add from the list, and click **Add to group**.
