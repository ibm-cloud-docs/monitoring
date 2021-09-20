---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, api token

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Working with Monitor API tokens
{: #api_monitoring_token}

You can use Monitor API tokens to authenticate with the {{site.data.keyword.mon_full_notm}} service when you use Python scripts or the {{site.data.keyword.mon_full_notm}} REST API to automate routine tasks and monitor notifications. 
{: shortdesc}

Consider the following information for each instance of the {{site.data.keyword.mon_full_notm}} service:

* There is a Monitor API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.


## Getting the Monitor API token through the monitoring UI
{: #api_token_get}

Complete the following steps to get the Monitor API token :

1. From the *Selector* button in the navigation bar, choose **Settings**
2. From the *Monitor API* section, copy the **Monitor API Token**.

After you get the token, you can run API calls and use this token in the `Authorization` header. 

When you copy the token include the `Bearer` keyword: `Authorization: Bearer MONITOR_API_TOKEN`
{: note}


## Resetting the Monitor API token through the monitoring UI
{: #api_token_reset}

Complete the following steps to reset the Monitor API token :

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. In the *Monitor API* section, click **Reset Token** to reset the API token.



## Getting the Monitor API token by using the API
{: #api_token_get_api}

You can use the Token API to get the Monitor API token .

For example, you can use the following cURL command to get the Monitor API token :

```shell
curl -X GET <MONITORING_REST_API_ENDPOINT>/api/token -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}


```
GET <MONITORING_REST_API_ENDPOINT>/api/token -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where 

* `<MONITORING_REST_API_ENDPOINT>` indicates the endpoint targetted by the REST API call. For more information, see [REST API endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com/api`

* You can pass multiple headers by using `-H`. 

    `Authorization` and `IBMInstanceID` are headers that are required for authentication. 

    `TeamID` defines the team for which you want to get the Monitor API token .
    
    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM Tokens](/docs/monitoring?topic=monitoring-mon-curl#mon-curl-headers-iam).


When the authorization that is allowed in a monitoring instance is set to `IAM_ONLY`, you get the following response `{"errors":[{"reason":"Not enough privileges to complete the action","message":"Access is denied"}]}` when you try to get the Monitor API token .
{: note}


### Sample JSON code
{: #api_token_get_api_json}

You can use the following sample JSON code to get the Monitor API token :

 ```json
def get_sysdig_api_token(self, instance_guid):
    """ Get the Monitor API token  by calling the /api/token endpoint """
    if self.access_token == None:
        self.get_iam_token()
    if self.access_token == None:
        # If the token is still None we have problems ....
        return None
    headers = { "Authorization": self.access_token,
                "Accept": "application/json",
                "IBMInstanceID": instance_guid }
    url = self.sysdig_endpoint + "/api/token"
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        data = response.json()
        return data["token"]["key"]
    else:
        print_error("Error getting Monitor API token  - {}".format(response.text))
        return None
```
{: codeblock}




