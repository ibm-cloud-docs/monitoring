---

copyright:
  years: 2018, 2021
lastupdated: "2021-03-28"

keywords: Sysdig, IBM Cloud, monitoring, security, connection

subcollection: Monitoring-with-Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}


# Securing your connection
{: #service-connection}

To ensure that you have enhanced control and security over your data when you use {{site.data.keyword.mon_full}}, you have the option of using private routes to {{site.data.keyword.cloud_notm}} service endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} private service endpoints feature, you can protect your data from threats from the public network and logically extend your private network.
{: shortdesc}


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

You can configure a monitoring agent to connect to an {{site.data.keyword.mon_full_notm}} instance through the public network or through the private network. By default, the agent connects through the public network.
{: note}

The type of network defines the level of isolation and security that is configured to move workloads between cloud-based resources in your account. Consider connecting the monitoring agent over the private network.



## Setting up private service endpoints for {{site.data.keyword.mon_full_notm}}
{: #endpoint-setup}

Private network endpoints support routing services over the {{site.data.keyword.cloud_notm}} private network instead of the public network. A private network endpoint provides a unique IP address that is accessible to you without a VPN connection.


### Step 1: Enabling your account
{: #endpoint-setup-step1}

To use private network endpoints, you must enable the Virtual routing and forwarding (VRF) account feature.

You must first enable virtual routing and forwarding in your account, and then you can enable the use of IBM Cloud private service endpoints. 
* To enable VRF, you create a support case. 
* To enable service endpoints, you use the {{site.data.keyword.cloud_notm}} CLI. For more information about how to enable your account, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).


### Step 2: Setting a private endpoint
{: #endpoint-setup-step2}

After your account is enabled for VRF and service endpoints, you can configure a monitoring agent to connect to an {{site.data.keyword.mon_full_notm}} instance through the private network. 

The monitoring service is available on both private and public endpoints. The monitoring service currently does not support only-public or only-private configurations.
{: note}

You can [configure the monitoring agent](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-config_agent) to use the private network by using a private endpoint as the ingestion URL. To get information about private endpoints, see [Private endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion_private).

What happens when you configure the monitoring agent to use a private endpoint?
* Private endpoints are not accessible from the public internet. 
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network. 



## Allowing outgoing network traffic
{: #network_outgoing_traffic}

When you have an extra firewall set up, or you customize the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure, you need to allow outgoing network traffic to the {{site.data.keyword.mon_full_notm}} service. 


### Ingestion through an endpoint
{: #network_send}

To send metric data to the {{site.data.keyword.mon_full_notm}} service, you may need to define a firewall rule in your host:

* To get information about private endpoints, see [Private endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion_private).
* To get information about public endpoints, see [Public endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion_public).


### Access to the web UI through a public endpoint
{: #network_ui}

To access the {{site.data.keyword.mon_full_notm}} web UI, you may need to define a firewall rule in your host. To get information about the endpoints, see [monitoring UI endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_sysdig).



### Alert Notifications via Webhooks
{: #network_alert_subnets}

To receive alert notifications using webhooks from the {{site.data.keyword.mon_full_notm}} service, you may need to define firewall rules for the subnets that are invoking your webhooks. To get information about the subnets, see [Subnets for webhook notifications](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_network_alert_subnets).




