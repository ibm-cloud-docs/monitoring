---

copyright:
  years:  2021, 2023
lastupdated: "2024-01-17"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Sending SMS alerts by using {{site.data.keyword.en_full_notm}}
{: #eventnotif_sms}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify support staff by an SMS (Short Message Service) message about problems that might require attention. Alerts can generate notifications to the {{site.data.keyword.en_full_notm}} service to be handled as configured in that service.
{: shortdesc}

Your {{site.data.keyword.mon_full_notm}} instances can send events to {{site.data.keyword.en_full_notm}} instances in the same accoount and in other accounts. [{{site.data.keyword.en_full_notm}} is available in a limited number of regions](/docs/event-notifications?topic=event-notifications-en-regions-endpoints).
{: important}

SMS messages can only be sent to phone numbers in the United States and Canada.
{: important}

{{site.data.keyword.en_full_notm}} supports message concatenation so SMS messages longer than 160 characters can be sent.  However, messages will be sent in blocks of at most 160 characters.  Multiple messages might result in additional charges to the recipient.
{: note}

{{site.data.keyword.en_full_notm}} supports a number of different destinations. This example describes sending an SMS message. For information on additional possible destinations, see the [{{site.data.keyword.en_full_notm}} documentation](/docs/event-notifications?topic=event-notifications-en-destination).
{: note}

For a step-by-step tutorial, see [Sending SMS notifications to {{site.data.keyword.en_full_notm}}](/docs/monitoring?topic=monitoring-tutorial-en-sms).
{: tip}

To configure 1 instance of the {{site.data.keyword.mon_full_notm}} service to send notifications to {{site.data.keyword.en_full_notm}} to be sent as an SMS message, do the following:

## Step 1. Provision an {{site.data.keyword.en_full_notm}} instance
{: #eventnotif_sms_step1}

Provision an [{{site.data.keyword.en_full_notm}} instance.](/docs/event-notifications?topic=event-notifications-en-create-en-instance)

The {{site.data.keyword.en_full_notm}} instance must be provisioned in the same account or ina different account as the {{site.data.keyword.mon_short}} instance.

The number of events and filters that are available with {{site.data.keyword.en_full_notm}} depends on the pricing plan selected.  Review the limitations statement when creating your {{site.data.keyword.en_full_notm}} instance for [plan limitations](https://cloud.ibm.com/catalog/services/event-notifications){: external}.
{: important}

## Step 2. Define authorizations
{: #eventnotif_sms_step2}

Configure an authorization that grants {{site.data.keyword.mon_full_notm}} access to {{site.data.keyword.en_full_notm}}.

When both service instances are in the same account, choose 1 of the following options:

- Option 1: To grant the {{site.data.keyword.mon_full_notm}} service access to the {{site.data.keyword.en_full_notm}} service, you must define an authorization where the **source service** is set to {{site.data.keyword.mon_full_notm}} and **all resources**; the **target service** is set to {{site.data.keyword.en_full_notm}} and **all resources**; and the **service access** includes both *Reader* and *Event Source Manager* access.

- Option 2: To grant an instance of the {{site.data.keyword.mon_full_notm}} service access to an instance of the {{site.data.keyword.en_full_notm}} service, you must define an authorization where the **source service** is set to {{site.data.keyword.mon_full_notm}} and **Resources based on selected attributes**; the **target service** is set to {{site.data.keyword.en_full_notm}} and **Resources based on selected attributes**; and the **service access** includes both *Reader* and *Event Source Manager* access.

When both service instances are in the different accounts, define an authorization in the account that hosts the {{site.data.keyword.en_full_notm}} service:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source account.

    If the source service that needs access to the target service is in this account, select **This account**.

    If the source service that needs access to the target service is in a different account, select **Other account**. Then, enter the account ID of the source account.

4. Select {{site.data.keyword.mon_full_notm}} as the source service. Then, set the scope of the access to **All resources**.

5. Select {{site.data.keyword.en_full_notm}} as the target service. Then, set the scope of the access to **All resources** or a single instance by configuring **Resources based on selected attributes** &gt; **Service Instance**.

    Other attributes are not supported for this type of authorization.

6. In the *Service Access* section, include both *Reader* and *Event Source Manager* access.

7. Click **Authorize**.

If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account number. 
{: note}

For more information on how to define authorizations, see [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth&interface=ui).

## Step 3. Configure the {{site.data.keyword.en_full_notm}} instance
{: #eventnotif_sms_step3}

1. [Configure a notification channel of type {{site.data.keyword.en_full_notm}}](/docs/event-notifications?topic=event-notifications-en-create-en-source).

    When you configure the channel, a source, with the same name as your {{site.data.keyword.mon_short}} instance instance name, is automatically added to your {{site.data.keyword.en_full_notm}} instance. You can view it in the {{site.data.keyword.en_full_notm}} UI, in the *Sources* section.

2. Create an [{{site.data.keyword.en_full_notm}} topic](/docs/event-notifications?topic=event-notifications-en-create-en-topic).

5. Create an [{{site.data.keyword.en_full_notm}} destination](/docs/event-notifications?topic=event-notifications-en-create-en-destination).

6. Create an [{{site.data.keyword.en_full_notm}} subscription](/docs/event-notifications?topic=event-notifications-en-create-en-subscription).

    For **Destination** specify, `IBM Cloud SMS service`.

## Next steps
{: #eventnotif_sms_step4}

Next, verify the setup. [Configure a {{site.data.keyword.mon_short}} alert to send to the configured notification channel](/docs/monitoring?topic=monitoring-alerts).
