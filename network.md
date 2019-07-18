---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, network traffic, firewall

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

 
# Managing network connectivity
{: #network}

You can configure the Sysdig agent to connect to a monitoring instance through the public network or through the private network. In addition, when you have an extra firewall set up, or you customize the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure, you need to allow outgoing network traffic to the {{site.data.keyword.mon_full_notm}} service. 
{:shortdesc}


## Choosing a network endpoint
{: #network_endpoints}

You can configure a Sysdig agent to connect to an {{site.data.keyword.mon_full_notm}} instance through the public network or through the private network. By default, the agent connects through the public network.

The type of network defines the level of isolation and security that is configured to move workloads between cloud-based resources in your account. 

Some factors that you must consider when you must decide which network to choose are:
* Corporate requirements on how services and applications can access cloud-based services in your account
* Security on production workloads
* Industry compliance regulations

For example, you might have the following requirements when you are working in the {{site.data.keyword.cloud_notm}}:
* No access to Internet to connect to {{site.data.keyword.cloud_notm}} services
* Isolated connectivity for workloads in your account

When you have these requirements, you should move from the public network to the private network. You should consider connecting the Sysdig agent over the private network. 

You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. To configure an agent to send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account. Once the account is VRF and service endpoint enabled, the Sysdig agent can be configured to use the private network by using the [Private Endpoint](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints) as the ingestion URL.
* Private endpoints are not accessible from the public internet. 
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network. 
* Services like {{site.data.keyword.mon_full_notm}} are no longer served on an internet routable IP address.

Notice that when you configure the agent to send metrics through the public network, the environment where the agent is running requires internet access to use the public endpoint.




## Allowing outgoing network traffic
{: #network_outgoing_traffic}

When you have an extra firewall set up, or you customize the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure, you need to allow outgoing network traffic to the {{site.data.keyword.mon_full_notm}} service. 

If you configure the Sysdig agent to connect to a monitoring instance through the private network, open a support ticket to request the private IP addresses that you must enable in your firewall. For information about opening an {{site.data.keyword.IBM_notm}} support ticket, see [Getting support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).
{: important}


### Ingestion through a public endpoint
{: #network_send}

To send metric data to the {{site.data.keyword.mon_full_notm}} service, you must define a firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses                                     | Ports    |
|-------------|---------------------------------------------------|---------------------------------------------------------|----------|
| `US South`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | TCP 6443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | TCP 6443 | 
| `US East`   | ingest.us-east.monitoring.cloud.ibm.com           | 169.60.112.74</br> 169.55.109.114 </br> 169.62.3.82     | TCP 6443 | 
{: caption="Table 1. IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}


### Access to the web UI through a public endpoint
{: #network_ui}

To access the {{site.data.keyword.mon_full_notm}} web UI, you must define a firewall rule in your host:

| Region      | Web UI endpoint                        | Public IP addresses                                       | Ports           |
|-------------|----------------------------------------|-----------------------------------------------------------|-----------------|
| `US South`  | us-south.monitoring.cloud.ibm.com      | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70        | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com         | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38     | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com         | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
| `JP TOK`    | jp-tok.monitoring.cloud.ibm.com        | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238       | https (TLS) 443 |
| `US East`   | us-east.monitoring.cloud.ibm.com       | 169.60.112.74</br> 169.55.109.114 </br> 169.62.3.82       | https (TLS) 443 | 
{: caption="Table 2. IP addresses to access the {{site.data.keyword.mon_full_notm}} web UI" caption-side="top"}


