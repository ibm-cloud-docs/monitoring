---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Controlling access through IAM
{: #iam}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and consistently control access to all cloud resources in the {{site.data.keyword.cloud_notm}}. You grant permissions through policies that you define on the {{site.data.keyword.mon_full_notm}} service in the account.
{: shortdesc}

**Users in an account must be assigned a platform role to manage instances and to launch the monitoring UI from the {{site.data.keyword.cloud_notm}}. In addition, users must have a service role that defines the permissions to work with {{site.data.keyword.mon_full_notm}}.**
{: important}

The policy determines the actions the user can perform within the context of the selected service or instance. The actions are customized and defined with operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

*Policies* enable access to be granted at different levels. Some of the options include the following:

* Access to all IAM-enabled services in your account
* Access across all instances of the service in a single region in your account
* Access to an individual service instance in your account
* Access to all instances of the service within the context of a resource group
* Access to all instances of the service in a single region within the context of a resource group
* Access to all IAM-enabled services within the context of a resource group

*Roles* define the actions that a user or serviceID can run. There are different types of roles in the {{site.data.keyword.cloud_notm}}:

* *Platform management roles* enables users to perform tasks on service resources at the platform level, for example assigning user access for the service, creating or deleting service IDs, creating instances, assigning policies for your service to other users, and binding instances to applications.
* *Service access roles* enables users to be assigned varying levels of permission when calling the service's API or running actions in the monitoring UI.

To organize a set of users and service IDs into a single entity that makes it easy for you to manage IAM permissions, use **access groups**. You can assign a single policy to the group instead of assigning the same access multiple times for each individual user or service ID.
{: tip}

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}


## Managing access by using access groups
{: #iam_groups}

To manage access groups, you must be the account owner, administrator or editor on all Identity and Access-enabled services in the account, or the assigned administrator or editor for the IAM Access Groups Service.
{: note}

Use the following actions to manage IAM access groups in the {{site.data.keyword.cloud_notm}}:

* [Creating an access group](/docs/account?topic=account-groups#create_ag).
* [Assigning access to a group](/docs/account?topic=account-groups#access_ag).


## Managing access by assigning policies directly to users
{: #iam_users}

To manage access or assign new access to users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance.

Use the following actions to manage IAM policies in the {{site.data.keyword.cloud_notm}}:

* To grant permissions to a user, see [Assigning access](/docs/account?topic=account-assign-access-resources#assign_new_access).
* To revoke permissions, see [Removing access](/docs/account?topic=account-assign-access-resources#removing_access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/account?topic=account-assign-access-resources#review_your_access).


## {{site.data.keyword.cloud_notm}} platform roles
{: #iam_platform}

Users must be granted a platform role to allow them to view and manage the {{site.data.keyword.mon_full_notm}} service in your account. You can grant permissions to work with all the instances in the {{site.data.keyword.cloud_notm}} account or you can restrict access to individual instances.

The folling table identifies the platform role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run the specified platform actions:

| Platform actions                                                        | Administrator                                     | Editor | Operator | Viewer  |
|-------------------------------------------------------------------------|:-------------------------------------------------:|:-------:|:--------:|:------:|
| `Grant other account members access to work with the service`           | ![Checkmark icon](../images/checkmark-icon.svg) |         |          |        |
| `Provision a service instance`                                          | ![Checkmark icon](../images/checkmark-icon.svg) |![Checkmark icon](../images/checkmark-icon.svg)         |          |        |
| `Delete a service instance`                                             | ![Checkmark icon](../images/checkmark-icon.svg) |![Checkmark icon](../images/checkmark-icon.svg)         |          |        |
| `Create a service ID`                                                   | ![Checkmark icon](../images/checkmark-icon.svg) |![Checkmark icon](../images/checkmark-icon.svg)         |          |        |
| `View details of a service instance`                                    | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)    | ![Checkmark icon](../images/checkmark-icon.svg)      | ![Checkmark icon](../images/checkmark-icon.svg)    |
| `View service instances in the Observability Monitoring dashboard`      | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)    | ![Checkmark icon](../images/checkmark-icon.svg)      | ![Checkmark icon](../images/checkmark-icon.svg)    |
{: caption="IAM user roles and actions" caption-side="top"}


A user with an **administrator** role automatically has the service **manager** role permissions.
{: note}



## {{site.data.keyword.cloud_notm}} service roles
{: #iam_svcroles}

The following table identifies the service role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run the specified actions:

| Action | Description | Manager | Writer | Reader | Administrator |
|--------|-------------|---------|--------|--------|---------------|
| `sysdig-monitor.launch.admin` | Run priviledge tasks. | ![Checkmark icon](../images/checkmark-icon.svg) | | | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.launch.viewer` | Perform read-only actions within a service. | ![Checkmark icon](../images/checkmark-icon.svg) | | | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.secure.manager` `[*]` | Run priviledge tasks. | ![Checkmark icon](../images/checkmark-icon.svg) | | | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.secure.user` `[*]` | Perform read-only actions within a service. |![Checkmark icon](../images/checkmark-icon.svg)  | | | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.secure.viewer` `[*]` |  Perform read-only actions within a service. | | | | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.agent-installation.read` | Agent installation access. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.agent.cli.agent-network-calls-to-remote-pods` | Access to network calls for the CLI. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.agent.cli.agent-status` | Access to agent status from the CLI. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.agent.cli.view` | Access to view the CLI. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.agent.cli.view-configuration` | Access to view the configuration from the CLI. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.alert-events.edit` | Edit alert events. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.alert-events.read` | View alert events. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.alert.edit` | Edit alerts. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.alerts.read` | View alerts. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.api-token.edit` | Edit API tokens. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.api-token.read` | View API tokens. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.captures.edit` | Edit captures. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.captures.read` | View captures. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.custom-events.edit` | Edit custom events. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.custom-events.read` | View custom events. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.dashboard-metrics-data.read` | Read dashboard metrics. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.dashboard.edit` | Edit dashboards. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.dashboards.read` | View dashboards. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.datastream.read` | View datastreams. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.downtimes.read` | View downtimes. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.events-forwarder.read` | View events forwarding. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.explore.edit` | Modify the Explore view. | ![Checkmark icon](../images/checkmark-icon.svg) |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.explore.read` | Use the Explore view. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.file-storage-config.read` | View file storage configuration. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.global.notification-channels.read` | View global notification channels. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.groupings.edit` | Edit groups | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.groupings.read` | View groups | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.helmsrenderer.read` | Access the helm renderer. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.infrastructure.read` | Access infrastructure. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.integrations.read` | Access integrations. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.manual-integrations.edit` | Edit manual integrations. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.memberships.edit` | Edit memberships. |  |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.metrics-data.read` | View metrics data. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.metrics-descriptors.read` | View metrics descriptors. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.notification-channels.edit` | Edit notification channels. | ![Checkmark icon](../images/checkmark-icon.svg) |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.notification-channels.view` | View notification channels. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.overviews.read` | View overviews. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.promcat.integration.edit`| Edit PromCat integrations. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.promcat.integrations.read` | View PromCat integrations. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.promcat.integrations.validates` | Test to see if PromCat integrations are properly configured. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.promql-metadata.read` | View PromQL metadata. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.providers.read` | View providers. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.spotlight.read` | View Spotlight. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.sysdig-storage.read` | View service storage use. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.team.sharing.groupings.toggle` | Configure team sharing. | ![Checkmark icon](../images/checkmark-icon.svg) |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.teams.manage` | Configure teams. | ![Checkmark icon](../images/checkmark-icon.svg) |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.teams.read` | View team configurations. |  |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.token.view` | View tokens. | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.user.read` | View users. |  |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.system-role.admin` | Configure system roles. | ![Checkmark icon](../images/checkmark-icon.svg) |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| `sysdig-monitor.platform-metric.publish` `[**]` | | | | |
{: caption="Service roles and actions" caption-side="top"}

`[*]` - This service role is used when {{site.data.keyword.mon_full_notm}} is connected to an {{site.data.keyword.sysdigsecure_full_notm}} instance. This role must also be defined for {{site.data.keyword.sysdigsecure_full_notm}}. For more information about {{site.data.keyword.sysdigsecure_full_notm}} functions, see the [{{site.data.keyword.sysdigsecure_full_notm}} documentation.](/docs/workload-protection)
{: note}

`[**]` - This service role is for internal use only and will not be used in your environment.
{: note}

The `sysdig-monitor.launch.viewer` action must be assigned at a minimum to access the instance. If not assigned, an error will be returned.

An additional role of `Supertenant Metrics Publisher` is a role that you will see in IAM. This role is for internal use only and will not be used in your environment.
{: important}

## How do I know which access policies are set for me?
{: #iam_accesspolicy}

You can see which access policies are set for you in the [{{site.data.keyword.cloud_notm}} UI](https://cloud.ibm.com/){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.
4. Click the **Access groups** tab to see the access groups where you are a member. Check the policies for each group.
