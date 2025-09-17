---

copyright:
  years:  2018, 2025
lastupdated: "2025-09-17"

subcollection: monitoring

keywords:

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring (ibmcloud monitoring) CLI
{: #monitor-cli}

The {{site.data.keyword.cloud}} command-line interface (CLI) provides extra capabilities for service offerings. This information describes how you can use the CLI to access information in {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Prerequisites
{: #monitor-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.cloud_notm}} Monitoring CLI by running the following command:

   ```sh
   ibmcloud plugin install monitoring
   ```
   {: pre}

You are notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## ibmcloud monitoring alert add
{: #alert-add}

Use this command to add an alert.

```sh
ibmcloud monitoring alert add --name NAME [--alert-name ALERT_NAME] [--description DESCRIPTION] [--type TYPE] [--timespan TIMESPAN] [--condition CONDITION] [--severity SEVERITY] [--severity-label LOW, MEDIUM OR HIGH] [--disable] [--segment SEGMENT] [--segment-condition SEGMENT_CONDITION] [--user-filter USER_FILTER] [--notify NOTIFY] [--file JSON_FILE] [--region REGION] [--output FORMAT] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #alert-add-options}

`--name <NAME>` | `--n <NAME>`
:   Name of the instance.

`--alert-name <ALERT_NAME>`
:   Name of the alert.

`--description <DESCRIPTION>`
:   Information about the alert.

`--type <TYPE>`
:   Type of alert. Valid values are MANUAL, BASELINE, and HOST_COMPARISON.

`--timespan <TIMESPAN>`
:   Minimum time interval, in microseconds, for which the alert condition must be met before the alert is triggered. The default value is 60,000,000 microseconds.

`--condition <CONDITION>`
:   Threshold of the alert. This parameter is required for manual alerts, and does not apply to other alert types.

`--severity <SEVERITY>` | `-s <SEVERITY>`
:   Level of severity. Valid values range from 0 to 7. 0 means emergency and 7 means debug. By default, severity is set to 4.

`--severity-label <LOW | MEDIUM | HIGH>`
:   Criticality of an alert. Valid values are `HIGH`, `MEDIUM`, `LOW`. A lower severity value indicates a higher severity.

`--disable`
:   State of the alert. By default, an alert is enabled when it is created. You must set this parameter to disable the alert when it is created.

`--segment <SEGMENT>`
:   Additional segmentation criteria. For example, you can segment an alert by `['host.mac', 'proc.name']`.

`--segment-condition <SEGMENT_CONDITION>`
:   Defines when the alert is triggered for each monitored entity that is specified in the `--segment` parameter. This parameter is required for manual alerts, and does not apply to other alert types. Valid values are `ANY` and `ALL`. `ANY` indicates that the alert is triggered when at least one of the monitored entities satisfies the condition. `ALL` indicates that the alert is triggered when all of the monitored entities satisfy the condition.

`--user-filter <USER_FILTER>`
:   Boolean expression that you can set to reduce the scope of the alert. Use this parameter to configure segments, such as filters like `kubernetes.namespace.name='production'` or `container.image='nginx'`.

`--notify <NOTIFY>`
:   Type of notification that you want this alert to generate. Options are `EMAIL`, `SNS`, `PAGER_DUTY`, and `SYSDIG_DUMP`.

`--file <FILE>` | `-f <JSON_FILE>`
:   Name of the JSON file that contains the data set for a new alert creation. Make sure you create the `alert.json` file before invoking this command.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--output <FORMAT>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #alert-add-examples}

The following are examples using the **`ibmcloud monitoring alert add`** command.

Add an alert for the `IBM Cloud Monitoring abc` instance to detect a CrashLoopBackOff in the last 5 minutes.

```sh
ibmcloud monitoring alert add \
        --name "IBM Cloud Monitoring abc" \
        --description "Alert to report crashLoopBackOffs that are detected" \
        --severity 2 \
        --timespan 300 \
        --condition 'sum(avg(kubernetes.pod.restart.count)) > 1' \
        --alert-name '[Kubernetes] Pod crash/restart loop'
```
{: pre}

Add an alert for the `IBM Cloud Monitoring abc` instance to detect a CrashLoopBackOff in the last 5 minutes with severity set to medium.

```sh
ibmcloud monitoring alert add \
        --name "IBM Cloud Monitoring abc" \
        --description "Alert to report crashLoopBackOffs that are detected" \
        --severity 2 \
        --severity-label MEDIUM \
        --timespan 300 \
        --condition 'sum(avg(kubernetes.pod.restart.count)) > 1' \
        --alert-name '[Kubernetes] Pod crash/restart loop'
```
{: pre}


## ibmcloud monitoring alert list
{: #alert-list}

Use this command to list the alerts for the specified instance.

```sh
ibmcloud monitoring alert list --name NAME [--severity SEVERITY] [--enabled TRUE or FALSE] [--region REGION] [--output FORMAT] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #alert-list-options}

`--name <NAME>` | `--n <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--severity <SEVERITY>` | `-s <SEVERITY>`
:   A comma-separated list of severity values enclosed in double-quotes (").  If only a single severity is specified, the double-quotes can be omitted.

`--output <FORMAT>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--enabled <TRUE | FALSE>` | `-e <TRUE | FALSE>`
:   Boolean that indicates the alerts to be listed based on the alert notification settings.  If specified, `--enabled true` will list alerts for instances where notifications, for example, email or Slack, are enabled.  Specifying `--enabled false` will return a list of alerts for instances where notifications are not enabled.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.


### Examples
{: #alert-list-examples}

The following are examples using the **`ibmcloud monitoring alert list`** command.

List all alerts for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring alert list --name "IBM Cloud Monitoring abc"
```
{: pre}

List all alerts for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring alert list --name "IBM Cloud Monitoring abc" --region us-south
```
{: pre}

List all alerts for the `IBM Cloud Monitoring abc` instance with `low` and `medium` severity where notifications are not enabled.

```sh
ibmcloud monitoring alert list --name "IBM Cloud Monitoring abc" --enabled false --severity low,medium
```
{: pre}




## ibmcloud monitoring alert get
{: #alert-get}

Use this command to get details on an alert by using the alert ID.

```sh
ibmcloud monitoring alert get --name NAME --id ALERT_ID [--region REGION] [--output FORMAT] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #alert-get-options}

`--name <NAME>` | `--n <NAME>`
:   Name of the instance.

`--id <ALERT_ID>`
:   ID of the alert.

`--region <REGIO>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--output <FORMAT>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #alert-get-examples}

The following are examples using the **`ibmcloud monitoring alert get`** command.

Get details for an alert with ID 1234567 for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring alert get --name "IBM Cloud Monitoring abc" --id 1234567
```
{: pre}

Get details for an alert with ID 1234567 for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring alert get --name "IBM Cloud Monitoring abc" --id 1234567 --region us-south
```
{: pre}


## ibmcloud monitoring alert update
{: #alert-update}

Use this command to modify an alert by using a JSON file.

To update of an alert, you must modify the JSON file that you get by running the `ibmcloud monitoring alert get` command.
{: note}

```sh
ibmcloud monitoring alert update --name NAME --id ALERT_ID --file JSON_FILE [--region REGION] [--output FORMAT] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #alert-update-options}

`--name <NAME>` | `--n <NAME>`
:   Name of the instance.

`--id <ALERT_ID>`
:   ID of the alert.

`--file <FILE>` | `-f <JSON_FILE>`
:   Name of the JSON file that contains the data with the alert definition. Make sure you create or modify the alert.json file before invoking this command.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--output <TYPE>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #alert-update-examples}

The following are examples using the **`ibmcloud monitoring alert update`** command.

Update an alert with ID 1234567 for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring alert update --name "IBM Cloud Monitoring abc" --id 1234567 --file alert.json
```
{: pre}

Update an alert with ID 1234567 for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring alert update --name "IBM Cloud Monitoring abc" --id 1234567 --file alert.json --region us-south
```
{: pre}



## ibmcloud monitoring alert delete
{: #alert-delete}

Use this command to delete an alert.

```sh
ibmcloud monitoring alert delete --name NAME --id ALERT_ID [--region REGION] [--force] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #alert-delete-options}

`--name <NAME>` | `--n <NAME>`
:   Name of the instance.

`--id <ALERT_ID>`
:   ID of the alert.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--force`
:   Supresses the prompt and deletes the alert from the instance that is specified by `--name`.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.


### Examples
{: #alert-delete-examples}

The following are examples using the **`ibmcloud monitoring alert delete`** command.

Delete an alert with ID 1234567 for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring alert delete --name "IBM Cloud Monitoring abc" --id 1234567 --file alert.json
```
{: pre}

Delete an alert with ID 1234567 for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring alert delete --name "IBM Cloud Monitoring abc" --id 1234567 --file alert.json --region us-south
```
{: pre}



## ibmcloud monitoring service-instances
{: #service-instances}

Use this command to list {{site.data.keyword.mon_full_notm}} service instances.

```sh
ibmcloud monitoring service-instances [--region REGION] [--all-regions] [--g RESOURCE_GROUP] [--all-resource-groups] [--quiet] [--output FORMAT]
```
{: pre}


### Command options
{: #service-instances-options}

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--all-regions`
:   Services hosted across all regions.

`-g <RESOURCE_GROUP>`
:   Resource Group associated with the hosted service.

`--all-resource-groups`
:   Services hosted across all resource groups.

`--quiet` | `-q`
:   Supresses verbose output.

`--output <FORMAT>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #service-instances-examples}

The following are examples using the **`ibmcloud monitoring service-instances`** command.

List all monitoring service instances.

```sh
ibmcloud monitoring service-instances
```
{: pre}

List all instances that are in the `test-rg` resource group.

```sh
ibmcloud monitoring service-instances -g test-rg
```
{: pre}

List all instances and include additional details, such as ID, GUID, and Resource ID.

```sh
ibmcloud monitoring service-instances --output wide
```
{: pre}

List all instances and include only the minimal details of Name, Region and State.

```sh
ibmcloud monitoring service-instances --quiet
```
{: pre}

List all instances for the `us-south` region.

```sh
ibmcloud monitoring service-instances --region us-south
```
{: pre}

Lists all instances in the `us-south` region and returns the output in JSON format.

```sh
ibmcloud monitoring service-instances --region us-south --output json
```
{: pre}

## ibmcloud monitoring platform-metrics-receiver
{: #platform-metrics-receiver}

Use this command to configure the specified {{site.data.keyword.mon_full_notm}} service instance to receive platform metrics.  When run, the command prompts the user to keep an existing service instance or replace it with the specified instance.

```sh
ibmcloud monitoring platform-metrics-receiver --name NAME [--region REGION] [--force]
```
{: pre}


### Command options
{: #platform-metrics-receiver-options}

`--name <NAME>` | `--n <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted is used.

`--force`
:   Supresses the prompt and replaces the existing platform metric instance with the instance specified by `--name`.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #platform-metrics-receiver-examples}

The following are examples using the **`ibmcloud monitoring platform-metrics-receiver`** command.

Configures the `IBM Cloud Monitoring abc` as the instance to receive platform metrics.

```sh
ibmcloud monitoring platform-metrics-receiver --name "IBM Cloud Monitoring abc"
```
{: pre}

Configures the `IBM Cloud Monitoring abc` in the `eu-gb` region as the instance to receive platform metrics.

```sh
ibmcloud monitoring platform-metrics-receiver --name "IBM Cloud Monitoring abc" --region eu-gb
```
{: pre}

## ibmcloud monitoring dashboard list
{: #dashboard-list}

Use this command to list all the dashboards that are visible to a user in a Monitoring instance.

```sh
ibmcloud monitoring dashboard list --name NAME [--region REGION] [--output FORMAT] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #dashboard-list-options}

`--name <NAME>` | `--sn <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--output <TYPE>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #dashboard-list-examples}

The following are examples using the **`ibmcloud monitoring dashboard list`** command.

List all dashboards for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring dashboard list
```
{: pre}

List all dashboards for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring dashboard list --region us-south
```
{: pre}



## ibmcloud monitoring dashboard get
{: #dashboard-get}

Use this command to get details for a dashboard by using the dashboard ID.

```sh
ibmcloud monitoring dashboard get --id DASHBOARD_ID --name NAME [OPTIONS] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #dashboard-get-options}

`--name <NAME>` | `--sn <NAME>`
:   Name of the instance.

`--id <DASHBOARD_ID>`
:   Dashboard_ID of a specific service Instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #dashboard-get-examples}

The following are examples using the **`ibmcloud monitoring dashboard get`** command.

Get information for a dashboard with ID 1234567 for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring dashboard get --name "IBM Cloud Monitoring abc"
```
{: pre}

Get information for a dashboard with ID 1234567 for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring dashboard get --name "IBM Cloud Monitoring abc" --region us-south
```
{: pre}



## ibmcloud monitoring dashboard add-json
{: #dashboard-add-json}

Use this command to create a dashboard by using a JSON file.

```sh
ibmcloud monitoring dashboard add-json --file JSON_FILE --name NAME [--region REGION] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #dashboard-add-json-options}

`--file <FILE>` | `-f <JSON_FILE>`
:   Name of the JSON file that contains the information for a new dashboard creation. Make sure you create the dashboard.json file before invoking this command.

`--name <NAME>` | `--sn <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.


### Examples
{: #dashboard-add-json-examples}

The following are examples using the **`ibmcloud monitoring dashboard add-json`** command.

Create a dashboard for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring dashboard add-json --name "IBM Cloud Monitoring abc" --file dashboard.json
```
{: pre}

Create a dashboard for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring dashboard add-json --name "IBM Cloud Monitoring abc" --file dashboard.json --region us-south
```
{: pre}

## ibmcloud monitoring event list
{: #event-list}

Use this command to list the events.

```sh
ibmcloud monitoring event list --name NAME [--region REGION] [--last DURATION] [--from TIMESTAMP] [--to TIMESTAMP] [--limit LIMIT] [--output FORMAT] [--team TEAM_NAME]
```
{: pre}


### Command options
{: #event-list-options}

`--name <NAME>` | `--sn <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--last <DURATION>`
:   Period of time for which you want to list events. For example, you can set `12h` to show events for the last 12 hours, `15m` to show events for the last 15 minutes, or `10d` to show events for the last 10 days.

`--from <TIMESTAMP>`
:   The UNIX timestamp in seconds for the beginning of the events.

`--to <TIMESTAMP>`
:   The UNIX timestamp in seconds for the end of the events.

`--limit <LIMIT>`
:   Maximum number of events to print in the period of time specified in the request. By default, the parameter is set to a 100 events. The maximum number of events hat you can set is 10000.

`--output <TYPE>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--team <TEAM_NAME>`
:   The name of the {{site.data.keyword.mon_full_notm}} team to be used for authorization. If no team is specified, the default team will be used.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #event-list-examples}

The following are examples using the **`ibmcloud monitoring event list`** command.

List events for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring event list --name "IBM Cloud Monitoring abc"
```
{: pre}

List events for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring event list --name "IBM Cloud Monitoring abc" --region us-south
```
{: pre}

List events for the `IBM Cloud Monitoring abc` instance in the `us-south` region for the last hour.

```sh
ibmcloud monitoring event list --name "IBM Cloud Monitoring abc" --region us-south --duration 1H
```
{: pre}

## ibmcloud monitoring settings notification list
{: #settings-notification-list}

Use this command to list notification channels.

```sh
ibmcloud monitoring settings notification list --name NAME [--region REGION] [--output FORMAT]
```
{: pre}


### Command options
{: #settings-notification-list-options}

`--name <NAME>` | `--sn <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--output <TYPE>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #settings-notification-list-examples}

The following are examples using the **`ibmcloud monitoring settings notification list`** command.

List the notification channels for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring settings notification list --name "IBM Cloud Monitoring abc"
```
{: pre}

List the notification channels for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring settings notification list --name "IBM Cloud Monitoring abc" --region us-south
```
{: pre}

## ibmcloud monitoring settings team list
{: #settings-team-list}

Use this command to list teams.

```sh
ibmcloud monitoring settings team list --name NAME [--region REGION] [--output FORMAT]
```
{: pre}


### Command options
{: #settings-team-list-options}

`--name <NAME>` | `--sn <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--output <TYPE>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #settings-team-list-examples}

The following are examples using the **`ibmcloud monitoring settings team list`** command.

List the teams for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring settings team list --name "IBM Cloud Monitoring abc"
```
{: pre}

List the teams for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring settings team list --name "IBM Cloud Monitoring abc" --region us-south
```
{: pre}


## ibmcloud monitoring settings user list
{: #settings-user-list}

Use this command to list users.

```sh
ibmcloud monitoring settings user list --name NAME [--region REGION] [--teamID TEAM_ID] [--output FORMAT]
```
{: pre}


### Command options
{: #settings-user-list-options}

`--name <NAME>` | `--sn <NAME>`
:   Name of the instance.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.

`--teamID <TEAM_ID>`
:   ID of the team.

`--output <TYPE>`
:   A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.

    If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

    `WIDE` returns additional details in the output.

`--help` | `-h`
:   List options available for the command.

### Examples
{: #settings-user-list-examples}

The following are examples using the **`ibmcloud monitoring settings user list`** command.

List the users for the `IBM Cloud Monitoring abc` instance.

```sh
ibmcloud monitoring settings user list --name "IBM Cloud Monitoring abc"
```
{: pre}

List the users for the `IBM Cloud Monitoring abc` instance in the `us-south` region.

```sh
ibmcloud monitoring settings user list --name "IBM Cloud Monitoring abc" --region us-south
```
{: pre}
