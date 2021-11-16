---

copyright:
  years:  2021
lastupdated: "2021-11-15"

keywords: IBM Cloud, monitoring, alerts, event notification

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Sending alerts using {{site.data.keyword.en_full_notm}}
{: #eventnotif}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify support staff about problems that might require attention. Alerts can generate notifications to the {{site.data.keyword.en_full_notm}} service to be handled as configured in that service. 
{: shortdesc}

[{{site.data.keyword.en_full_notm}} is available in a limited number of regions](/docs/event-notifications?topic=event-notifications-en-regions-endpoints). Your {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.en_full_notm}} instances must be in the same region to communicate with one another.  Because of this, support for integration with {{site.data.keyword.en_full_notm}} is limited to the regions where {{site.data.keyword.en_full_notm}} is supported and where {{site.data.keyword.mon_full_notm}} is also installed.
{: important}

To configure 1 instance of the {{site.data.keyword.mon_full_notm}} service to send notifications to {{site.data.keyword.en_full_notm}}, do the following:

1. Create an [{{site.data.keyword.en_full_notm}} service instance.](/docs/event-notifications?topic=event-notifications-en-create-en-instance)

    The {{site.data.keyword.en_full_notm}} instance must be provisioned in the same region as the {{site.data.keyword.mon_short}} instance.
    
    The number of events and filters that are available with {{site.data.keyword.en_full_notm}} depends on the pricing plan selected.  Review the limitations statement when creating your {{site.data.keyword.en_full_notm}} instance for [plan limitations](https://cloud.ibm.com/catalog/services/event-notifications){: external}.
    {: important}

2. Configure an authorization that grants {{site.data.keyword.mon_full_notm}} access to {{site.data.keyword.en_full_notm}}. 

    To grant the {{site.data.keyword.mon_full_notm}} service access to the {{site.data.keyword.en_full_notm}} service, you must define an authorization where the **source service** is set to {{site.data.keyword.mon_full_notm}} and **all resources**; the **target service** is set to {{site.data.keyword.en_full_notm}} and **all resources**; and the **service access** includes both *Reader* and *Event Source Manager* access.
    
    To grant an instance of the {{site.data.keyword.mon_full_notm}} service access to an instance of the {{site.data.keyword.en_full_notm}} service, you must define an authorization where the **source service** is set to {{site.data.keyword.mon_full_notm}} and **Resources based on selected attributes**; the **target service** is set to {{site.data.keyword.en_full_notm}} and **Resources based on selected attributes**; and the **service access** includes both *Reader* and *Event Source Manager* access.
    
    For more information on how to define authorizations, see [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth&interface=ui).

3. [Configure a notification channel of type {{site.data.keyword.en_full_notm}}](/docs/event-notifications?topic=event-notifications-en-create-en-source).

    When you configure the channel, a source, with the same name as your {{site.data.keyword.mon_short}} instance instance name, is automatically added to your {{site.data.keyword.en_full_notm}} instance. You can view it in the {{site.data.keyword.en_full_notm}} UI, in the *Sources* section.

4. Create an [{{site.data.keyword.en_full_notm}} topic in your service instance](/docs/event-notifications?topic=event-notifications-en-create-en-topic).

5. Create an [{{site.data.keyword.en_full_notm}} destination in your service instance](/docs/event-notifications?topic=event-notifications-en-create-en-destination).

6. Create an [{{site.data.keyword.en_full_notm}} subscription in your service instance.](/docs/event-notifications?topic=event-notifications-en-create-en-destination)

Next, verify the setup. [Configure a {{site.data.keyword.mon_short}} alert to send to the configured notification channel](/docs/monitoring?topic=monitoring-alerts).

