---

copyright:
  years:  2018, 2025
lastupdated: "2025-03-03"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Sending SMS alerts using PagerDuty
{: #pd_sms}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify support staff about problems that might require attention. Using PagerDuty, these alerts can trigger SMS (short message service) messages.
{: shortdesc}

To configure SMS notification using the PagerDuty On Call Service, do the following.

1. [Configure the support user in PagerDuty who will receive SMS alert messages.](https://support.pagerduty.com/main/docs/user-profile){: external}

   Make sure a valid mobile number is provided for **SMS** in the user's **Contact Information** and that the **Notification Rules** for the user indicates that an SMS is to be sent to the mobile number.  If these items are not configured correctly, the user will not receive SMS messages.
   {: important}

2. [Configure a PagerDuty Escalation Policy](https://support.pagerduty.com/main/docs/escalation-policies#section-create-an-escalation-policy){: external} and for **Notify** specify the user configured in the previous step.

3. [After completing the prior steps, access {{site.data.keyword.mon_full_notm}} and configure an {{site.data.keyword.mon_full_notm}} notification channel that will send the desired alerts to PagerDuty.](/docs/monitoring?topic=monitoring-notifications#notifications_create)

4. [Configure an {{site.data.keyword.mon_full_notm}} alert to send to the configured notification channel.](/docs/monitoring?topic=monitoring-alerts)
