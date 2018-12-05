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


# Working with the Sysdig Python library and REST API
{: #sysdig_python_lib}

Use the Sysdig REST API to automate routine tasks and monitor notifications. You can also use the Sysdig Python library. Notice that the library exposes part of the Sysdig REST API functionality. 
{:shortdesc}

When you use the API from your custom scripts or programs, you must use a Sysdig token to authenticate with the IBM Cloud Monitoring with Sysdig instance. 
{: tip}

## Configuring the local environment to run Python scripts
{: #config_env}

Complete the following steps to configure your local environment to run programmatic dashboard tasks:

1. Install the following software:

    * Python 2.x (2.7.x)

    * pip version 1.3 or later. (Note: pip is installed as part of the Python package for version 2.7 and later versions.)

2. Install the Sysdig Python client. Choose one of the following options:

    * Option 1: Install the client by using **pip**. Run the following command: 
    
        ```
        pip install sdcclient
        ```
        {: codeblock}

    * Option 2: Download [Sysdig Monitor/Secure Python client library [External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/draios/python-sdc-client){:new_window}. Then, unpack the *.zip* file.

    * Option 3: Clone the repository. Run the following command:

        ```
        git clone https://github.com/draios/python-sdc-client.git
        ```
        {: codeblock}

        Change to the *python-sdc-client* directory, and run the following command:

        ```
        python setup.py install
        ```
        {: codeblock}



The library exports the *SdcClient* library. To instantiate its functions, you can use the following code:

```
#! /usr/bin/python

# import client
from sdcclient import SdcClient

# Input Sysdig API token
api_token = "SYSDIG_API_TOKEN"

# Instantiate the Sysdig client

sdclient = SdcClient(sdc_token)
```
{: codeblock}



## Creating a dashboard by using the API
{: #create_api}

You can create a dashboard by duplicating an existing dashboard.  

Complete the following steps to create a dashboard:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#token).

2. Create the json file that describes the dashboard. The following fields must be set as indicated:

    * *name*: Enter the name of the dashboard.

    * *id*: Set to *null*.

    * *version*: Set to *null*.

    * username: Set to the email that is associated with your IBMid.

    * *isShared*: Set to true to share the dashboard with other team members.

    * *isPublic*: Set to true if you want the dashboard to be avalilable publicly.

    * Configure filters to define the dashboard scope.
    
3. Create the dashboard. Run the following cURL command:

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    where

    * *ENDPOINT* is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

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
{: #save_api}

Complete the following steps to download the dashboards that are available for a team:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#token).

2. Run the following cURL command:

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    where

    * *ENDPOINT* is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

    * *SYSDIG_API_TOKEN* is the API token you got in the previous step.

For example, to download the dashboards for a team working in the US South region, you can run the following command:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

The output is a JSON file where each dashboard starts with the field **id**. The name of the dashboard is specified in the field **name**.


## Deleting a dashboard by using the API
{: #delete_api}

Complete the following steps to delete a dashboard from the list of dashboards that is available for a team:

1. Get the Sysdig API token for the team whose dashboards you want to save. For more information, see [Getting the Sysdig API token](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#token).

2. Get all the dashboards that are available for the team. For more information, see [Saving dashboards by using the API](/docs/services/Monitoring-with-Sysdig/sysdig_python_lib.html#save_api).

3. Find the ID of the dashboard you want to delete. Look for the the **id** value that is associated with the dashboard **name** that you want to delete.

4. Run the following cURL command:

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    where

    * *ID* is the ID of the dashboard that you want to delete.

    * *ENDPOINT* is the URL for the region where the monitoring instance is available. For more information, see [Sysdig endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

    * *SYSDIG_API_TOKEN* is the API token you got in the previous step.

For example, to delete the dashboard with ID *391* from the list of dashboards for a team working in the US South region, you can run the following command:

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




