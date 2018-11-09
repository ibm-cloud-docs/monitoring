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

# Managing data
{: #manage}

You can use labels to group infrastructure resources into logical hierarchies, filter out data, and split aggregated data into segments. You can customize how data is aggregated when you configure a graph or create an alert for a metric. You can set the scope of a dashboard, a panel, or an alert to filter out data points
{:shortdesc}

## Concepts
{: #concepts}

**Labels** define the characteristics of a metric. You can use labels to identify and differentiate characteristics of a metric. 

Labels are classified as infrastructure labels and metric descriptor labels. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels. 

* You can use **infrastructure labels** to identify objects within the infrastructure. These labels are obtained from the infrastructure. For example, a label can be *kubernetes.pod.name*.
* You can use **metric descriptor labels**. These labels are key-value pairs that are applied directly to metrics, and obtained from integrations like StatsD, Prometheus, and JMX. 

**Groups** group infrastructure objects into logical hierarchies. Use groups to structure how to monitor your environment.

In the Explore view of the Web UI, you can use labels to define new groups. 


**Aggregation** of data occurs automatically when you configure a graph or create an alert for a metric. There are two types of aggregation: time aggregation and group aggregation. 
* Time aggregation is always performed before group aggregation.
* To create multi-series comparisons and multiple alerts, you can also split aggregated data into smaller sections called **segments** by using labels. 

**Scope** is a collection of labels that are used to filter out or define the boundaries of a group of data points when creating dashboards, dashboard panels, alerts, and teams. 

You can define the scope at the dashboard level or at a panel level.



## Aggregating data in graphs and alerts
{: #aggregate}

You can customize how data is aggregated when you configure a graph or create an alert for a metric.

There are two forms of aggregation used for metrics: 
* Time aggregation
* Group aggregation

Time aggregation is always performed before group aggregation.
{: tip}


### Time aggregation
{: #time}

By default, a Sysdig agent collects and reports metrics at a 10 second resolution.
{: tip}

In Time series charts that include data for five minutes or less, 
* Data points are drawn at 10 second resolution
* Time aggregation does not occur.

Time aggregation automatically occurs in any of the following situations:

* In Time series charts that include data for an amount of time greater than five minutes, data points are drawn as an aggregate for an appropriate time interval. For example, for a chart that shows data for one hour, each data point represents a one minute interval.
* When you display historical data. Data rolls up over time. You can choose which data points to utilize when you view older data.

The following table lists different aggregation types for time series charts:

| Aggregation type | Description                                                              |
|------------------|--------------------------------------------------------------------------|
| average          | Average of the retrieved metric values across the time period evaluated. |
| rate (timeAvg)   | Average value of the metric across the time period evaluated.            |
| maximum	         | Highest value during the time period evaluated.                          |
| minimum	         | Lowest value during the time period evaluated.                           |
| sum              | Combined sum of the metric across the time period evaluated.             |
{: caption="Table 1. Aggregation types for time series charts" caption-side="top"} 

By default, average is used to display data points for a time interval.
{:tip}

Rate and average are very similar aggregation types. They often provide the same result. However, the calculation of each is different. If time aggregation is set to one minute, the Sysdig agent is set to retrieve six samples, one every 10 seconds. Notice that in some cases, samples may not be there due to disconnections or other circumstances.


### Group aggregation
{: #group}

By default, metrics that are applied to a group of resources, such as several containers, hosts, or nodes, are averaged between the members of the group.
{: tip}

For example, if three hosts report different CPU usage for one sample interval, the three values are averaged, and reported on the chart as a single data point for that metric.

The following table lists different types of group aggregation types:

| Aggregation type | Description                                        |
|------------------|----------------------------------------------------|
| average          | Average value of the interval's samples.           |
| maximum	         | Highest value of the interval's samples.           |
| minimum	         | Lowest value of the interval's samples.            |
| sum              | Combined value of the interval's samples.          |
{: caption="Table 2. Aggregation types for group aggregation" caption-side="top"} 


**Group aggregation is dependent on segmentation.** For a view that shows metrics for a group of items, if the *Segment By* selection is changed to break out the individual items, group aggregation does not occur.
