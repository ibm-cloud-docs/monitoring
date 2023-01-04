---

copyright:
  years:  2018, 2023
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, iam

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
{: caption="Table 1. IAM user roles and actions" caption-side="top"}


A user with an **administrator** role automatically has the service **manager** role permissions.
{: note}



## {{site.data.keyword.cloud_notm}} service roles
{: #iam_svcroles}

The following table identifies the service role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run the specified actions:

| Actions                                       | Manager                                           | Writer                         | Reader |
|-----------------------------------------------|---------------------------------------------------|--------------------------------|--------|
| `Reset the access key`                    | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Create, configure, and delete teams`            | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Configure and remove notifications channels`    | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Configure and remove monitoring agents`             | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |
| `Create, delete, and edit content in the monitoring UI`| ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Create and delete dashboards`                   | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Create and delete alerts`                       | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Create and delete events`                   | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Create and delete captures`                     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `Modify the scope of dashboards/panels`        | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | |
| `View metrics, dashboards, alerts, events, and captures`  | ![Checkmark icon](../images/checkmark-icon.svg)      | ![Checkmark icon](../images/checkmark-icon.svg)                    | ![Checkmark icon](../images/checkmark-icon.svg)    |
{: caption="Table 2. Service roles and actions" caption-side="top"}


## IAM actions
{: #iam_actions}

The following table identifies the IAM actions that are assigned to the platform and service roles for the {{site.data.keyword.mon_full_notm}} service:

| Role type         | Role              | IAM actions |
|-------------------|-------------------|--------------|
| Platform          | `administrator`   | `sysdig-monitor.launch.admin` </br>`sysdig-monitor.launch.user` </br>`sysdig-monitor.launch.viewer` |
| Service           | `manager`         | `sysdig-monitor.launch.admin` </br>`sysdig-monitor.launch.user` </br>`sysdig-monitor.launch.viewer` |
| Service           | `writer`          | `sysdig-monitor.launch.user` </br>`sysdig-monitor.launch.viewer` |
| Service           | `reader`          | `sysdig-monitor.launch.viewer` |
{: caption="Table 3. IAM actions assigned to platform and service roles" caption-side="top"}



## How do I know which access policies are set for me?
{: #iam_accesspolicy}

You can see which access policies are set for you in the [{{site.data.keyword.cloud_notm}} UI](https://cloud.ibm.com/){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.
4. Click the **Access groups** tab to see the access groups where you are a member. Check the policies for each group.
