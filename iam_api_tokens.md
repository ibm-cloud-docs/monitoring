---

copyright:
  years:  2018, 2021
lastupdated: "2021-01-20"

keywords: Sysdig, IBM Cloud, monitoring, api token

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

# Using IAM API tokens to authenticate Sysdig services
{: #iam_api_tokens}

In {{site.data.keyword.cloud_notm}}, you can use IAM tokens to authenticate with Sysdig services while using the Sysdig Python scripts or the REST APIs to automate regular monitoring tasks, such as creating dashboards or alerts. The caller can optionally indicate the team they are attempting to access, as opposed to defaulting to the Monitoring Operations team.

## Prerequisites

Complete the tasks listed in the following:

* [Working with API tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-api_token)
* [Granting permissions to launch the Sysdig UI or to make REST API calls](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-iam_grant)
* Retrieve the Sysdig team ID. For more information, see [Retrieving the Sysdig team ID](#retrieving-the-sysdig-team-ID)

## HTTP authorization request headers

* **Authorization**: The IBM IAM bearer token that is used to authenticate with the IBM Cloud Monitoring with Sysdig service instance.
* **IBMInstanceID**: The unique ID of the IBM Cloud Monitoring with Sysdig instance that you want to target with the cURL command.
* **SysdigTeamID**: The unique identification code for the Sysdig team that the IBM Cloud user or the service ID is part of. SysdigTeamID is an optional header. Specifying a team ID overrides the sysdig default team that the user automatically launched into.


## Retrieving the Sysdig team ID

### Example request

The following POST (using cURL) command gets a list of teams and their IDs for an authorized user:

```
curl -v -H "Authorization: Bearer IBM_IAM_TOKEN_HERE"   -H "IBMInstanceID: INSTANCE_ID_HERE"   https://<region>-<host>.cloud.ibm.com/api/teams

```
Replace <region> and <host> with the region and the hostname of your IBM Cloud. Replace IBM_IAM_TOKEN_HERE with your IAM token. Replace INSTANCE_ID_HERE with the ID of the Sysdig service instance.

### Example responses

The following response retrieves all the teams that the authorized user is associated with. Identify the team and copy the team ID for team-specific tasks.

```
{
  "teams": [
    {
      "description": "Immutable Monitor team with full visibility",
      "version": 0,
      "name": "Monitor Operations",
      "properties": {},
      "id": 1478,
      "default": true,
      "origin": "SYSDIG",
      "dateCreated": 1602710062000,
      "entryPoint": {
        "module": "Explore"
      },
      "show": "host",
      "customerId": 1566,
      "products": [
        "SDC"
      ],
      "theme": "#7BB0B2",
      "lastUpdated": 1602710062000,
      "defaultTeamRole": "ROLE_TEAM_EDIT",
      "namespaceFilters": {},
      "immutable": true,
      "canUseSysdigCapture": true,
      "userCount": 1,
      "canUseCustomEvents": true,
      "canUseAwsMetrics": true,
      "canUseBeaconMetrics": true
    },
    {
      "description": "",
      "version": 0,
      "name": "TestTeam1",
      "properties": {},
      "id": 1489,
      "default": false,
      "origin": "SYSDIG",
      "dateCreated": 1602710654000,
      "entryPoint": {
        "module": "Explore"
      },
      "show": "host",
      "customerId": 1566,
      "products": [
        "SDC"
      ],
      "theme": "#73A1F7",
      "lastUpdated": 1602710654000,
      "defaultTeamRole": "ROLE_TEAM_EDIT",
      "namespaceFilters": {},
      "immutable": false,
      "canUseSysdigCapture": false,
      "userCount": 1,
      "canUseCustomEvents": false,
      "canUseAwsMetrics": false,
      "canUseBeaconMetrics": false
    }
  ]
}
```

## Making data requests

### Example request

The following POST (using cURL) command retrieves the dashboards associated with a given team:

```
curl -v -H "Authorization: Bearer IBM_IAM_TOKEN_HERE"  -H "IBMInstanceID: INSTANCE_ID_HERE"  -H "SysdigTeamID: SYSDIG_TEAM_ID_HERE"   https://<region>-<host>.cloud.ibm.com/api/v3/dashboards
```

Replace SYSDIG_TEAM_ID_HERE with the [team ID](#getting-the-sysdig-team-ID)that you have retrieved. Replace <region> and <host> with the region and the hostname of your IBM Cloud.

### Example response

A redacted example response is given below:

```
{
  "dashboards": [
    {
      "id": 3442,
      "teamId": 1478,
      "userId": 1267,
      "name": "New Dashboard",
      "panels": [
        {
          ...
      ],
      "shared": false,
      "public": false,
      "version": 1,
      "createdOn": 1602710683000,
      "modifiedOn": 1602710683000,
      "description": "",
      "layout": [
        {
          "panelId": 1,
          "x": 0,
          "y": 0,
          "w": 8,
          "h": 8
        }
      ],
      "sharingSettings": [],
      "publicToken": "abc123",
      "favorite": false,
      "schema": 3,
      "username": "User Name (your_name@account.com)",
      "permissions": [
        "dashboards.read",
        "dashboards.sharing",
        "dashboards.delete",
        "dashboards.edit",
        "dashboards.transfer"
      ]
    }
  ]
}
```
