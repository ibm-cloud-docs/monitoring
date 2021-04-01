---

copyright:
  years:  2018, 2021
lastupdated: "2021-03-28"

keywords: IBM Cloud, monitoring, dashboard, api

subcollection: monitoring

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

# Managing dashboards by using the Python client
{: #dashboard_python}

Use the Python Client to manage dashboards programmatically.
{: shortdesc}

To learn how to use the Python client, see [Using the Python client](/docs/monitoring?topic=monitoring-python-client).

To work with resources in a specific team, you must use the Monitoring (sysdig) token.
{: important}

The following table lists some of the Python functions that you can use to manage dashboards:

| Action | Function |
|--------|----------|
| Create a dashboard | `sdclient.create_dashboard(dashboard_name)` |
| Create a dashboard from a file | `sdclient.create_dashboard_from_file('dashboard_name', 'dashboard_name.json', scope_filter, shared=False, public=True)` |
| Copy a dashboard | `sdclient.create_dashboard_from_dashboard(dashboard_name, existing_dashboard_name, scope_filter, shared=False, public=True)` |
| Download a dashboard | `sdclient.get_dashboards()` |
| Update a dashboard | `sdclient.update_dashboard(dashboard_name)` |
| Delete a dashboard | `sdclient.delete_dashboard(dashboard_name)` |
| Find a dashboard | `sdclient.find_dashboard_by(dashboard_name)` |
| Add a time series | `sdclient.add_dashboard_panel(dashboard_name, panel_name, panel_type, metrics, scope=scope)` |
| Add dashboard panel | `sdclient.add_dashboard_panel(dashboard_name, panel_name, panel_type, metrics, sort_direction=sort_direction, limit=limit, layout=layout)` |
| Remove a panel | `sdclient.remove_dashboard_panel(dashboard_name, 'CPU Over Time')` |
| Save a dashboard to a file | `sdclient.save_dashboard_to_file('dashboard_name', 'dashboard_name.json')` |
{: caption="Table 1. Dashboard Python functions" caption-side="top"} 


## List dashboards per team
{: #dashboard_python_list}


### List the dashboards that are available in the default team
{: #dashboard_python_list_default}


The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
 def usage():
    print('usage: %s <endpoint-url> <apikey> <instance-guid>' % sys.argv[0])
    print('endpoint-url: The endpoint URL that should point to IBM Cloud')
    print('apikey: IBM Cloud IAM apikey that will be used to retrieve an access token')
    print('instance-guid: GUID of an IBM Cloud Monitoring with monitoring instance')
    sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]

# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Show the list of dashboards
ok, res = sdclient.get_dashboards()

if not ok:
    print(res)
    sys.exit(1)

for db in res['dashboards']:
    print("%s [Team ID: %s] Name: %s, # Charts: %d" % ( db['id'], db['teamId'], db['name'], len(db['widgets'] if 'widgets' in db else [])))
```
{: codeblock}



### List the dashboards that are available in a team
{: #dashboard_python_list_team}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))

from sdcclient import SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <endpoint-url> <sysdig_token>' % sys.argv[0])
   print('endpoint-url: The endpoint URL that should point to IBM Cloud')
   print('sysdig_token: Sysdig token for the team')
   sys.exit(1)

if len(sys.argv) != 3:
   usage()

URL = sys.argv[1]

# Set to the Sysdig token of the team
SYSDIG_TOKEN = sys.argv[2]

sdclient = SdMonitorClient(token=SYSDIG_TOKEN,sdc_url=URL)

# Show the list of dashboards
ok, res = sdclient.get_dashboards()

if not ok:
    print(res)
    sys.exit(1)

for db in res['dashboards']:
    print("%s [Team ID: %s] Name: %s, # Charts: %d" % ( db['id'], db['teamId'], db['name'], len(db['widgets'] if 'widgets' in db else [])))
```
{: codeblock}


## Create a dashboard
{: #dashboard_python_create}


## Create a dashboard in the default team
{: #dashboard_python_create_default}

The following code shows the structure of a Python script to create a dashboard from scratch:

```python
The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
 def usage():
    print('usage: %s <endpoint-url> <apikey> <instance-guid>' % sys.argv[0])
    print('endpoint-url: The endpoint URL that should point to IBM Cloud')
    print('apikey: IBM Cloud IAM apikey that will be used to retrieve an access token')
    print('instance-guid: GUID of an IBM Cloud Monitoring with monitoring instance')
    sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]

DASHBOARD_NAME = 'My New Dashboard from Python'
PANEL_NAME = 'CPU Over Time'

# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Create an empty dashboard
ok, res = sdclient.create_dashboard(DASHBOARD_NAME)

# Check the result
dashboard_name = None
if ok:
    print('Dashboard %d created successfully' % res['dashboard']['id'])
    dashboard_name = res['dashboard']
else:
    print(res)
    sys.exit(1)

# Add a time series panel
panel_type = 'timeSeries'
metrics = [
    {'id': 'proc.name'},
    {'id': 'cpu.used.percent', 'aggregations': {'time': 'avg', 'group': 'avg'}}
]
ok, res = sdclient.add_dashboard_panel(
    dashboard_name, PANEL_NAME, panel_type, metrics)

# Check the result
if ok:
    print('Panel added successfully')
    dashboard_name = res['dashboard']
else:
    print(res)
    sys.exit(1)
```
{: codeblock}

## Create a dashboard in a team
{: #dashboard_python_create_team}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))

from sdcclient import SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <endpoint-url> <sysdig_token>' % sys.argv[0])
   print('endpoint-url: The endpoint URL that should point to IBM Cloud')
   print('sysdig_token: Sysdig token for the team')
   sys.exit(1)

if len(sys.argv) != 3:
   usage()

URL = sys.argv[1]

# Set to the Sysdig token of the team
SYSDIG_TOKEN = sys.argv[2]

DASHBOARD_NAME = 'My New Dashboard from Python'
PANEL_NAME = 'CPU Over Time'

sdclient = SdMonitorClient(token=SYSDIG_TOKEN,sdc_url=URL)

# Create an empty dashboard
ok, res = sdclient.create_dashboard(DASHBOARD_NAME)

# Check the result
dashboard_name = None
if ok:
    print('Dashboard %d created successfully' % res['dashboard']['id'])
    dashboard_name = res['dashboard']
else:
    print(res)
    sys.exit(1)

# Add a time series panel
panel_type = 'timeSeries'
metrics = [
    {'id': 'proc.name'},
    {'id': 'cpu.used.percent', 'aggregations': {'time': 'avg', 'group': 'avg'}}
]
ok, res = sdclient.add_dashboard_panel(
    dashboard_name, PANEL_NAME, panel_type, metrics)

# Check the result
if ok:
    print('Panel added successfully')
    dashboard_name = res['dashboard']
else:
    print(res)
    sys.exit(1)
```
{: codeblock}


## Copy a dashboard
{: #dashboard_python_copy}


### Copy a custom dashboard in the default team
{: #dashboard_python_copy_default}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
 def usage():
    print('usage: %s <endpoint-url> <apikey> <instance-guid>' % sys.argv[0])
    print('endpoint-url: The endpoint URL that should point to IBM Cloud')
    print('apikey: IBM Cloud IAM apikey that will be used to retrieve an access token')
    print('instance-guid: GUID of an IBM Cloud Monitoring with monitoring instance')
    sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]

# Name for the dashboard to create
dashboard_name = "My new CPU dashboard"
# Existing dashboard to copy
existing_dashboard_name = "My Existing Dashboard"
# New filter to apply
scope_filter = 'host.hostName = "virtualserver02"'

# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Copy a dashboard
ok, res = sdclient.create_dashboard_from_dashboard(dashboard_name, existing_dashboard_name, scope_filter, shared=False, public=True)

# Check the result
#
if ok:
    print('Dashboard created successfully')
else:
    print(res)
    sys.exit(1)
```
{: codeblock}

### Copy a pre-defined dashboard in the default team
{: #dashboard_python_copy_pre_default}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
 def usage():
    print('usage: %s <endpoint-url> <apikey> <instance-guid>' % sys.argv[0])
    print('endpoint-url: The endpoint URL that should point to IBM Cloud')
    print('apikey: IBM Cloud IAM apikey that will be used to retrieve an access token')
    print('instance-guid: GUID of an IBM Cloud Monitoring with monitoring instance')
    sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]

# Name for the dashboard to create
dashboard_name = "My Overview by Process"
# Existing dashboard to copy
default_dashboard_name = "Overview by Process"
# New filter to apply
scope_filter = 'host.hostName = "virtualserver02"'

# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Copy a dashboard
ok, res = sdclient.create_dashboard_from_view(dashboard_name, default_dashboard_name, scope_filter, shared=False, public=True)

# Check the result
#
if ok:
    print('Dashboard created successfully')
else:
    print(res)
    sys.exit(1)
```
{: codeblock}


### Copy a dashboard in a team
{: #dashboard_python_copy_team}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))

from sdcclient import SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <endpoint-url> <sysdig_token>' % sys.argv[0])
   print('endpoint-url: The endpoint URL that should point to IBM Cloud')
   print('sysdig_token: Sysdig token for the team')
   sys.exit(1)

if len(sys.argv) != 3:
   usage()

URL = sys.argv[1]

# Set to the Sysdig token of the team
SYSDIG_TOKEN = sys.argv[2]

# Name for the dashboard to create
dashboard_name = "My new CPU dashboard"
# Existing dashboard to copy
existing_dashboard_name = "My Existing Dashboard"
# New filter to apply
scope_filter = 'host.hostName = "virtualserver02"'

sdclient = SdMonitorClient(token=SYSDIG_TOKEN,sdc_url=URL)


# Copy a dashboard
ok, res = sdclient.create_dashboard_from_dashboard(dashboard_name, existing_dashboard_name, scope_filter, shared=False, public=True)

# Check the result
#
if ok:
    print('Dashboard created successfully')
else:
    print(res)
    sys.exit(1)
```
{: codeblock}



## Delete a dashboard
{: #dashboard_python_delete}

You must know the ID of a dashboard to delete it.
{: note}

## Delete a dashboard from the default team
{: #dashboard_python_delete_default}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
def usage():
    print('usage: %s <endpoint-url> <apikey> <instance-guid>' % sys.argv[0])
    print('endpoint-url: The endpoint URL that should point to IBM Cloud')
    print('apikey: IBM Cloud IAM apikey that will be used to retrieve an access token')
    print('instance-guid: GUID of an IBM Cloud Monitoring with monitoring instance')
    sys.exit(1)

if len(sys.argv) != 4:
   usage()

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]

# Name of the dashboard that you want to delete
DASHBOARD_NAME = "Nginx production"


# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

# Show the list of dashboards
ok, res = sdclient.get_dashboards()

# Loop through all fetched dashboards
for dashboard in res[1]['dashboards']:
    # Delete dashboard if it matches the pattern (one or many)
    if DASHBOARD_NAME in dashboard['name']:
        print("Deleting " + dashboard['name'])
        res = sdclient.delete_dashboard(dashboard)
```
{: codeblock}


## Delete a dashboard from a team
{: #dashboard_python_delete_team}


The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))

from sdcclient import SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <endpoint-url> <sysdig_token>' % sys.argv[0])
   print('endpoint-url: The endpoint URL that should point to IBM Cloud')
   print('sysdig_token: Sysdig token for the team')
   sys.exit(1)

if len(sys.argv) != 3:
   usage()

URL = sys.argv[1]

# Set to the Sysdig token of the team
SYSDIG_TOKEN = sys.argv[2]

sdclient = SdMonitorClient(token=SYSDIG_TOKEN,sdc_url=URL)

# Show the list of dashboards
ok, res = sdclient.get_dashboards()

# Loop through all fetched dashboards
for dashboard in res[1]['dashboards']:
    # Delete dashboard if it matches the pattern (one or many)
    if DASHBOARD_NAME in dashboard['name']:
        print("Deleting " + dashboard['name'])
        res = sdclient.delete_dashboard(dashboard)
```
{: codeblock}


## Download custom dashboards
{: #dashboard_python_download}

When you download dashboards, you only download custom dashboards.
{: important}

## Download custom dashboards in the default team
{: #dashboard_python_download_default}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))
from sdcclient import IbmAuthHelper, SdMonitorClient

# Parse arguments.
 def usage():
    print('usage: %s <endpoint-url> <apikey> <instance-guid>' % sys.argv[0])
    print('endpoint-url: The endpoint URL that should point to IBM Cloud')
    print('apikey: IBM Cloud IAM apikey that will be used to retrieve an access token')
    print('instance-guid: GUID of an IBM Cloud Monitoring with monitoring instance')
    sys.exit(1)

if len(sys.argv) != 4:
   usage()


def zipdir(path, ziph):
    # ziph is zipfile handle
    for root, dirs, files in os.walk(path):
        for file in files:
            ziph.write(os.path.join(root, file))


def cleanup_dir(path):
    if os.path.exists(path) == False:
        return
    if os.path.isdir(path) == False:
        print('Provided path is not a directory')
        sys.exit(-1)

    for file in os.listdir(path):
        file_path = os.path.join(path, file)
        try:
            if os.path.isfile(file_path):
                os.unlink(file_path)
            else:
                print('Cannot clean the provided directory due to delete failure on %s' % file_path)
        except Exception as e:
            print(e)
    os.rmdir(path)

sysdig_dashboard_dir = 'sysdig-dashboard-dir'

URL = sys.argv[1]
APIKEY = sys.argv[2]
GUID = sys.argv[3]

# Instantiate the client
ibm_headers = IbmAuthHelper.get_headers(URL, APIKEY, GUID)
sdclient = SdMonitorClient(sdc_url=URL, custom_headers=ibm_headers)

ok, res = sdclient.get_dashboards()

if not ok:
    print(res)
    sys.exit(1)

# Creating sysdig dashboard directory to store dashboards
if not os.path.exists(sysdig_dashboard_dir):
    os.makedirs(sysdig_dashboard_dir)

for db in res['dashboards']:
    sdclient.save_dashboard_to_file(db, os.path.join(sysdig_dashboard_dir, str(db['id'])))

    print("Name: %s, # Charts: %d" % (db['name'], len(db['widgets'])))
```
{: codeblock}

## Download custom dashboards in a team
{: #dashboard_python_download_team}

The following code shows the structure of a Python script:

```python
#!/usr/bin/env python3

import os
import sys
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(sys.argv[0])), '..'))

from sdcclient import SdMonitorClient

# Parse arguments.
def usage():
   print('usage: %s <endpoint-url> <sysdig_token>' % sys.argv[0])
   print('endpoint-url: The endpoint URL that should point to IBM Cloud')
   print('sysdig_token: Sysdig token for the team')
   sys.exit(1)

if len(sys.argv) != 3:
   usage()

URL = sys.argv[1]

# Set to the Sysdig token of the team
SYSDIG_TOKEN = sys.argv[2]

def zipdir(path, ziph):
    # ziph is zipfile handle
    for root, dirs, files in os.walk(path):
        for file in files:
            ziph.write(os.path.join(root, file))


def cleanup_dir(path):
    if os.path.exists(path) == False:
        return
    if os.path.isdir(path) == False:
        print('Provided path is not a directory')
        sys.exit(-1)

    for file in os.listdir(path):
        file_path = os.path.join(path, file)
        try:
            if os.path.isfile(file_path):
                os.unlink(file_path)
            else:
                print('Cannot clean the provided directory due to delete failure on %s' % file_path)
        except Exception as e:
            print(e)
    os.rmdir(path)

sysdig_dashboard_dir = 'sysdig-dashboard-dir'

sdclient = SdMonitorClient(token=SYSDIG_TOKEN,sdc_url=URL)

ok, res = sdclient.get_dashboards()

if not ok:
    print(res)
    sys.exit(1)

# Creating sysdig dashboard directory to store dashboards
if not os.path.exists(sysdig_dashboard_dir):
    os.makedirs(sysdig_dashboard_dir)

for db in res['dashboards']:
    sdclient.save_dashboard_to_file(db, os.path.join(sysdig_dashboard_dir, str(db['id'])))

    print("Name: %s, # Charts: %d" % (db['name'], len(db['widgets'])))
```
{: codeblock}



