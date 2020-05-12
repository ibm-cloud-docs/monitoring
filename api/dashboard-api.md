---

copyright:
  years:  2018, 2019
lastupdated: "2019-06-26"

keywords: Sysdig, IBM Cloud, monitoring, dashboard, api

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

# Dashboard API Operations

## Working with cURL
{: #curl-guide}

```shell
curl -X <METHOD> <SYSDIG_ENDPOINT>/<API_URL> <-H HEADERS,> [-d DATA]
```

An example being:
```shell
curl -X POST \
  https://us-south.monitoring.test.cloud.ibm.com/api/v2/dashboards \
  -H 'Authorization: Bearer eyJraW...' \
  -H 'IBMInstanceID: fc8ceb8a-...' \
  -H 'Content-Type: application/json' \
  -d @dashboard.json
```

* [Sysdig endpoints](https://test.cloud.ibm.com/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_sysdig)

**Headers for IAM Tokens (Recommended)**:
```shell
-H "Authorization: Bearer $AUTH_TOKEN"
-H "IBMInstanceID: $GUID"
```
* `AUTH_TOKEN=$(ibmcloud iam oauth-tokens | awk '{print $4}')`
* `GUID=$(ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid')`

**Headers for Sysdig Token**:
```shell
-H "Authorization: Bearer $SYSDIG_TOKEN"
```
* `SYSDIG_TOKEN` can be found in the Sysdig dashboard settings under Sysdig Monitor API

## Fetch all of a user's dashboards

Useful for finding a specific dashboard's ID for subsequent HTTP methods.

### Using python client

  ```python
  from sdcclient import IbmAuthHelper, SdMonitorClient

  URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
  APIKEY = <IAM_APIKEY>
  GUID = <GUID>
  ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
  sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

  json_res = sdclient.get_dashboards()
  print(json_res)
  ```

### Using curl

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| GET | `api/v2/dashboards` | |

## Fetch a user's dashboard

Fetching an existing dashboard requires the user to know the ID of that dashboard.

### Using curl to fetch a single dashboard

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| GET | `api/v2/dashboards/<ID>` | |

## Create a new dashboard

### Using the python client to create a dashboard from scratch

  ```python
  from sdcclient import IbmAuthHelper, SdMonitorClient

  URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
  APIKEY = <IAM_APIKEY>
  GUID = <GUID>
  ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
  sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

  ok, res = sdclient.create_dashboard("My New Dashboard from Python")
  if not ok:
      print("Dashboard creation failed")
  ```

### Using the python client to create new dashboard from existing ones

#### Creating a dashboard by copying an existing dashboard (and applying a new filter on it)

  ```python
  from sdcclient import IbmAuthHelper, SdMonitorClient

  # Name for the dashboard to create
  new_name = "My new cpu dashboard"
  # Existing dashboard to copy
  existing_name = "My Existing Dashboard"
  # New filter to apply
  scope_filter = "container.name = carboncache"

  URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
  APIKEY = <IAM_APIKEY>
  GUID = <GUID>
  ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
  sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

  res = sdclient.create_dashboard_from_dashboard(new_name, existing_name, scope_filter)
  if not res[0]:
      print("Dashboard creation failed")
  ```

#### Creating a dashboard by copying an existing view (and applying a new filter on it)

  ```python
  from sdcclient import IbmAuthHelper, SdMonitorClient

  # Name for the dashboard to create
  new_name = "K8s processes in prod"
  # Existing dashboard to copy
  existing_view_name = "Overview by Process"
  # New filter to apply
  scope_filter = "kubernetes.namespace.name = prod and proc.name = cassandra"

  URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
  APIKEY = <IAM_APIKEY>
  GUID = <GUID>
  ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
  sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

  res = sdclient.create_dashboard_from_view(new_name, existing_view_name, scope_filter)
  if not res[0]:
      print("Dashboard creation failed")
  ```

### Using curl to create a new dashboard from json body

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| POST | `api/v2/dashboards` | dashboard.json |

Here's a minimal dashboard.json for example:

- `name` needs to be set accordingly
- `widgets` needs to be set
- `id` tag needs to be `null`
- `version` tag needs to be `null`
- `username` should be your IBM email i.e. `you@ibm.com`

  ```json
  {
    "dashboard": {
      "filterExpression": null,
      "name": "My Brand New Dashboard",
      "widgets": [
        {
          "showAs": "summary",
          "name": "Average Request Time",
          "gridConfiguration": {
            "col": 7,
            "row": 1,
            "size_x": 3,
            "size_y": 2
          },
          "customDisplayOptions": {
            "valueLimit": {
              "count": 10,
              "direction": "desc"
            },
            "histogram": {
              "numberOfBuckets": 10
            },
            "yAxisScale": "linear",
            "yAxisLeftDomain": {
              "from": 0,
              "to": null
            },
            "yAxisRightDomain": {
              "from": 0,
              "to": null
            },
            "xAxis": {
              "from": 0,
              "to": null
            }
          },
          "scope": null,
          "overrideScope": false,
          "metrics": [
            {
              "id": "net.http.request.time",
              "propertyName": "v0",
              "timeAggregation": "avg",
              "groupAggregation": "avg"
            }
          ],
          "compareToConfig": null,
          "colorCoding": null
        }
      ],
      "username": "you@ibm.com",
      "version": null,
      "schema": 1,
      "id": null
    }
  }
  ```

## Update a user's dashboard

Modification of an existing dashboard requires the user to know the ID of that dashboard.

### Using curl to modify a dashboard from json body

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| PUT | `api/v2/dashboards/<ID>` | dashboard.json |

The dashboard.json is the same as GET, but _omit_ the following keys:

- customerId
- userId
- domain
- schema
- createdOn
- modifiedOn

  ```json
  {
    "dashboard": {
      "autoCreated": false,
      "eventsOverlaySettings": {
        "showNotificationsEnabled": true,
        "filterNotificationsUserInputFilter": "",
        "eventOverlayLimit": 1000,
        "filterNotificationsTypeFilter": "all",
        "filterNotificationsStateFilter": "all",
        "filterNotificationsSeverityFilter": "all",
        "filterNotificationsResolvedFilter": "all"
      },
      "scopeExpressionList": null,
      "teamId": 12345,
      "widgets": [
        ...
      ],
      "version": 1,
      "name": "My Modified Dashboard",
      "public": false,
      "publicToken": null,
      "shared": false,
      "username": "you@ibm.com",
      "id": 12345
    }
  }
  ```

## Delete a user's dashboard

Deletion of an existing dashboard requires the user to know the ID of that dashboard.

### Using python client

  ```python
  from sdcclient import IbmAuthHelper, SdMonitorClient

  # Name of the dashboard you want to delete
  pattern = "Nginx production"

  URL = <SYSDIG-ENDPOINT> # ex: "https://us-south.monitoring.cloud.ibm.com"
  APIKEY = <IAM_APIKEY>
  GUID = <GUID>
  ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
  sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

  # Fetch all dashboards first
  res = sdclient.get_dashboards()

  # Loop through all fetched dashboards
  for dashboard in res[1]['dashboards']:
      # Delete dashboard if it matches the pattern (one or many)
      if pattern in dashboard['name']:
          print("Deleting " + dashboard['name'])
          res = sdclient.delete_dashboard(dashboard)
  ```

### Using curl

Check out [Working with cURL](#curl-guide)

| Method | API_URL | Data File |
|----|---|----|
| DELETE | `api/v2/dashboards/<ID>` | |

Finally, for further information on getting started with the Sysdig monitor interface, you can check out the [getting started docs](https://docs.sysdig.com/en/getting-started.html).
