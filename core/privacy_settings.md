---

copyright:
  years:  2018, 2026
lastupdated: "2026-09-29"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Managing access for {{site.data.keyword.mon_full_notm}} support by configuring privacy settings
{: #privacy_settings}

{{site.data.keyword.cloud_notm}} support might need to access your environment to troubleshoot a support case.
You can use privacy settings to control how {{site.data.keyword.mon_full_notm}} support accesses your environment, in addition to the platform and service access controls that are already available. 
{: shortdesc}


## Before you begin 
{: #privacy_settings_prereq}

* You must have the administrator role to configure support account access and grant or revoke temporary access for support engineers at any time.


## Launching the privacy settings panel
{: #privacy_settings_launch} 

Complete the following steps to launch the *Privacy settings* panel in an {{site.data.keyword.cloud_notm}} instance:

1. [Launch the web UI](/docs/monitoring?topic=monitoring-launch#launch).

2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Click **Privacy Settings**.

The privacy settings panel opens.


## Managing the IBM Cloud support account setting
{: #privacy_settings_1}

**Allow IBM Cloud Support Account** allow IBM to access your data using a support account in your environment. The account will be called IBM Cloud Support and will appear initially with the **View Only** role in the default team. You can manage or remove it any time.

When you toggle **Allow IBM Cloud Support Account**, IBM creates an account named **IBM Support** and adds it to your default team with the **View Only** access. You can change the account’s role, remove it, or select **View User** to see its details at any time.
{: #note}


## Managing the Allow User Temporary Access Settings
{: #privacy_settings_2}

**Allow User Temporary Access** allows IBM Cloud support engineers to access your data for a fixed duration (max 30 days). The access ends automatically when the timer expires.

Select a duration from the list. The remaining time counts down untill the access expires. To extend access, select a duration and click **Save** again. You can extend access upto 30 days in total. 

You can revoke the access
{: #note}
