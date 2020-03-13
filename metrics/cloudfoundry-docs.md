---

copyright:
  years:  2019, 2020
lastupdated: "2020-02-03"

keywords: Sysdig, IBM Cloud, monitoring, service, CF, cf

subcollection: Sysdig

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

# Monitoring Cloud Foundry metrics
{: #monitor-cf-sysdig}

{{site.data.keyword.mon_full}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}


## Enabling platform metrics
{: #platform_metrics}

Platform metrics are metrics that are exposed by enabled-Sysdig resources in {{site.data.keyword.cloud_notm}}. You must configure a Sysdig instance in a region to monitor these metrics.

You can configure 1 instance only of the {{site.data.keyword.mon_full_notm}} service per region to collect platform metrics. 
* To configure the Sysdig instance, you must set on the *platform metrics* configuration setting. [Learn more](/docs/Monitoring-with-Sysdig?topic=Sysdig-platform_metrics_enabling).
* If a Sysdig instance in a region is already enabled to collect platform metrics, metrics from enabled-Sysdig resources are collected automatically and available for monitoring through this instance. For more information about enabled-Sysdig services, see [Cloud services](/docs/Monitoring-with-Sysdig?topic=Sysdig-cloud_services).

To monitor Cloud Foundry (CF) apps, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where your apps are running.
{: important}


## Navigating to the Sysdig web UI
{: #launch_sysdig_ui}

To monitor CF apps, you must launch the Sysdig web UI in the region where your CF apps are running.
{: important}

Complete the following steps to launch the Sysdig web UI from the *Observability* page and open the pre-defined CF dashboard:

1.[Launch the Sysdig web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch).
2. Select **DASHBOARDS**.
3. In the **Default Dashboards** section, expand **IBM**.
4. Choose the pre-defined CF dashboard **Overview CF apps** from the list.

## Viewing metrics
{: #view_metrics}

You cannot customize a pre-defined CF dashboard. To be able to monitor CF apps, you must complete the following steps:
1. [Copy the pre-defined dashboard](/docs/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy). 
2. [Change the scope of the new dashboard](/docs/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope).

    You can change the scope for all the metrics that are included in the dashboard. You can also change the scope of each metric.

    When you change the scope, you can change the scope to report on a specific CF app, on a CF app index, on apps running in a CF organization, or on apps running in a CF space.


## Metrics dictionary
{: #metrics_dictionary}

| Metric Name |
|-----------|
| [CPU entitlement of the CF application](#ibm_cloudfoundry_app_cpu_entitlement) | 
| [CPU usage of the CF application](#ibm_cloudfoundry_app_cpu_usage) | 
| [CPU utilization of the CF application](#ibm_cloudfoundry_app_cpu_utilization) | 
| [Container age of the CF application](#ibm_cloudfoundry_app_container_age) | 
| [Disk usage of the CF application](#ibm_cloudfoundry_app_disk_bytes_used) | 
| [Disk utilization of the CF application](#ibm_cloudfoundry_app_disk_utilization) | 
| [Memory usage of the CF application](#ibm_cloudfoundry_app_memory_bytes_used) | 
| [Memory utilization of the CF application](#ibm_cloudfoundry_app_memory_utilization) | 
| [Total disk size of the CF application](#ibm_cloudfoundry_app_disk_bytes_total) | 
| [Total memory of the CF application](#ibm_cloudfoundry_app_memory_bytes_total) | 
{: caption="Table 1: Metrics dictionary" caption-side="top"}




### CPU entitlement of the CF application
{: #ibm_cloudfoundry_app_cpu_entitlement}

Indicates the CPU entitlement of a CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_cpu_entitlement`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 2: CPU entitlement of the CF application metric metadata" caption-side="top"}

### CPU usage of the CF application
{: #ibm_cloudfoundry_app_cpu_usage}

Indicates the CPU usage of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_cpu_usage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 3: CPU usage of the CF application metric metadata" caption-side="top"}


### CPU utilization of the CF application
{: #ibm_cloudfoundry_app_cpu_utilization}

Indicates the CPU utilization of a CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_cpu_utilization`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 4: CPU utilization of the CF application metric metadata" caption-side="top"}

### Container age of the CF application
{: #ibm_cloudfoundry_app_container_age}

Indicates the container age of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_container_age`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 5: Container age of the CF application metric metadata" caption-side="top"}

### Disk usage of the CF application
{: #ibm_cloudfoundry_app_disk_bytes_used}

Indicates the disk usage of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_disk_bytes_used`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 6: Disk usage of the CF application metric metadata" caption-side="top"}

### Disk utilization of the CF application
{: #ibm_cloudfoundry_app_disk_utilization}

Indicates the disk utilization of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_disk_utilization`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 7: Disk utilization of the CF application metric metadata" caption-side="top"}

### Memory usage of the CF application
{: #ibm_cloudfoundry_app_memory_bytes_used}

Indicates the memory usage of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_memory_bytes_used`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 8: Memory usage of the CF application metric metadata" caption-side="top"}

### Memory utilization of the CF application
{: #ibm_cloudfoundry_app_memory_utilization}

Indicates the memory utilization of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_memory_utilization`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 9: Memory utilization of the CF application metric metadata" caption-side="top"}

### Total disk size of the CF application
{: #ibm_cloudfoundry_app_disk_bytes_total}

Indicates the total disk size of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_disk_bytes_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 10: Total disk size of the CF application metric metadata" caption-side="top"}

### Total memory of the CF application
{: #ibm_cloudfoundry_app_memory_bytes_total}

Indicates the total memory of the CF application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_memory_bytes_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM CF organization name`, `IBM CF organization GUID`, `IBM CF space name`, `IBM CF space GUID`, `IBM CF application name`, `IBM CF application index` |
{: caption="Table 11: Total memory of the CF application metric metadata" caption-side="top"}



## Attributes for segmentation
{: attributes}

### Global attributes
{: global-attributes}

The following attributes are available for segmenting all of the metrics:

| Attribute | Attribute Name | Attribute Description | Valid values |
|-----------|----------------|-----------------------|--------------|
| `Cloud Type` | `ibm_ctype` | Type of Cloud         | Valid values are `public`, `dedicated`, or `local`. |
| `Location` | `ibm_location` | Location of the monitored resource | You can specify a region, a data center, or `global`. |
| `Resource` | `ibm_resource` | Resource that is measured | Name or GUID of the resource |
| `Resource Type` | `ibm_resource_type` | Type of the resource that is measured | Valid value is `cf-application` |
| `Resource group` | `ibm_resource_group_name` | Resource group that is associated to the service instance. | Choose a resource group from the ones that are available in your account. |
| `Scope` | `ibm_scope` | The extent of the data samples that are considered  | You can choose the scope to be the account, an organization, or a space GUID that is associated with this metric. |
| `Service name` | `ibm_service_name` | Name of the service that generates this metric | `cloud-foundry` | 
{: caption="Global segmentation attributes" caption-side="top"}


### Additional attributes
{: additional-attributes}

The following attributes are available for segmenting one or more attributes. Check each metric definition to find out the segmentation options that are allowed with a metric type.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `IBM CF application index` | `ibm_cloudfoundry_app_index` | IBM CF application index |
| `IBM CF application name` | `ibm_cloudfoundry_app_name` | IBM CF application name |
| `IBM CF organization GUID` | `ibm_cloudfoundry_org_guid` | IBM CF organization GUID |
| `IBM CF organization name` | `ibm_cloudfoundry_org_name` | IBM CF organization name |
| `IBM CF space GUID` | `ibm_cloudfoundry_space_guid` | IBM CF space GUID |
| `IBM CF space name` | `ibm_cloudfoundry_space_name` | IBM CF space name |
{: caption="Additional segmentation attributes" caption-side="top"}


## CF dashboards dictionary
{: #dashboards_dictionary}

The following table outlines the pre-defined dashboards that you can use to monitor CF metrics:

| Dashboard name                  | Description    |
|---------------------------------|----------------|
| `Overview CF apps`   | Default dashboard when you launch the Sysdig web UI from your service instance UI. |
{: caption="Pre-defined dashboards" caption-side="top"}

These dashboards cannot be changed.
{: important}


