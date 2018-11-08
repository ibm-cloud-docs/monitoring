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

Use dashboards to monitor your infrastructure, applications, and services. You can use pre-defined dashboards. You can also create custom dashboards through the Web UI or programmatically.
{:shortdesc}

A **dashboard** shows groups of metrics that report on the health, performance, and state of your infrastructure, applications, and services for a single host or a group of hosts. Dashboards offer a specialized insight into network data, application data, topology, services, hosts, and containers.

In the **DASHBOARDS** section of the Web UI, dashboards are organized into three main groups:

* *My Dashboards*: These are the dashboards that are created by the user who is currently logged in.
* *My Shared Dashboards*: These are the dashboards that are created by the user who is currently logged in, and that are shared with other users.
* *Dashboards Shared With Me*: These are the dashboards that are created by other users, and shared with the current user.

In the **EXPLORE** section of the Web UI, dashboards are organized into two groups:
* *Default dashboards*: These are the pre-defined dashboards.
* *My Dashboards*: These are the dashboards that are created by the user who is currently logged in.

 

## Pre-defined dashboards
{: #predefined}

Pre-defined dashboards are designed around various supported applications, network topologies, infrastructure layouts, and services. 

Pre-defined dashboards include a series of panels that are already configured.

The following table lists the different types of pre-defined dashboards:

| Type | Description | More information | 
|------|-------------|------------------|
| Applications | Dashboards that you can use to monitor your applications and infrastructure components.  | [Application dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#applications) |
| Host and containers | Dashboards that you can use to monitor resource utilization and system activity on your hosts and in your containers. | [Host and container dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#host_container) |
| Network | Dashboards that you can use to monitor your network connections and activity. | [Network dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#network) |
| Service | Dashboards that you can use to monitor the performance of your services, even if those services are deployed in orchestrated containers. | [Service dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#service) |
| Topology | Dashboards that you can use to monitor the logical dependencies of your application tiers and overlay metrics. | [Topology dashboards](/docs/services/Monitoring-with-Sysdig/default_dashboards.html#topology) |
{: caption="Table 1. List of pre-defined dashboards" caption-side="top"} 


## Creating custom dashboards through the Web UI
{: #custom_ui}

When you create a custom dashboard, you can start from a template such as a pre-defined dashboard, or choose a blank dashboard. A dashboard includes panels that are configured to display specific data in a number of different formats. You also set how data is aggregated. The **scope** defines what data is used for aggregation and displayed. You can set the scope at a dashboard level, or override for individual panels. 

Complete the following steps to create a custom dashboard:

1. From the *DASHBOARD** section in the Web UI, select **Add Dashboard**. The *Create a New Dashboard* page opens.

    * Select a pre-defined dashboard or choose the *Blank Dashboard*. 

    * Enter a name for your dashboard.

    * Click **Create Dashboard**.

2. Set the dashboard scope. Click **Edit Scope** to change the default scope. By default, **Everywhere** is selected.
    
    * Select the scope. 

    * Optionally, click **Override the custom panel scopes** to override the scope for all panels which currently have a custom scope defined. **Note: This action cannot be undone.** 

    **Note:** To reset the dashboard scope to the entire infrastructure, or to update an existing dashboard's scope to the entire infrastructure, select **Everywhere**.

    * Click **Save**.

3. Configure panels. Repeat this step for any of the panels in the dashboard that you want to modify.

    1. Identify the panel that you want to modify.

    2. Select **Edit Panel**. This is the pencil icon.
    
    3. Change the a chart type.

    4. Change the metric, and rate. Rate defines the type of aggregation that is done to the data.

    5. Change the scope of the panel. Click **Override Dashboard Scope**. Then, change the scope. If you need to restore the dashboard scope to the panel, select **Default to Dashboard Scope**.

    6. In the *Compare to* field, click **Configure**. Set the time range for the comparison.

    7. Set the panel background color based on metric thresholds. Click **Override Color Coding**, then, **Enable**. Set values for the different thresholds.

    8. Click **Save**.



## Working with dashboards programmatically
{: #programmatically}



