---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

keywords: Sysdig, IBM Cloud, monitoring, Sysdig agent, event filters

subcollection: Monitoring-with-Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Filtering events by severity
{: #agent_events_level}

When you delete an {{site.data.keyword.mon_full_notm}} instance, or if you want to stop collecting metrics from a source, you must uninstall the Sysdig agent from sources where it was installed as a service. If you deployed a Sysdig agent as a container, you must run docker commands to remove the agent.
{:shortdesc}




## Filtering events by severity
{: #severity}

To filter events by severity, you can also change the log entry type for events in the *dragent.yaml* file. 

The default log level is **information**. This means that only warning and higher severity events are transmitted.

Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*. **Note**: The values are listed from high priority to low priority.

For example, to filter out low severity events (*notice*, *information*, *debug*), you must set the log section **event_priority** to *warning*:

```
log:
  event_priority: warning
```
{: codeblock}


To block collection of events, you must set the log section **event_priority** to *none*:

```
log:
  event_priority: none
```
{: codeblock}




### Filtering Kubernetes events by severity
{: #change_kube_agent_event_filterby_severity}

* The **event_priority** in the **log** section controls the type of events that are sent from the agent
* The default log level is *information*. This means that only information and higher severity events are transmitted.
* Valid levels are: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* and *none*. **Note**: The values are listed from high priority to low priority.
* Setting the level to `none` will block all event collection.

