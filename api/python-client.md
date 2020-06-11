---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-12"

keywords: Sysdig, IBM Cloud, monitoring, alerting, api, python

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


# Using a Python client to make Sysdig REST API calls
{: #python-client}

You can use the [Python Client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/draios/python-sdc-client){:new_window} to manage the {{site.data.keyword.mon_full_notm}} service. The client is also known as the **sdcclient**.
{:shortdesc}


## Installing the Python client
{: #python-client-install}


### Installing the Python client by using pip
{: #python-client-install-pip}

From a terminal, run the following comnmnand:

The **sddclient** version must be at least 0.9.x.
{: important}

```shell
# sddclient version must be at least 0.9.0
pip install sdcclient
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

3. Create a Python script.

    ```shell
    touch script.py
    ```
    {: pre}

4. Confirm `python-sdc-client/script.py is listed when you verify the contents of the folder `python-client`.

    ```shell
    ls
    ```
    {: pre}


## Reference the Python client in your Python script
{: #python-client-reference-client}
    
## Reference the Python client that is installed by using pip
{: #python-client-reference-pip-client}

You can reference the Python client by adding the following statement to your application:

```python
from sdcclient import IbmAuthHelper, SdMonitorClient
```
{: pre}


## Reference the Python client that is installed by cloning a GitHub repo
{: #python-client-reference-github-client}

Add the following entries to your Python script to import the GitHub cloned package into your script:

```python
import sys
sys.path.append("python-sdc-client")
from sdcclient import IbmAuthHelper, SdMonitorClient
```
{: codeblock}


## Authenticate your user or service ID by using IAM
{: #python-client-iam-auth}

To use {{site.data.keyword.cloud_notm}} IAM authentication with the Python client, you must use a Sysdig endpoint, an API key, and the GUID from your {{site.data.keyword.mon_full_notm}} instance.

Complete the following steps:

1. From a terminal, get the GUID of your {{site.data.keyword.mon_full_notm}} instance. Run the following command:

    ```
    ibmcloud resource service-instance <NAME>
    ```
    {: pre}

2. Add the following entries to your Python script:

    ```python
    from sdcclient import IbmAuthHelper, SdMonitorClient

    URL = <SYSDIG-ENDPOINT>
    APIKEY = <IAM_APIKEY>
    GUID = <GUID>
    ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
    sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)
    ```
    {: codeblock}

    Where

    `<SYSDIG-ENDPOINT>` must be replaced with the endpoint where the monitoring instance is available. For more inforamtion, see [Sysdig endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_sysdig). For example, the endpoint for an instance that is available in us-south is the following: `https://us-south.monitoring.cloud.ibm.com`

    `<IAM_APIKEY>` must be replaced with a valid IAM API key. For more information, see [Working With API Tokens](/docs/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

    `<GUID>` must be replaced with the GUID of the monitoring instance that you obtain in the previous step. To get the GUID of the monitoring instance, run the following command: `ibmcloud resource service-instance <NAME> --output json | jq -r '.[].guid')`


You can now use the `sdclient` to perform actions that will be authenticated by using IAM.





