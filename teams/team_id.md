---

copyright:
  years:  2018, 2024
lastupdated: "2024-06-28"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Getting the ID of a team
{: #team_id}

You can use the Teams REST API to get the ID of a team.
{: shortdesc}


## Step 1. Get the IAM token
{: #team_id_step1}

Get the IAM access token:

```text
export AUTH_TOKEN=`ibmcloud iam oauth-tokens | grep IAM | cut -d \: -f 2 | sed 's/^ *//'`
```
{: pre}


## Step 2. List teams by using cURL
{: #team_id_step2}


You can use the following [cURL command](/docs/monitoring?topic=monitoring-mon-curl) to list the teams that are available in a monitoring instance and identify the ID of a specific team:

```shell
curl <REST_API_ENDPOINT>/teams -H "Authorization: $AUTH_TOKEN" -H "content-type: application/json" -H "IBMInstanceID: $GUID"
```
{: codeblock}

Where

* `<REST_API_ENDPOINT>`indicates the endpoint targetted by the REST API call. For more information, see [REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).



## Sample
{: #team_id_sample}

For example, to get the ID of a team that is available in a monitoring instance in US-South, you can run the following command:

```text
curl -v  https://us-south.monitoring.cloud.ibm.com/api/teams  -H "Authorization:  $AUTH_TOKEN"   -H "content-type: application/json"  -H "IBMInstanceID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```
{: codeblock}


The response includes information about all the teams where the user is a member. To get the ID of a team, identify the team in the response.

For example, a sample response looks as follows:

```json
{
    "teams": [
        {
            "version": 4,
            "name": "Monitor Operations",
            "properties": {},
            "id": 26055,
            "default": true,
            "products": [
                "SDC"
            ],
            "origin": "SYSDIG",
            "description": "Immutable Monitor team with full visibility",
            "dateCreated": 1599751614000,
            "lastUpdated": 1610313489000,
            "entryPoint": {
                "module": "Overview"
            },
            "customerId": 99999,
            "namespaceFilters": {
                "ibmPlatformMetrics": null
            },
            "theme": "#7BB0B2",
            "show": "host",
            "defaultTeamRole": "ROLE_TEAM_EDIT",
            "immutable": true,
            "canUseSysdigCapture": true,
            "canUseCustomEvents": true,
            "canUseAwsMetrics": false,
            "canUseBeaconMetrics": true,
            "userCount": 3
        }
    ]
}
```
{: screen}
