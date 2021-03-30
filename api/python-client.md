---

copyright:
  years:  2018, 2020
lastupdated: "2020-07-10"

keywords: IBM Cloud, monitoring, alerting, api, python

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


# Using the Python client
{: #python-client}

You can use the Python Client to manage the {{site.data.keyword.mon_full_notm}} service. The client is also known as the **sdcclient**.
{:shortdesc}

These instructions apply to Python version 3.x.
{: note}

To manage resources that are associated with the default team, use IAM as your authentication method.
{: important}

To manage resources that are associated with a team, you must use the Sysdig token that is active for the team.
{: important}

## Step 1. Installing the Python client
{: #python-client-install}

### Prerequisites
{: #python-client-install-prereqs}

Install the following Python packages that you need when you use Python version 3 or above:

1. Run the following command to install the `request` package:

    ```shell
    pip3 install requests
    ```
    {: pre}

2. Run the following command to install the `pyyaml` package:

    ```
    python3 -m pip install pyyaml
    ```
    {: pre}

### Installing the Python client by using pip
{: #python-client-install-pip}

From a terminal, run the following comnmnand:

The **sddclient** version must be at least 0.9.x.
{: important}

```shell
# sddclient version must be at least 0.9.0
pip3 install sdcclient
```
{: pre}


### Installing the Python client from a GitHub repo
{: #python-client-install-github}

Complete the following steps:

1. Make a folder to copy the client code.

    ```shell
    mkdir python-client && cd python-client
    ```
    {: pre}

2. Clone the repository.

    ```shell
    git clone https://github.com/draios/python-sdc-client.git
    ```
    {: pre}

3. Create an empty Python script.

    ```shell
    touch script.py
    ```
    {: pre}

4. Confirm `python-sdc-client/script.py is listed when you verify the contents of the folder `python-client`.

    ```shell
    ls
    ```
    {: pre}



## Step 2. Reference the Python client in your Python script
{: #python-client-reference-client}
    
### Reference the Python client that is installed by using pip
{: #python-client-reference-pip-client}

You can reference the Python client by adding the following statement to your Python script:

```python
from sdcclient import IbmAuthHelper, SdMonitorClient
```
{: pre}


### Reference the Python client that is installed by cloning a GitHub repo
{: #python-client-reference-github-client}

Add the following entries to your Python script to import the GitHub cloned package into your script:

```python
import sys
sys.path.append("python-sdc-client")
from sdcclient import IbmAuthHelper, SdMonitorClient
```
{: codeblock}


## Step 3. Instantiate the {{site.data.keyword.mon_short}} Python client
{: #python-client-step3}


### Option 1. Authenticate your user or service ID by using IAM
{: #python-client-iam-auth}

To use {{site.data.keyword.cloud_notm}} IAM authentication with the Python client, you must specify a {{site.data.keyword.mon_short}} endpoint, an API key, and the GUID from your {{site.data.keyword.mon_full_notm}} instance.
{: note}

Complete the following steps from a terminal:

1. Get the GUID of your {{site.data.keyword.mon_full_notm}} instance. Run the following command:

    ```
    ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid'
    ```
    {: pre}

2. Get the API key. Run the following command to generate a user API key:

    ```
    ibmcloud iam api-key-create KEY_NAME
    ```
    {: pre}

3. Get the endpoint for the region where the monitoring instance is available. 

    To see the list of endpoints that are available, see [{{site.data.keyword.mon_short}} endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_sysdig). 
    
    For example, the endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com`

4. Add the following entries to your Python script:

    ```python
    from sdcclient import IbmAuthHelper, SdMonitorClient

    URL = <SYSDIG-ENDPOINT>
    # For example: URL = 'https://us-south.monitoring.cloud.ibm.com'

    APIKEY = <IAM_APIKEY>

    GUID = <GUID>

    ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
    sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)
    ```
    {: codeblock}

    Where

    `<SYSDIG-ENDPOINT>` must be replaced with the endpoint where the monitoring instance is available. 

    `<IAM_APIKEY>` must be replaced with a valid IAM API key. [Learn more](/docs/account?topic=account-userapikey).

    `<GUID>` must be replaced with the GUID of the monitoring instance that you obtain in the previous step. 


You can now use the **sdclient** to perform actions that will be authenticated by using IAM.


If you get the error `400 Client Error: Bad Request for url: https://iam.cloud.ibm.com/identity/token`, check the API key. The value that you are passing is not valid.
{: note}



### Option 2. Authenticate by using the Sysdig token
{: #python-client-token-auth}


You must specify a {{site.data.keyword.mon_short}} endpoint, and the Sysdig token that is associated to the team that you want to manage with the Python client.
{: note}

Complete the following steps from a terminal:

1. [Get the Sysdig token](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-api_token#api_token_get).

2. Get the endpoint for the region where the monitoring instance is available. 

    To see the list of endpoints that are available, see [{{site.data.keyword.mon_short}} endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_sysdig). 
    
    For example, the endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com`

3. Add the following entries to your Python script:

    ```python
    from sdcclient import IbmAuthHelper, SdMonitorClient

    URL = <SYSDIG-ENDPOINT>
    # For example: URL = 'https://us-south.monitoring.cloud.ibm.com'
    
    SYSDIG_TOKEN = <SYSDIG_TOKEN>
    # For example: SYSDIG_TOKEN = 'xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

    sdclient = SdMonitorClient(token=SYSDIG_TOKEN,sdc_url=URL)
    ```
    {: codeblock}

    Where

    `<SYSDIG-ENDPOINT>` must be replaced with the endpoint where the monitoring instance is available. 

    `<SYSDIG_TOKEN>` must be replaced with the Sysdig token.


You can now use the **sdclient** to perform actions that will be authenticated by using IAM.


## Sample 1. Python script that uses IAM API key
{: #python-client-sample1}

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <ENDPOINT_URL> <API_KEY> <INSTANCE_GUID>' % sys.argv[0])
   print('ENDPOINT_URL: IBM Cloud endpoint URL (e.g. https://us-south.monitoring.cloud.ibm.com')
   print('API_KEY: IBM Cloud IAM API key. This key is used to retrieve an IAM access token.')
   print('INSTANCE_GUID: GUID of an IBM Cloud Monitoring with {{site.data.keyword.mon_short}} instance.')
   sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]


# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)
```
{: codeblock}


## Sample 2. Python script that uses a Sysdig token
{: #python-client-sample2}

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))

from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <ENDPOINT_URL> <SYSDIG_TOKEN> <INSTANCE_GUID>' % sys.argv[0])
   print('ENDPOINT_URL: IBM Cloud endpoint URL (e.g. https://us-south.monitoring.cloud.ibm.com')
   print('SYSDIG_TOKEN: Sysdig token that is associated to a team.')
   sys.exit(1)

if len(sys.argv) != 3:
   usage()

URL = sys.argv[1]
SYSDIG_TOKEN = sys.argv[2]

# Instantiate the client
sdclient = SdMonitorClient(token=SYSDIG_TOKEN,sdc_url=URL)
```
{: codeblock}


## References
{: #python-client_references}

* [Extracting metrics from a {{site.data.keyword.mon_short}} instance by using the {{site.data.keyword.mon_short}} Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-metrics_python)
* [Managing dashboards by using the {{site.data.keyword.mon_short}} Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-dashboard_python)
* [Managing alerts by using the Python client](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-alert_python)
* [Python Client](https://github.com/draios/python-sdc-client){: external}
* [{{site.data.keyword.mon_short}} Python samples](https://github.com/draios/python-sdc-client/tree/master/examples){: external}

