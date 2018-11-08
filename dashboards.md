---

copyright:
  years: 2018
lastupdated: "2018-11-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Working with dashboards
{: #dashboards}
You can use any of the pre-defined dashboards to monitor your infrastructure. You can also create custom dashboards.
{:shortdesc}

Once the agent has started sending metrics to Sysdig for your environment, you can use the Sysdig Monitor UI to view and analyze that data. This doc will help you understand the UI and various scenarios compared to Grafana.



## Pre-defined dashboards
{: #predefined}

Sysdig provides a number of pre-built dashboards, designed around various supported applications, network topologies, infrastructure layouts, and services. These can be used to jumpstart the dashboard building process, as templates for further configuration.

Pre-built dashboards come with a series of panels already configured, based on the information most relevant users.

| Type | Description | More information | 
|------|-------------|------------------|
| Applications | Dashboards that you can use to monitor your applications and infrastructure components.  | [Application dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#applications) |
| Host and containers | Dashboards that you can use to monitor resource utilization and system activity on your hosts and in your containers. | [Host and container dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#host_container) |
| Network | Dashboards that you can use to monitor your network connections and activity. | [Network dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#network) |
| Service | Dashboards that you can use to monitor the performance of your services, even if those services are deployed in orchestrated containers. | [Service dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#service) |
| Topology | Dashboards that you can use to monitor the logical dependencies of your application tiers and overlay metrics. | [Topology dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#topology) |
{: caption="Table 1. List of pre-defined dashboards" caption-side="top"} 


## Custom dashboards
{: #custom}

create customized dashboards to display the most useful/relevant views and metrics for the infrastructure in a single location. Each dashboard is comprised of a series of panels configured to display specific data in a number of different formats:


## Programmatic dashboard operations
{: #programmatic}


