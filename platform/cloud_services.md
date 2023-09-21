---

copyright:
  years:  2018, 2023

lastupdated: "2023-08-04"

keywords:

subcollection: monitoring


---

{{site.data.keyword.attribute-definition-list}}


# Services generating metrics
{: #cloud_services}

List of {{site.data.keyword.cloud}} services that send metrics to {{site.data.keyword.mon_full_notm}}.
{: shortdesc}


There are 2 ways that services send metrics:
- As platform metrics

    You monitor these metrics through the monitoring instance that is configured to receive platform metrics. [Learn more about enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).

- By configuring a {{site.data.keyword.mon_short}} agent

    You configure the agent to send metrics to the {{site.data.keyword.mon_short}} instance that you choose. You monitor these metrics through that instance.


## Classic
{: #compute_classic}

The following table lists infrastructure services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.BluVirtServers}}](/docs/virtual-servers?topic=virtual-servers-getting-started-tutorial) | Scalable virtual servers that are purchased with cores and memory allocations. | [Platform metrics](/docs/virtual-servers?topic=cloud-infrastructure-monitoring-iaas)|
{: caption="Table 1. List of classic infrastructure services (generation 1)" caption-side="top"}



## Container services
{: #container}

The following table lists container services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started) | {{site.data.keyword.registrylong}} provides a multi-tenant, highly available, scalable, and encrypted private image registry that is hosted and managed by {{site.data.keyword.IBM}}. | [Platform metrics](/docs/Registry?topic=Registry-registry_monitor)|
| [{{site.data.keyword.containerlong}}](/docs/containers?topic=containers-getting-started) | You can use the {{site.data.keyword.containerlong_notm}} service to deploy highly available apps in Docker containers that run in Kubernetes clusters. | [Metrics sent by agent](/docs/containers?topic=containers-health-monitor#monitoring) |
| [{{site.data.keyword.openshiftlong}}](/docs/openshift?topic=openshift-getting-started) | With {{site.data.keyword.openshiftlong_notm}}, you can deploy apps on highly available clusters that come installed with the Red Hat OpenShift on IBM Cloud Container Platform software installed on Red Hat Enterprise Linux. | [Metrics sent by agent](/docs/openshift?topic=openshift-health-monitor#openshift_monitoring) |
{: caption="Table 2. List of {{site.data.keyword.cloud_notm}} container services" caption-side="top"}




## Database services
{: #database}

The following table lists database services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service           | Description    | Metrics |
|-------------------|----------------|---------|
| [{{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant)    | {{site.data.keyword.cloudant_short_notm}} is a document-oriented database as a service (DBaaS). It stores data as documents in JSON format. | [Platform metrics](/docs/Cloudant?topic=Cloudant-monitor-ibm-cloud-pm) |
| [{{site.data.keyword.databases-for-postgresql_full_notm}}](/docs/databases-for-postgresql) | {{site.data.keyword.databases-for-postgresql_full_notm}} is a managed PostgreSQL service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.  | [Platform metrics](/docs/databases-for-postgresql?topic=databases-for-postgresql-monitoring) |
| [{{site.data.keyword.databases-for-mysql_fullnotm}}](/docs/databases-for-mysql) | {{site.data.keyword.databases-for-mysql_fullnotm}} is a managed MySQL service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.  | [Platform metrics](/docs/databases-for-mysql?topic=databases-for-mysql-monitoring) |
| [{{site.data.keyword.databases-for-redis_full_notm}}](/docs/databases-for-redis) | {{site.data.keyword.databases-for-redis_full_notm}} is a managed service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.  | [Platform metrics](/docs/databases-for-redis?topic=databases-for-redis-monitoring) |
| [{{site.data.keyword.databases-for-etcd_full_notm}}](/docs/databases-for-etcd) | {{site.data.keyword.databases-for-etcd_full_notm}} is a managed etcd service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Platform metrics](/docs/databases-for-etcd?topic=databases-for-etcd-monitoring) |
| [{{site.data.keyword.databases-for-elasticsearch_full_notm}}](/docs/databases-for-elasticsearch) | {{site.data.keyword.databases-for-elasticsearch_full_notm}} is a managed Elasticsearch service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Platform metrics](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-monitoring) |
| [{{site.data.keyword.databases-for-mongodb_full_notm}}](/docs/databases-for-mongodb) | {{site.data.keyword.databases-for-mongodb_full_notm}} is a managed MongoDB service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Platform metrics](/docs/databases-for-mongodb?topic=databases-for-mongodb-monitoring) |
| [{{site.data.keyword.messages-for-rabbitmq_full_notm}}](/docs/messages-for-rabbitmq)  | {{site.data.keyword.messages-for-rabbitmq_full_notm}} is a managed RabbitMQ service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.   | [Platform metrics](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-monitoring) |
| [{{site.data.keyword.databases-for-enterprisedb_full_notm}}](/docs/databases-for-enterprisedb)  | {{site.data.keyword.databases-for-enterprisedb_full_notm}} is a managed service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services.   | [Platform metrics](/docs/databases-for-enterprisedb?topic=databases-for-enterprisedb-monitoring) |
| [{{site.data.keyword.sqlquery_full}}](/docs/services/sql-query?topic=sql-query-gettingstarted)| {{site.data.keyword.sqlquery_full}} is a fully-managed service that lets you run SQL queries (that is, SELECT statements) to analyze, transform, or clean up rectangular data. | [Platform metrics](/docs/services/sql-query?topic=sql-query-metrics) |
| [{{site.data.keyword.ihsdbaas_mongodb_full}}](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-gettingstarted) | {{site.data.keyword.ihsdbaas_mongodb_full}} is a highly secure MongoDB service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Platform metrics](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-monitor) |
| [{{site.data.keyword.ihsdbaas_postgresql_full}}](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-gettingstarted) | {{site.data.keyword.ihsdbaas_postgresql_full}} is a highly secure PostgreSQL service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. | [Platform metrics](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-monitor) |
| [{{site.data.keyword.dv_full}}](/docs/data-virtualization?topic=data-virtualization-getting-started) | {{site.data.keyword.dv_full}} is a fully managed service on {{site.data.keyword.cloud_notm}} that you can use to easily and securely access data across many data sources. | [Platform metrics](/docs/data-virtualization?topic=data-virtualization-monitor) |
| [{{site.data.keyword.Db2_on_Cloud_long}}](/docs/Db2onCloud?topic=Db2onCloud-about) | {{site.data.keyword.Db2_on_Cloud_long_notm}} is a fully managed public cloud service on IBM Cloud. As a relational database, it delivers fast query processing with enterprise-level performance and capabilities for online transactional processing (OLTP). | [Platform metrics](/docs/Db2onCloud?topic=Db2onCloud-monitor) |
| [{{site.data.keyword.lakehouse_full_notm}}](/docs/watsonxdata?topic=watsonxdata-getting-started) | {{site.data.keyword.lakehouse_full_notm}} is a unique solution that allows co-existence of open source technologies and proprietary products. It offers a single platform where you can store the data or attach data sources for managing and analyzing your enterprise data. | [Platform metrics](/docs/watsonxdata?topic=watsonxdata-monitor_wxd) |
{: caption="Table 3. List of database services" caption-side="top"}



## Developer tools
{: #devops}

The following table lists developer tools and DevOps services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.contdelivery_full}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started)| With {{site.data.keyword.contdelivery_short}}, you can build, test, and deliver applications by using DevOps practices and industry-leading tools. | [Platform metrics](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd-monitor-sysdig) |
| [{{site.data.keyword.appconfig_full}}](/docs/app-configuration?topic=app-configuration-getting-started)| Instrument your applications with {{site.data.keyword.appconfig_short}} SDKs, and use the {{site.data.keyword.appconfig_short}} dashboard or {{site.data.keyword.appconfig_short}} administrator API to define features flags or properties. | [Platform metrics](/docs/app-configuration?topic=app-configuration-ac-monitoring) |
| [{{site.data.keyword.en_full}}](/docs/event-notifications?topic=event-notifications-getting-started)|  A centralized alerts management service that notifies and alerts you to events occurring in your {{site.data.keyword.Bluemix_notm}} account.| [Platform metrics](/docs/event-notifications?topic=event-notifications-en-monitoring) |
{: caption="Table 4. List of developer tools and DevOps services" caption-side="top"}


## Integration services
{: #integration}

The following table lists integration services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-getting_started)| {{site.data.keyword.messagehub}} is a high-throughput message bus that is built with Apache Kafka. It is optimized for event ingestion into {{site.data.keyword.IBM_notm}} and event stream distribution between your services and applications. | [Platform metrics](/docs/EventStreams?topic=EventStreams-metrics) |
| [{{site.data.keyword.mq_full}}](/docs/mqcloud?topic=mqcloud-getting_started)| {{site.data.keyword.mq_full}} is an enterprise grade messaging middleware service that provides secure messaging capabilities, such as point-to-point and publish and subscribe models. | [Platform metrics](/docs/mqcloud?topic=mqcloud-monitor_sysdig) |
{: caption="Table 5. List of integration services" caption-side="top"}


## Networking services
{: #networking}

The following table lists services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.dns_full}}](/docs/dns-svcs?topic=dns-svcs-getting-started) | {{site.data.keyword.dns_full_notm}} provides private DNS to Virtual Private Cloud (VPC) users. | [Platform metrics](/docs/dns-svcs?topic=dns-svcs-monitor-ibm-cloud-pm) |
{: caption="Table 6. List of networking services" caption-side="top"}


## Platform
{: #platform}

The following table lists integration services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started) | {{site.data.keyword.bplong_notm}} delivers Terraform-as-a-Service so that you can use a high-level scripting language to model the resources that you want in your {{site.data.keyword.cloud_notm}} environment, and enable Infrastructure as Code (IaC).  | [Platform metrics](/docs/schematics?topic=schematics-monitoring-instances) |
| [{{site.data.keyword.atracker_full_notm}}](/docs/atracker) | You can use {{site.data.keyword.atracker_full_notm}} to configure how to route auditing events, both global and location-based event data, in your {{site.data.keyword.cloud_notm}}. | [Platform metrics](/docs/atracker?topic=atracker-monitoring_metrics) |
| [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router) | Use {{site.data.keyword.metrics_router_full_notm}} to configure the routing of platform metrics generated in your {{site.data.keyword.cloud_notm}} account. | [Platform metrics](/docs/metrics-router?topic=metrics-router-platform-metrics) |
{: caption="Table 7. List of platform services" caption-side="top"}

## Satellite
{: #satellite}

The following table lists services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.satellitelong}}](/docs/satellite?topic=satellite-getting-started) | With {{site.data.keyword.satellitelong_notm}}, you can bring your own compute infrastructure to run {{site.data.keyword.cloud_notm}} services and consistently deploy, manage, and control your app workloads. | [Platform metrics](/docs/satellite?topic=satellite-monitor) |
{: caption="Table 8. Satellite" caption-side="top"}

## Security services
{: #security}

The following table lists Cloud services that are enabled for {{site.data.keyword.mon_full_notm}}:


| Service     | Description | More info |
|-------------|-------------|-------------------------------------------------------------------------|
| [{{site.data.keyword.keymanagementservicelong}}](/docs/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) | You can use the {{site.data.keyword.keymanagementserviceshort}} service to provision encrypted keys for apps across the {{site.data.keyword.cloud_notm}}. | [Platform metrics](/docs/key-protect?topic=key-protect-operational-metrics) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started) | You can use the {{site.data.keyword.hscrypto}} to control your cloud data encryption keys in cloud hardware security modules for apps across the {{site.data.keyword.cloud_notm}}. | [Platform metrics](/docs/hs-crypto?topic=hs-crypto-operational-metrics) |
{: caption="Table 9. List of security services" caption-side="top"}



## Serverless
{: #compute_serverless}

The following table lists container services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.codeenginefull_notm}}](/docs/codeengine?topic=codeengine-getting-started) | {{site.data.keyword.codeengineshort}} is a fully managed, serverless platform that runs your containerized workloads. | [Platform metrics](/docs/codeengine?topic=codeengine-monitor)|
| [{{site.data.keyword.openwhisk}}](/docs/openwhisk?topic=openwhisk-getting-started) | A Functions-as-a-Service (FaaS) programming platform based on Apache OpenWhisk. | [Platform metrics](/docs/openwhisk?topic=openwhisk-monitor-functions)|
{: caption="Table 10. List of serverless services" caption-side="top"}


## Storage services
{: #storage}

The following table lists Cloud services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.cos_full}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage)| You can use {{site.data.keyword.cos_full_notm}} to store unstructured data in the {{site.data.keyword.cloud_notm}}.  | [Platform metrics](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration&programming_language=Console) |
{: caption="Table 11. List of storage services" caption-side="top"}

## VMware as a Service
{: #vmware}

The following table lists Cloud services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics           |
|-------------|-------------|-------------------|
| [{{site.data.keyword.vmware-service_short}}](/docs/vmware-service?topic=vmware-service-single-tenant-monitoring) | Deploys a comprehensive portfolio of automated and on-demand services for VMware workloads to the cloud. | [Platform metrics](/docs/vmware-service?topic=vmware-service-single-tenant-monitoring#single-tenant-monitoring-metrics)|
{: caption="Table 12. VMware as a Service" caption-side="top"}

## VMware Shared
{: #vmware-shared}

The following table lists Cloud services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics           |
|-------------|-------------|-------------------|
| [VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared-monitor) | Provides standardized and customizable deployment choices of VMware® virtual data center environments. | [Platform metrics](/docs/vmwaresolutions?topic=vmwaresolutions-shared-monitor#shared-monitor-metrics)|
{: caption="Table 13. VMware Shared" caption-side="top"}

## VPC
{: #vpc}

With {{site.data.keyword.vpc_full}} (VPC), you can provision a VPC in the {{site.data.keyword.cloud_notm}} to run an isolated environment within the public cloud. VPC gives you the security of a private cloud, with the agility and ease of a public cloud. The VPC infrastructure contains a number of Infrastructure-as-a-Service (IaaS) offerings, including Virtual Servers for VPC. [Learn more](/docs/vpc?topic=vpc-getting-started).


You can monitor various aspects of VPC services with {{site.data.keyword.mon_full_notm}} dashboards. For more information, see [{{site.data.keyword.cloud_notm}} VPC monitoring dashboards](/docs/vpc?topic=vpc-ibm-monitoring).

The following table lists services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | Description | Metrics             |
|-------------|-------------|-------------------|
| [VPC virtual server instances](/docs/vpc?topic=vpc-about-advanced-virtual-servers&interface=ui) | With virtual server instances for VPC, you can quickly provision instances with high network performance. | [Platform metrics](/docs/vpc?topic=vpc-vpc-monitoring-metrics)|
| [Flow Logs for VPC](/docs/vpc?topic=vpc-flow-logs) | Flow Logs for VPC enable the collection, storage, and presentation of information about the Internet Protocol (IP) traffic going to and from network interfaces within your Virtual Private Cloud (VPC). | [Platform metrics](/docs/vpc?topic=vpc-fl-monitoring-metrics) |
| [Load Balancer for VPC](/docs/vpc?topic=vpc-network-load-balancers)| Distributes traffic among multiple server instances within the same region of your VPC.  | [Application Load Balancer platform metrics](/docs/vpc?topic=vpc-monitoring-metrics-alb) \n [Network Load Balancer platform metrics](/docs/vpc?topic=vpc-nlb_monitoring-metrics) |
| [VPN for VPC ( site-to-site VPN)](/docs/vpc?topic=vpc-using-vpn)| Securely connect your VPC to another private network. You can use VPN to set up an IPsec site-to-site tunnel between your VPC and your on-premises private network or another VPC. | [Platform metrics](/docs/vpc?topic=vpc-vpn-monitoring-metrics) |
| [Client VPN for VPC](/docs/vpc?topic=vpc-vpn-client-to-site-overview)| Client VPN for VPC provides client-to-site connectivity, which allows remote devices to securely connect to the VPC network using an OpenVPN software client. | [Platform metrics](/docs/vpc?topic=vpc-vpn-client-to-site-monitoring) |
{: caption="Table 14. List of VPC services (generation 2)" caption-side="top"}

In addition, some VPC resources have quotas associated with them that you can monitor through the VPC resource quota overview dashboard. For more information, see [VPC resource quota overview](/docs/vpc?topic=vpc-vpc-quota-metrics).
