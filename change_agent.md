---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Filtering data by editing the Sysdig agent configuration file
{: #change_agent}

After you provision an instance of the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{:shortdesc}


Out of the box, the Sysdig agent will gather and report on a wide variety of pre-defined metrics. It can also accommodate any number of custom parameters for additional metrics collection. 

Use this section when you need to change the default or pre-defined settings by editing the agent configuration files, or for other special circumstances. 

Integrations also require editing the agent config files.
By default, the Sysdig agent is configured to collect metric data from a range of platforms and applications. You can edit the agent config files to extend the default behavior, including additional metrics for JMX, StatsD, Prometheus, or a wide range of other applications.  You can also monitor log files for targeted text strings.

Another way of filtering data is by configuring the Sysdig agent to include or exclude data.

## Filtering event data
{: #event_data}

Sysdig Monitor supports event integrations with certain applications by default. The Sysdig agent will automatically discover these services and begin collecting event data from them.

The following applications are currently supported:

    Docker
    Kubernetes

Other methods of ingesting custom events into Sysdig Monitor are touched upon in Custom Events.

By default, only a limited set of events is collected for a supported application, and are listed in the agent's default settings configuration file (/opt/draios/etc/dragent.default.yaml).

To enable collecting other supported events, add an events entry to dragent.yaml.

You can also change log entry in dragent.yaml to filter events by severity. 

[Docker events](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents)

[Kubernetes events](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents)

[Enable/Disable Events Collection with events Parameter](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-Enable/DisableEventsCollectionwitheventsParameter)

[Change Event Collection by Severity with log Parameter](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-ChangeEventCollectionbySeveritywithlogParameter)

## Filtering custom metrics
{: #custom_metrics}

It is possible to filter custom metrics in the following ways: 

    Ability to include/exclude custom metrics using configurable patterns,
    Ability to log which custom metrics are exceeding limits

After you identify those key custom metrics that must be received, use the new 'include' and 'exclude' filtering parameters to make sure you receive them before the metrics limit is hit.

## Filtering designated containers
{: #containers}


## Changing the log level
{: #log_level}


## Agent auto-config
{: #auto_config}

Agent Auto-Config: Describes how to use the Sysdig REST APIs and Python client wrappers to auto-orchestrate changes to all agents in an environment, in the (rare) situation in which a standard orchestration tool such as Kubernetes, Chef, or Ansible is not being used. 