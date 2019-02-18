---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

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

Use labels to group infrastructure resources into logical hierarchies, filter out data, and split aggregated data into segments. Customize how data is aggregated when you configure a graph or create an alert for a metric. Set the scope of a dashboard, a panel, or an alert to filter out data points. Restrict access to data by managing users' data access through teams. 
{:shortdesc}



## Labels
{: #manage_labels}

**Labels** define the characteristics of a metric. You can use labels to identify and differentiate characteristics of a metric. 

Labels are classified as infrastructure labels and metric descriptor labels. Each metric has a set of pre-defined labels. For custom metrics, you can configure more labels. 

* You can use **infrastructure labels** to identify objects within the infrastructure. These labels are obtained from the infrastructure. For example, a label can be *kubernetes.pod.name*.
* You can use **metric descriptor labels** to define custom labels. These labels are key-value pairs that are applied directly to metrics, and obtained from integrations like StatsD, Prometheus, and JMX. 

## Groups
{: #manage_groups}

**Groups** organize infrastructure objects into logical hierarchies. Use groups to structure your infrastructure and ease how you monitor your environment.

In the *Explore* view of the Web UI, you can run any of the following actions:

| Task                                                                                        | Description     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Copy a group](/docs/services/Monitoring-with-Sysdig/groups.html#copy_group)                | Copy a group to other teams. |
| [Create a group](/docs/services/Monitoring-with-Sysdig/groups.html#create_group)            | Create a new group. |
| [Delete a group](/docs/services/Monitoring-with-Sysdig/groups.html#delete_group)            | Delete a group. |
| [Rename a group](/docs/services/Monitoring-with-Sysdig/groups.html#rename_group)            | Rename a group. |
| [Share a group](/docs/services/Monitoring-with-Sysdig/groups.html#share_group)              | Share a group with other members in the team. |
{: caption="Table 1. Tasks grouping labels" caption-side="top"} 



## Aggregation
{: #manage_aggregation}

**Aggregation** of data occurs automatically when you configure a graph or create an alert for a metric. There are two types of aggregation: time aggregation and group aggregation. 
* Time aggregation is always performed before group aggregation.
* To create multi-series comparisons and multiple alerts, you can also split aggregated data into smaller sections called **segments** by using labels. 

Sysdig aggregates data over time. Then, takes those data points, and groups them to display the data in metrics, dashboards, or calculate alert's thresholds. 
{: tip}

You can customize how data is aggregated when you configure a graph or create an alert for a metric.

There are two forms of aggregation used for metrics: 
* Time aggregation
* Group aggregation

**Time aggregation is always performed before group aggregation.**


### Time aggregation
{: #manage_time_aggregation}

**By default, a Sysdig agent collects and reports metrics at a 10 second resolution.**

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
{: caption="Table 2. Aggregation types for time series charts" caption-side="top"} 

**Note:** By default, average is used to display data points for a time interval.

Rate and average are very similar aggregation types. They often provide the same result. However, the calculation of each is different. If time aggregation is set to one minute, the Sysdig agent is set to retrieve six samples, one every 10 seconds. Notice that in some cases, samples may not be there due to disconnections or other circumstances.


### Group aggregation
{: #manage_group_aggregation}

**By default, metrics that are applied to a group of resources, such as several containers, hosts, or nodes, are averaged between the members of the group.**

For example, if three hosts report different CPU usage for one sample interval, the three values are averaged, and reported on the chart as a single data point for that metric.

The following table lists different types of group aggregation types:

| Aggregation type | Description                                        |
|------------------|----------------------------------------------------|
| average          | Average value of the interval's samples.           |
| maximum	         | Highest value of the interval's samples.           |
| minimum	         | Lowest value of the interval's samples.            |
| sum              | Combined value of the interval's samples.          |
{: caption="Table 3. Aggregation types for group aggregation" caption-side="top"} 


**Group aggregation is dependent on segmentation.** For a view that shows metrics for a group of items, if the *Segment By* selection is changed to break out the individual items, group aggregation does not occur.



## Scope
{: #manage_scope}

**Scope** is a collection of labels that define the conditions to filter out data points when you create dashboards and panels, configure alerts, and customize teams. 

The following table lists the tasks that you can run to change the scope in the monitoring service:

| Task                                                                                        | Description     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Changing the scope of a dashboard](/docs/services/Monitoring-with-Sysdig/dashboards.html#dashboards_scope) | Change the scope of a dashboard to filter out data points for all metrics displayed through panels on the dashboard. |
| [Changing the scope of a panel](/docs/services/Monitoring-with-Sysdig/panel.html#panel_scope) | Change the scope of a panel to filter out data for a specific metric that is displayed through the panel. |
| [Changing the scope of a team](/docs/services/Monitoring-with-Sysdig/teams.html#teams_scope) | Change the scope of the data that is visible to users that are members of a team. |
{: caption="Table 4. Tasks to change the scope" caption-side="top"} 


## Teams
{: #manage_teams}

**Teams** group users and control the data and the permissions to work with Sysdig captures and infrastructure events for those users. 

A Sysdig administrator can define any number of teams. For each team, he can configure the following information:
* The *default team*: You can set this team to be the team that any user that logs in to the web UI for the first time gets assigned by default.
* The *default entrypoint*: You can specify the view in the web UI that opens every time a user logs in. Valid entrypoints are: *Explore* view, *Dashboards* view, *Events* view, *Alerts* view, and *Settings* view.
* The scope: You can limit what data users can see. You can choose *Host* or *Container* to define the level of data that is visible. Then, you can add one or more conditions. If the scope is set to *Host*, users can see all host-level and container-level information. If the scope is set to *Container*, users can see only container-level information.
* Permissions: You can enable or disable the following features: *Sysdig captures*, and *infrastructure events*. Capture files will only be visible to members of the team. **Note:** Captures include detailed information from every container on a host, regardless of the team’s scope. When infrastructure events is enabled, users can view all custom infrastructure events from every user and Sysdig agent in the instance.

By default, there is a **Monitor Operations** team that is predefined for each IBM Cloud Monitoring with Sysdig instance.
* This team cannot be deleted.
* Users are automatically added as members of this team and granted full visibility on all the resources that are available in the instance. 

**Note:** 
* An administrator must switch to the *Monitor Operations* team before he can create teams or change the settings for others teams.
* After a user logs in to the {{site.data.keyword.Bluemix_notm}} and launches the Sysdig web UI, an administrator can manage that user in the Sysdig web UI. The user is created in the Sysdig database when the user logs in to the Sysdig web UI for the first time. 

To restrict users viewing permissions, an administrator can do any of the following actions:
* Change the user's role in the default *Monitor Operations* team to *Read* User. 
* Create a default team with limited scope and visibility. Then, manually assign users to other teams. 

The following table lists the tasks that you can run when you work with teams:

| Task                                                                            | Description                 |
|---------------------------------------------------------------------------------|-----------------------------|
| [Creating a team](/docs/services/Monitoring-with-Sysdig/teams.html#teams_create)      | Create a team to control data visibility.  |
| [Deleting a team](/docs/services/Monitoring-with-Sysdig/teams.html#teams_delete)      | Delete a team. </br>**Note:** When you delete a team, users that only belong to this team will be moved to the default team. |
| [Adding team members](/docs/services/Monitoring-with-Sysdig/teams.html#teams_users)   | Add more users to a team. |
| [Edit a team ](/docs/services/Monitoring-with-Sysdig/teams.html#teams_scope)          | Change the scope of the data that is visible to users that are members of a team.  |
{: caption="Table 5. Tasks to work with teams" caption-side="top"} 





    


