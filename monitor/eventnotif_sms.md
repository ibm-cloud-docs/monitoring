---

copyright:
  years:  2021, 2022
lastupdated: "2021-12-17"

keywords: IBM Cloud, monitoring, alerts, event notification

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Sending SMS alerts by using {{site.data.keyword.en_full_notm}}
{: #eventnotif_sms}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify support staff by an SMS (Short Message Service) message about problems that might require attention. Alerts can generate notifications to the {{site.data.keyword.en_full_notm}} service to be handled as configured in that service. 
{: shortdesc}

[{{site.data.keyword.en_full_notm}} is available in a limited number of regions](/docs/event-notifications?topic=event-notifications-en-regions-endpoints). Your {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.en_full_notm}} instances must be in the same region to communicate with one another.  Because of this, support for integration with {{site.data.keyword.en_full_notm}} is limited to the regions where {{site.data.keyword.en_full_notm}} is supported and where {{site.data.keyword.mon_full_notm}} is also installed.
{: important}

SMS messages can only be sent to phone numbers in the United States and Canada.  
{: important}

{{site.data.keyword.en_full_notm}} supports message concatenation so SMS messages longer than 160 characters can be sent.  However, messages will be sent in blocks of at most 160 characters.  Multiple messages might result in additional charges to the recipient.
{: note}

For a step-by-step tutorial, see [Sending SMS notifications to {{site.data.keyword.en_full_notm}}](/docs/monitoring?topic=monitoring-tutorial-en-sms).
{: tip}

To configure 1 instance of the {{site.data.keyword.mon_full_notm}} service to send notifications to {{site.data.keyword.en_full_notm}} to be sent as an SMS message, do the following:

## Step 1. Provision an {{site.data.keyword.en_full_notm}} instance
{: #eventnotif_sms_step1}

Provision an [{{site.data.keyword.en_full_notm}} instance.](/docs/event-notifications?topic=event-notifications-en-create-en-instance)

The {{site.data.keyword.en_full_notm}} instance must be provisioned in the same region as the {{site.data.keyword.mon_short}} instance.
    
The number of events and filters that are available with {{site.data.keyword.en_full_notm}} depends on the pricing plan selected.  Review the limitations statement when creating your {{site.data.keyword.en_full_notm}} instance for [plan limitations](https://cloud.ibm.com/catalog/services/event-notifications){: external}.
{: important}

## Step 2. Define authorizations
{: #eventnotif_sms_step2}

Configure an authorization that grants {{site.data.keyword.mon_full_notm}} access to {{site.data.keyword.en_full_notm}}. Choose 1 of the following options:

- Option 1: To grant the {{site.data.keyword.mon_full_notm}} service access to the {{site.data.keyword.en_full_notm}} service, you must define an authorization where the **source service** is set to {{site.data.keyword.mon_full_notm}} and **all resources**; the **target service** is set to {{site.data.keyword.en_full_notm}} and **all resources**; and the **service access** includes both *Reader* and *Event Source Manager* access.
    
- Option 2: To grant an instance of the {{site.data.keyword.mon_full_notm}} service access to an instance of the {{site.data.keyword.en_full_notm}} service, you must define an authorization where the **source service** is set to {{site.data.keyword.mon_full_notm}} and **Resources based on selected attributes**; the **target service** is set to {{site.data.keyword.en_full_notm}} and **Resources based on selected attributes**; and the **service access** includes both *Reader* and *Event Source Manager* access.
    
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

