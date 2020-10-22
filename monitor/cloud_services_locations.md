---

copyright:
  years: 2018, 2020
lastupdated: "2020-10-22"

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



## Compute infrastructure services
{: #cloud_services_locations_infrastructure}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.BluVirtServers}}                          | `NO`                | ![Checkmark icon](images/checkmark-icon.svg)  |          
{: caption="Infrastructure services integration in Europe locations" caption-side="top"}
{: #cs_infra-table-1}
{: tab-title="Europe"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.BluVirtServers}}           | ![Checkmark icon](images/checkmark-icon.svg)   | ![Checkmark icon](images/checkmark-icon.svg)    |          
{: caption="Infrastructure services integration in America's locations" caption-side="top"}
{: #cs_infra-table-2}
{: tab-title="America"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | 
|------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.BluVirtServers}}           | `NO` | `NO` |     
{: caption="Infrastructure services integration in AP locations" caption-side="top"}
{: #cs_infra-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_infra"}
{: class="simple-tab-table"}
{: row-headers}


## Compute Cloud Foundry resources
{: #cloud_services_locations_platform_cfapps}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| Cloud Foundry                                                 | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg)  |          
{: caption="CF integration in Europe locations" caption-side="top"}
{: #cs_cf-table-1}
{: tab-title="Europe"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| Cloud Foundry                                  | ![Checkmark icon](images/checkmark-icon.svg)   | ![Checkmark icon](images/checkmark-icon.svg)    |          
{: caption="CF integration in America's locations" caption-side="top"}
{: #cs_cf-table-2}
{: tab-title="America"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| Cloud Foundry                                  |                  | ![Checkmark icon](images/checkmark-icon.svg) |      
{: caption="CF integration in AP locations" caption-side="top"}
{: #cs_cf-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

## Container services
{: #cloud_services_locations_container}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.registrylong_notm}}          | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg)  |          
{: caption="Containers integration in Europe locations" caption-side="top"}
{: #cs_cont-table-1}
{: tab-title="Europe"}
{: tab-group="cs_cont"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.registrylong_notm}}        | ![Checkmark icon](images/checkmark-icon.svg)   | ![Checkmark icon](images/checkmark-icon.svg) `[*]` |          
{: caption="Containers integration in America's locations" caption-side="top"}
{: #cs_cont-table-2}
{: tab-title="America"}
{: tab-group="cs_cont"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.registrylong_notm}}        | ![Checkmark icon](images/checkmark-icon.svg)   | ![Checkmark icon](images/checkmark-icon.svg) |      
{: caption="Containers integration in AP locations" caption-side="top"}
{: #cs_cont-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_cont"}
{: class="simple-tab-table"}
{: row-headers}

`[*]` {{site.data.keyword.registrylong_notm}} global registry metrics are available through the Sysdig Washington (us-east) instance.


## Platform database services
{: #cloud_services_locations_database}


| Service                                                         | `Frankfurt (eu-de)`                                | `London (eu-gb)`                                   |
|-----------------------------------------------------------------|----------------------------------------------------|----------------------------------------------------|
| {{site.data.keyword.cloudant_short_notm}}                        | `NO`  | ![Checkmark icon](images/checkmark-icon.svg) |
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.sqlquery_full}}                             | ![Checkmark icon](images/checkmark-icon.svg)  | `NO`  |
{: caption="Database services integration in Europe locations" caption-side="top"}
{: #cs_db-table-1}
{: tab-title="Europe"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Dallas (us-south)`                                | `Washington (us-east)`                             |
|-----------------------------------------------------------------|----------------------------------------------------|----------------------------------------------------|
| {{site.data.keyword.cloudant_short_notm}}                       | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](images/checkmark-icon.svg)` | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.sqlquery_full}}                             | ![Checkmark icon](images/checkmark-icon.svg)  | `NO`  |
{: caption="Database services integration in America's locations" caption-side="top"}
{: #cs_db-table-2}
{: tab-title="America"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` | `Sydney (au-syd)`          |
|-----------------------------------------------------------------|------------------|----------------------------|
| {{site.data.keyword.cloudant_short_notm}}                        | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) | 
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  | 
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |
| {{site.data.keyword.sqlquery_full}}                             | `NO`  | `NO`  |
{: caption="Database services integration in AP locations" caption-side="top"}
{: #cs_db-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}



## Platform integration services
{: #cloud_services_locations_integration}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| {{site.data.keyword.messagehub}}                              | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |          
{: caption="Integration services integration in Europe locations" caption-side="top"}
{: #cs_integration-table-1}
{: tab-title="Europe"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](images/checkmark-icon.svg)   | ![Checkmark icon](images/checkmark-icon.svg)    |          
{: caption="Integration services integration in America's locations" caption-side="top"}
{: #cs_integration-table-2}
{: tab-title="America"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Seoul 01 (seo01)` | `Chennai 01 (che01)` |
|------------------------------------------------|------------------|----------------------------|--------------------|----------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |  `Metrics are available through the platform metrics Sysdig instance in Tokyo` | `Metrics are available through the platform metrics Sysdig instance in Tokyo` |       
{: caption="Integration services integration in AP locations" caption-side="top"}
{: #cs_integration-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}




## Networking services
{: #cs_locations_networking}

| Service                                                         | `Dallas (us-south)` | `Washington (us-east)`                   |
|-----------------------------------------------------------------|---------------------|--------------------------------------|
| {{site.data.keyword.loadbalancer_full}}                 | ![Checkmark icon](images/checkmark-icon.svg)               | `NO`                                 |            
{: caption="Table 10. Security services integration in America's locations" caption-side="top"}
{: #cs-int-table-1}
{: tab-title="America"}
{: tab-group="cs_int"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` |`Sydney (au-syd)`           |
|-----------------------------------------------------------------|----------------|---------------------------|
| {{site.data.keyword.loadbalancer_full}}                   | `NO`    | `NO`  |
{: caption="Table 11. Security services integration in AP locations" caption-side="top"}
{: #cs-int-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_int"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                       |`Frankfurt (eu-de)`  | `London (eu-gb)` |
|---------------------------------------------------------------|-------------------|----------------|
| {{site.data.keyword.loadbalancer_full}}                |  `NO`              | `NO`  |
{: caption="Table 12. Security services  integration in Europe locations" caption-side="top"}
{: #cs-int-table-3}
{: tab-title="Europe"}
{: tab-group="cs_int"}
{: class="simple-tab-table"}
{: row-headers}


## Platform storage services
{: #cloud_services_locations_storage}

| Service                                        | `Dallas (us-south)`                                | `Washington (us-east)`               |
|------------------------------------------------|----------------------------------------------------|--------------------------------------|
| {{site.data.keyword.cos_full_notm}}            | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg)  |          
{: caption="Storage services integration in America's locations" caption-side="top"}
{: #cs_storage-table-1}
{: tab-title="America"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                  | `Tokyo (jp-tok)`                                  |`Sydney (au-syd)`           |
|----------------------------------------------------------|---------------------------------------------------|----------------------------|
| {{site.data.keyword.cos_full_notm}}                      | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |     
{: caption="Storage services integration in AP locations" caption-side="top"}
{: #cs_storage-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                       |`Frankfurt (eu-de)`                                | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------------------------------------|------------------|
| {{site.data.keyword.cos_full_notm}}                           | ![Checkmark icon](images/checkmark-icon.svg) |  ![Checkmark icon](images/checkmark-icon.svg)  |     
{: caption="Storage services integration in Europe locations" caption-side="top"}
{: #cs_storage-table-3}
{: tab-title="Europe"}
{: tab-group="cs_storage"}
{: class="simple-tab-table"}
{: row-headers}



## VPC infrastructure services
{: #cloud_services_locations_vpc_infrastructure}

### VPC Gen 1 (Classic)
{: #cloud_services_locations_vpc_infrastructure_gen1}

| Service                                | `Dallas (us-south)`                                | `Washington (us-east)`               |
|----------------------------------------|----------------------------------------------------|--------------------------------------|
| Load Balancer                          | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) |
| VPN                                    | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) |
{: caption="VPC events in America's locations" caption-side="top"}
{: #cs-vpc-loc-table-1}
{: tab-title="America"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` |`Sydney (au-syd)`           |
|-----------------------------------------------------------------|------------------|----------------------------|
| Load Balancer           | `NO`   | `NO`  |
| VPN                     | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) |
{: caption="VPC events in AP locations" caption-side="top"}
{: #cs-vpc-loc-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                       |`Frankfurt (eu-de)`  | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| Load Balancer              | `NO`  | `NO`  |
| VPN                        |  ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) |    
{: caption="VPC events in Europe locations" caption-side="top"}
{: #cs-vpc-loc-table-3}
{: tab-title="Europe"}
{: tab-group="cs_vpc"}
{: class="simple-tab-table"}
{: row-headers}






