---

copyright:
  years: 2020, 2020
lastupdated: "2020-03-16"

keywords: Sysdig, IBM Cloud, monitoring, security, connection

subcollection: Sysdig

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

You can configure a Sysdig agent to connect to an {{site.data.keyword.mon_full_notm}} instance through the public network or through the private network. By default, the agent connects through the public network.
{: note}

The type of network defines the level of isolation and security that is configured to move workloads between cloud-based resources in your account. Consider connecting the Sysdig agent over the private network.


## Setting up private service endpoints for {{site.data.keyword.mon_full_notm}}
{: #endpoint-setup}

Private network endpoints support routing services over the {{site.data.keyword.cloud_notm}} private network instead of the public network. A private network endpoint provides a unique IP address that is accessible to you without a VPN connection.


### Step 1: Enabling your account
{: #endpoint-setup-step1}

To use private network endpoints, the following account features must be enabled for your account:
* Virtual routing and forwarding (VRF)
* Service endpoints

    Enabling service endpoints means that all users in the account can connect to private network endpoints.
    {: note}

You must first enable virtual routing and forwarding in your account, and then you can enable the use of IBM Cloud private service endpoints. 
* To enable VRF, you create a support case. 
* To enable service endpoints, you use the {{site.data.keyword.cloud_notm}} CLI. For more information about how to enable your account, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).


### Step 2: Setting a private endpoint
{: #endpoint-setup-step2}

After your account is enabled for VRF and service endpoints, you can configure a Sysdig agent to connect to an {{site.data.keyword.mon_full_notm}} instance through the private network. 

A service instance can have a private network endpoint, a public network endpoint, or both.
* Public network endpoint: A service endpoint on the {{site.data.keyword.cloud_notm}} public network.
* Private network endpoint: A service endpoint that is accessible only on the {{site.data.keyword.cloud_notm}} private network with no access from the public internet.
* Both public and private network endpoints: Service endpoints that allow access over both networks.

The {{site.data.keyword.mon_full_notm}} service offers the following private endpoints:

| Region      | Ingestion endpoint                                   | Private IP addresses                              |   Ports   |
|-------------|------------------------------------------------------|---------------------------------------------------|-----------|
| `US South`  | `ingest.private.us-south.monitoring.cloud.ibm.com`   | 166.9.12.247 </br>166.9.16.99 </br>166.9.15.123   | TCP 6443  | 
| `EU DE`     | `ingest.private.eu-de.monitoring.cloud.ibm.com`      | 166.9.30.20 </br>166.9.28.32 </br>166.9.32.16     | TCP 6443  | 
| `EU GB`     | `ingest.private.eu-gb.monitoring.cloud.ibm.com`      | 166.9.34.20 </br>166.9.36.7                       | TCP 6443  |
| `JP TOK`    | `ingest.private.jp-tok.monitoring.cloud.ibm.com`     | 166.9.40.25 </br>166.9.42.8 </br>166.9.44.2       | TCP 6443  | 
| `US East`   | `ingest.private.us-east.monitoring.cloud.ibm.com`    | 166.9.22.6 </br>166.9.20.39 </br>166.9.24.21      | TCP 6443  | 
| `AU SYD`    | `ingest.private.au-syd.monitoring.cloud.ibm.com`     | 166.9.54.2 </br>166.9.52.10  </br>166.9.56.24     | TCP 6443  |
{: caption="Table 1. Private IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}


You can [configure the Sysdig agent](/docs/Monitoring-with-Sysdig?topic=Sysdig-config_agent) to use the private network by using a private endpoint as the ingestion URL.

What happens when you configure the Sysdig agent to use a private endpoint?
* Private endpoints are not accessible from the public internet. 
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network. 
* Services like {{site.data.keyword.mon_full_notm}} are no longer served on an internet routable IP address.





