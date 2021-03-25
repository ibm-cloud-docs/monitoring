---

copyright:
  years: 2018, 2021
lastupdated: "2021-04-24"

keywords: Sysdig, IBM Cloud, monitoring, platform metrics

subcollection: Monitoring-with-Sysdig

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
{:external: target="_blank" .external}


# Cloud services by location
{: #cloud_services_locations}

List of locations where {{site.data.keyword.cloud_notm}} services are enabled to send metrics to {{site.data.keyword.mon_full_notm}}. You monitor these metrics through the Sysdig instance that is configured to receive platform metrics. [Learn more about enabling platform metrics](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-platform_metrics_enabling).
{:shortdesc}

## Cloud Foundry
{: #cloud_services_locations_cf}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| Cloud Foundry                                                 | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  |          
{: caption="CF integration in Europe locations" caption-side="top"}
{: #cs_cf-table-1}
{: tab-title="Europe"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| Cloud Foundry                                  | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |          
{: caption="CF integration in America's locations" caption-side="top"}
{: #cs_cf-table-2}
{: tab-title="America"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| Cloud Foundry                                  |                  | ![Checkmark icon](../images/checkmark-icon.svg) |      
{: caption="CF integration in AP locations" caption-side="top"}
{: #cs_cf-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}


## Compute services
{: #cloud_services_locations_compute}

For more information, see [Compute services](/docs/cloud-infrastructure?topic=cloud-infrastructure-compute).

### Serverless
{: #cloud_services_locations_compute_serverless}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.openwhisk}}          | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  |          
{: caption="Serverless integration in Europe locations" caption-side="top"}
{: #cs_sv-table-1}
{: tab-title="Europe"}
{: tab-group="cs_sv"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.openwhisk}}        | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg) `[*]` |          
{: caption="Serverless integration in America's locations" caption-side="top"}
{: #cs_sv-table-2}
{: tab-title="America"}
{: tab-group="cs_sv"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.openwhisk}}        | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg) |      
{: caption="Serverless integration in AP locations" caption-side="top"}
{: #cs_sv-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_sv"}
{: class="simple-tab-table"}
{: row-headers}

### VPC
{: #cloud_services_locations_compute_vpc}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| VPC virtual server instances                          | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  |          
{: caption="Infrastructure services integration in Europe locations" caption-side="top"}
{: #cs_vpcinfra-table-1}
{: tab-title="Europe"}
{: tab-group="cs_vpcinfra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| VPC virtual server instances           | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |          
{: caption="Infrastructure services integration in America's locations" caption-side="top"}
{: #cs_vpcinfra-table-2}
{: tab-title="America"}
{: tab-group="cs_vpcinfra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | 
|------------------------------------------------|------------------|----------------------------|
| VPC virtual server instances           | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |     
{: caption="Infrastructure services integration in AP locations" caption-side="top"}
{: #cs_vpcinfra-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_vpcinfra"}
{: class="simple-tab-table"}
{: row-headers}

### Classic
{: #cloud_services_locations_compute_classic}


| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.BluVirtServers}}                          |                  | ![Checkmark icon](../images/checkmark-icon.svg)  |          
{: caption="Infrastructure services integration in Europe locations" caption-side="top"}
{: #cs_infra-table-1}
{: tab-title="Europe"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.BluVirtServers}}           | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |          
{: caption="Infrastructure services integration in America's locations" caption-side="top"}
{: #cs_infra-table-2}
{: tab-title="America"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | 
|------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.BluVirtServers}}           |   |   |     
{: caption="Infrastructure services integration in AP locations" caption-side="top"}
{: #cs_infra-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

## Container services
{: #cloud_services_locations_container}

You can choose the Sysdig instance where you want to collect {{site.data.keyword.containerlong}} service metrics.

You can choose the Sysdig instance where you want to collect {{site.data.keyword.openshiftlong}} service metrics.

You can monitor {{site.data.keyword.satellitelong}} through the Sysdig instance that is configured with **service platform logs** in the same region that your {{site.data.keyword.satelliteshort}} location is managed from.

The following tables list the locations where automatic collection of registry service metrics is enabled. For more information, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor_sysdig).

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.registrylong_notm}}          | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  |          
{: caption="Containers integration in Europe locations" caption-side="top"}
{: #cs_cont-table-1}
{: tab-title="Europe"}
{: tab-group="cs_cont"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.registrylong_notm}}        | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg) `[*]` |          
{: caption="Containers integration in America's locations" caption-side="top"}
{: #cs_cont-table-2}
{: tab-title="America"}
{: tab-group="cs_cont"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Osaka (jp-osa)`  | `Sydney (au-syd)`   |
|------------------------------------------------|------------------|----------------------------|----------------------------|
| {{site.data.keyword.registrylong_notm}}        | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |      
{: caption="Containers integration in AP locations" caption-side="top"}
{: #cs_cont-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_cont"}
{: class="simple-tab-table"}
{: row-headers}

`[*]` {{site.data.keyword.registrylong_notm}} global registry metrics are available through the Sysdig Washington (us-east) instance.


## Developer tools
{: #cloud_services_locations_devops}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.contdelivery_full}} | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Developer tools and DevOps services in Europe locations" caption-side="top"}
{: #cs_devops-table-1}
{: tab-title="Europe"}
{: tab-group="cs_devops"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.contdelivery_full}} | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Developer tools and DevOps services in America's locations" caption-side="top"}
{: #cs_devops-table-2}
{: tab-title="America"}
{: tab-group="cs_devops"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Seoul 01 (seo01)` | `Chennai 01 (che01)` |
|------------------------------------------------|------------------|----------------------------|--------------------|----------------------|
| {{site.data.keyword.contdelivery_full}} | ![Checkmark icon](../images/checkmark-icon.svg) |   |   |   |  
{: caption="Developer tools and DevOps services in AP locations" caption-side="top"}
{: #cs_devops-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_devops"}
{: class="simple-tab-table"}
{: row-headers}



## Networking services
{: #cloud_services_locations_networking}

For more information, see [Networking services](/docs/cloud-infrastructure?topic=cloud-infrastructure-network).

### VPC
{: #cloud_services_locations_networking_vpc}

| Service                                                       |`Frankfurt (eu-de)`  | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| Load Balancer for VPC   | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| VPN for VPC             | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |    
{: caption="VPC events in Europe locations" caption-side="top"}
{: #cs-vpc-loc-table-3}
{: tab-title="Europe"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                | `Dallas (us-south)`                                | `Washington (us-east)`               |
|----------------------------------------|----------------------------------------------------|--------------------------------------|
| Load Balancer for VPC                  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| VPN for VPC                            | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="VPC events in America's locations" caption-side="top"}
{: #cs-vpc-loc-table-1}
{: tab-title="America"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` |`Sydney (au-syd)`           |
|-----------------------------------------------------------------|------------------|----------------------------|
| Load Balancer for VPC           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| VPN for VPC                     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="VPC events in AP locations" caption-side="top"}
{: #cs-vpc-loc-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}





### Classic
{: #cloud_services_locations_networking_classic}

| Service                                                       |`Frankfurt (eu-de)`  | `London (eu-gb)` |
|---------------------------------------------------------------|-------------------|----------------|
| {{site.data.keyword.loadbalancer_full}}                |                 |    |
| Load Balancer for VPC              |    |    |
| VPN for VPC                       |  ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |    
{: caption="Table 12. Security services  integration in Europe locations" caption-side="top"}
{: #cs-csint-table-3}
{: tab-title="Europe"}
{: tab-group="cs_csint"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Dallas (us-south)` | `Washington (us-east)`               |
|-----------------------------------------------------------------|---------------------|--------------------------------------|
| {{site.data.keyword.loadbalancer_full}}         | ![Checkmark icon](../images/checkmark-icon.svg)               |            |          
| Load Balancer for VPC                          | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| VPN for VPC                                    | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |  
{: caption="Table 10. Security services integration in America's locations" caption-side="top"}
{: #cs-csint-table-1}
{: tab-title="America"}
{: tab-group="cs_csint"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` |`Sydney (au-syd)`           |
|-----------------------------------------------------------------|----------------|---------------------------|
| {{site.data.keyword.loadbalancer_full}}                   |      |    |
| Load Balancer for VPC          |     |    |
| VPN for VPC                    | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Table 11. Security services integration in AP locations" caption-side="top"}
{: #cs-csint-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_csint"}
{: class="simple-tab-table"}
{: row-headers}






## Database services
{: #cloud_services_locations_database}


| Service        | `Frankfurt (eu-de)`           | `London (eu-gb)`                                   |
|----------------|-------------------------------|----------------------------------------------------|
| {{site.data.keyword.cloudant_short_notm}}                        |    | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.sqlquery_full}}                             | ![Checkmark icon](../images/checkmark-icon.svg)  |    |
| {{site.data.keyword.ihsdbaas_mongodb_full}}| ![Checkmark icon](../images/checkmark-icon.svg)  |    |
| {{site.data.keyword.ihsdbaas_postgresql_full}}| ![Checkmark icon](../images/checkmark-icon.svg)  |    |
{: caption="Database services integration in Europe locations" caption-side="top"}
{: #cs_db-table-1}
{: tab-title="Europe"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}

| Service               | `Dallas (us-south)`             | `Washington (us-east)`                             |
|-----------------------|---------------------------------|----------------------------------------------------|
| {{site.data.keyword.cloudant_short_notm}}                       | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](../images/checkmark-icon.svg)` | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.sqlquery_full}}                             | ![Checkmark icon](../images/checkmark-icon.svg)  |    |
| {{site.data.keyword.ihsdbaas_mongodb_full}}| ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.ihsdbaas_postgresql_full}}| ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Database services integration in America's locations" caption-side="top"}
{: #cs_db-table-2}
{: tab-title="America"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|-----------------------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.cloudant_short_notm}}                        | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | 
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | 
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.sqlquery_full}}                             |    |    |
| {{site.data.keyword.ihsdbaas_mongodb_full}}|    | ![Checkmark icon](../images/checkmark-icon.svg)  |
| {{site.data.keyword.ihsdbaas_postgresql_full}}|    | ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="Database services integration in AP locations" caption-side="top"}
{: #cs_db-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}



## Integration services
{: #cloud_services_locations_integration}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.messagehub}}             | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)|
| {{site.data.keyword.mobilepushshort}}        |  |   |        
{: caption="Integration services integration in Europe locations" caption-side="top"}
{: #cs_integration-table-1}
{: tab-title="Europe"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |  
| {{site.data.keyword.mobilepushshort}}        |  |   |           
{: caption="Integration services integration in America's locations" caption-side="top"}
{: #cs_integration-table-2}
{: tab-title="America"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Seoul 01 (seo01)` | `Chennai 01 (che01)` |
|------------------------------------------------|------------------|----------------------------|--------------------|----------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  `Metrics are available through the platform metrics Sysdig instance in Tokyo` | `Metrics are available through the platform metrics Sysdig instance in Tokyo` |  
| {{site.data.keyword.mobilepushshort}}        |  |   |        
{: caption="Integration services integration in AP locations" caption-side="top"}
{: #cs_integration-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}



## Security services
{: #cloud_services_locations_security}

The following tables list the locations where automatic collection of security service logs is enabled. You can monitor logs through the instance that is available in the same location as your security resources, if you enable 1 instance in this location to host service platform logs. For locations where you can provision a service instance but the {{site.data.keyword.at_full_notm}} service is not available, specific detail about the location where you can monitor those logs is provided in each case.


| Service                                                         | `Dallas (us-south)`                               | `Washington (us-east)`                |
|-----------------------------------------------------------------|---------------------------------------------------|---------------------------------------|
| {{site.data.keyword.keymanagementservicelong}}                  | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |
| {{site.data.keyword.security-advisor_long}}                     | ![Checkmark icon](images/checkmark-icon.svg) |    |   
{: caption="Security services integration in America's locations" caption-side="top"}
{: #cs-sec-table-1}
{: tab-title="America"}
{: tab-group="cs_sec"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)`                                   |`Sydney (au-syd)`           |
|-----------------------------------------------------------------|----------------------------------------------------|----------------------------|
| {{site.data.keyword.keymanagementservicelong}}                  | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} |      | ![Checkmark icon](images/checkmark-icon.svg) |
| {{site.data.keyword.security-advisor_long}}                     |      |     |         
{: caption="Security services integration in AP locations" caption-side="top"}
{: #cs-sec-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_sec"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                       |`Frankfurt (eu-de)`                                 | `London (eu-gb)` |
|---------------------------------------------------------------|----------------------------------------------------|------------------|
| {{site.data.keyword.keymanagementservicelong}}                | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} | ![Checkmark icon](images/checkmark-icon.svg) |    |
| {{site.data.keyword.security-advisor_long}}                     |   | ![Checkmark icon](images/checkmark-icon.svg) |
{: caption="Security services integration in Europe locations" caption-side="top"}
{: #cs-sec-table-3}
{: tab-title="Europe"}
{: tab-group="cs_sec"}
{: class="simple-tab-table"}
{: row-headers}

## Storage services
{: #cloud_services_locations_storage}

For more information, see [Storage services](/docs/cloud-infrastructure?topic=cloud-infrastructure-compute).


### VPC
{: #cloud_services_locations_storage_vpc}


| Service                                                       |`Frankfurt (eu-de)`                                | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------------------------------------|------------------|
| {{site.data.keyword.cos_full_notm}}                    | ![Checkmark icon](../images/checkmark-icon.svg) |  ![Checkmark icon](../images/checkmark-icon.svg)  |     
{: caption="Storage services integration in Europe locations" caption-side="top"}
{: #cs_storage-table-3}
{: tab-title="Europe"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)`                                | `Washington (us-east)`               |
|------------------------------------------------|----------------------------------------------------|--------------------------------------|
| {{site.data.keyword.cos_full_notm}}            | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |          
{: caption="Storage services integration in America's locations" caption-side="top"}
{: #cs_storage-table-1}
{: tab-title="America"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                  | `Tokyo (jp-tok)`                                  |`Sydney (au-syd)`           |
|----------------------------------------------------------|---------------------------------------------------|----------------------------|
| {{site.data.keyword.cos_full_notm}}                      | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |     
{: caption="Storage services integration in AP locations" caption-side="top"}
{: #cs_storage-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}

## AI
{: #cloud_services_locations_ai}

| Service                             | `Dallas (us-south)`                            | `Washington (us-east)`                     |
|-------------------------------------|------------------------------------------------|--------------------------------------------|
| {{site.data.keyword.wh-acd_short}}  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |          
{: caption="AI / Machine Learning services integration in America's locations" caption-side="top"}
{: #ai-table-1}
{: tab-title="America"}
{: tab-group="cs_ai"}
{: class="simple-tab-table"}
{: row-headers}
