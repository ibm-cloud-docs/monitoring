---

copyright:
  years: 2020, 2020
lastupdated: "2020-03-16"

keywords: Sysdig, IBM Cloud, monitoring, disaster recovery, ha, high availability, redundancy

subcollection: Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.mon_full_notm}} is a highly available, multi-tenant, regional service for monitoring your applications, platform resources and infrastructure. In this topic, you can learn more about {{site.data.keyword.mon_full_notm}}'s availability and disaster recovery strategies.
{: shortdesc}



## Availability zones
{: #ha-dr_locations}

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
| `Europe`              | `Frankfurt (eu-de)`      | `MZR`     |
| `Europe`              | `London (eu-gb)`         | `MZR`     |
| `North America`       | `Dallas (us-south)`      | `MZR`     |
| `North America`       | `Washington (us-east)`   | `MZR`     |
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
* Metric data and the monitoring metadata such as dashboards, alerts, teams, and users, are backed up every 24 hours. In the event of an un-recoverable disaster, up to 24 hours of metric data and metadata changes to the monitoring instance in the failure region can be lost.
* The estimated recovery time for rebuilding the regional site and restoring the service at another location is 24 hours.
* Due to the large volume of data, historical data will not be available at the time the service is restored, as this process requires additional time to recover data from the backups.  
* You might have 1 or more monitoring instances in the region. When these service instances are available in the new location, you will be able to use them while the historical data is restored into the newly constructed region.
* You will have to update the endpoints of applications and Sysdig agents to point to the ingestion endpoint in the new location. 




### Manual recovery of the service
{: #dr-rebuilt}

If a regional disaster occurs, the recovery time of the service depends on the recovery time for the region. To minimize the downtime of the service and impact to your business, you could implement a manual failover to switch to another region while the region is being restored. To reduce the time to get up and running in a new location, consider using access groups to manage permissions working with the service, and backup the monitoring metadata of each instance. You should backup your alerts, notifications, dashboards and team definitions on a regular basis.

How to continue working while a DR site is rebuilt?

If the applications and services that you are monitoring through a monitoring instance are all co-located in the same region, then you must wait for the region to be available again for business.

If you have deployed Sysdig agents on your systems, and those systems are not impacted by the regional failure, you may choose to redirect metrics to other instances of Sysdig in a different region. To redirect metric data, complete the following steps:
1. [Provision a Sysdig instance](/docs/Monitoring-with-Sysdig?topic=Sysdig-provision)
2. Reconfigure the Sysdig agent of each system: Change the access key and ingestion endpoints in the agent configuration. [Learn more](/docs/Monitoring-with-Sysdig?topic=Sysdig-config_agent).
3. Define IAM permissions to work with the new monitoring instance.

    Using access groups to manage permissions to work with a Sysdig monitoring instance, reduces the amount of work that you might have to do to set the correct policies and users to work with a new instance. Information about access groups is global and not region based.
    {: tip}

4. Launch the Sysdig instance and import the alerts, notifications, teams, and dashboards to monitor your applications and systems.






