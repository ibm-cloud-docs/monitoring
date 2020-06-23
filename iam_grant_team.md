---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-24"

keywords: Sysdig, IBM Cloud, monitoring, iam, access groups

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
{:external: target="_blank" .external}

 
# Granting permissions to work in a team
{: #iam_grant_team}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.cloud_notm}}. Complete the following steps to grant a user or service ID administration permissions to work with the {{site.data.keyword.mon_full_notm}} service:
{:shortdesc}


## Prerequisites
{: #iam_grant_team_prereq}

Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.mon_full_notm}} service. Contact the account administrator. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/iam?topic=iam-userroles).


## Step 1. Create an access group
{: #iam_grant_team_step1}

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




## Step 2. Add team policy to manage data
{: #iam_grant_team_step2}

After you set up your group, you can assign a common access policy to the group. 

Any policy that you set for an access group applies to all entities, users, and service IDs, within the group. 
{: note}

You can assign the policy by using the UI or through the command line.


### Add team policy to manage data through the {{site.data.keyword.cloud_notm}} UI
{: #iam_grant_team_step2_ui}

Complete the following steps to assign a policy to an access group through the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to. 
3. Click **Access policies**.
4. Click **Assign access**.
5. Select **Assign access to resources**.
6. In the *Service Instance* section, select 1 instance.
7. In the *Sysdig Team* section, choose 1 team.
5. Select a service role. [Learn more about the roles that you need](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-iam).
6. Click **Assign**.

### Add team policy to manage data through the CLI
{: #iam_grant_team_step2_cli}

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

You must use a JSON file to create the team policy.
{: important}

For example, you can run the following command:

```
ibmcloud iam access-group-policy-create accessGroupName accessGroupGUID --file policy.json
```
{: codeblock}

Where 

* `accessGroupName` is the acces group name.
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


## Step 3. Add a user or service ID to the access group
{: #iam_grant_team_step3}

Continue to set up your group by adding users or service IDs.

### Add a user to the access group
{: #iam_grant_team_step3_user}

Complete the following steps to add a user:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to. 
3. Click **Add users** on the **Users** tab.
4. Select the users that you want to add from the list, and click **Add to group**.


### Add a service ID to the access group
{: #iam_grant_team_step3_svcid}

Complete the following steps to add a service ID:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to. 
3. Click the **Service IDs** tab, and click **Add service ID**.
4. Select the IDs that you want to add from the list, and click **Add to group**.




