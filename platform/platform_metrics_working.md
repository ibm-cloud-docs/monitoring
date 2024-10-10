---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Working with platform metrics
{: #platform_metrics_working}

Platform metrics are metrics that are exposed by enabled-monitoring services and the platform in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

* Platform metrics are regional.

    You can monitor metrics from enabled-monitoring services on the {{site.data.keyword.cloud_notm}} in the region where the service is available.

* You can configure only 1 instance of the {{site.data.keyword.mon_full_notm}} service per region to collect *platform metrics* in that location.

    To configure a monitoring instance, you must set the *platform metrics* configuration setting.

    To configure platform metrics, you must be assigned the IAM Editor role or higher for the {{site.data.keyword.mon_full_notm}} service.

* If a monitoring instance in a region is already enabled to collect platform metrics, metrics from enabled-monitoring services are collected automatically and are available for monitoring through this instance. For more information about enabled-monitoring services, see [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).

* To monitor platform metrics for a service instance, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where the service instance that you want to monitor is provisioned.


## Controlling what data is visible
{: #global-attributes}

You can use attributes to segment metrics so that you can define what data is visible to users.

The following global attributes are available for segmenting metrics:

| Attribute               | Attribute Name              | Attribute Description |
|-------------------------|-----------------------------|-----------------------|
| `Cloud Type`            | `ibm_ctype`                 | Type.  \n Valid values: `public`, `dedicated`, or `local` |
| `Location`              | `ibm_location`              | Location of the monitored resource.  \n This field can be set to a region, a data center, or global. |
| `Scope`                 | `ibm_scope`                 | Scope of the metric.  \n This field can be set to the account GUID, an organization GUID, or a space GUID. |
| `Service name`          | `ibm_service_name`          | Name of the service generating this metric. |
| `Service instance`      | `ibm_service_instance`      | Service instance GUID that identifies the instance the metric is associated with. |
| `Service instance name` | `ibm_service_instance_name` | Service instance name.  \n This field provides the user-provided name of the service instance which isn't necessarily a unique value depending on the name provided by the user. |
| `Resource group name`   | `ibm_resource_group_name`   | The resource group name where the service instance is created. |
| `Resource group ID`     | `ibm_resource_group_id`     | The resource group GUID where the service instance is created. |
{: caption="Global attributes" caption-side="top"}

Other attributes are available per {{site.data.keyword.cloud_notm}} service. In the [Cloud services](/docs/monitoring?topic=monitoring-cloud_services) topic, identify the service that you want to monitor and go to the *More info* section. Look for the section **Attributes for segmentation** to get the list of attributes that you can use to segment metrics for that service.

You can control the data that is visible for analysis per team, per dashboard, and per panel in a dashboard.

### Dashboards
{: #global-attributes-1}

You can use global attributes to set the scope of dashboards:
- The scope defines the data that is valid for aggregation.
- Only the data that is in scope is displayed.
- The scope that is set at the dashboard level applies to all panels in the dashboard.
- You can override the main dashboard scope and specify a specific scope for a panel.

### Panels
{: #global-attributes-2}

You can use global attributes to set the scope of a panel:
- The scope defines the data that is valid for aggregation.
- Only the data that is in scope is displayed.

### Teams
{: #global-attributes-3}

You can use global attributes to define the data that is visible and available for analysis by a team.



## Monitoring platform metrics through dashboards
{: #platform_metrics_working_dash}

{{site.data.keyword.mon_full_notm}} provides 1 or more dashboard templates that you can use to monitor services.

- Dashboard templates are available in the **Dashboards** > **Dashboard Manager** section of the monitoring UI.

- Dashboard templates are only visible in the monitoring UI if you have an instance of the service running in that region.

- Dashboard templates cannot be customized. You can create a copy of a dashboard template and then customize the copy to create your dashboard.

### Creating a custom dashboard
{: #platform_metrics_working_dash_1}

Complete the following steps to create a custom dashboard:

1. Navigate to the **Dashboards** section in the Web UI

2. You can create a dashboard using a template or by creating a dashboard manually.

    * To create a dashboard using a template:

        1. Click **Dashboard Manager**.

        2. Click **Dashboard Library**.

        3. Click the template you want to use to create your dashboard.

        4. Click **Copy to My Dashboards**.

        5. Name your dashboard.

        6. Click **Create and Open**

    * To create a dashboard without a template:

        1. Click **+ New Dashboard**. The *New Dashboard* page opens.

        2. Modify your dashboard as desired.

        3. Click **Save**.

        4. Click *New Dashboard* to rename your dashboard.  Click the check mark to save your name change.

3. Set the dashboard scope. Click the *Pencil* icon ![Pencil icon](../images/pencil.png). The select the desired scope. By default, **Entire infrastructure** is selected.

    1. Select the scope.

    2. Click **Save**.

4. Configure panels. Repeat this step for any of the panels in the dashboard that you want to modify.

    1. Identify the panel that you want to modify.

    2. Select **Edit Panel**. This is the *Pencil* icon ![Pencil icon](../images/pencil.png).

    3. Change the visualization if needed.

    4. Change the query used to select the data.

    5. For **Number** and **Gauge** chart types you can set the panel color based on metric thresholds. Click **Thresholds**. Set values for the different thresholds.  
    
       For **Timechart** set the axes and legend for the chart.

    6. For **Panel** specify the name of the panel and an optional description.

    7. Change the scope of the panel. Click the *Pencil* icon ![Pencil icon](../images/pencil.png). Then, change the scope. If you need to restore the dashboard scope to the panel, delete the custom scope.  Click **Apply**.

    8. Click **Save**.



### Defining the scope of a dashboard
{: #platform_metrics_working_dash_2}

Complete the following steps to define the scope of the data that is displayed through the dashboard:

1. [Launch the monitoring UI](/docs/monitoring?topic=monitoring-launch).
2. Click **Dashboards**.
3. Select a custom dashboard that monitors {{site.data.keyword.cloud_notm}} services in the **My Dashboards** section.
4. To modify the scope, click the pencil icon to  **Edit Dashboard Scope**.
5. In the drop-down box, enter **ibm** and select an attribute.
6. Select an operator.
7. Select 1 or more values

   You can also leave the value empty, and select **var** to define a variable so that users can choose 1 or more values when they analyze data through the dashboard.
   {: tip}

8. Continue adding more attributes. When you have the scope defined, click **Save**.


### Defining the scope of a panel
{: #platform_metrics_working_dash_3}

Complete the following steps to define the scope of the data that is displayed through a panel in a dashboard:

1. [Launch the monitoring UI](/docs/monitoring?topic=monitoring-launch).
2. Click **Dashboards**.
3. Select a custom dashboard that monitors {{site.data.keyword.cloud_notm}} services in the **My Dashboards** section.
4. Select a panel where you want to change the scope of the data.
5. Click the *Pencil* icon ![Pencil icon](../images/pencil.png). 
6. By default, the panel inherits the dashboard scope. To specify a custom scope, you must change the scope for the panel.

    1. In the drop-down box, enter **ibm** and select an attribute.
    2. Select an operator.
    3. Select 1 or more values

       You can also leave the value empty, and select **var** to define a variable so that users can choose 1 or more values when they analyze data through the dashboard.
       {: tip}

    4. Continue adding more attribute if needed.

7. To save the scope, click **Save** at the panel level.


## Configuring an alert on a platform metric
{: #platform_metrics_working_alert}

### Configuring an alert from a panel
{: #platform_metrics_working_alert_1}

Complete the following steps to define an alert on a metric:

1. [Launch the monitoring UI](/docs/monitoring?topic=monitoring-launch).
2. Verify that you have a notification channel that defines how you want to be notified.

    You can enabled 1 or more notification channels when you configure an alert. If you need multiple notification channels, check they are available.

3. Click **Dashboards**.
4. Select a custom dashboard that monitors {{site.data.keyword.cloud_notm}} services in the **My Dashboards** section.
5. Identify the panel for which you want to define the alert.

    Before you create the alert, check the scope of the metric that is configured in the panel. This scope is automatically included in the alert definition.
    {: note}

6. Click the *Actions* icon ![Three dots icon](../images/actions.png) and select **Create Alert**.

    ![Panel options](images/sysdig-platform-15.png "Panel options"){: caption="Panel options" caption-side="bottom"}

    If you have multiple queries defined in a panel, you are prompted to select the metric for which you want to create an alert.
    {: note}

7. Select the alert type. Options are `Metric`, `Change`, `Downtime`, `Event`, or `PromQL`.

8. Set the following fields:

    **Alert Name**: Enter a name for the alert.

    **Alert Description**: Add a description that other users can read to get more context. This field is optional.

    **Group**: The alert group this alert will be part of.  If not specified, the alert will be part of the default group.

    **Severity**: Set the level of criticality of the alert. Valid values are `High`, `Medium`, `Low`, and `Info`.

    **Scope**: This field is set to the scope that you have defined for the metric in the panel. Check that the scope is the one that you need.

    **Notifications**: Enable 1 or more notification channels.

9. Depending on the alert type, you need to configure what will trigger the alert.

    For `Metric` alerts:

    **Metric**: This field is set to the metric that you have selected from the panel. Check that the metric and aggregation are the ones that you need.

    **Threshold**: Define the condition and threshold value that must be evaluated. It also defines whether the alert sends a single alert or multiple alerts. Valid time scales are `minute`, `hour`, or `day`. A single alert fires an alert for the entire scope. Multiple Alerts are sent if 1 or more segments breach the threshold at once. An alert is sent for each segment that you specify.

    For `Change` alerts:

    **Metric**: This field is set to the metric that you have selected from the panel. Check that the metric and aggregation are the ones that you need.

    **Threshold**: Define the condition and threshold value that must be evaluated. Indicates that an alert is to be sent when the configured value changes within a defined duration as compared to a previous time duration. The percent of change can also be configured into the alert evaluation. For example, if the change is greater than 50%.

    For `Downtime` alerts:

    **Metric**: This field is set to the metric that you have selected from the panel. Check that the metric and aggregation are the ones that you need.

    **Threshold**: Define the condition and threshold value that must be evaluated. Indicates that an alert is to be sent when the configured value has a downtime of a configured time duration. Alerting can also be configured based on the percentage of time the resource is down over a given time perios.

    For `Event` alerts:

    **Threshold**: Define the condition and threshold value that must be evaluated. Indicates that an alert is to be sent when the number of events configured for the panel has reached, exceeded, or is less than a specific value. The threshold can also factor in the amount of time. For example, more than 50 events in a minute.


    For `Prometheus/PromQL` alerts:

    **Threshold**: Define the condition and threshold value that must be evaluated as a PromQL query. The query can factor in a duration of time and can also trigger alerts for a specified amount of time before automatically resolving the alert.

10. Click **Save** to save your alert.



## Configuring an alert from the Alerts section
{: #platform_metrics_working_alert_2}

You can define an alert directly from the *Alerts* section.

Complete the following steps to define an alert on a metric:

1. [Launch the monitoring UI](/docs/monitoring?topic=monitoring-launch).

2. Verify that you have a notification channel that defines how you want to be notified.

    You can enabled 1 or more notification channels when you configure an alert. If you need multiple notification channels, check they are available.

3. Navigate to the **Alerts** section in the Web UI.

4. Click **New Alert**.

5. Select your desired alert type.

7. Select the alert type. Options are `Metric`, `Change`, `Downtime`, `Event`, or `PromQL`.

8. Set the following fields:

    **Alert Name**: Enter a name for the alert.

    **Alert Description**: Add a description that other users can read to get more context. This field is optional.

    **Group**: The alert group this alert will be part of.  If not specified, the alert will be part of the default group.

    **Severity**: Set the level of criticality of the alert. Valid values are `High`, `Medium`, `Low`, and `Info`.

    **Scope**: This field is set to the scope that you have defined for the metric in the panel. Check that the scope is the one that you need.

    **Notifications**: Enable 1 or more notification channels.

9. Depending on the alert type, you need to configure what will trigger the alert.

    For `Metric` alerts:

    **Metric**: This field is set to the metric that you have selected from the panel. Check that the metric and aggregation are the ones that you need.

    **Threshold**: Define the condition and threshold value that must be evaluated. It also defines whether the alert sends a single alert or multiple alerts. Valid time scales are `minute`, `hour`, or `day`. A single alert fires an alert for the entire scope. Multiple Alerts are sent if 1 or more segments breach the threshold at once. An alert is sent for each segment that you specify.

    For `Change` alerts:

    **Metric**: This field is set to the metric that you have selected from the panel. Check that the metric and aggregation are the ones that you need.

    **Threshold**: Define the condition and threshold value that must be evaluated. Indicates that an alert is to be sent when the configured value changes within a defined duration as compared to a previous time duration. The percent of change can also be configured into the alert evaluation. For example, if the change is greater than 50%.

    For `Downtime` alerts:

    **Metric**: This field is set to the metric that you have selected from the panel. Check that the metric and aggregation are the ones that you need.

    **Threshold**: Define the condition and threshold value that must be evaluated. Indicates that an alert is to be sent when the configured value has a downtime of a configured time duration. Alerting can also be configured based on the percentage of time the resource is down over a given time perios.

    For `Event` alerts:

    **Threshold**: Define the condition and threshold value that must be evaluated. Indicates that an alert is to be sent when the number of events configured for the panel has reached, exceeded, or is less than a specific value. The threshold can also factor in the amount of time. For example, more than 50 events in a minute.


    For `Prometheus/PromQL` alerts:

    **Threshold**: Define the condition and threshold value that must be evaluated as a PromQL query. The query can factor in a duration of time and can also trigger alerts for a specified amount of time before automatically resolving the alert.

10. Click **Save** to save your alert.



## Controlling the access to platform metrics for a team
{: #platform_metrics_working_team}

You can control the data that is visible to all the users that are members of a team.

1. [Launch the monitoring UI](/docs/monitoring?topic=monitoring-launch).

2. Click the user icon and then click **Settings**.

3. Click **Teams**.


As an administrator of the service, you can create, modify, and delete teams. When you configure a team, you can define the scope of the data in the **Team Scope** section.

To allow a team to view platform metrics, you must select **Platform metrics**.

Enabling platform metrics grants access to all platform metrics. However, you can reduce the scope by configuring 1 or more platform metrics labels. Notice that the order of the labels is applied from the beginning of the list to the end.




### Limiting access to platform metrics by instance
{: #platform_metrics_working_team_1}

Complete the following steps:

1. [Launch the monitoring UI](/docs/monitoring?topic=monitoring-launch).

2. Click the user icon and then click **Settings**.

3. Click **Teams**.

4. In the **Team Scope** section, select **Platform metrics**.

5. Select the attribute `ibm_service_instance`to segment data by instance ID.

6. Select 1 or more instance IDs for which you want the data to be visible to users that are members of this team.

7. Add additional `global` attributes. Other attributes are available per {{site.data.keyword.cloud_notm}} service. In the [Cloud services](/docs/monitoring?topic=monitoring-cloud_services) topic, identify the service that you want to monitor and go to the *More info* section. Look for the section **Attributes for segmentation** to get the list of attributes that you can use to segment metrics for that service.

8. Click **Save**.
