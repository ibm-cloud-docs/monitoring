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


{:shortdesc}



Alerts form the framework for Sysdig's monitoring capabilities, notifying users when an event/issue occurs that requires their attention. The Alerts module displays a complete list of all existing alerts, as well as providing create/edit functionality for users to create their own alerts, or modify existing ones, to tailor the monitoring facility to the infrastructure's particular needs.

Host comparison alerts are also configurable for one-to-many comparisons between an individual host and its associated group.

Setting up alerts involves two basic steps:

    Prerequisite: Configure the notification channels you want to use for alert notification. 
    Configure alerts by defining an alert type, name, parameters, notification channel to be used, etc. 

When an alert notification is sent (for example, when it is triggered, marked as resolved in the web UI, or when it ceases triggering) it contains the following information:

    The name of the alert.
    The type of notification: active, resolved, or OK.
    The value of the segmentation. For example, when segmenting on host.hostName the relevant hostName will be provided.