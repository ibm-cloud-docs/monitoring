---

copyright:
  years:  2018, 2025
lastupdated: "2025-02-27"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Securing your connection
{: #service-connection}

To ensure that you have enhanced control and security over your data when you use {{site.data.keyword.mon_full_notm}}, you have the option of using private routes to {{site.data.keyword.cloud_notm}} service endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} private service endpoints feature, you can protect your data from threats from the public network and logically extend your private network.
{: shortdesc}

- You can configure the {{site.data.keyword.mon_short}} agent to only use private endpoints.
- You can configure the {{site.data.keyword.mon_short}} instance to only allow API calls through the private endpoints.

The {{site.data.keyword.mon_short}} service can be configured to send and receive data on either public-only or private-only endpoints. The web UI is available only on the public endpoint.
{: note}


## Before you begin
{: #prereq-service-endpoint}

Some factors that you must consider when you must decide which network to choose are:
* Corporate requirements on how services and applications can access cloud-based services in your account
* Security on production workloads
* Industry compliance regulations

For example, you might have the following requirements when you are working in the {{site.data.keyword.cloud_notm}}:
* No access to Internet to connect to {{site.data.keyword.cloud_notm}} services
* Isolated connectivity for workloads in your account

When you have these requirements, you should move from the public network to the private network.

You can configure a {{site.data.keyword.mon_short}} agent to connect to a {{site.data.keyword.mon_short}} instance through the public network or through the private network. By default, the agent connects through the public network.

You can make API calls through the public network or through the private network. By default, you make them through the public network.

The type of network defines the level of isolation and security that is configured to move workloads between cloud-based resources in your account. Consider connecting the {{site.data.keyword.mon_short}} agent over the private network.



## Setting up private service endpoints
{: #endpoint-setup}

Private network endpoints support routing services over the {{site.data.keyword.cloud_notm}} private network instead of the public network. A private network endpoint provides a unique IP address that is accessible to you without a VPN connection.

### Step 1: Enabling your account
{: #endpoint-setup-step1}

If you want to use connections over the public internet, you do not have to enable Service Endpoints on your {{site.data.keyword.cloud_notm}} account.

To use private network endpoints, you must enable the Virtual routing and forwarding (VRF) account feature.

You must first enable virtual routing and forwarding in your account, and then you can enable the use of {{site.data.keyword.cloud_notm}} private service endpoints.
* To enable VRF, you create a support case.
* To enable service endpoints, you use the {{site.data.keyword.cloud_notm}} CLI. For more information about how to enable your account, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).


### Step 2: Enforcing API calls through private endpoints
{: #endpoint-setup-step2}

After your account is enabled for VRF and service endpoints, you can configure a {{site.data.keyword.mon_short}} instance to only allow API calls through the private endpoints.

After you provision an instance of the {{site.data.keyword.mon_short}} service, you can use the following CLI command to update the instance configuration and enforce private endpoints for all API commands:

```shell
ibmcloud resource service-instance-update <my-service-instance> --service-endpoints 'private'
```
{: pre}

Or you can use the [Resource Controller API](https://cloud.ibm.com/apidocs/resource-controller), with a `PATCH` request to the [/resource_instances/{id}](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#update-resource-instance) endpoint.

After you enable private endpoints, the API calls that are made through a public endpoint are rejected.


### Step 3: Configuring a {{site.data.keyword.mon_short}} agent to connect through private endpoints
{: #endpoint-setup-step3}

After your account is enabled for VRF and service endpoints, you can configure a {{site.data.keyword.mon_short}} agent to connect to an {{site.data.keyword.mon_full_notm}} instance through the private network.


You can [configure the {{site.data.keyword.mon_short}} agent](/docs/monitoring?topic=monitoring-config_agent) to use the private network by using a private endpoint as the ingestion URL. To get information about private endpoints, see [Private endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion_private).

What happens when you configure the {{site.data.keyword.mon_short}} agent to use a private endpoint?
* Private endpoints are not accessible from the public internet.
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network.


## Allowing network traffic
{: #network_outgoing_traffic}

When you have an extra firewall set up, or you customize the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure, you need to allow network traffic to the {{site.data.keyword.mon_short}} service.


### Ingestion through an endpoint
{: #network_send}

You can choose to send data to the {{site.data.keyword.mon_short}} service through a public or private endpoint. Notice that you may need to define a firewall rule in your host.
- To get information about private endpoints, see [Private endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion_private).
- To get information about public endpoints, see [Public endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion_public).


### Access to the web UI through a public endpoint
{: #network_ui}

To access the {{site.data.keyword.mon_full_notm}} web UI, you may need to define a firewall rule in your host. To get information about the web UI endpoints, see [Web UI endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_sysdig).



### Alert Notifications via Webhooks
{: #network_alert_subnets}

To receive alert notifications by using webhooks from the {{site.data.keyword.mon_short}} service, you may need to define firewall rules for the subnets that are invoking your webhooks. To get information about the subnets, see [Subnets for webhook notifications](/docs/monitoring?topic=monitoring-endpoints#endpoints_network_alert_subnets).
