---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-21"

keywords: IBM Cloud Monitoring with Sysdig

subcollection: eventstreams

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}

<!-- Name your file `at-events.md` and include it in the Reference nav group in your toc file. -->

# {{site.data.keyword.cloudaccesstrailshort}} events 
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.mon_full_notm}} service on the Standard and Enterprise plans in {{site.data.keyword.Bluemix}}. 
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.Bluemix_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started){:new_window}.

<!-- You can create different sections to group events by area. -->

## List of events
{: #events}

<!-- Make sure you introduce the table with a detailed description that immediately precedes it. For example, see https://cloud.ibm.com/docs/services/cloud-activity-tracker/services?topic=cloud-activity-tracker-cf#catalog. -->

{{site.data.keyword.mon_full_notm}} automatically generate events so that you can track activity on your service.

| Action | Description |
|:-------|:------------|
| sysdig-monitor.dashboard.create | An event is created when you create a dashboard |
| sysdig-monitor.dashboard.read   | An event is created when you load a dashboard |
| sysdig-monitor.dashboard.update | An event is created when you update a dashboard |
| sysdig-monitor.dashboard.delete | An event is created when you delete a dashboard |
| sysdig-monitor.alert.create | An event is created when you create an alert definition |
| sysdig-monitor.alert.read | An event is created when you read an alert definition |
| sysdig-monitor.alert.update | An event is created when you update an alert definition |
| sysdig-monitor.alert.delete | An event is created when you delete an alert definition |
| sysdig-monitor.capture.create | An event is created when you create a Sysdig capture |
| sysdig-monitor.capture.read | An event is created when you load a Sysdig capture in the dashboard |
| sysdig-monitor.capture.update | An event is created when you update a Sysdig capture |
| sysdig-monitor.capture.delete | An event is created when you delete a Sysdig capture |
| sysdig-monitor.team.create | An event is created when you create a Sysdig team |
| sysdig-monitor.team.read | An event is created when you view a Sysdig team definition |
| sysdig-monitor.team.update | An event is created when you update a Sysdig team definition |
| sysdig-monitor.team.delete | An event is created when you delete a Sysdig team |

## Where to view the events
{: #ui}

<!-- For example, choose one of the following two options. -->

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} location (region) where the events are generated.
