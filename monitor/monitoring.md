---

copyright:
  years:  2018, 2023
lastupdated: "2022-03-12"

keywords: IBM Cloud, monitoring

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Viewing metrics
{: #monitoring}

Through the {{site.data.keyword.mon_short}} UI, you can analyze data in the *Advisor* tab, the *Explore* tab, and in the *Dashboard* tab. You monitor the data through metric views and dashboards.
{: shortdesc}

Consider the following information when monitoring your data:
* In the *Explorer* tab, you can monitor individual metrics.
* In the *Advisor* tab, you can monitor Kubernetes or host level metrics.

    This tab is only available for users that belong to a team that has access to monitor Kubernetes or host level metrics.
    {: note}

* In the *Dashboard* tab, you can monitor through panels predefined dashboards or custom ones and get a specialized insight into network data, application data, topology, services, hosts, and containers. A panel displays a metric or group of metrics in a dashboard.


For each metric view and dashboard, you can define the scope of the data, how to aggregate data, and what time and group filters to apply to the data. For more information, see [Managing panels](/docs/monitoring?topic=monitoring-panels).


You can configure a dashboard as the default entry point for a team, unifying a team's experience, and allowing users to focus their immediate attention on the most relevant information for them.
{: tip}


## Advisor
{: #monitoring_advisor}

In the *Advisor* tab, you can monitor and troubleshoot the health, risk, and capacity of hosts and Kubernetes clusters.

![Advisor tab](../images/advisor-tab.png "Advisor tab")

- Data is refreshed every 10 minutes.
- Metrics are prioritized by event count and severity.
- For more information, see [Advisor](https://docs.sysdig.com/en/docs/sysdig-monitor/advisor/){: external}.

In the *Advisor* section, you can choose to monitor your Kubernetes clusters by cluster, by node, by namespace, or by workload. Each option offers a set of predefined dashboards that you can use to monitor the health of your resources. You can also select to monitor by host.

### Monitoring Kubernetes clusters by cluster
{: #monitoring_advisor_1}

When you choose to monitor your Kubernetes clusters by cluster, you can select more filters to display data by node or by namespace, or you can choose any of the following dashboards:
- Workload Status & Performance
- Node Status & Performance
- Pod Rightsizing & Workload Capacity Optimization
- Cluster Capacity Planning
- Cluster / Namespace Available Resources
- Cluster Overview
- CPU Allocation Optimization
- Memory Allocation Optimization

![Advisor predefined dashboards by cluster](../images/overview-tab-clusters.png "Advisor prefedined dashboards by cluster")

For more information on how to interpret this view, see [About Clusters Overview](https://docs.sysdig.com/en/docs/sysdig-monitor/advisor/overview/clusters-data/){: external}.

### Monitoring Kubernetes clusters by node
{: #monitoring_advisor_2}

When you choose to monitor your Kubernetes clusters by node, you can choose any of the following dashboards:
- Node Status & Performance
- Pod Scheduling Troubleshooting
- Node Overview
- CPU Allocation Optimization
- Memory Allocation Optimization


For more information on how to interpret this view, see [About Nodes Overview](https://docs.sysdig.com/en/docs/sysdig-monitor/advisor/overview/nodes-data/){: external}.

### Monitoring Kubernetes clusters by namespace
{: #monitoring_advisor_3}

When you choose to monitor your Kubernetes clusters by namespace, you can select more filters to display data by workload, or you can choose any of the following dashboards:
- Workload Status & Performance
- Pod Status & Performance
- Pod Rightsizing & Workload Capacity Optimization
- Namespace Overview
- Workloads CPU Usage and Allocation
- Workloads Memory Usage and Allocation

For more information on how to interpret this view, see [About Namespaces Overview](https://docs.sysdig.com/en/docs/sysdig-monitor/advisor/overview/namespaces-data/){: external}.

### Monitoring Kubernetes clusters by workloads
{: #monitoring_advisor_4}

When you choose to monitor your Kubernetes clusters by workloads, you can choose any of the following dashboards:
- Container Resource Usage & Troubleshooting
- Pod Status & Performance
- Pod Rightsizing & Workload Capacity Optimization
- Workload Status & Performance
- Deployment Overview
- Pod Overview
- Workloads CPU Usage and Allocation
- Workloads Memory Usage and Allocation


For more information on how to interpret this view, see [About Workloads Overview](https://docs.sysdig.com/en/docs/sysdig-monitor/advisor/overview/workloads-data/){: external}.

### Monitoring hosts
{: #monitoring_advisor_5}

When you choose to monitor by host, you can choose any of the following dashboards:
- Host Resource Usage
- File System Usage & Performance
- Memory Usage
- Network
- Sysdig Agent Health & Status





## Dashboards
{: #monitoring_dashboards}

A dashboard is composed of a series of panels that are configured to display metrics that report on the health, performance, and state of your infrastructure, applications, and services for a single host or a group of hosts. Dashboards offer a specialized insight into network data, application data, topology, services, hosts, and containers. Use dashboards to monitor your infrastructure, applications, and services.

In the *Dashboards* section of the web UI, dashboards are organized in the following sections:
- *My favorites*: These section displays the top dashboards.
- *My Dashboards*: These section displays custom dashboards that you create.
- *Shared By My Team*: These dashboards displays custom dashboards that are shared by users within a team.
- *Dashboard Templates*: These section groups predefined dashboards by type. Predefined dashboards that are provided by {{site.data.keyword.cloud_notm}} services are located in the **IBM** section.



You can use pre-defined dashboards. You can also create custom dashboards through the web UI or programmatically. You can back up and restore dashboards by using Python scripts or the {{site.data.keyword.mon_full_notm}} REST API. You can also copy and share dashboards through the web UI.

For more information, see [Dashboards](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/){: external}.


## Panels
{: #monitoring_panels}

A panel displays a metric or group of metrics in a dashboard.

You can use any of the following panel types to visualize metrics:
- `Histogram`: Use a histogram panel to monitor a metric, that is segmented by a dimension or label, and understand its value across multiple segments. [Learn more](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/configure-panels/types-of-panels/histogram/#histogram){: external}.

- `Timechart Panel`: Use timecharts to monitor how the value of a metric changes over time. A Timechart is a graph that is produced by applying statistical aggregation to a label over an interval. The X-axis of a timechart is always time. [Learn more](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/configure-panels/types-of-panels/timechart-panel/){: external}.

- `Number Panel`: Use a number panel to monitor the value of a metric. You can also use it to see the average value over a time range. [Learn more](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/configure-panels/types-of-panels/number-panel/){: external}.

- `Table Panel`: Use a table panel to monitor actual values instead of visual representations. The Table panel displays metric data in tabular form. [Learn more](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/configure-panels/types-of-panels/table-panel/){: external}.

- `Text`: Use a text panel to provide context or information in the dashboard. [Learn more](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/configure-panels/types-of-panels/text/){: external}.

- `Toplist`: Use a toplist panel to display metric values in order. [Learn more](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/configure-panels/types-of-panels/toplist/){: external}.


You can copy, change the scope, duplicate, delete, export, and explore panels.

You can export data from a panel. Consider the following information when you export data:

* You can export data to a **json file** from a line chart.
* You can export data to a **csv file** from a table chart or from a line chart.

There is a limit of 10000 rows per export.
{: note}




## Explore
{: #monitoring_explore}

In the Explore section, you can view and troubleshoot key metrics and entities of your infrastructure stack through any of the following tabs:
- *Metrics*: Use this section to view and analyze individual metrics.

    When you analyze metrics, you can drill down into layers of your infrastructure hierarchy and view granular-level data. You can use the *Grouping selection* to control how entities are organized in Explore such as *All Workloads*, *Containerized Apps*, *DaemonSets*, *Deployments*, and more.

    In the metrics tab, you can view and analyze individual metrics. You can also view troubleshooting views and topology views.

- *PromQL Query*: Use the PromQL Metric Explorer to build PromQL queries.
- *PromQL library*: Try predefined PromQL queries. Then, create an alert based on a query that you try or create a dashboard panel from a predefined query.




For more information, see [Explore](https://docs.sysdig.com/en/docs/sysdig-monitor/explore/){: external}.
