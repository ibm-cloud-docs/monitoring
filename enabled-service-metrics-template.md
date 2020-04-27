---

copyright:
  years:  2019, 2020
lastupdated: "2020-02-03"

keywords: Sysdig, IBM Cloud, monitoring, service, cloud foundry, cf

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


## Platform metrics overview
{: #platform_metrics}

You can configure 1 instance only of the {{site.data.keyword.mon_full_notm}} service per region to collect platform metrics. 
* To configure the Sysdig instance, you must set on the *platform metrics* configuration setting. 
* If a Sysdig instance in a region is already enabled to collect platform metrics, metrics from enabled-Sysdig services are collected automatically and available for monitoring through this instance. For more information about enabled-Sysdig services, see [Cloud services](/docs/Monitoring-with-Sysdig?topic=Sysdig-cloud_services).

To monitor platform metrics, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where the {{site.data.keyword.messagehub}} instance is provisioned.
{: important}

## Enabling platform metrics from the {{site.data.keyword.messagehub}} dashboard
{: #enable_platform_metrics}

Complete the following steps to configure platform metrics:

1. Log in to {{site.data.keyword.cloud_notm}}. 

    The {{site.data.keyword.cloud_notm}} dashboard. 
    
2. Click **View resources**.

3. In the *Services* section, click the {{site.data.keyword.messagehub}} instance that you plan to monitor. 

    The {{site.data.keyword.messagehub}} UI *Manage* page opens.

4. Click the overflow menu ![overflow menu](icons/actions-icon-vertical.svg "Overflow menu"). Then, select **Add monitoring** to configure *platform metrics* in the region of your {{site.data.keyword.messagehub}} instance.

    If the menu choices include the option **Monitoring**, then your instance is already configured for platform metrics. 
    {: note}
    
5. Provision an instance of the {{site.data.keyword.mon_full_notm}} service.

After you provision the Sysdig instance, the *Observabvility* page opens. To continue working with {{site.data.keyword.messagehub}}, go back to the {{site.data.keyword.messagehub}} UI.
{: note}


## Viewing metrics
{: #view_metrics}

To monitor {{site.data.keyword.messagehub}} metrics, you must launch the Sysdig web UI instance that id enabled for platform metrics in the region where your {{site.data.keyword.messagehub}} instance is available.
{: important}

There are different options to launch the Sysdig web UI and monitor metrics:

### Launching Sysdig web UI from the {{site.data.keyword.messagehub}} dashboard
{: #view_metrics_opt1}

Complete the following steps to launch the Sysdig web UI from the {{site.data.keyword.messagehub}} dashboard:

1. Log in to {{site.data.keyword.cloud_notm}}. 

    The {{site.data.keyword.cloud_notm}} dashboard. 
    
2. Click **View resources**.

3. In the *Services* section, click the {{site.data.keyword.messagehub}} instance that you plan to monitor. 

    The {{site.data.keyword.messagehub}} UI *Manage* page opens.

4. Click the overflow menu ![overflow menu](../../icons/actions-icon-vertical.svg "Overflow menu"). Then, select **Monitoring**.

    A new tab in your browser opens and displays the *Default* dashboard named **IBM Event Streams** within the context of your {{site.data.keyword.messagehub}} instance.


### Launching Sysdig web UI from the Observability page
{: #view_metrics_opt2}

Complete the following steps to launch the Sysdig web UI from the *Observability* page:

1.[Launch the Sysdig web UI.](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch)
2. Select **DASHBOARDS**.
3. In the **Default Dashboards** section, expand **IBM**.
4. Choose the {{site.data.keyword.messagehub}} dashboard from the list.

Next, change the scope or make a copy of the *Default* dashboard to monitor a {{site.data.keyword.messagehub}} instance.  




## Metrics available by service plan
{: #metrics_by_plan}

| Metric Name |Lite|Standard|Enterprise|
|-----------|--------|--------|--------|
| [Accumulated Producer Conversion Time](#ibm_eventstreams_instance_produce_conversions_time_quantile) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Accumulated message conversion time](#ibm_eventstreams_instance_consume_conversions_time_quantile) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Authentication failure count](#ibm_eventstreams_kafka_authentication_failure_total) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Bytes In Per Second](#ibm_eventstreams_instance_bytes_in_per_second) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Bytes out per second](#ibm_eventstreams_instance_bytes_out_per_second) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Consumer group rebalancing count](#ibm_eventstreams_instance_rebalancing_consumergroups) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Disk Utilization](#ibm_eventstreams_instance_utilised_disk_space_percent) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Inactive consumer group count](#ibm_eventstreams_instance_inactive_consumergroups) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Kafka API connections count](#ibm_eventstreams_kafka_connected_clients_estimated) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Number of partitions](#ibm_eventstreams_instance_partitions) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Number of topics](#ibm_eventstreams_instance_topics) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Rejected connections Unsupported SNI](#ibm_eventstreams_kafka_missing_sni_host_total) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Reserved Disk Space](#ibm_eventstreams_instance_reserved_disk_space_percent) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Stable consumer group count](#ibm_eventstreams_instance_stable_consumergroups) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Topic bytes consumed per second](#ibm_eventstreams_instance_topic_bytes_out_per_second) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Topic bytes in per second](#ibm_eventstreams_instance_topic_bytes_in_per_second) |    | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 1: Metrics Available by Plan Names" caption-side="top"}


## Metrics dictionary
{: #metrics_dictionary}


| Metric Name |
|-----------|
| [CPU entitlement of the Cloud Foundry application](#ibm_cloudfoundry_app_cpu_entitlement) | 
| [CPU usage of the Cloud Foundry application](#ibm_cloudfoundry_app_cpu_usage) | 
| [CPU utilization of the Cloud Foundry application](#ibm_cloudfoundry_app_cpu_utilization) | 
| [Container age of the Cloud Foundry application](#ibm_cloudfoundry_app_container_age) | 
| [Disk usage of the Cloud Foundry application](#ibm_cloudfoundry_app_disk_bytes_used) | 
| [Memory usage of the Cloud Foundry application](#ibm_cloudfoundry_app_memory_bytes_used) | 
| [Total disk size of the Cloud Foundry application](#ibm_cloudfoundry_app_disk_bytes_total) | 
| [Total memory of the Cloud Foundry application](#ibm_cloudfoundry_app_memory_bytes_total) | 
{: caption="Table 1: Metrics Available" caption-side="top"}

### CPU entitlement of the Cloud Foundry application
{: #ibm_cloudfoundry_app_cpu_entitlement}

CPU entitlement of the Cloud Foundry application

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_cloudfoundry_app_cpu_entitlement`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `IBM Cloud Foundry organization name, IBM Cloud Foundry organization GUID, IBM Cloud Foundry space name, IBM Cloud Foundry space GUID, IBM Cloud Foundry application name, IBM Cloud Foundry application index` |
{: caption="Table 2: CPU entitlement of the Cloud Foundry application metric metadata" caption-side="top"}




## Attributes for Segmentation
{: attributes}

### Global Attributes
{: global-attributes}

The following attributes are available for segmenting all of the metrics listed above

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of public, dedicated or local |
| `Location` | `ibm_location` | The location of the monitored resource - this may be a region, data center or global |
| `Resource` | `ibm_resource` | The resource being measured by the service - typically a indentifying name or GUID |
| `Resource Type` | `ibm_resource_type` | The type of the resource being measured by the service |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created |
| `Scope` | `ibm_scope` | The scope is the account, organization or space GUID associated with this metric |
| `Service name` | `ibm_service_name` | Name of the service generating this metric |

### Additional Attributes
{: additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the reference above.  Please see the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `IBM Cloud Foundry application index` | `ibm_cloudfoundry_app_index` | IBM Cloud Foundry application index |
| `IBM Cloud Foundry application name` | `ibm_cloudfoundry_app_name` | IBM Cloud Foundry application name |
| `IBM Cloud Foundry organization GUID` | `ibm_cloudfoundry_org_guid` | IBM Cloud Foundry organization GUID |
| `IBM Cloud Foundry organization name` | `ibm_cloudfoundry_org_name` | IBM Cloud Foundry organization name |
| `IBM Cloud Foundry space GUID` | `ibm_cloudfoundry_space_guid` | IBM Cloud Foundry space GUID |
| `IBM Cloud Foundry space name` | `ibm_cloudfoundry_space_name` | IBM Cloud Foundry space name |
