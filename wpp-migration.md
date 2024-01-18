---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-09"


keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# Migrating to independent instances
{: #wpp-migration}

Currently, you can run {{site.data.keyword.mon_full}} and {{site.data.keyword.sysdigsecure_short}} (also known as Sysdig Secure) concurrently on the same compute node by using an instance of {{site.data.keyword.mon_full_notm}} that has the `Graduated Tier - Sysdig Secure + Monitor` plan (sometimes referred to as the `combined plan`). {{site.data.keyword.sysdigsecure_short}} is now available as a standalone service as {{site.data.keyword.sysdigsecure_full_notm}}, and the {{site.data.keyword.mon_full_notm}} combined plan will be retired soon.

{{site.data.content.combined-plan-deprecated}}

Consider migrating to the standalone service as soon as possible.
{: important}

## Why migrate?
{: #wpp-migration-1}

The combined plan is planned to be deprecated in the coming months.

In addition, {{site.data.keyword.sysdigsecure_full_notm}} is less expensive than the {{site.data.keyword.mon_full_notm}} combined plan. Migration should only take a few minutes, and can be done with no loss of existing data and no downtime in your monitoring process.

## How do I migrate?
{: #wpp-migration-2}

Complete the following steps:

1. If you do not have the latest IBM Cloud CLI, [download and install it.](/docs/cli?topic=cli-install-ibmcloud-cli)

2. Ensure you or someone on your team has the correct access level to do the migration. You will need to have an IAM role at the IBM Cloud platform level and another role at the service level.

    - The IBM Cloud platform `Editor` role is required for the person who will downgrade the existing {{site.data.keyword.mon_full_notm}} plan and create a new {{site.data.keyword.sysdigsecure_short}} instance.

    - The IBM Cloud platform `Administrator` role is required for the person who will assign access to the new {{site.data.keyword.sysdigsecure_short}} instance. Note the `Administrator` can also perform all `Editor` tasks.

    - The {{site.data.keyword.sysdigsecure_short}} service `Manager` role for the person who will configure the new {{site.data.keyword.sysdigsecure_short}} instance.

    For more information about managing access, see [the Workload Protection documentation](/docs/workload-protection?topic=workload-protection-getting-started).

3. From your terminal, log in to the account containing the {{site.data.keyword.mon_full_notm}} instance you would like to migrate.

4. Downgrade your {{site.data.keyword.mon_full_notm}} instance to the `Graduated Tier` plan by running the following command: `ibmcloud resource service-instance-update "<monitoring instance name>" --service-plan-id 231bb072-1b2f-4d7e-ae9e-9574d382be32`

   The service-plan-id `231bb072-1b2f-4d7e-ae9e-9574d382be32` is plan ID for `Graduated Tier` and is the same for everyone.

   You can find your {{site.data.keyword.mon_short}} instance name in your Resource List found in the {{site.data.keyword.cloud_notm}} console, or in the upper left corner of your {{site.data.keyword.mon_full_notm}} dashboard. Next to the instance name on the {{site.data.keyword.mon_short}} dashboard, you will find the region in parentheses. You will need this in the next step.

5. Create a new {{site.data.keyword.sysdigsecure_short}} instance that is associated with the {{site.data.keyword.mon_short}} instance you downgraded in the previous step:

    1. Designate a resource group for the new {{site.data.keyword.sysdigsecure_short}} instance by running the following command: `ibmcloud target -g <resource group name>`

      You can target any resource group, but to make the instances easier to manage, you can target the group that contains your {{site.data.keyword.mon_short}} instance.

    2. To create the new instance, run the following command: `ibmcloud resource service-instance-create <new instance name> "sysdig-secure" "graduated-tier" "<region>" -p '{"cloud_monitoring_connected_instance": "<monitoring instanceID>"}'`

       The new instance name can be any string.

       The region for your new {{site.data.keyword.sysdigsecure_short}} instance should be the same as your {{site.data.keyword.mon_short}} instance region. The region will be an abbreviation such as “us-south”, “eu-de”, or “jp-tok”. You can find the region in your {{site.data.keyword.mon_short}} dashboard in parentheses next to the instance name.
       {: note}

       The parameter `cloud_monitoring_connected_instance` is required to make the connection between your new {{site.data.keyword.sysdigsecure_short}} instance and the existing {{site.data.keyword.mon_full_notm}} instance. This parameter allows you to run {{site.data.keyword.mon_short}} and {{site.data.keyword.mon_short}} on the same target node. You can find the instanceID in the GUID field in of the response to the `service-instance-update` command, or as the last string in the URL for your {{site.data.keyword.mon_short}} dashboard.

    Access privileges will not be migrated to the new {{site.data.keyword.sysdigsecure_short}} instance. Your {{site.data.keyword.cloud_notm}} platform administrator will need to assign access for the new {{site.data.keyword.sysdigsecure_short}} instance.

    Existing agent configurations will continue to work after the migration of instances has been completed.

After performing these steps, the migration process is complete and you should see a new {{site.data.keyword.sysdigsecure_full_notm}} instance in the Security
section of your Resource List in the {{site.data.keyword.cloud_notm}} Console. You can access the new instance directly from the Resource List, or from the dashboard of the downgraded {{site.data.keyword.mon_short}} instance.

## Who do I contact if I have problems migrating?
{: #wpp-migration-3}

If you encounter problems in the migration process, go to [IBM Cloud Support](https://cloud.ibm.com/login?redirect=%2Funifiedsupport%2Fsupportcenter){: external} and open a case against “Security and Compliance Center Workload Protection”.
