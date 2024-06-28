---

copyright:
  years:  2018, 2024
lastupdated: "2024-06-28"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.mon_full_notm}} is a highly available, multi-tenant, regional service for monitoring your applications, platform resources and infrastructure. In this topic, you can learn more about {{site.data.keyword.mon_full_notm}}'s availability and disaster recovery strategies.
{: shortdesc}



## Availability zones
{: #ha-dr-locations}

An availability zone is a logically and physically isolated location within an {{site.data.keyword.cloud_notm}} region where your data is processed and hosted.
* An availability zone has independent power, cooling, and network infrastructures that are isolated from other zones to strengthen fault tolerance by avoiding single points of failure between zones.
* An availability zone offers high bandwidth and low inter-zone latency within a region.

A region (location) is a geographically and physically separate group of one or more availability zones with independent electrical and network infrastructures isolated from other regions.
* Regions are designed to remove shared single points of failure with other regions and guarantee low inter-zone latency within the region.
* Each region has 3 different data centers (DC) for redundancy.

The following table lists the high-availability (HA) status for the regions (locations) where the {{site.data.keyword.mon_full_notm}} service is available:

| Geography             | Region                   | HA Status |
|-----------------------|--------------------------|-----------|
| `Asia Pacific`        | `Sydney (au-syd)`        | `MZR`     |
| `Asia Pacific`        | `Tokyo (jp-tok)`         | `MZR`     |
| `Asia Pacific`        | `Osaka (jp-osa)`         | `MZR`     |
| `Europe`              | `Frankfurt (eu-de)`      | `MZR`     |
| `Europe`              | `London (eu-gb)`         | `MZR`     |
| `Europe`              | `Madrid (eu-es)`         | `MZR`     |
| `North America`       | `Dallas (us-south)`      | `MZR`     |
| `North America`       | `Washington (us-east)`   | `MZR`     |
| `North America`       | `Toronto (ca-tor)`       | `MZR`     |
| `South America`       | `São-Paulo (br-sao)`     | `MZR`     |
{: caption="Table 1. List of locations where the service is available" caption-side="top"}

Where
* A *geography* is a geographic area or larger political body that contains one or more regions.
* A *region* is a defined geographic territory.

    A region could be a specific postal code area, a town, a city, a state, a group of states, or even a group of countries.

    A region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

* `N/A` means feature that is not applicable to that geography.
* `MZR` means multi-zone region. [Learn more](/docs/overview?topic=overview-locations#mzr-table).



## Availability of a monitoring instance
{: #ha-dr-region}

When you provision a monitoring instance, you select the MZR (location) where the instance is created. The region determines where the monitoring data is processed and the data is hosted.

A multizone region (MZR) consist of 3 or more availability zones that are independent from each other to ensure that single failure events affect only a single zone.

By default, each monitoring instance consist of 3 zones, one primary zone and two secondary zones:
* Each zone is located in a different data center in the region.
* The data in your primary zone is automatically replicated to the secondary zones with low latency. You don't need to do anything to enable the replication.
* When the primary zone fails, a secondary zone is elected as the primary to prevent your service instance from being affected.
* If 2 zones fail at the same time, the service is down.

The MZR architecture offers automatic failover between 2 zones, and high availability for a monitoring instance withing a region.



## Disaster recovery (DR) of the monitoring service in a region
{: #dr}

Disaster recovery is about surviving a catastrophic failure or loss of availability in a single location.

{{site.data.keyword.mon_full_notm}} follows {{site.data.keyword.cloud_notm}} requirements for [planning and recovering from disaster events](/docs/overview?topic=overview-zero-downtime#disaster-recovery).

If a regional disaster occurs, consider the following information:
* The estimated recovery time for rebuilding the regional site and restoring the service at another location is 24 hours.
* You will have to update the endpoints of applications and monitoring agents to point to the ingestion endpoint in the new location.
* You will have to restore the service instance's metadata, that is, dashboards and alerts definitions, from your backups.

Historical data may be lost during a disaster. If you require historical metrics for auditing purposes, backup the metrics regularly by querying the metrics from the service and storing them at a remote backup site. For more information, see [Extracting metrics from a {{site.data.keyword.mon_short}} instance by using the API](/docs/monitoring?topic=monitoring-metrics_api).
{: note}

### Manual recovery of the service
{: #dr-rebuilt}

If a regional disaster occurs, the recovery time of the service depends on the recovery time for the region. To minimize the downtime of the service and impact to your business, you could implement a manual failover to switch to another region while the region is being restored. To reduce the time to get up and running in a new location, consider using access groups to manage permissions working with the service, and backup the monitoring metadata of each instance. You should backup your alerts, notifications, dashboards and team definitions on a regular basis.

How to continue working while a DR site is rebuilt?

If the applications and services that you are monitoring through a monitoring instance are all co-located in the same region, then you must wait for the region to be available again for business.

If you have deployed monitoring agents on your systems, and those systems are not impacted by the regional failure, you may choose to redirect metrics to other instances of monitoring in a different region. To redirect metric data, complete the following steps:
1. [Provision a monitoring instance](/docs/monitoring?topic=monitoring-provision)
2. Reconfigure the monitoring agent of each system: Change the access key and ingestion endpoints in the agent configuration. [Learn more](/docs/monitoring?topic=monitoring-config_agent).
3. Define IAM permissions to work with the new monitoring instance.

    Using access groups to manage permissions to work with a monitoring instance, reduces the amount of work that you might have to do to set the correct policies and users to work with a new instance. Information about access groups is global and not region based.
    {: tip}

4. Launch the monitoring instance and import the alerts, notifications, teams, and dashboards to monitor your applications and systems.



### DR recovery time
{: #dr_recovery_time}

The following table indicates the estimated recovery times in the event of a DR situation:

| Recovery objective for DR | Estimated time |
|---------------------------|----------------|
| Maximum Tolerable Downtime (MTD) / Recovery Time Objective (RTO)  | Up to 24 hours |
| Recovery Point Objective (RPO) | Up to 24 hours |
{: caption="Table 2. Recovery objectives for DR" caption-side="top"}
