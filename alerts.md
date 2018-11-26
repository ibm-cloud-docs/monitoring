---

copyright:
  years: 2018
lastupdated: "2018-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Working with alerts
{: #alerts}

You can use alerts to notify users of problems that require attention. 
{:shortdesc}

The *Alerts* section in the web UI shows the list of pre-defined alerts. From this view, you can enable and disable pre-defined alerts; you can modify existing alerts; and you can create new alerts.
 



## Customizing the Alerts view
{: #customize}

You can configure the table columns that are displayed in the *Alerts* view.

Complete the following steps to customize the table:

1. Navigate to the *ALERTS* section in the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/services/Monitoring-with-Sysdig/launch.html#launch).
2. Click the actions icon ![three dots icon](images/actions.png). The **Table columns configuration** view opens.
3. Check the columns that you want to show. Valid options are: *Name*, *Scope*, *Alert When*, *Segment By*, *Notifications*, *Enabled*, *Modified*, *Captures*, *Channels*, *Created*, *Description*, *Email recipients*, *For at least*, *OpsGenie*, *PagerDuty*, *Severity*, *Slack*, *WebHook*, *SNS topics*, *Type*, *VictorOps*
4. Click **Apply** to save the changes. 

    *Note*: You can click *Restore* to go back to the original configuration.
    


## Configuring an alert
{: #configure}


Complete the following steps to to create an alert or modify an existing alert:

1. Navigate to the *ALERTS* section in the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/services/Monitoring-with-Sysdig/launch.html#launch).

2. Click **Add alert** to launch the *Alerts* wizard. 
3. Choose an alert type.

    | Alert type         | Description |
    |-------------------|-------------|
    | Anomaly Detection | Use to monitor hosts based on their historical behaviors, and alert when they deviate. |
    | Downtime          | Use to monitor any type of entity, for example, host, container, process, or service, and alert when the entity goes down. |
    | Event             | Use to monitor occurrences of specific events, and alert if the total number of occurrences violates a threshold. For example, you can use it to alert on restarts and deployments of containers, orchestrations, and service events.|
    | Group Outlier     | Use to monitor a group of hosts and be notified when one acts differently from the rest. |
    | Metric            | Use to monitor time series metrics, and alert if they violate user-defined thresholds. |
    {: caption="Table 1. Alert types" caption-side="top"} 

    **Note:** When you edit an existing alert, you cannot change the alert type.

4. Configure the alert name and severity.

    1. Enter a name for the alert. Click **New ...**.

    2. Enter a description for the alert. Click **Insert alert description**.

    3. Choose the severity of the alert. Valid values are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *informational*, debug* The default value is *warning*.

5. In the *Define* section, configure the rule and threshold for the alert to be triggered.

    1. Define the alert, by configuring what the alert should look for, the scope of the alert, and the boundaries for triggering the alert.

Configure the notification channels that you want to use for this alert. 

6. In the *Notify* section, select the notification channels. whether a notification should be sent every 30 minutes if the issue remains unresolved, and the format of the message.

7. (Optional) In the *Act* section, enable Sysdig captures for this alerts. Sysdig capture files are not available for event alerts.

 8. Click the Create or Save button to save the alert.


## Enabling an alert
{: #enable}

Alerts can be enabled or disabled using the customization bar:

    From the Alerts module, check the boxes beside the relevant alert/s.

    Click the Enable button or the Disable button as necessary.

## Disabling an alert
{: #disable}

Alerts can be enabled or disabled using the customization bar:

    From the Alerts module, check the boxes beside the relevant alert/s.

    Click the Enable button or the Disable button as necessary.



## Search for an alert
{: #search}

Search for an Alert

The Alerts table can be searched using partial or full strings. For example, the search below displays only events that contain kubernetes:

## Edit an Existing Alert

To edit an existing alert:

    Click the checkbox beside the alert:


    Click the Edit button on the customization bar:


    Edit the alert, and click the Save button to confirm the changes.

## Copy an Alert

Alerts can be copied within the current team to allow for similar alerts to be created quickly, or copied to a different team to share alerts.
Copy an Alert to the same team

To copy an alert within the current team:

    Click the checkbox beside the alert to be copied.
    Click the Copy button on the customization bar:


    Check that the Current Team option is selected.
    Rename the alert, and click the Copy and Open button to save the changes.

## Copy an Alert to a Different Team

To copy an alert within the current team:

    Click the checkbox beside the alert to be copied.
    Click the Copy button on the customization bar:


    Select the Other Team(s) option.
    Open the Select Team drop-down menu, and click the checkbox beside the team/s that the alert should be copied to:


    Rename the alert, and click the Send Copy button to save the changes.

## Export Alert JSON

A JSON file can be exported to a local machine, containing JSON snippets for each selected alert:

    Click the checkbox/es beside the relevant alert/s to be exported.
    Click the Export JSON button on the customization bar:


## Creating an alert by using the Sysdig API
{: #api} 

Sysdig Monitor also allows for alerts to be created via the Sysdig API. For more information, refer to the API Alerts documentation.