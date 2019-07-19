---

copyright:
  years:  2018, 2019
lastupdated: "2019-07-21"

keywords: Sysdig, IBM Cloud, monitoring, sysdig rest api

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


# Managing the Sysdig REST API
{: #api}

Use the Sysdig REST API to automate routine tasks and monitor notifications.
{:shortdesc}

When you use the API from your custom scripts or programs, you must use a Sysdig token to authenticate with the {{site.data.keyword.mon_full_notm}} instance. 
{: tip}

## Creating a dashboard by using the API
{: #api_create_dashboard}

You can create a dashboard by duplicating an existing dashboard.  

Complete the following steps to create a dashboard:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Create the json file that describes the dashboard. The following fields must be set as indicated:

    * `name`: Enter the name of the dashboard.

    * `id`: Set to *null*.

    * `version`: Set to *null*.

    * `username`: Set to the email that is associated with your IBMid.

    * `shared`: Set to true to share the dashboard with other team members.

    * `public`: Set to true if you want the dashboard to be available publicly.

    * Configure filters to define the dashboard scope.
    
3. Create the dashboard. Run the following cURL command:

    ```
    curl -X POST ENDPOINT/api/v2/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    Where

    * `ENDPOINT` is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * `SYSDIG_API_TOKEN` is the API token that you got in the previous step.

    * `dashboard.json` is the file that describes the new dashboard, including panels and metrics.

For example, to create a dashboard, a sample json file looks as follows:

```
{
  "dashboard": {
    "name": "My new dashboard",
    "widgets": [
      {
        "customDisplayOptions": {
          "yAxisLeftDomain": {
            "to": null,
            "from": 0
          },
          "yAxisScale": "linear",
          "yAxisRightDomain": {
            "to": null,
            "from": 0
          },
          "valueLimit": {
            "count": 10,
            "direction": "desc"
          },
          "histogram": {
            "numberOfBuckets": 10
          },
          "xAxis": {
            "to": null,
            "from": 0
          }
        },
        "name": "CPU usage",
        "overrideScope": true,
        "showAs": "timeSeries",
        "groupId": "My new cpu dashboardcontainer.namecarboncache1",
        "metrics": [
          {
            "propertyName": "k0",
            "id": "timestamp"
          },
          {
            "propertyName": "v0",
            "id": "cpu.used.percent",
            "timeAggregation": "avg",
            "groupAggregation": "avg"
          }
        ],
        "compareToConfig": null,
        "gridConfiguration": {
          "size_y": 4,
          "size_x": 6,
          "col": 1,
          "row": 1
        },
        "filter": {
          "filters": {
            "filters": [
              {
                "metric": "container.name",
                "filters": null,
                "value": "carboncache",
                "op": "="
              }
            ],
            "logic": "and"
          }
        }
      }
    ],
    "public": false,
    "annotations": {
      "createdByEngine": true
    },
    "username": "ENTER YOUR EMAIL ADDRESS",
    "version": null,
    "schema": 1,
    "id": null,
    "shared": false
  }
}
```
{: screen}


## Saving all the dashboards of a team by using the API
{: #api_save_dashboard}

Complete the following steps to download the dashboards that are available for a team:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Run the following cURL command:

    ```
    curl -X GET ENDPOINT/api/v2/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Where

    * `ENDPOINT` is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * `SYSDIG_API_TOKEN` is the API token that you got in the previous step.

For example, to download the dashboards for a team that works in the US South region, you can run the following command:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/api/v2/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

The output is a JSON file where each dashboard starts with the field **id**. The name of the dashboard is specified in the field **name**.


## Saving a single dashboard of a team by using the API
{: #api_save_single_dashboard}

Complete the following steps to download a dashboard that is available for a team:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Run the following cURL command:

    ```
    curl -X GET ENDPOINT/api/v2/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Where

    * `ENDPOINT` is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * `SYSDIG_API_TOKEN` is the API token that you got in the previous step.

For example, to download a dashboard for a team that works in the US South region, you can run the following command:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/api/v2/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

The output is a JSON file that contains a single dashboard. The id and name of the dashboard is specified in the **id** and **name** fields respectively.


## Editing a dashboard of a team by using the API
{: #api_edit_dashboard}

Complete the following steps to edit an existing dashboard:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Follow [Saving a Single Dashboard](#api_save_single_dashboard) to get the existing dashboard properties you want to modify.

3. Run the following cURL command:

    ```
    curl -X PUT ENDPOINT/api/v2/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' -d @dashboard.json
    ```
    {: codeblock}

    Where

    * `ENDPOINT` is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * `SYSDIG_API_TOKEN` is the API token that you got in the previous step.

    * `dashboard.json` is the json file that describes the dashboard.

For example, to modify a dashboard, the json file is what you got from step 2, but omit the following keys:

* `customerId`
* `userId`
* `domain`
* `schema`
* `createdOn`
* `modifiedOn`

Then make your desired modifications. For example, a dashboard.json looks as follows:

```
{
  "dashboard": {
    "autoCreated": true,
    "eventsOverlaySettings": {...},
    "scopeExpressionList": null,
    "teamId": ...,
    "widgets": [...],
    "version": 1,
    "name": "My Modified Dashboard Name",
    "public": false,
    "publicToken": null,
    "shared": true,
    "username": "...",
    "id": ...
  }
}
```
{: screen}


## Deleting a dashboard by using the API
{: #api_delete_dashboard}

Complete the following steps to delete a dashboard from the list of dashboards that is available for a team:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Get all the dashboards that are available for the team. For more information, see [Saving dashboards by using the API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard).

3. Find the ID of the dashboard you want to delete. Look for the the **id** value that is associated with the dashboard **name** that you want to delete.

4. Run the following cURL command:

    ```
    curl -X DELETE ENDPOINT/api/v2/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Where

    * `ID` is the ID of the dashboard that you want to delete.

    * `ENDPOINT` is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * `SYSDIG_API_TOKEN` is the API token that you got in the previous step.

For example, to delete the dashboard with ID *391* from the list of dashboards for a team that works in the US South region, you can run the following command:

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/api/v2/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}
