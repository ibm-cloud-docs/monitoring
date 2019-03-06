---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

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


# Working with the Sysdig REST API
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

    * *name*: Enter the name of the dashboard.

    * *id*: Set to *null*.

    * *version*: Set to *null*.

    * username: Set to the email that is associated with your IBMid.

    * *isShared*: Set to true to share the dashboard with other team members.

    * *isPublic*: Set to true if you want the dashboard to be available publicly.

    * Configure filters to define the dashboard scope.
    
3. Create the dashboard. Run the following cURL command:

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    where

    * *ENDPOINT* is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* is the API token you got in the previous step.

    * *dashboard.json* is the file that describes the new dashboard, including panels and metrics.

For example, to create a dashboard, a sample json file looks as follows:
```
{
  "dashboard": {
    "filterExpression": null,
    "name": "My new dashboard",
    "items": [
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
        "overrideFilter": true,
        "showAsType": "line",
        "showAs": "timeSeries",
        "groupId": "My new cpu dashboardcontainer.namecarboncache1",
        "metrics": [
          {
            "propertyName": "k0",
            "metricId": "timestamp"
          },
          {
            "propertyName": "v0",
            "metricId": "cpu.used.percent",
            "aggregation": "avg",
            "groupAggregation": "avg"
          }
        ],
        "paging": {
          "to": 9,
          "from": 0
        },
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
    "isPublic": false,
    "annotations": {
      "createdByEngine": true
    },
    "username": "ENTER YOUR EMAIL ADDRESS",
    "version": null,
    "layout": [
      {
        "size_y": 4,
        "size_x": 6,
        "col": 1,
        "row": 1
      }
    ],
    "schema": 1,
    "id": null,
    "isShared": false
  }
}
```
{: screen}



## Saving the dashboards of a team by using the API
{: #api_save_dashboard}

Complete the following steps to download the dashboards that are available for a team:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Run the following cURL command:

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    where

    * *ENDPOINT* is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* is the API token you got in the previous step.

For example, to download the dashboards for a team working in the US South region, you can run the following command:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

The output is a JSON file where each dashboard starts with the field **id**. The name of the dashboard is specified in the field **name**.


## Deleting a dashboard by using the API
{: #api_delete_dashboard}

Complete the following steps to delete a dashboard from the list of dashboards that is available for a team:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Get all the dashboards that are available for the team. For more information, see [Saving dashboards by using the API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard).

3. Find the ID of the dashboard you want to delete. Look for the the **id** value that is associated with the dashboard **name** that you want to delete.

4. Run the following cURL command:

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    where

    * *ID* is the ID of the dashboard that you want to delete.

    * *ENDPOINT* is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* is the API token you got in the previous step.

For example, to delete the dashboard with ID *391* from the list of dashboards for a team working in the US South region, you can run the following command:

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




