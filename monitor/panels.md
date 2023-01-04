---

copyright:
  years:  2018, 2023
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, panels

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Managing panels
{: #panels}

Use a panel to display a metric or group of metrics in a dashboard. You can copy, change the scope, duplicate, delete, export, and explore panels.
{: shortdesc}

You can use any of the following panel types:

| Type | Description |
|------|-------------|
| `Line` | Use this panel to view trends over time for one or more metrics.  |
| `Top list` | Use this panel to compare a metric across groups of entities. The bar chart is sorted in descending order.  |
| `Histogram` | Use this panel to view the frequency distribution of a metric in buckets.  |
| `Number` | Use this panel to view a single number that represents the value of an aggregated metric over time for one or more entities.  |
| `Table` | Use this panel to display numerical data for your infrastructure based on metrics and segments.  |
| `Text` | Use this panel to add text. Use markdown to add your text.  |
{: caption="Table 1. Panel types" caption-side="top"}



## Copy a panel into a dashboard
{: #panels_copy}

Complete the following steps to copy a panel:

1. Navigate to the **Dashboards** section (![dashboard section](images/dashboards.png)) in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Click the *Actions* icon ![Three dots icon](images/actions.png) and select **Copy to Dashboard** ![Copy to Dashboard icon](images/copy.png).

3. Select one of the dashboards that are listed, or enter a name for a new dashboard.

4. Click **Copy and Open**.



## Change the scope of a panel
{: #panels_scope}

Complete the following steps to change the scope of a panel:

1. Navigate to the *Dashboards* section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric for which you want to change the scope.

2. In the panel, click the *Pencil* icon ![Pencil icon](../images/pencil.png) to **Edit Dashboard Scope**.


3. Define your dashboard scope.

4. Click **Apply**.



## Duplicate a panel
{: #panels_duplicate}

Complete the following steps to duplicate a panel in the current dashboard:

1. Navigate to the *Dashboards** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Click the *Actions* icon ![Three dots icon](images/actions.png) and select **Duplicate Panel** ![Duplicate Panel icon](images/duplicate.png).


## Delete a panel
{: #panels_delete}

Complete the following steps to delete a panel in the current dashboard:

1. Navigate to the *Dashboards** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Click the *Actions* icon ![Three dots icon](images/actions.png) and select **Delete** ![Delete icon](images/delete.png).

3. Click **Delete Panel** to confirm the deletion of the panel.



## Export data from a panel
{: #panels_export}

Complete the following steps to export data from a panel:

1. Navigate to the *Dashboards** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Click the *Actions* icon ![Three dots icon](images/actions.png).

3. Click **Export Data**.

4. Choose the *Format* of the file to be exported:

    * Select **JSON** to export data to a `JSON` formatted file.

    * Select **CSV** to export data to a `CSV` formatted file.

5. Enter a *File name* for the exported file.

6. Click **Export**.




## Create Alert
{: #panels_alert}

You can create alerts directly from a panel.

Complete the following steps to create an alert:

1. Navigate to the **Dashboards** section in the Web UI. Select a dashboard. Then, identify the panel that displays the metric that you want to copy.

2. Click the *Actions* icon ![Three dots icon](images/actions.png).

3. Select **Create Alert**.

4. Configure the alert.

5. Click **Create**.
