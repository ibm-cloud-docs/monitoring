---

copyright:
  years:  2018, 2024
lastupdated: "2024-01-11"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Silencing alerts
{: #alert-silence}

{{site.data.keyword.mon_full_notm}} helps to reduce noise and alert fatigue with *Silence Rules*. Silences Rules temporarily mute alert notifications that might result from maintenance activities, scheduled downtime, or known issues. Alerts that are silenced by scope or by alert will still trigger but alert notifications to the notification channels will not be sent.
{: shortdesc}

## Configuring a silence rule
{: #alert-silence-config}

You can silence alert notifications in two ways.

By scope
:   For instance, configuring a silence on the `region=us-east` scope will silence all alerts in the `us-east` region.

By alert
:   Silence can be configured for one or more alerts. Silencing the `Datacenter Down` alert instead of the `region=us-east` scope allows other alerts within the scope to continue notifying.

You can also configure a silence definition to include both a scope and alert.

Silence Rules can be triggered immediately or scheduled for the future. This provides the flexibility to plan ahead and avoid unnecessary disruptions.

Additionally, you can send an optional `info` message to a notification channel to keep teams updated on when a Silence starts and ends.

To configure a Silence Rule:

1. From the *Alert* section of the UI, select **Silence**. All existing silence definitions are displayed.

2. Click **Set a Silence**.

3. Specify the following:

   Name: Specify a name to identify the silence.

   Silence Criteria: Create a silence by alert, scope, or both.

      By Scope: Specify the entity you want to apply the scope as. For example, a particular workload or namespace.

      By Alert: Specify the alert you want to mute.

   Begins: Specify one of the following for when alerts are to be silenced: `Today`, `Tomorrow`, `Pick Another Day`. Select the time from the drop-down.

   Duration: Specify how long notifications should be muted in minutes, hours, or days.

   Notify: Select a [notification channel](/docs/monitoring?topic=monitoring-notifications) you want to notify about the silence.

   If no notification channels are configured, the **Notify** list will be empty.
   {: note}

4. Click **Save**.

## Silencing alerts from the alerts page
{: #alert-silence-alerts}

You can also silence an alert directly from the **Alerts** page. For more information, see [Silence an alert](/docs/monitoring?topic=monitoring-alert-silence).


## Silencing alert notifications from **Events**
{: #alert-silence-event}

You can also silence alerts from the **Events** page. On the **Events** page, find the alert event created when an alert is triggered. From the alert event, you can configure the silence rule to include both the scope and the alert that generated the event.

When an alert is silenced, it will not send notifications to your configured notification channels, but it will still generate alert events. These events will include information indicating that the alert was triggered during an active silence.
{: important}

Uou can review the event history to see when the alert was silenced and when it resumed normal notifications. This helps provide visibility into what happened during the silence and can help with troubleshooting any issues that may arise.

Alerts without a notification channel won’t be marked as silenced, and won’t have the crossed bell icon or option to silence events in the events feed.
{: note}


## Managing silence rules
{: #alert-silence-manage}

Silences can be managed individually, or as a group, by using the checkboxes on the left side of the Silence page. You can select a group of silences to delete multiple silences. You can select individual silences to enable, disable, copy or edit them.

### Enabling or disabling a silence
{: #alert-silence-enable}

Enable or disable a silence by sliding the state slider next to the silence. Active Silences include both running silences and scheduled silences.

Completed silences cannot be re-enabled, but can be duplicated with a new silence period.
{: note}

### Duplicating a silence rule
{: #alert-silence-copy}

To duplicate a silence rule, click the Duplicate icon on the menu. You can then modify the copied rule as needed.

### Finding a configured silence rule
{: #alert-silence-search}

Search silences by name using the search bar. Silence Rules can also be filtered by `Active`, `Scheduled`, or `Completed`.

### Editing a silence rule
{: #alert-silence-edit}

Scheduled silence rules can be edited before they begin.

Active silences can only be extended or disabled. If a notification channel was configured for the silence rule, the channel will be updated accordingly.


