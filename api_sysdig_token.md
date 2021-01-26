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


# Working with Sysdig tokens
{: #api_sysdig_token}

You can use Sysdig API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the Sysdig REST API to automate routine tasks and monitor notifications. 
{:shortdesc}

Consider the following information for each instance of the {{site.data.keyword.mon_full_notm}} service:

* There is a Sysdig API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.


## Getting the Sysdig API token through the Sysdig web UI
{: #api_token_get}

Complete the following steps to get the Sysdig token:

1. From the *Selector* button in the navigation bar, choose **Settings**
2. From the *Sysdig Monitor API* section, copy the **Sysdig Monitor API Token**.

After you get the token, you can run API calls and use this token in the `Authorization` header. 

When you copy the token include the `Bearer` keyword: `Authorization: Bearer SYSDIG_TOKEN`
{: note}


## Resetting the Sysdig API token through the Sysdig web UI
{: #api_token_reset}

Complete the following steps to reset the Sysdig token:

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. In the *Sysdig Monitor API* section, click **Reset Token** to reset the API token.



## Getting the Sysdig API token by using the Sysdig API
{: #api_token_get_api}

You can use the Token API to get the Sysdig token.

For example, you can use the following cURL command to get the Sysdig token:

```shell
curl -X GET <SYSDIG_REST_API_ENDPOINT>/api/token -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}


```
GET <SYSDIG_REST_API_ENDPOINT>/api/token -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "SysdigTeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where 

* `<SYSDIG_REST_API_ENDPOINT>` indicates the endpoint targetted by the REST API call. For more information, see [Sysdig REST API endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. 

    `SysdigTeamID` defines the team for which you want to get the Sysdig token.
    
    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mon-curl#mon-curl-headers-iam).


When the authorization that is allowed in a Sysdig instance is set to `IAM_ONLY`, you get the following response `{"errors":[{"reason":"Not enough privileges to complete the action","message":"Access is denied"}]}` when you try to get the Sysdig token.
{: note}


### Sample JSON code
{: #api_token_get_api_json}

You can use the following sample JSON code to get the Sysdig token:

 ```json
def get_sysdig_api_token(self, sysdig_instance_guid):
    """ Get the Sysdig token by calling the /api/token endpoint """
    if self.access_token == None:
        self.get_iam_token()
    if self.access_token == None:
        # If the token is still None we have problems ....
        return None
    headers = { "Authorization": self.access_token,
                "Accept": "application/json",
                "IBMInstanceID": sysdig_instance_guid }
    url = self.sysdig_endpoint + "/api/token"
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        data = response.json()
        return data["token"]["key"]
    else:
        print_error("Error getting Sysdig token - {}".format(response.text))
        return None
```
{: codeblock}




