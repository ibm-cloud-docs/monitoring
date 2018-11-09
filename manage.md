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

You can use labels to group infrastructure objects into logical hierarchies, filter out data, and split aggregated data into segments.
{:shortdesc}

Labels define the characteristics of a metric. You can use labels to identify and differentiate characteristics of a metric. 

Labels are classified as infrastructure labels and metric descriptor lables. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels. 

In the Explore view of the Web UI, you can use labels to define new groups, aggregate data, and define segments:
* *Groups*: Use labels to group infrastructure objects into logical hierarchies.
* *Segments*: 
* *Aggregation*: 




## Aggregating data
{: #aggregate}


Sysdig Monitor allows users to adjust the aggregation settings when graphing or creating alerts for a metric, informing how Sysdig rolls up the available data samples in order to create the chart or evaluate the alert. There are two forms of aggregation used for metrics in Sysdig: time aggregation and group aggregation.

Time aggregation is always performed before group aggregation.


### Time aggregation
{: #time}

By default, Sysdig agents collect and report metrics at a 10 second resolution.
{: tip}

Time aggregation comes into effect in two overlapping situations:

    Charts can only render a limited number of data points. To look at a wide range of data, Sysdig Monitor may need to aggregate granular data into larger samples for visualization.

    Sysdig Monitor rolls up historical data over time.

    Sysdig retains rollups based on each aggregation type, to allow users to choose which datapoints to utilize when evaluating older data.

By default, Sysdig agents collect and report metrics at a 10 second resolution. For time series charts covering five minutes or less, datapoints are drawn at this 10 second resolution, and any time aggregation selections will have no effect. When an amount of time greater than five minutes is displayed, data points are drawn as an aggregate for an appropriate time interval. For example, for a chart covering one hour, each datapoint would reflect a one minute interval.

At time intervals of one minute and above, charts can be configured to display different aggregates for the 10 second metrics used to calculate each datapoint.
average	The average of the retrieved metric values across the time period.
rate	

The average value of the metric across the time period evaluated.
maximum	The highest value during the time period evaluated.
minimum	

The lowest value during the time period evaluated.
sum	The combined sum of the metric across the time period evaluated.


Rate and average are very similar, and often provide the same result. However, the calculation of each is different. If time aggregation is set to one minute, the agent is supposed to retrieve six samples (one every 10 seconds). In some cases, samples may not be there, due to disconnections or other circumstances.

Most metrics are sampled once for each time interval, resulting in average and rate returning the same value. However, there will be a distinction for any metrics not reported at every time interval (for example, some custom statsd metrics).

Rate is currently referred to as timeAvg in the Sysdig Monitor API and advanced alerting language.

By default, average is used when displaying datapoints for a time interval.



### Group aggregation
{: #group}

Group Aggregation

Metrics applied to a group of items (for example, several containers, hosts, or nodes) are averaged between the members of the group by default. For example, three hosts report different CPU usage for one sample interval. The three values will be averaged, and reported on the chart as a single datapoint for that metric.

There are several different types of group aggregation:
average	The average value of the interval's samples.
maximum	The maximum value of the interval's samples.
minimum	The minimum value of the interval's samples.
sum	The combined value of all of the interval's samples.

Group aggregation is dependent on the segmentation. For a view showing metrics for a group of items, if the Segment By selection is changed to break out the individual items, the group aggregation setting will be nullified.
