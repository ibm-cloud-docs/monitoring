---

copyright:
  years: 2018, 2020
lastupdated: "2020-03-14"

keywords: Sysdig, IBM Cloud, monitoring, platform metrics

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


# Cloud services by location
{: #cloud_services_locations}

List of locations where {{site.data.keyword.cloud_notm}} services are enabled to send metrics to {{site.data.keyword.mon_full_notm}}. You monitor these metrics through the Sysdig instance that is configured to receive platform metrics. [Learn more about enabling platform metrics](/docs/Monitoring-with-Sysdig?topic=Sysdig-enabling-platform-metrics).
{:shortdesc}




## Compute Cloud Foundry resources
{: #cloud_services_locations_platform_cfapps}

| Service                                                       | `Frankfurt (eu-de)` | `London (eu-gb)` |
|---------------------------------------------------------------|---------------------|------------------|
| Cloud Foundry                                                 | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg)  |          
{: caption="CF integration in Europe locations" caption-side="top"}
{: #cs_cf-table-1}
{: tab-title="Europe"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| Cloud Foundry                                  | `NO`   | ![Checkmark icon](../../icons/checkmark-icon.svg)    |          
{: caption="CF integration in America's locations" caption-side="top"}
{: #cs_cf-table-2}
{: tab-title="America"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Seoul 01 (seo01)` | `Chennai 01 (che01)` |
|------------------------------------------------|------------------|----------------------------|--------------------|----------------------|
| Cloud Foundry                                  | `NO`           | ![Checkmark icon](../../icons/checkmark-icon.svg) | `NO` | `NO`  |       
{: caption="CF integration in AP locations" caption-side="top"}
{: #cs_cf-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_cf"}
{: class="simple-tab-table"}
{: row-headers}


## Platform database services
{: #cloud_services_locations_database}

 us-south, us-east, eu-gb, jp-tok, au-syd

| Service                                                         | `Frankfurt (eu-de)`                                | `London (eu-gb)`                                   |
|-----------------------------------------------------------------|----------------------------------------------------|----------------------------------------------------|
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
{: caption="Database services integration in Europe locations" caption-side="top"}
{: #cs_db-table-1}
{: tab-title="Europe"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Dallas (us-south)`                                | `Washington (us-east)`                             |
|-----------------------------------------------------------------|----------------------------------------------------|----------------------------------------------------|
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](../../icons/checkmark-icon.svg)` | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  |
{: caption="Database services integration in America's locations" caption-side="top"}
{: #cs_db-table-2}
{: tab-title="America"}
{: tab-group="cs_db"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                                         | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Seoul 01 (seo01)` | `Chennai 01 (che01)` |
|-----------------------------------------------------------------|------------------|----------------------------|--------------------|----------------------|
| {{site.data.keyword.databases-for-elasticsearch_full_notm}}     | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  | `NO`  | `NO`  |
| {{site.data.keyword.databases-for-etcd_full_notm}}              | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  | `NO`  | `NO`  |
| {{site.data.keyword.databases-for-mongodb_full_notm}}           | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  | `NO`  | `NO`  |
| {{site.data.keyword.databases-for-postgresql_full_notm}}        | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  | `NO`  | `NO`  |
| {{site.data.keyword.messages-for-rabbitmq_full_notm}}           | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  | `NO`  | `NO`  |
| {{site.data.keyword.databases-for-redis_full_notm}}             | ![Checkmark icon](../../icons/checkmark-icon.svg)  | ![Checkmark icon](../../icons/checkmark-icon.svg)  | `NO`  | `NO`  |
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
| {{site.data.keyword.messagehub}}                              | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg)  |          
{: caption="Integration services integration in Europe locations" caption-side="top"}
{: #cs_integration-table-1}
{: tab-title="Europe"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Dallas (us-south)` | `Washington (us-east)`             |
|------------------------------------------------|---------------------|------------------------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](../../icons/checkmark-icon.svg)   | ![Checkmark icon](../../icons/checkmark-icon.svg)    |          
{: caption="Integration services integration in America's locations" caption-side="top"}
{: #cs_integration-table-2}
{: tab-title="America"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}

| Service                                        | `Tokyo (jp-tok)` | `Sydney (au-syd)`          | `Seoul 01 (seo01)` | `Chennai 01 (che01)` |
|------------------------------------------------|------------------|----------------------------|--------------------|----------------------|
| {{site.data.keyword.messagehub}}               | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |  `Metrics are available through the platform metrics Sysdig instance in Tokyo` | `Metrics are available through the platform metrics Sysdig instance in Tokyo` |       
{: caption="Integration services integration in AP locations" caption-side="top"}
{: #cs_integration-table-3}
{: tab-title="Asia Pacific"}
{: tab-group="cs_integration"}
{: class="simple-tab-table"}
{: row-headers}


