---

copyright:
  years:  2018, 2023
lastupdated: "2023-10-31"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

---

# Migrating to independent instances
{: #wpp-migration}

Currently, you can run {{site.data.keyword.mon_full}} and Workload Protection (also known as Sysdig Secure) concurrently on the same compute node by using an instance of IBM Cloud Monitoring that has the `Graduated Tier - Sysdig Secure + Monitor` plan (sometimes referred to as the `combined plan`). Workload Protection is now available as a standalone service under the IBM Cloud Security and Compliance brand, and the combined plan will be retired soon.

Consider migrating to the standalone service as soon as possible, preferably before the end of 2023.
{: important}

## Why migrate?
{: #wpp-migration-1}

The combined plan is slated for deprecation in the coming months.

In addition, Workload Protection is less expensive in the standalone service than in the combined plan. Migration should only take a few minutes, and can be done with no loss of existing data and no downtime in your monitoring process.

## How do I migrate?
{: #wpp-migration-2}

Complete the following steps:

1. If you do not have the latest IBM Cloud CLI, download and install it.

2. Ensure you or someone on your team has the correct access level to do the migration. You will need to assume an IAM role at the IBM Cloud platform level and another role at the service level.

    - IBM Cloud platform `Editor` role for the person who will downgrade the existing IBM Cloud Monitoring plan and to create a new Workload Protection instance.

    - IBM Cloud platform `Administrator` role for the person who will assign access to the new Workload Protection instance. Note the Administrator can also perform all Editor tasks.

    - Workload Protection service `Manager`` role for the person who will configure the new Workload Protection instance.

    For more information on managing access, see [the Workload Protection documentation](/docs/workload-protection?topic=workload-protection-getting-started).

3. From your terminal, log in to the account containing the IBM Cloud Monitoring instance you would like to migrate.

4. Downgrade your Monitoring instance to the “Graduated Tier” plan.

    - Run the following command: `ibmcloud resource service-instance-update "<monitoringinstance name here>" --service-plan-id 231bb072-1b2f-4d7e-ae9e-9574d382be32`

    The service-plan-id `231bb072-1b2f-4d7e-ae9e-9574d382be32` is plan ID for Graduated Tier and is the same for everyone.

    You can find your monitoring instance name in your Resource List found in the IBM Cloud console, or in the upper left corner of your IBM Cloud Monitoring dashboard. Next to the instance name on the Monitoring dashboard, you will find the region in parentheses. You will need this in the next step.

5. Create a new Workload Protection instance that is associated with the Monitoring instance you just downgraded:

    - Designate a resource group for the new Workload Protection instance by running the following command: `ibmcloud target -g <resource group name>`

    - You can target any resource group, but to make the instances easier to manage, you might target the group that contains your Monitoring instance.

    - To create the new instance, run this command: `ibmcloud resource service-instance-create <new instance name here> "sysdig-secure" "graduated-tier" "<region here>" -p '{"cloud_monitoring_connected_instance": "<monitoring instanceId here>"}'`

    The new instance name can be anything you like.

    The region for your new Workload Protection instance should be the same as your Monitoring instance region. It will be an abbreviation like “us-south”, “eu-de”, or “jp-tok”. You can find it in your Monitoring dashboard in parentheses next to the instance name.
    {: note}

    The parameter ‘cloud_monitoring_connected_instance’ is required to make the connection between your new Workload Protection instance and the existing IBM Cloud Monitoring instance. This allows you to run Monitoring and Workload Protection on the same target node. You can find the instanceID in the GUID field in of the response to the previous command, or as the last string in the URL for your Monitoring dashboard.

    Access privileges will not carry over to the new Workload Protection instance. Have your IBM Cloud platform administrator re-assign access.

After performing these steps, the migration process is complete and you should see a new Security and Compliance Center Workload Protection instance in the Security
section of your Resource List in the IBM Cloud Console. You can access this new instance directly from the Resource List, or from the dashboard of the downgraded Monitoring instance.

## Who do I contact if I have problems migrating?
{: #wpp-migration-3}

If you encounter issues in the migration process, please visit [IBM Cloud Support](https://cloud.ibm.com/login?redirect=%2Funifiedsupport%2Fsupportcenter){: extrenal} and open a case against “Security and Compliance Center Workload Protection”.
