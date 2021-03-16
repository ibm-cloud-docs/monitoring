---
 
copyright:
  years:  2021
lastupdated: "2021-03-16"

subcollection: sysdig-monitor-plugin-cli

keywords: IBM Cloud Monitoring CLI, IBM Cloud Monitoring command line , IBM Cloud Monitoring terminal, IBM Cloud Monitoring shell

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}


# {{site.data.keyword.mon_full_notm}} (ibmcloud monitoring) CLI
{: #sysdig-monitor-cli}

The {{site.data.keyword.cloud}} command-line interface (CLI) provides extra capabilities for service offerings. This information describes how you can use the CLI to list all the service instances for {{site.data.keyword.mon_full_notm}} for an account.
{: shortdesc} 

## Prerequisites
{: #sysdig-monitor-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.mon_full_notm}} CLI by running the following command:

   ```sh
   ibmcloud plugin install monitoring
   ```
   {: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}



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
<dt>--service-name &lt;NAME&gt;> | --sn &lt;NAME&gt;</dt>
<dd>Name of the service.</dd>
<dt>-region &lt;NAME&gt; | -r &lt;NAME&gt;</dt>
<dd>Name of the region, for example, `us-south` or `eu-gb`. If not specified, the targeted region will be used.</dd>
<dt>-g &lt;GROUP&gt;</dt>
<dd>Resource Group associated with the hosted service.</dd>
<dt>--all-resource-groups | --arg</dt>
<dd>Services hosted across all resource groups.</dd>
<dt>--long | -l</dt>
<dd>Show additional fields in the output.</dd>
<dt>--quiet | -q</dt>
<dd>Supresses verbose output.</dd>
<dt>--json | -j</dt>
<dd>Produces output as raw JSON.</dd>
<dt>--help</dt>
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
ibmcloud monitoring service-instances --long
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

