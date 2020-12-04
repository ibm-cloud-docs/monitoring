---

copyright:
  years: 2018, 2020
lastupdated: "2020-11-26"

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


# Cloud services
{: #cloud_services}

List of {{site.data.keyword.cloud}} services that send metrics to {{site.data.keyword.mon_full_notm}}. You monitor these metrics through the Sysdig instance that is configured to receive platform metrics. [Learn more about enabling platform metrics](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-platform_metrics_enabling).
{:shortdesc}


## Cloud Foundry
{: #platform_cfapps}

The following table lists CF resources that are Sysdig-enabled:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [Cloud Foundry (CF)](/docs/cloud-foundry-public?topic=cloud-foundry-public-getting-started) | CF is the premier industry standard Platform-as-a-Service (PaaS), that ensures the fastest, easiest, and most reliable deployment of cloud-native applications.  | [Metrics collected by CF](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-monitor-cf-sysdig)|
{: caption="List of CF resources" caption-side="top"} 


## Compute services
{: #compute}

For more information, see [Compute services](/docs/cloud-infrastructure?topic=cloud-infrastructure-compute).

### Serverless
{: #compute_serverless}

The following table lists container services that are Sysdig-enabled:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.openwhisk}}](/docs/openwhisk?topic=openwhisk-getting-started) | A Functions-as-a-Service (FaaS) programming platform based on Apache OpenWhisk. | [Monitoring metrics for {{site.data.keyword.openwhisk}}](/docs/openwhisk?topic=openwhisk-monitor-sysdig)|
{: caption="List of {{site.data.keyword.cloud_notm}} serverless services" caption-side="top"} 

### VPC
{: #compute_vpc}

With {{site.data.keyword.vpc_full}} (VPC), you can provision a VPC in the {{site.data.keyword.cloud_notm}} to run an isolated environment within the public cloud. VPC gives you the security of a private cloud, with the agility and ease of a public cloud. The VPC infrastructure contains a number of Infrastructure-as-a-Service (IaaS) offerings, including Virtual Servers for VPC. [Learn more](/docs/vpc?topic=vpc-getting-started).

The following table lists VPC infrastructure services that are Sysdig-enabled:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [VPC virtual server instances](/docs/vpc?topic=vpc-about-advanced-virtual-servers) | Virtual servers for VPC is an Infrastructure-as-a-Service (IaaS) offering that you can use to quickly provision instances with high network performance. | [Metrics collected by {{site.data.keyword.BluVirtServers}}](/docs/cloud-infrastructure?topic=cloud-infrastructure-vpc-sysdig-metrics)|
{: caption="List of VPC infrastructure services (generation 2)" caption-side="top"} 


### Classic
{: #compute_classic}

The following table lists infrastructure services that are Sysdig-enabled:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.BluVirtServers}}](/docs/virtual-servers?topic=virtual-servers-getting-started-tutorial) | Scalable virtual servers that are purchased with cores and memory allocations. | [Metrics collected by {{site.data.keyword.BluVirtServers}}](/docs/cloud-infrastructure?topic=cloud-infrastructure-classic-sysdig-metrics)|
{: caption="List of VPC classic infrastructure services (generation 1)" caption-side="top"} 

## Container services
{: #container}

The following table lists container services that are Sysdig-enabled:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started) | {{site.data.keyword.registrylong}} provides a multi-tenant, highly available, scalable, and encrypted private image registry that is hosted and managed by {{site.data.keyword.IBM}}. | [Monitoring metrics for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_monitor_sysdig)|
{: caption="List of {{site.data.keyword.cloud_notm}} container services" caption-side="top"} 


## Developer tools
{: #devops}

The following table lists developer tools and DevOps services that are Sysdig-enabled:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.contdelivery_full}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started)| With {{site.data.keyword.contdelivery_short}}, you can build, test, and deliver applications by using DevOps practices and industry-leading tools. | [Metrics collected by {{site.data.keyword.contdelivery_short}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd-monitor-sysdig) |
{: caption="List of developer tools and DevOps services" caption-side="top"} 


## Networking services
{: #networking}

For more information, see [Networking services](/docs/cloud-infrastructure?topic=cloud-infrastructure-network).


### VPC
{: #networking_vpc}

The following table lists VPC infrastructure services that are Sysdig-enabled:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [Load Balancer for VPC](/docs/vpc?topic=vpc-network-load-balancers)| Distributes traffic among multiple server instances within the same region of your VPC.  | [Monitoring metrics using IBM Load Balancer for VPC with Sysdig](/docs/vpc?topic=vpc-nlb_monitoring-metrics-sysdig) |
| [VPN for VPC](/docs/vpc?topic=vpc-using-vpn)| Securely connect your VPC to another private network. You can use VPN to set up an IPsec site-to-site tunnel between your VPC and your on-premises private network or another VPC. | [Monitoring VPC VPN metrics](/docs/vpc?topic=vpc-sysdig-monitoring-metrics) |
{: caption="List of VPC services (generation 2)" caption-side="top"} 


### Classic
{: #networking_classic}

The following table lists infrastructure services that are Sysdig-enabled:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.loadbalancer_full}}](/docs/loadbalancer-service?topic=loadbalancer-service-getting-started) | Distributes processing and communications evenly across multiple servers within a data center so that a single device does not carry an entire load. | [Metrics collected by {{site.data.keyword.loadbalancer_full}}](/docs/loadbalancer-service?topic=loadbalancer-service-monitoring-metrics) |
| [{{site.data.keyword.cloud}} Load Balancer for VPC](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-load-balancers-in-ibm-cloud-vpc)| Use this service to distribute traffic among multiple server instances within the same region of your VPC.  | [Monitoring metrics using IBM Load Balancer for VPC with Sysdig](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-monitoring-metrics-sysdig) |
| [{{site.data.keyword.cloud}} VPN for VPC](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-vpn-with-your-vpc)| Use this service to connect private networks in a secure fashion. You can use VPN to set up an IPsec site-to-site tunnel between your VPC and your on-premise private network or another VPC. | [VPN for VPC](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-sysdig-monitoring-metrics) |
{: caption="List of VPC classic services (generation 1)" caption-side="top"} 


## Database services
{: #database}

The following table lists database services that are Sysdig-enabled:

| Service           | Description    | Metrics |
|-------------------|----------------|---------|
| [{{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant)    | {{site.data.keyword.cloudant_short_notm}} is a document-oriented database as a service (DBaaS). It stores data as documents in JSON format. | [Metrics that are generated by {{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-monitor-sysdig-pm) |
| [{{site.data.keyword.databases-for-postgresql_full_notm}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started) | {{site.data.keyword.databases-for-postgresql_full_notm}} is a managed PostgreSQL service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.  | [Metrics that are generated by {{site.data.keyword.databases-for-postgresql_full_notm}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-sysdig-monitoring) |
| [{{site.data.keyword.databases-for-redis_full_notm}}](/docs/databases-for-redis?topic=databases-for-redis-getting-started) | {{site.data.keyword.databases-for-redis_full_notm}} is a managed service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.  | [Metrics that are generated by {{site.data.keyword.databases-for-redis_full_notm}} ](/docs/databases-for-redis?topic=databases-for-redis-sysdig-monitoring) |
| [{{site.data.keyword.databases-for-etcd_full_notm}}](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started) | {{site.data.keyword.databases-for-etcd_full_notm}} is a managed etcd service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics that are generated by {{site.data.keyword.databases-for-etcd_full_notm}}](/docs/databases-for-etcd?topic=databases-for-etcd-sysdig-monitoring) |
| [{{site.data.keyword.databases-for-elasticsearch_full_notm}}](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-getting-started) | {{site.data.keyword.databases-for-elasticsearch_full_notm}} is a managed Elasticsearch service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics that are generated by {{site.data.keyword.databases-for-elasticsearch_full_notm}}](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-sysdig-monitoring) |
| [{{site.data.keyword.databases-for-mongodb_full_notm}}](/docs/databases-for-mongodb?topic=databases-for-mongodb-getting-started) | {{site.data.keyword.databases-for-mongodb_full_notm}} is a managed MongoDB service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics that are generated by {{site.data.keyword.databases-for-mongodb_full_notm}}](/docs/databases-for-mongodb?topic=databases-for-mongodb-sysdig-monitoring) |
| [{{site.data.keyword.messages-for-rabbitmq_full_notm}}](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started)  | {{site.data.keyword.messages-for-rabbitmq_full_notm}} is a managed RabbitMQ service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.   | [Metrics that are generated by {{site.data.keyword.messages-for-rabbitmq_full_notm}}](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-sysdig-monitoring) |
| [{{site.data.keyword.sqlquery_full}}](/docs/services/sql-query?topic=sql-query-gettingstarted)| {{site.data.keyword.sqlquery_full}} is a fully-managed service that lets you run SQL queries (that is, SELECT statements) to analyze, transform, or clean up rectangular data. | [Metrics that are generated by {{site.data.keyword.sqlquery_full}}](/docs/services/sql-query?topic=sql-query-metrics) |
| [{{site.data.keyword.ihsdbaas_mongodb_full}}](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-gettingstarted) | {{site.data.keyword.ihsdbaas_mongodb_full}} is a highly secure MongoDB service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics that are generated by {{site.data.keyword.ihsdbaas_mongodb_full}}](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-monitor) |
| [{{site.data.keyword.ihsdbaas_postgresql_full}}](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-gettingstarted) | {{site.data.keyword.ihsdbaas_postgresql_full}} is a highly secure PostgreSQL service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics that are generated by {{site.data.keyword.ihsdbaas_postgresql_full}}](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-monitor) |
{: caption="List of database services" caption-side="top"} 




## Integration services
{: #integration}

The following table lists integration services that are Sysdig-enabled:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-getting_started)| {{site.data.keyword.messagehub}} is a high-throughput message bus that is built with Apache Kafka. It is optimized for event ingestion into {{site.data.keyword.IBM_notm}} and event stream distribution between your services and applications. | [Metrics collected by {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-metrics) |
| [{{site.data.keyword.mobilepushshort}}](/docs/mobilepush?topic=mobilepush-getting-started)| {{site.data.keyword.mobilepushshort}} is available as an IBM Cloud catalog service in the **Mobile** category and helps you to send and manage mobile and web push notifications. A push notification is an alert to indicate a change or update on a mobile device or browser.| [Metrics collected by {{site.data.keyword.mobilepushshort}}](/docs/mobilepush?topic=mobilepush-push_sysdig#pn_metrics_details) |
{: caption="List of integration Cloud services" caption-side="top"} 


## Platform
{: #platform}

The following table lists integration services that are Sysdig-enabled:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started) | {{site.data.keyword.bplong_notm}} delivers Terraform-as-a-Service so that you can use a high-level scripting language to model the resources that you want in your {{site.data.keyword.cloud_notm}} environment, and enable Infrastructure as Code (IaC).  |  |
{: caption="List of platform services" caption-side="top"} 


## Storage services
{: #storage}

For more information, see [Storage services](/docs/cloud-infrastructure?topic=cloud-infrastructure-compute).


### VPC
{: #storage_vpc}

The following table lists VPC infrastructure services that are Sysdig-enabled:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.cos_full}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage)| You can use {{site.data.keyword.cos_full_notm}} to store unstructured data in the {{site.data.keyword.cloud_notm}}.  | [Metrics that are collected by {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration&programming_language=Console) |
{: caption="List of VPC services (generation 2)" caption-side="top"} 

## AI / Machine Learning
{: #ai_machine_learning}

The following table lists AI / Machine Learning services that are Sysdig-enabled:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.wh-acd_short}}](/docs/wh-acd)| You can use {{site.data.keyword.wh-acd_short}} to analyze text and extract medical codes and concepts. | [Metrics that are collected by {{site.data.keyword.wh-acd_short}}](/docs/wh-acd?topic=wh-acd-monitor-sysdig-pm#metrics-available-by-service-plan) |
{: caption="List of AI / Machine Learning services" caption-side="top"}
