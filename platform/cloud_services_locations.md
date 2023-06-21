---

copyright:
  years:  2018, 2023
lastupdated: "2023-02-01"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Services generating metrics by location
{: #cloud_services_locations}

List of locations where {{site.data.keyword.cloud_notm}} services are enabled to send metrics to {{site.data.keyword.mon_full_notm}}. You monitor these metrics through the monitoring instance that is configured to receive platform metrics. [Learn more about enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).
{: shortdesc}

## Cloud Foundry
{: #cloud_services_locations_cf}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| Cloud Foundry                                                 | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="CF integration in Europe locations" caption-side="top"}
{: #cs-cf-table-1}
{: tab-title="Europe"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| Cloud Foundry                                  | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |
{: caption="CF integration in America's locations" caption-side="top"}
{: #cs-cf-table-2}
{: tab-title="America"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| Cloud Foundry                                  |                  | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="CF integration in AP locations" caption-side="top"}
{: #cs-cf-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}


## Compute services
{: #cloud_services_locations_compute}

### Serverless
{: #cloud_services_locations_compute_serverless}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.codeenginefull_notm}}                | ![Checkmark icon](../images/checkmark-icon.svg) |    |
| {{site.data.keyword.openwhisk}}          | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="Serverless integration in Europe locations" caption-side="top"}
{: #cs-sv-table-1}
{: tab-title="Europe"}
{: tab-group="cs_sv"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.codeenginefull_notm}}                | ![Checkmark icon](../images/checkmark-icon.svg) |    |
| {{site.data.keyword.openwhisk}}        | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg) `[*]` |
{: caption="Serverless integration in America's locations" caption-side="top"}
{: #cs-sv-table-2}
{: tab-title="America"}
{: tab-group="cs_sv"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.codeenginefull_notm}}                | ![Checkmark icon](../images/checkmark-icon.svg) |    |
| {{site.data.keyword.openwhisk}}        | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Serverless integration in AP locations" caption-side="top"}
{: #cs-sv-table-3}
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
{: #cs-vpcinfra-table-1}
{: tab-title="Europe"}
{: tab-group="cs_vpcinfra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| VPC virtual server instances           | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |
{: caption="Infrastructure services integration in America's locations" caption-side="top"}
{: #cs-vpcinfra-table-2}
{: tab-title="America"}
{: tab-group="cs_vpcinfra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| VPC virtual server instances           | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Infrastructure services integration in AP locations" caption-side="top"}
{: #cs-vpcinfra-table-3}
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
{: #cs-infra-table-1}
{: tab-title="Europe"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.BluVirtServers}}           | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |
{: caption="Infrastructure services integration in America's locations" caption-side="top"}
{: #cs-infra-table-2}
{: tab-title="America"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.BluVirtServers}}           |   |   |
{: caption="Infrastructure services integration in AP locations" caption-side="top"}
{: #cs-infra-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

### {{site.data.keyword.vmware-service_full}}
{: #cloud_services_locations_compute_vmware-service}

| Service              | `Frankfurt (eu-de)` | `London (eu-gb)` |
|----------------------|---------------------|------------------|
| {{site.data.keyword.vmware-service_short}} | ![Checkmark icon](../images/checkmark-icon.svg) |   |
{: caption="{{site.data.keyword.vmware-service_short}} services integration in Europe locations" caption-side="top"}
{: #cs-vmware-service-table-1}
{: tab-title="Europe"}
{: tab-group="cs_vmware-service"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.vmware-service_short}} | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="{{site.data.keyword.vmware-service_short}} services integration in America's locations" caption-side="top"}
{: #cs-vmware-service-table-2}
{: tab-title="America"}
{: tab-group="cs_vmware-service"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.vmware-service_short}}     |   |   |
{: caption="{{site.data.keyword.vmware-service_short}} services integration in AP locations" caption-side="top"}
{: #cs-vmware-service-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_vmware-service"}
{: class="simple-tab-table"}
{: row-headers}

## Container services
{: #cloud_services_locations_container}

{{site.data.keyword.registrylong_notm}}
:   You can configure one monitoring instance in each region to collect platform metrics for {{site.data.keyword.registrylong}}. For information about the locations where the automatic collection of {{site.data.keyword.registryshort_notm}} service metrics is enabled, see [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor#registry_monitor_locations).

{{site.data.keyword.containerlong_notm}}
:   You can choose the monitoring instance where you want to collect {{site.data.keyword.containerlong}} service metrics.

{{site.data.keyword.openshiftlong_notm}}
:   You can choose the monitoring instance where you want to collect {{site.data.keyword.openshiftlong}} service metrics.

## Satellite
{: #cloud_services_locations_satellite}

{{site.data.keyword.satellitelong_notm}}
:   You can monitor {{site.data.keyword.satellitelong}} through the monitoring instance that is configured with **service platform metrics** in the same region that your {{site.data.keyword.satelliteshort}} location is managed from.


## Developer tools
{: #cloud_services_locations_devops}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.contdelivery_full}} | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.appconfig_full}}    |                                                 |![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.en_full}}    |                                                 |![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Developer tools and DevOps services in Europe locations" caption-side="top"}
{: #cs-devops-table-1}
{: tab-title="Europe"}
{: tab-group="cs_devops"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`  |`Toronto (ca-tor)` | `Sao Paulo (br-sao)` |
|------------------------------------------------|---------------------|-------------------------|-------------------|----------------------|
| {{site.data.keyword.contdelivery_full}} | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.appconfig_full}}    | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.en_full}}    | ![Checkmark icon](../images/checkmark-icon.svg) |                             |
{: caption="Developer tools and DevOps services in America's locations" caption-side="top"}
{: #cs-devops-table-2}
{: tab-title="America"}
{: tab-group="cs_devops"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)`    | `Sydney (au-syd)` | `Osaka (jp-osa)` | `Chennai (in-che)` |
|------------------------------------------------|---------------------|-------------------|------------------|--------------------|
| {{site.data.keyword.contdelivery_full}}        |![Checkmark icon](../images/checkmark-icon.svg) |![Checkmark icon](../images/checkmark-icon.svg)|![Checkmark icon](../images/checkmark-icon.svg)|   |
| {{site.data.keyword.appconfig_full}}           |           | ![Checkmark icon](../images/checkmark-icon.svg) |  |
| {{site.data.keyword.en_full}}           |                                               | ![Checkmark icon](../images/checkmark-icon.svg) |    |  |
{: caption="Developer tools and DevOps services in AP locations" caption-side="top"}
{: #cs-devops-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_devops"}
{: class="simple-tab-table"}
{: row-headers}


## Networking services
{: #cloud_services_locations_networking}

### VPC
{: #cloud_services_locations_networking_vpc}

| Service                                                       |`Frankfurt (eu-de)`  | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| Load Balancer for VPC   | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| VPN for VPC             | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| Client VPN for VPC      | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="VPC events in Europe locations" caption-side="top"}
{: #cs-vpc-loc-table-3}
{: tab-title="Europe"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                | `Dallas (us-south)`                                | `Washington (us-east)`               | `São-Paulo (br-sao)`                 | `Toronto (ca-tor)`                   |
|----------------------------------------|----------------------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| Load Balancer for VPC                  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |                                                 |                                                 |
| VPN for VPC                            | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| Client VPN for VPC                     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="VPC events in America's locations" caption-side="top"}
{: #cs-vpc-loc-table-1}
{: tab-title="America"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Osaka (jp-osa)`          |
|-----------------------------------------------------------------|------------------|----------------------------|----------------------------|
| Load Balancer for VPC           | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |                                                 |
| VPN for VPC                     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| Client VPN for VPC              | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
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
| {{site.data.keyword.dv_full_notm}}                        |    | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.Db2_on_Cloud_long_notm}}     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="Database services integration in Europe locations" caption-side="top"}
{: #cs-db-table-1}
{: tab-title="Europe"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}

| Service               | `Dallas (us-south)`             | `Washington (us-east)`                             | `São-Paulo (br-sao)`                       | `Toronto (ca-tor)`         |
|-----------------------|---------------------------------|----------------------------------------------------|--------------------------------------------|----------------------------|
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
| {{site.data.keyword.dv_full_notm}}                             | ![Checkmark icon](../images/checkmark-icon.svg)  |    |
| {{site.data.keyword.Db2_on_Cloud_long_notm}}     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="Database services integration in America's locations" caption-side="top"}
{: #cs-db-table-2}
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
| {{site.data.keyword.Db2_on_Cloud_long_notm}}     | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="Database services integration in AP locations" caption-side="top"}
{: #cs-db-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}



## Integration services
{: #cloud_services_locations_integration}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.messagehub}}             | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)|
| {{site.data.keyword.mq_full}}             | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg)|
{: caption="Integration services integration in Europe locations" caption-side="top"}
{: #cs-integration-table-1}
{: tab-title="Europe"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |
| {{site.data.keyword.mq_full}}               | ![Checkmark icon](../images/checkmark-icon.svg)   | ![Checkmark icon](../images/checkmark-icon.svg)    |
{: caption="Integration services integration in America's locations" caption-side="top"}
{: #cs-integration-table-2}
{: tab-title="America"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Chennai 01 (che01)` |
|------------------------------------------------|------------------|----------------------------|----------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |   `Metrics are available through the platform metrics monitoring instance in Tokyo` |
| {{site.data.keyword.mq_full}}               |  | ![Checkmark icon](../images/checkmark-icon.svg) |  |
{: caption="Integration services integration in AP locations" caption-side="top"}
{: #cs-integration-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}



## Security services
{: #cloud_services_locations_security}

| Service                                                         | `Dallas (us-south)`                               | `Washington (us-east)`                |
|-----------------------------------------------------------------|---------------------------------------------------|---------------------------------------|
| {{site.data.keyword.keymanagementservicelong}}                  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Security services integration in America's locations" caption-side="top"}
{: #cs-sec-table-1}
{: tab-title="America"}
{: tab-group="cs_sec"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)`                                   |`Sydney (au-syd)`           |
|-----------------------------------------------------------------|----------------------------------------------------|----------------------------|
| {{site.data.keyword.keymanagementservicelong}}                  | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} |      | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Security services integration in AP locations" caption-side="top"}
{: #cs-sec-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_sec"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                       |`Frankfurt (eu-de)`                                 | `London (eu-gb)` |
|---------------------------------------------------------------|----------------------------------------------------|------------------|
| {{site.data.keyword.keymanagementservicelong}}                | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg) |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} | ![Checkmark icon](../images/checkmark-icon.svg) |    |
{: caption="Security services integration in Europe locations" caption-side="top"}
{: #cs-sec-table-3}
{: tab-title="Europe"}
{: tab-group="cs_sec"}
{: class="simple-tab-table"}
{: row-headers}

## Storage services
{: #cloud_services_locations_storage}


| Service                                                       |`Frankfurt (eu-de)`                                | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------------------------------------|------------------|
| {{site.data.keyword.cos_full_notm}}                    | ![Checkmark icon](../images/checkmark-icon.svg) |  ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="Storage services integration in Europe locations" caption-side="top"}
{: #cs-storage-table-3}
{: tab-title="Europe"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)`                                | `Washington (us-east)`               |
|------------------------------------------------|----------------------------------------------------|--------------------------------------|
| {{site.data.keyword.cos_full_notm}}            | ![Checkmark icon](../images/checkmark-icon.svg)  | ![Checkmark icon](../images/checkmark-icon.svg)  |
{: caption="Storage services integration in America's locations" caption-side="top"}
{: #cs-storage-table-1}
{: tab-title="America"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                  | `Tokyo (jp-tok)`                                  |`Sydney (au-syd)`           |
|----------------------------------------------------------|---------------------------------------------------|----------------------------|
| {{site.data.keyword.cos_full_notm}}                      | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
{: caption="Storage services integration in AP locations" caption-side="top"}
{: #cs-storage-table-2}
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
