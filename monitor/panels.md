---

copyright:
  years:  2018, 2020
lastupdated: "2020-11-12"

keywords: Sysdig, IBM Cloud, monitoring, panels

subcollection: Monitoring-with-Sysdig

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
{:external: target="_blank" .external}


# Managing panels
{: #panels}

Use a panel to display a metric or group of metrics in a dashboard. You can copy, change the scope, duplicate, delete, export, and explore panels.
{:shortdesc}

You can use any of the following panel types:

| Type | Description |
|------|-------------|
| `Line` | Use this panel to view trends over time for one or more metrics.  |
| `Area` | Use this panel to view trends over time for one or more metrics.  |
| `Top list` | Use this panel to compare a metric across groups of entities. The bar chart is sorted in descending order.  |
| `Histogram` | Use this panel to view the frequency distribution of a metric in buckets.  |
| `Topology` | Use this panel to visualize the infrastructure as a topology map, and the relations between entities in the map.  |
| `Number` | Use this panel to view a single number that represents the value of an aggregated metric over time for one or more entities.  |
| `Table` | Use this panel to display numerical data for your infrastructure based on metrics and segments.  |
| `Text` | Use this panel to add text. Use markdown to add your text.  |
{: caption="Table 1. Panel types" caption-side="top"} 



## Copy a panel into a dashboard
{: #panels_copy}

Complete the following steps to copy a panel:

1. Navigate to the **DASHBOARD** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Select the *More options* icon ![Three dots icon](images/actions.png) and select **Copy to Dashboard** ![Copy to Dashboard icon](images/copy.png).

3. Select one of the dashboards that are listed, or enter a name for a new dashboard. 

4. Click **Copy and Open**.



## Change the scope of a panel
{: #panels_scope}

Complete the following steps to change the scope of a panel:

1. Navigate to the *DASHBOARD** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric for which you want to change the scope.

2. In the panel, click **Edit Scope** to change the default scope. 

    By default, **Everywhere** is selected.
    
3. Select the scope. 

4. Optionally, click **Override the custom panel scopes** to override the scope for all panels with a custom scope defined. 

    **Note: This action cannot be undone.** 

    To reset the dashboard scope to the entire infrastructure, or to update an existing dashboard's scope to the entire infrastructure, select **Everywhere**.
    {: tip}

5. Click **Save**.



## Duplicate a panel
{: #panels_duplicate}

Complete the following steps to duplicate a panel in the current dashboard:

1. Navigate to the *DASHBOARD** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Select the *More options* icon ![Three dots icon](images/actions.png) and select **Duplicate Panel** ![Duplicate Panel icon](images/duplicate.png).


## Delete a panel
{: #panels_delete}

Complete the following steps to delete a panel in the current dashboard:

1. Navigate to the *DASHBOARD** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Select the *More options* icon ![Three dots icon](images/actions.png) and select **Delete** ![Delete icon](images/delete.png).

3. Click **Yes, delete panel** to confirm the deletion of the panel.



## Export data from a panel
{: #panels_export}

Consider the following information when you export data:

* You can export data to a **json file** from a line chart.
* You can export data to a **csv file** from a table chart or from a line chart.

Complete the following steps to export data from a panel:

1. Navigate to the *DASHBOARD** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Select the *More options* icon ![Three dots icon](images/actions.png).

3. Choose one of the following options:

    * Select **Export JSON** to export data to a json formatted file.

    * Select **Export CSV** to export data to a csv formatted file.

4. Click **Save the file**.




## Create Alert
{: #panels_alert}

You can create alerts directly from a panel.

Complete the following steps to create an alert:

1. Navigate to the *DASHBOARD** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Select the *More options* icon ![Three dots icon](images/actions.png).

3. Select **Create Alert**.

4. Configure the alert.

5. Click **Create**.


