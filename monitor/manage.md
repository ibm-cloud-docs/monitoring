---

copyright:
  years:  2018, 2023
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, manage

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Organizing metric data
{: #manage}

Use labels to group infrastructure resources into logical hierarchies, filter out data, and split aggregated data into segments. Customize how data is aggregated when you configure a graph or create an alert for a metric. Set the scope of a dashboard, a panel, or an alert to filter out data points. Restrict access to data by managing users' data access through teams.
{: shortdesc}



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

| Task                                                                                        |
|---------------------------------------------------------------------------------------------|
| [Create a group](https://docs.sysdig.com/en/groupings-editor.html#UUID-08496372-f14f-0aaf-f2a6-8bbd8be259e2_section-idm232111411977818){: external}  |
| Delete a group. |
| [Rename a group](https://docs.sysdig.com/en/groupings-editor.html#UUID-08496372-f14f-0aaf-f2a6-8bbd8be259e2_section-idm232111412708997){: external}            |
| [Share a group with other members in the team](https://docs.sysdig.com/en/groupings-editor.html#UUID-08496372-f14f-0aaf-f2a6-8bbd8be259e2_section-idm232113126392123){: external} |
{: caption="Table 1. Tasks grouping labels" caption-side="top"}



## Aggregation
{: #manage_aggregation}

**Aggregation** of data occurs automatically when you configure a graph or create an alert for a metric.

There are different types of aggregation that are used for metrics:
* Time aggregation is always performed before group aggregation.
* To create multi-series comparisons and multiple alerts, you can also split aggregated data into smaller sections that are called **segments** by using labels.

Time aggregation is always performed before group aggregation.

{{site.data.keyword.mon_full_notm}} aggregates data over time. Then, take those data points, and groups them to display the data in metrics, dashboards, or calculate alert's thresholds.
{: tip}

You can customize how data is aggregated when you configure a graph or create an alert for a metric.





### Time aggregation
{: #manage_time_aggregation}

**By default, a monitoring agent collects and reports metrics at a 10-second resolution.**

In Time series charts that include data for 5-minutes or less,
* Data points are drawn at 10-second resolution
* Time aggregation does not occur.

Time aggregation automatically occurs in any of the following situations:

* In Time series charts that include data for an amount of time greater than 5-minutes, data points are drawn as an aggregate for an appropriate time interval. For example, for a chart that shows data for 1-hour, each data point represents a 1-minute interval.
* When you display historical data, data rolls up over time. You can choose which data points to utilize when you view older data.

The following table lists different aggregation types for time series charts:

| Aggregation type | Description                                                              |
|------------------|--------------------------------------------------------------------------|
| `average`          | Average of the retrieved metric values across the time period evaluated. |
| `rate (timeAvg)`   | Average value of the metric across the time period evaluated.            |
| `maximum`	         | Highest value during the time period evaluated.                          |
| `minimum`         | Lowest value during the time period evaluated.                           |
| `sum`              | Combined sum of the metric across the time period evaluated.             |
{: caption="Table 2. Aggregation types for time series charts" caption-side="top"}

**Note:** By default, average is used to display data points for a time interval.

Rate and average are similar aggregation types. They often provide the same result. However, the calculation of each is different. If time aggregation is set to 1-minute, the monitoring agent is set to retrieve six samples, one every 10 seconds. Notice that in some cases, samples might not be there due to disconnections or other circumstances.


### Group aggregation
{: #manage_group_aggregation}

**By default, metrics that are applied to a group of resources, such as several containers, hosts, or nodes, are averaged between the members of the group.**

For example, if three hosts report different CPU usage for one sample interval, the three values are averaged, and reported on the chart as a single data point for that metric.

The following table lists different types of group aggregation types:

| Aggregation type | Description                                        |
|------------------|----------------------------------------------------|
| `average`          | Average value of the interval's samples.           |
| `maximum`	         | Highest value of the interval's samples.           |
| `minimum`	         | Lowest value of the interval's samples.            |
| `sum`              | Combined value of the interval's samples.          |
{: caption="Table 3. Aggregation types for group aggregation" caption-side="top"}


**Group aggregation depends on segmentation.** For a view that shows metrics for a group of items, if the *Segment By* selection is changed to break out the individual items, group aggregation does not occur.



## Scope
{: #manage_scope}

**Scope** is a collection of labels that define the conditions to filter out data points when you create dashboards and panels, configure alerts, and customize teams.

The following table lists the tasks that you can run to change the scope in the monitoring service:

| Task                                                                                        | Description     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Changing the scope of a dashboard](/docs/monitoring?topic=monitoring-dashboards#dashboards_scope) | Change the scope of a dashboard to filter out data points for all metrics displayed through panels on the dashboard. |
| [Changing the scope of a panel](/docs/monitoring?topic=monitoring-panels#panels_scope) | Change the scope of a panel to filter out data for a specific metric that is displayed through the panel. |
| [Changing the scope of a team](/docs/monitoring?topic=monitoring-teams#teams_scope) | Change the scope of the data that is visible to users that are members of a team. |
{: caption="Table 4. Tasks to change the scope" caption-side="top"}


## Teams
{: #manage_teams}

**Teams** group users and control the data and the permissions to work with {{site.data.keyword.mon_full_notm}} captures and infrastructure events for those users.

an  {{site.data.keyword.mon_full_notm}} administrator can define any number of teams. For each team, an admin can configure the following information:
* `The default team`: You can set this team to be the team that any user that logs in to the web UI for the first time.
* `The default entrypoint`: You can specify the view in the web UI that opens every time that a user logs in. Valid entrypoints are *Explore* view, *Dashboards* view, *Events* view, *Alerts* view, and *Settings* view.
* `The scope`: You can limit what data users can see. You can choose *Host* or *Container* to define the level of data that is visible. Then, you can add one or more conditions. If the scope is set to *Host*, users can see all host-level and container-level information. If the scope is set to *Container*, users can see only container-level information.
* `Permissions`: You can enable or disable the following features: *captures*, and *infrastructure events*. Capture files are visible to members of the team. **Note:** Captures include detailed information from every container on a host, regardless of the team’s scope. When infrastructure events are enabled, users can view all custom infrastructure events from every user and monitoring agent in the instance.

By default, a **Monitor Operations** team is predefined for each {{site.data.keyword.mon_full_notm}} instance.
* This team cannot be deleted.
* Users are automatically added as members of this team and granted full visibility on all the resources that are available in the instance.

An administrator must switch to the *Monitor Operations* team to create teams or change the settings for others teams.
{: note}

An administrator can do any of the following actions to restrict the viewing permissions of a user:
* Change the user's role in the default *Monitor Operations* team to *Read* User.
* Create a default team with limited scope and visibility. Then, grant permissions to users to work in other teams. [Learn more](/docs/monitoring?topic=monitoring-iam_grant_team).

The following table lists the tasks that you can run when you work with teams:

| Task                                                                            | Description                 |
|---------------------------------------------------------------------------------|-----------------------------|
| [Creating a team](/docs/monitoring?topic=monitoring-teams#teams_create)      | Create a team to control data visibility.  |
| [Deleting a team](/docs/monitoring?topic=monitoring-teams#teams_delete)      | Delete a team. </br>**Note:** When you delete a team, users that belong only to this team are moved to the default team. |
| [Grant permissions to work in a team](/docs/monitoring?topic=monitoring-iam_grant_team) | Grant a user or service ID administration permissions. |
| [Edit a team](/docs/monitoring?topic=monitoring-teams#teams_scope)          | Change the scope of the data that is visible to users that are members of a team.  |
{: caption="Table 5. Tasks to work with teams" caption-side="top"}
