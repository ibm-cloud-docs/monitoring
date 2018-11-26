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


# Working with events
{: #events}

The Events module displays a complete list of events that have occurred within the environment, allowing users to review, track, and resolve issues.
{:shortdesc}



There are two primary types of events displayed in the Events module: alert events, and custom events.


## Alert Events
{: #alert}

Alert events are events triggered by user-configured alerts. For more information on configuring alerts, refer to the Alerts documentation.




## Custom Events
{: #custom}

Custom events include infrastructure-based events (for example, Docker and Kubernetes), and other events configured by the user through integrations.
Infrastructure-Based Events

Infrastructure-based events are pulled from infrastructure components. Sysdig currently supports infrastructure-based events from the following components:

    Docker
    Kubernetes

The Sysdig agent will automatically discover these services and begin collecting event data from them. The agent is configured by default to collect a select group of events automatically; others can be added by editing the agent configuration file.
