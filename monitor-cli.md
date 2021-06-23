---
 
copyright:
  years:  2021
lastupdated: "2021-03-28"

subcollection: monitor-plugin-cli

keywords: IBM Cloud Monitoring CLI, IBM Cloud Monitoring command line , IBM Cloud Monitoring terminal, IBM Cloud Monitoring shell

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}


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

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## ibmcloud monitoring alert list
{: #alert-list}

Use this command to list {{site.data.keyword.mon_full_notm}} alerts for the specified instance. 

```sh
ibmcloud monitoring alert list --name <NAME> [OPTIONS]
```
{:pre}


### Command options 
{: #alert-list-options}

<dl>
<dt>--name &lt;NAME&gt; | --n &lt;NAME&gt;</dt>
<dd>Name of the instance.</dd>
<dt>--region &lt;NAME&gt; | -r &lt;NAME&gt;</dt>
<dd>Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.</dd>
<dt>--severity &lt;SEVERITY&gt; | -s &lt;SEVERITY&gt;</dt>
<dd>A comma-separated list of severity values enclosed in double-quotes (").  If only a single severity is specified, the double-quotes can be omitted. </dd>
<dt>--output &lt;TYPE&gt;</dt>
<dd>A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.  <p>If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.</p> 
<p>`WIDE` returns additional details in the output.</p></dd>
<dt>--enabled &lt;SETTING&gt; | -e &lt;SETTING&gt;</dt>
<dd>Indicates the alerts to be listed based on configured notification setting.  If specified, `--enabled true` will list alerts for instances where notifications, for example, email or Slack, are enabled.  Specifying `--enabled false` will return a list of alerts for instances where notifications are not enabled.  </dd>
<dt>--help | -h</dt>
<dd>List options available for the command</dd>
</dl>
  
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

## ibmcloud monitoring service-instances
{: #service-instances}

Use this command to list {{site.data.keyword.mon_full_notm}} service instances. 

```sh
ibmcloud monitoring service-instances [OPTIONS]
```
{:pre}


### Command options 
{: #service-instances-options}

<dl>
<dt>--service-name &lt;NAME&gt; | --sn &lt;NAME&gt;</dt>
<dd>Name of the service.</dd>
<dt>--region &lt;NAME&gt; | -r &lt;NAME&gt;</dt>
<dd>Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.</dd>
<dt>--all-regions</dt>
<dd>Services hosted across all regions.</dd>
<dt>-g &lt;GROUP&gt;</dt>
<dd>Resource Group associated with the hosted service.</dd>
<dt>--all-resource-groups</dt>
<dd>Services hosted across all resource groups.</dd>
<dt>--quiet | -q</dt>
<dd>Supresses verbose output.</dd>
<dt>--output &lt;TYPE&gt;</dt>
<dd>A comma-separated list of output preferences enclosed in double-quotes (").  If only a single preference is specified, the double-quotes can be omitted. Supported options are `WIDE` and `JSON`.  <p>If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.</p> 
<p>`WIDE` returns additional details in the output.</p></dd>
<dt>--help | -h</dt>
<dd>List options available for the command</dd>
</dl>
  
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
ibmcloud monitoring platform-metrics-receiver --name <NAME> [OPTIONS]
```
{:pre}


### Command options 
{: #platform-metrics-receiver-options}

<dl>
<dt>--name &lt;NAME&gt; | --n &lt;NAME&gt;</dt>
<dd>Name of the instance.</dd>
<dt>--region &lt;NAME&gt; | -r &lt;NAME&gt;</dt>
<dd>Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into or targeted will be used.</dd>
<dt>--force</dt>
<dd>Supresses the prompt and replaces the existing platform metric instance with the instance specified by `--name`.</dd>
<dt>--help | -h</dt>
<dd>List options available for the command</dd>
</dl>
  
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
