---

copyright:
  years:  2018, 2023
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, alerting, api

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Managing alerts by using the Python client
{: #alert_python}

You can manage alerts in an {{site.data.keyword.mon_full_notm}} instance by using the {{site.data.keyword.mon_short}} Python client.
{: shortdesc}

To learn how to use the Python client, see [Using the Python client](/docs/monitoring?topic=monitoring-python-client).

## Create an alert (POST)
{: #alert-python-create-alert}

The following code shows the structure of a Python script that you can use to create an alert:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <MONITORING-ENDPOINT>
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Add the notification channels to send an alert when the alert is triggered
notify_channels = [
  {
    'type': 'SLACK',
    'channel': '<SLACK_CHANNEL_NAME>'
  },
  {
    'type': 'EMAIL',
    'emailRecipients': [
      'user1@ibm.com', 'user2@ibm.com'
    ]
  }
]

# Get the IDs of the notification channels that you have configured
res = sdclient.get_notification_ids(notify_channels)
if not res[0]:
    print("Failed to fetch notification channel ID's")

notification_channel_ids = res

# Create and define the alert details
res = sdclient.create_alert(
    name=<ALERT_NAME>,
    description=<ALERT_DESCRIPTION>,
    severity=<SEVERITY>,
    for_atleast_s=<FOR_ATLEAST_S>,
    condition=<CONDITION>,
    segmentby=<SEGMENTBY>,
    segment_condition=<SEGMENT_CONDITION>,
    user_filter=<USER_FILTER>,
    notify=<NOTIFICATION_CHANNEL_IDS>,
    enabled=<ENABLED>,
    annotations=<ANNOTATIONS>,
    alert_obj=<ALERT_OBJ>
)

if not res[0]:
    print("Alert creation failed")
```
{: codeblock}

Consider the following information when you create a Python script:

* You must include the following information: `<MONITORING-ENDPOINT>`, `<IAM_APIKEY>`, and `<GUID>` These data is required to authenticate the request with the monitoring instance. To get the monitoring instance information, see [Authenticate your user or service ID by using IAM](/docs/monitoring?topic=monitoring-python-client#python-client-iam-auth).

* You must define the notification channels through which you want to be notified when the alert is triggered.

    Valid notification channel types are `SLACK`, `PAGER_DUTY`, `VICTOROPS`, `WEBHOOK`, and `EMAIL`.

    When you define the notification channels, the channels must be configured in the monitoring instance.

    When you add an email notification channel, you can add multiple recipients. You separate values by using a comma.

    When you define a Slack channel, replace `<SLACK_CHANNEL_NAME>` with the name of your channel. You must include the symbol `#` with the name of the channel, for example, `#my_monitoring_alert_channel`.


When you configure the alert, complete the following sections:

* [`name` and `description`]: You must define a unique name for the alert name by replacing `<ALERT_NAME>`, and optionally, add a description by replacing `<ALERT_DESCRIPTION>`.

* [`severity`]: You must define the severity of the alert by replacing `<SEVERITY>` with a number. Valid values are `0`, `1`, `2`, `3`, `4`, `5`, `6`, and `7`.

* [`for_atleast_s`]: You must define the number of consecutive seconds that the condition is met before the alert is triggered. Replace `<FOR_ATLEAST_S>` with the number of seconds.

* [`condition`]: You must define the condition that defines when the alert is triggered. For example, you can set this parameter to `['host.mac', 'proc.name']` to check a CPU alert for every process on every machine.

    For more information, see [Multi-Condition Alerts](/docs/monitoring?topic=monitoring-alerts).

* [`segmentby`]: You can define the scope of an alert by configuring the `segmentedby` section. The default value is `ANY`.

* [`segment_condition`]: When the parameter *segmentby* is specified, set this field to determine when the alert will be triggered. Valid values are **ANY** and **ALL**.

* [`user_filter`]: You can define a filter that indicates when a notification is sent. For example, you could define this entry if you want to receive a notification only if the name of the process meets the condition.

* [`notify`]: You can define the type of notifications that you want the alert to generate. Set this entry to the notification IDs of the channels that you have defined.

* [`enabled`]: You can configure the status of the alert when it is created. By default, alerts are enabled and the entry is set to `true`. Set to `false` if you do not want it enabled when you create it.

* [`annotations`]: You can add custom properties that you can associate with the alert.

* [`alert_obj`]: You can attach an alert object instead of specifying the individual parameters.



## Updating an alert (PUT)
{: #alert-python-update-alert}

To update an existing alert, you need the ID of that alert.
{: note}

The following code shows the structure of a Python script that you can use to update an alert:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <MONITORING-ENDPOINT>
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

res = sdclient.get_alerts()
if not res[0]:
    print("Failed to fetch existing alerts")

alert_found = False

for alert in res['alerts']:
    if alert['name'] == alert_name:
        alert_found = True
        if 'notificationChannelIds' in alert:
            alert['notificationChannelIds'] = alert['notificationChannelIds'][0:-1]
        update_txt = '(changed by update_alert)'
        if alert['description'][-len(update_txt):] != update_txt:
            alert['description'] = alert['description'] + update_txt
        alert['timespan'] = alert['timespan'] * 2  # Note: Expressed in seconds * 1000000
        res_update = sdclient.update_alert(alert)

        if not res_update:
            print("Alert update failed")

if not alert_found:
    print('Alert to be updated not found')
```
{: codeblock}


## Deleting an alert (DELETE)
{: #alert-python-delete-alert}

To delete an existing alert, you need the ID of that alert.
{: note}

The following code shows the structure of a Python script that you can use to delete an alert:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <MONITORING-ENDPOINT>
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

res = sdclient.get_alerts()
if not res[0]:
    print("Failed to fetch existing alerts")

for alert in res['alerts']:
    if alert['name'] == alert_name:
        print("Deleting alert")
        res = sdclient.delete_alert(alert)
        if not res:
            print("Alert deletion failed")
```
{: codeblock}


## Get all user alerts (GET)
{: #alert-python-fetch-user-alerts}


The following code shows the structure of a Python script that you can use to get information about all the alerts:

```python
# Reference the Python client
from sdcclient import IbmAuthHelper, SdMonitorClient

# Add the monitoring instance information that is required for authentication
URL = <MONITORING-ENDPOINT>
APIKEY = <IAM_APIKEY>
GUID = <GUID>
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)

# Instantiate the Python client
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

json_res = sdclient.get_alerts()
print(json_res)
```
{: codeblock}
