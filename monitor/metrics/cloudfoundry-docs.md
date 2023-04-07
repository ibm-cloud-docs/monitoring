---

copyright:
  years:  2019, 2023
lastupdated: "2020-07-16"

keywords: IBM Cloud, monitoring, service, CF, cf

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring Cloud Foundry metrics
{: #monitor-cf-sysdig}

{{site.data.keyword.mon_full}} is a cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by {{site.data.keyword.mon_full_notm}} in partnership with {{site.data.keyword.IBM_notm}}.
{: shortdesc}


## Enabling platform metrics
{: #platform_metrics}

Platform metrics are metrics that are exposed by {{site.data.keyword.mon_full_notm}} enabled resources in {{site.data.keyword.cloud_notm}}. You must configure an {{site.data.keyword.mon_full_notm}} instance in a region to monitor these metrics.

You can configure only 1 instance of the {{site.data.keyword.mon_full_notm}} service per region to collect platform metrics.
* To configure the {{site.data.keyword.mon_full_notm}} instance, you must set the *platform metrics* configuration setting. [Learn more](/docs/monitoring?topic=monitoring-platform_metrics_enabling).
* If an {{site.data.keyword.mon_full_notm}} instance in a region is already enabled to collect platform metrics, metrics from Monitoring-enabled resources are collected automatically and available for monitoring through this instance. For more information about Monitoring-enabled services, see [Cloud services](/docs/monitoring?topic=monitoring-cloud_services).

To monitor Cloud Foundry apps, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where your apps are running.
{: important}


## Navigating to the monitoring UI
{: #launch_monitoring_ui}

To monitor Cloud Foundry apps, you must launch the monitoring UI in the region where your Cloud Foundry apps are running.
{: important}

Complete the following steps to launch the monitoring UI from the *Observability* page and open the pre-defined Cloud Foundry dashboard:

1. [Launch the monitoring UI](/docs/services/monitoring?topic=monitoring-launch).
2. Select **Dashboards**.
3. In the **Default Dashboards** section, expand **IBM**.
4. Choose the pre-defined Cloud Foundry dashboard **Overview CF apps** from the list.

## Viewing metrics
{: #view_metrics}

You cannot customize a pre-defined Cloud Foundry dashboard. To be able to monitor Cloud Foundry apps, you must complete the following steps:
1. [Copy the pre-defined dashboard](/docs/monitoring?topic=monitoring-dashboards#dashboards_copy).
2. [Change the scope of the new dashboard](/docs/monitoring?topic=monitoring-dashboards#dashboards_scope).

    You can change the scope for all the metrics that are included in the dashboard. You can also change the scope of each metric.

    When you change the scope, you can change the scope to report on a specific Cloud Foundry app, on a Cloud Foundry app index, on apps running in a Cloud Foundry organization, or on apps running in a Cloud Foundry space.


## Metrics dictionary
{: #metrics_dictionary}

* [CPU entitlement of the Cloud Foundry application](#ibm_cloudfoundry_app_cpu_entitlement)
* [CPU usage of the Cloud Foundry application](#ibm_cloudfoundry_app_cpu_usage)
* [CPU utilization of the Cloud Foundry application](#ibm_cloudfoundry_app_cpu_utilization)
* [Container age of the Cloud Foundry application](#ibm_cloudfoundry_app_container_age)
* [Disk usage of the Cloud Foundry application](#ibm_cloudfoundry_app_disk_bytes_used)
* [Memory usage of the Cloud Foundry application](#ibm_cloudfoundry_app_memory_bytes_used)
* [Total disk size of the Cloud Foundry application](#ibm_cloudfoundry_app_disk_bytes_total)
* [Total memory of the Cloud Foundry application](#ibm_cloudfoundry_app_memory_bytes_total)

For more information, see [the Cloud Foundry documentation: Container metrics](https://docs.cloudfoundry.org/loggregator/container-metrics.html){: external}.


### CPU entitlement of the Cloud Foundry application
{: #ibm_cloudfoundry_app_cpu_entitlement}

Indicates the CPU entitlement of a Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_cpu_entitlement`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 1: CPU entitlement of the Cloud Foundry application metric metadata" caption-side="top"}

### CPU usage of the Cloud Foundry application
{: #ibm_cloudfoundry_app_cpu_usage}

Indicates the CPU usage of the Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_cpu_usage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 2: CPU usage of the Cloud Foundry application metric metadata" caption-side="top"}


### CPU utilization of the Cloud Foundry application
{: #ibm_cloudfoundry_app_cpu_utilization}

Indicates the CPU utilization of a Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_cpu_utilization`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 3: CPU utilization of the Cloud Foundry application metric metadata" caption-side="top"}

### Container age of the Cloud Foundry application
{: #ibm_cloudfoundry_app_container_age}

Indicates the container age of the Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_container_age`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 4: Container age of the Cloud Foundry application metric metadata" caption-side="top"}

### Disk usage of the Cloud Foundry application
{: #ibm_cloudfoundry_app_disk_bytes_used}

Indicates the disk usage of the Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_disk_bytes_used`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 5: Disk usage of the Cloud Foundry application metric metadata" caption-side="top"}

### Memory usage of the Cloud Foundry application
{: #ibm_cloudfoundry_app_memory_bytes_used}

Indicates the memory usage of the Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_memory_bytes_used`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 6: Memory usage of the Cloud Foundry application metric metadata" caption-side="top"}

### Total disk size of the Cloud Foundry application
{: #ibm_cloudfoundry_app_disk_bytes_total}

Indicates the total disk size of the Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_disk_bytes_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 7: Total disk size of the Cloud Foundry application metric metadata" caption-side="top"}

### Total memory of the Cloud Foundry application
{: #ibm_cloudfoundry_app_memory_bytes_total}

Indicates the total memory of the Cloud Foundry application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_memory_bytes_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes` |
| `Segment By` | `IBM Cloud Foundry organization name`, `IBM Cloud Foundry organization GUID`, `IBM Cloud Foundry space name`, `IBM Cloud Foundry space GUID`, `IBM Cloud Foundry application name`, `IBM Cloud Foundry application index` |
{: caption="Table 8: Total memory of the Cloud Foundry application metric metadata" caption-side="top"}



## Attributes for segmentation
{: #attributes}

### Global attributes
{: #global-attributes}

The following attributes are available for segmenting all of the metrics:

| Attribute | Attribute Name | Attribute Description | Valid values |
|-----------|----------------|-----------------------|--------------|
| `Cloud Type` | `ibm_ctype` | Type of Cloud         | Valid value is `public`. |
| `Location` | `ibm_location` | Location of the monitored resource | Valid value is the region where you are monitoring metrics. |
| `Resource` | `ibm_resource` | Resource that is measured | Name or GUID of the resource |
| `Resource Type` | `ibm_resource_type` | Type of the resource that is measured | Valid value is `cf-application` |
| `Resource group` | `ibm_resource_group_name` | Resource group that is associated to the service instance. | Choose a resource group from the ones that are available in your account. |
| `Scope` | `ibm_scope` | The extent of the data samples that are considered </br>Use this attribute to set the scope to be your account | Valid value is your account.  |
| `Service name` | `ibm_service_name` | Name of the service that generates this metric | `cloud-foundry` |
{: caption="Table 9: Global segmentation attributes" caption-side="top"}



### Additional attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes. Check each metric definition to find out the segmentation options that are allowed with a metric type.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `IBM CF application index` | `ibm_cloudfoundry_app_index` | IBM Cloud Foundry application index |
| `IBM CF application name` | `ibm_cloudfoundry_app_name` | IBM Cloud Foundry application name |
| `IBM CF organization GUID` | `ibm_cloudfoundry_org_guid` | IBM Cloud Foundry organization GUID |
| `IBM CF organization name` | `ibm_cloudfoundry_org_name` | IBM Cloud Foundry organization name |
| `IBM CF space GUID` | `ibm_cloudfoundry_space_guid` | IBM Cloud Foundry space GUID |
| `IBM CF space name` | `ibm_cloudfoundry_space_name` | IBM Cloud Foundry space name |
{: caption="Table 10: Additional segmentation attributes" caption-side="top"}



## Cloud Foundry dashboards dictionary
{: #dashboards_dictionary}

The following table outlines the pre-defined dashboards that you can use to monitor Cloud Foundry metrics:

| Dashboard name                  | Description    |
|---------------------------------|----------------|
| `Overview CF apps`   | Default dashboard when you launch the monitoring UI from your service instance UI. |
{: caption="Table 11: Pre-defined dashboards" caption-side="top"}

These dashboards cannot be changed.
{: important}
