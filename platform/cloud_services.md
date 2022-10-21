---

copyright:
  years:  2018, 2022
lastupdated: "2022-10-20"

keywords: IBM Cloud, monitoring, platform metrics

subcollection: monitoring


---

{{site.data.keyword.attribute-definition-list}}


# Services generating metrics
{: #cloud_services}

List of {{site.data.keyword.cloud}} services that send metrics to {{site.data.keyword.mon_full_notm}}. You monitor these metrics through the monitoring instance that is configured to receive platform metrics. [Learn more about enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).
{: shortdesc}


## Cloud Foundry
{: #platform_cfapps}

The following table lists Cloud Foundry resources that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [Cloud Foundry](/docs/cloud-foundry-public?topic=cloud-foundry-public-getting-started) | Cloud Foundry is the premier industry standard Platform-as-a-Service (PaaS), that ensures the fastest, easiest, and most reliable deployment of cloud-native applications.  | [Metrics](/docs/monitoring?topic=monitoring-monitor-cf-sysdig)|
{: caption="List of Cloud Foundry resources" caption-side="top"} 


## Compute services
{: #compute}

For more information, see [Compute services](/docs/cloud-infrastructure?topic=cloud-infrastructure-compute).

### Serverless
{: #compute_serverless}

The following table lists container services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.codeenginefull_notm}}](/docs/codeengine?topic=codeengine-getting-started) | {{site.data.keyword.codeengineshort}} is a fully managed, serverless platform that runs your containerized workloads. | [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor)|
| [{{site.data.keyword.openwhisk}}](/docs/openwhisk?topic=openwhisk-getting-started) | A Functions-as-a-Service (FaaS) programming platform based on Apache OpenWhisk. | [Metrics](/docs/openwhisk?topic=openwhisk-monitor-functions)|
{: caption="List of {{site.data.keyword.cloud_notm}} serverless services" caption-side="top"} 

### VPC
{: #compute_vpc}

With {{site.data.keyword.vpc_full}} (VPC), you can provision a VPC in the {{site.data.keyword.cloud_notm}} to run an isolated environment within the public cloud. VPC gives you the security of a private cloud, with the agility and ease of a public cloud. The VPC infrastructure contains a number of Infrastructure-as-a-Service (IaaS) offerings, including Virtual Servers for VPC. [Learn more](/docs/vpc?topic=vpc-getting-started).

The following table lists VPC infrastructure services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [Virtual Servers for VPC](/docs/vpc?topic=vpc-about-advanced-virtual-servers) | Virtual Servers for VPC is an Infrastructure-as-a-Service (IaaS) offering that you can use to quickly provision instances with high network performance. | [Metrics](/docs/vpc?topic=vpc-vpc-quota-metrics)|
{: caption="List of VPC infrastructure services (generation 2)" caption-side="top"} 


### Classic
{: #compute_classic}

The following table lists infrastructure services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.BluVirtServers}}](/docs/virtual-servers?topic=virtual-servers-getting-started-tutorial) | Scalable virtual servers that are purchased with cores and memory allocations. | [Metrics](/docs/virtual-servers?topic=cloud-infrastructure-monitoring-iaas)|
{: caption="List of VPC classic infrastructure services (generation 1)" caption-side="top"} 

## Container services
{: #container}

The following table lists container services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started) | {{site.data.keyword.registrylong}} provides a multi-tenant, highly available, scalable, and encrypted private image registry that is hosted and managed by {{site.data.keyword.IBM}}. | [Metrics](/docs/Registry?topic=Registry-registry_monitor)|
| [{{site.data.keyword.containerlong}}](/docs/containers?topic=containers-getting-started) | You can use the {{site.data.keyword.containerlong_notm}} service to deploy highly available apps in Docker containers that run in Kubernetes clusters. | [Metrics](/docs/containers?topic=containers-health-monitor#monitoring) | 
| [{{site.data.keyword.openshiftlong}}](/docs/openshift?topic=openshift-getting-started) | With {{site.data.keyword.openshiftlong_notm}}, you can deploy apps on highly available clusters that come installed with the Red Hat OpenShift on IBM Cloud Container Platform software installed on Red Hat Enterprise Linux. | [Metrics](/docs/openshift?topic=openshift-health-monitor#openshift_monitoring) |
| [{{site.data.keyword.satellitelong}}](/docs/satellite?topic=satellite-getting-started) | With {{site.data.keyword.satellitelong_notm}}, you can bring your own compute infrastructure to run {{site.data.keyword.cloud_notm}} services and consistently deploy, manage, and control your app workloads. | [Metrics](/docs/satellite?topic=satellite-monitor) |
{: caption="List of {{site.data.keyword.cloud_notm}} container services" caption-side="top"} 


## Developer tools
{: #devops}

The following table lists developer tools and DevOps services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.contdelivery_full}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started)| With {{site.data.keyword.contdelivery_short}}, you can build, test, and deliver applications by using DevOps practices and industry-leading tools. | [Metrics](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd-monitor-sysdig) |
| [{{site.data.keyword.appconfig_full}}](/docs/app-configuration?topic=app-configuration-getting-started)| Instrument your applications with {{site.data.keyword.appconfig_short}} SDKs, and use the {{site.data.keyword.appconfig_short}} dashboard or {{site.data.keyword.appconfig_short}} administrator API to define features flags or properties. | [Metrics](/docs/app-configuration?topic=app-configuration-ac-monitoring) |
| [{{site.data.keyword.en_full}}](/docs/event-notifications?topic=event-notifications-getting-started)|  A centralized alerts management service that notifies and alerts you to events occurring in your {{site.data.keyword.Bluemix_notm}} account.| [Metrics](/docs/event-notifications?topic=event-notifications-en-monitoring) |
{: caption="List of developer tools and DevOps services" caption-side="top"} 

## Networking services
{: #networking}

For more information, see [Networking services](/docs/cloud-infrastructure?topic=cloud-infrastructure-network).


### VPC
{: #networking_vpc}

The following table lists VPC infrastructure services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [Load Balancer for VPC](/docs/vpc?topic=vpc-network-load-balancers)| Distributes traffic among multiple server instances within the same region of your VPC.  | [Metrics](/docs/vpc?topic=vpc-ibm-cloud-vpc-monitoring-dashboards) |
| [VPN for VPC](/docs/vpc?topic=vpc-using-vpn)| Securely connect your VPC to another private network. You can use VPN to set up an IPsec site-to-site tunnel between your VPC and your on-premises private network or another VPC. | [Metrics](/docs/vpc?topic=vpc-vpn-monitoring-metrics) |
{: caption="List of VPC services (generation 2)" caption-side="top"} 


### Classic
{: #networking_classic}

The following table lists infrastructure services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.cloud}} Load Balancer for VPC](/docs/vpc?topic=vpc-nlb-vs-elb)| Use this service to distribute traffic among multiple server instances within the same region of your VPC.  | [Metrics](/docs/vpc?topic=vpc-ibm-cloud-vpc-monitoring-dashboards) |
{: caption="List of VPC services (classic)" caption-side="top"} 

## Database services
{: #database}

The following table lists database services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service           | Description    | Metrics |
|-------------------|----------------|---------|
| [{{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant)    | {{site.data.keyword.cloudant_short_notm}} is a document-oriented database as a service (DBaaS). It stores data as documents in JSON format. | [Metrics](/docs/Cloudant?topic=Cloudant-monitor-ibm-cloud-pm) |
| [{{site.data.keyword.databases-for-postgresql_full_notm}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started) | {{site.data.keyword.databases-for-postgresql_full_notm}} is a managed PostgreSQL service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.  | [Metrics](/docs/databases-for-postgresql?topic=databases-for-postgresql-monitoring) |
| [{{site.data.keyword.databases-for-redis_full_notm}}](/docs/databases-for-redis?topic=databases-for-redis-getting-started) | {{site.data.keyword.databases-for-redis_full_notm}} is a managed service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.  | [Metrics](/docs/databases-for-redis?topic=databases-for-redis-monitoring) |
| [{{site.data.keyword.databases-for-etcd_full_notm}}](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started) | {{site.data.keyword.databases-for-etcd_full_notm}} is a managed etcd service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics](/docs/databases-for-etcd?topic=databases-for-etcd-monitoring) |
| [{{site.data.keyword.databases-for-elasticsearch_full_notm}}](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-getting-started) | {{site.data.keyword.databases-for-elasticsearch_full_notm}} is a managed Elasticsearch service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-monitoring) |
| [{{site.data.keyword.databases-for-mongodb_full_notm}}](/docs/databases-for-mongodb?topic=databases-for-mongodb-getting-started) | {{site.data.keyword.databases-for-mongodb_full_notm}} is a managed MongoDB service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics](/docs/databases-for-mongodb?topic=databases-for-mongodb-monitoring) |
| [{{site.data.keyword.messages-for-rabbitmq_full_notm}}](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started)  | {{site.data.keyword.messages-for-rabbitmq_full_notm}} is a managed RabbitMQ service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.   | [Metrics](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-monitoring) |
| [{{site.data.keyword.sqlquery_full}}](/docs/services/sql-query?topic=sql-query-gettingstarted)| {{site.data.keyword.sqlquery_full}} is a fully-managed service that lets you run SQL queries (that is, SELECT statements) to analyze, transform, or clean up rectangular data. | [Metrics](/docs/services/sql-query?topic=sql-query-metrics) |
| [{{site.data.keyword.ihsdbaas_mongodb_full}}](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-gettingstarted) | {{site.data.keyword.ihsdbaas_mongodb_full}} is a highly secure MongoDB service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-monitor) |
| [{{site.data.keyword.ihsdbaas_postgresql_full}}](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-gettingstarted) | {{site.data.keyword.ihsdbaas_postgresql_full}} is a highly secure PostgreSQL service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Metrics](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-monitor) |
| [{{site.data.keyword.dv_full}}](/docs/data-virtualization?topic=data-virtualization-getting-started) | {{site.data.keyword.dv_full}} is a fully managed service on {{site.data.keyword.cloud_notm}} that you can use to easily and securely access data across many data sources. | [Metrics](/docs/data-virtualization?topic=data-virtualization-monitor) |
| [{{site.data.keyword.Db2_on_Cloud_long}}](/docs/Db2onCloud?topic=Db2onCloud-about) | {{site.data.keyword.Db2_on_Cloud_long_notm}} is a fully managed public cloud service on IBM Cloud. As a relational database, it delivers fast query processing with enterprise-level performance and capabilities for online transactional processing (OLTP). | [Metrics](/docs/Db2onCloud?topic=Db2onCloud-monitor) |
{: caption="List of database services" caption-side="top"} 




## Integration services
{: #integration}

The following table lists integration services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-getting_started)| {{site.data.keyword.messagehub}} is a high-throughput message bus that is built with Apache Kafka. It is optimized for event ingestion into {{site.data.keyword.IBM_notm}} and event stream distribution between your services and applications. | [Metrics](/docs/EventStreams?topic=EventStreams-metrics) |
{: caption="List of integration Cloud services" caption-side="top"} 

## Security services
{: #security}

The following table lists Cloud services that are enabled for {{site.data.keyword.mon_full_notm}}:


| Service     | Description | More info |
|-------------|-------------|-------------------------------------------------------------------------|
| [{{site.data.keyword.keymanagementservicelong}}](/docs/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) | You can use the {{site.data.keyword.keymanagementserviceshort}} service to provision encrypted keys for apps across the {{site.data.keyword.cloud_notm}}. | [Metrics](/docs/key-protect?topic=key-protect-operational-metrics) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started) | You can use the {{site.data.keyword.hscrypto}} to control your cloud data encryption keys in cloud hardware security modules for apps across the {{site.data.keyword.cloud_notm}}. | [Metrics](/docs/hs-crypto?topic=hs-crypto-operational-metrics) |
{: caption="List of security Cloud services" caption-side="top"} 

## Platform
{: #platform}

The following table lists integration services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics | 
|-------------|-------------|-------------------|
| [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started) | {{site.data.keyword.bplong_notm}} delivers Terraform-as-a-Service so that you can use a high-level scripting language to model the resources that you want in your {{site.data.keyword.cloud_notm}} environment, and enable Infrastructure as Code (IaC).  | [Metrics](/docs/schematics?topic=schematics-monitoring-instances) |
{: caption="List of platform services" caption-side="top"} 


## Storage services
{: #storage}

The following table lists Cloud services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.cos_full}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage)| You can use {{site.data.keyword.cos_full_notm}} to store unstructured data in the {{site.data.keyword.cloud_notm}}.  | [Metrics](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration&programming_language=Console) |
{: caption="List of VPC services (generation 2)" caption-side="top"} 


