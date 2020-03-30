---

copyright:
  years:  2018, 2020
lastupdated: "2020-03-06"

keywords: Sysdig, IBM Cloud, monitoring, faq, frequently asked questions

subcollection: Sysdig

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

# FAQs
{: #faqs}

## Getting Started
{: #faqs-gs}

### I'm new to Sysdig - where should I start?
{: #faqs-gs-1}

Use the [Getting started tutorial](/docs/Monitoring-with-Sysdig?topic=Sysdig-getting-started#prereqs) to provision an instance of Sysdig, connect an agent to Sysdig and launch the web UI.  There are also a number of getting started videos on https://learn.sysdig.com/ to help you become familiar with Sysdig agents, Web UI, dashboards and alerts. Notice that these tutorials make references to sysdig.com, but the same functionality is also available within the {{site.data.keyword.mon_full_notm}} service.

### What are the Sysdig endpoints I should be using?
{: #faqs-gs-2}

You can access the Sysdig web application from the View Sysdig links on the [Observability Monitoring page](https://cloud.ibm.com/observe/monitoring).  The endpoints are also documented [here](/docs/Monitoring-with-Sysdig?topic=Sysdig-endpoints).

### Where can I see the available versions for the Sysdig agents?
{: #faqs-gs-3}

You can see the version history of the agents that are available from the [Agent Release Notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html) on the Sysdig site.

The docker containers are labelled using the release versions from the above link.  For example, if you are looking for version 0.89.5, then pull the `sysdig/agent:0.89.5` container for your deployment.

By default the agent installation instructions reference `latest` tag, but once you build the Sysdig agents into your deployment process, you should reference the agents by their version number to control which versions are being run in your production environment and plan for a regular update cadence for the agents.

### How do I know which versions of the Sysdig agent I am running?
{: #faqs-gs-4}

Using the Sysdig Spotlight, you can see the number of agents that are up to date.  Click the `View All Agents` link to see specifically which agents still need to be updated.

### Can I use Grafana to view my Sysdig metrics and dashboards?
{: #faqs-gs-5}

Yes, you can use the [grafana plugin](https://github.com/draios/grafana-sysdig-datasource) to install Sysdig's plugin into your Grafana instance.  Notice that this is a `run your own Grafana` solution and not a SaaS offering.  When you follow the instructions to configure it, you should use the [IBM Cloud Monitoring with Sysdig endpoints](/docs/Monitoring-with-Sysdig?topic=Sysdig-endpoints) and tokens.  Follow the on-premise directions where directed in the instructions since that will give you the opportunity to provide a different URL from the sysdig.com default that is otherwise assumed in the plugin documentation.


## Platform Metrics
{: #faqs-platform}

### Why don't I see any metrics for the IBM service that I'm using in Sysdig?
{: #faqs-platform-1}

Service will be enabling platform metrics on their own schedule.  To see if the service you want to use is available, please check the [Cloud Services](/docs/Monitoring-with-Sysdig?topic=Sysdig-cloud_services) and the [Cloud services by location](/docs/Monitoring-with-Sysdig?topic=Sysdig-cloud_services_locations) topics to ensure the service is enabled in the region your service instance to be monitored is running.  If the service you wish to use is listed, then the next step would be to confirm that you have a Sysdig instance created in the same region as your instance generating the metrics, and that the Sysdig instance has been [enabled for Platform Metrics](/docs/Monitoring-with-Sysdig?topic=Sysdig-platform_metrics_enabling).

### Why can't I edit the default dashboards?
{: #faqs-platform-2}

This is by design. Over time we expect that the default dashboards will change and we don't want to overwrite customizations that you might be making to the dashboards.  You can make a copy of a default dashboard by selecting `Copy dashboard` from the Options menu ( ellipsis icon ) in the top right of the dashboard.

### Why are the default dashboards showing An error occurred load data?
{: #faqs-platform-3}

When using the 10S, 1M and 10M views, Sysdig will use the 10s timeline to fetch the data.  Platform metrics are currently only available with a 1 minute granularity and thus are only visible in the 1 minute timeline.  If you see a message like `The requested metric is not available at 10 seconds granularity. Please specify a larger granularity`, then zooming out to the 1H view should reveal the metrics that you are looking for.

## Security and Access Control
{: #faqs-security}

### Why can't people on my team see my dashboards?
{: #faqs-security-1}

There are a number of dashboards available out the box for a team to use and share.  If you build a new dashboard, you must share the dashboard with members of your team for them to be able to see your dashboard.  This allows you to have your own private set of dashboards that you work on before making them available for your team to use.  To share a dashboard, from the dashboard choose the `Options` menu (ellipsis icon) in the top right and choose `Share`.  Choose the slider to share with your team.

### Can I share dashboards with people that are not part of my account?
{: #faqs-security-2}

Yes!  While viewing the dashboard choose the `Options` menu (ellipsis icon) and choose `Share`.  You will be presented with two options `Share with Team` and `Share Public URL`.  Choosing the public URL will mean that anyone with the URL will be able to view the metrics on the dashboard.  

**Just make sure you are careful not to expose any confidential information since there is no access control on these links.**
{: important}

### Is the Sysdig agent restricted in its namespace or kernel isolated?
{: #faqs-security-3}

The Sysdig agent shares the network and PID namespace of the host.  All other namespaces are private.
The agent does require mounting certain locations from the host file system in read-only mode. These are /run, /var/run, /proc, /boot, /lib/modules, /usr.
