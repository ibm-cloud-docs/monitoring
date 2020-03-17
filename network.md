---

copyright:
  years:  2018, 2020
lastupdated: "2020-02-12"

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

You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. To configure an agent to send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account. Once the account is VRF and service endpoint enabled, the Sysdig agent can be configured to use the private network by using the [Private Endpoint](/docs/Monitoring-with-Sysdig?topic=Sysdig-endpoints) as the ingestion URL.
* Private endpoints are not accessible from the public internet. 
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network. 
* Services like {{site.data.keyword.mon_full_notm}} are no longer served on an internet routable IP address.

Notice that when you configure the agent to send metrics through the public network, the environment where the agent is running requires internet access to use the public endpoint.




## Allowing outgoing network traffic
{: #network_outgoing_traffic}

When you have an extra firewall set up, or you customize the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure, you need to allow outgoing network traffic to the {{site.data.keyword.mon_full_notm}} service. 


### Ingestion through a public endpoint
{: #network_send}

To send metric data to the {{site.data.keyword.mon_full_notm}} service, you must define a firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses                                     |   Ports    |
|-------------|---------------------------------------------------|---------------------------------------------------------|----------|
| `US South`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | TCP 6443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | TCP 6443 | 
| `US East`   | ingest.us-east.monitoring.cloud.ibm.com           | 169.60.112.74 </br>169.55.109.114 </br>169.62.3.82      | TCP 6443 |
| `AU SYD`    | ingest.au-syd.monitoring.cloud.ibm.com            | 135.90.73.100 </br>130.198.80.155 </br>168.1.213.78     | TCP 6443 | 
{: caption="Table 1. Public IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}


### Access to the web UI through a public endpoint
{: #network_ui}

To access the {{site.data.keyword.mon_full_notm}} web UI, you must define a firewall rule in your host:

| Region      | Web UI endpoint                        | Public IP addresses                                       |  Ports           |
|-------------|----------------------------------------|-----------------------------------------------------------|-----------------|
| `US South`  | us-south.monitoring.cloud.ibm.com      | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70        | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com         | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38     | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com         | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
| `JP TOK`    | jp-tok.monitoring.cloud.ibm.com        | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238       | https (TLS) 443 |
| `US East`   | us-east.monitoring.cloud.ibm.com       | 169.60.112.74 </br>169.55.109.114 </br>169.62.3.82        | https (TLS) 443 | 
| `AU SYD`    | au-syd.monitoring.cloud.ibm.com        | 135.90.73.100 </br>130.198.80.155 </br>168.1.213.78       | https (TLS) 443 | 
{: caption="Table 2. Public IP addresses to access the {{site.data.keyword.mon_full_notm}} web UI" caption-side="top"}

### Ingestion through a private endpoint
{: #network_send_private}

To send metric data to the {{site.data.keyword.mon_full_notm}} service, you must define a firewall rule in your host:

| Region      | Ingestion endpoint                                | Private IP addresses                          |   Ports    |
|-------------|---------------------------------------------------|-----------------------------------------------|----------|
| `US South`  | ingest.private.us-south.monitoring.cloud.ibm.com  | 166.9.12.247 </br>166.9.16.99 </br>166.9.15.123  | TCP 6443 | 
| `EU DE`     | ingest.private.eu-de.monitoring.cloud.ibm.com     | 166.9.30.20 </br>166.9.28.32 </br>166.9.32.16  | TCP 6443 | 
| `EU GB`     | Not available                                     | Not available   | | 
| `JP TOK`    | ingest.private.jp-tok.monitoring.cloud.ibm.com    | 166.9.40.25 </br>166.9.42.8 </br>166.9.44.2 | TCP 6443 | 
| `US East`   | ingest.private.us-east.monitoring.cloud.ibm.com   | 166.9.22.6 </br>166.9.20.39 </br>166.9.24.21   | TCP 6443 | 
| `AU SYD`    | Not available                                     | Not available   |  | 
{: caption="Table 3. Private IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}


### Alert Notifications via Webhooks
{: #network_alert_subnets}

To receive alert notifications using webhooks from the {{site.data.keyword.mon_full_notm}} service, you may need to define firewall rules for the subnets that are invoking your webhooks.

| Region     | Alert Notification Source Subnets                                                                          |
|------------|------------------------------------------------------------------------------------------------------------|
| `US South` | 169.61.248.224/28 </br>169.46.0.64/29 </br>169.48.214.64/29 </br>169.48.235.16/28 </br>169.62.221.32/28 </br>169.60.151.168/29      |
| `EU DE`    | 169.50.9.0/28 </br>159.122.102.32/29 </br>161.156.102.200/29 </br>161.156.69.144/28 </br>149.81.99.192/28 </br>149.81.77.72/29      |
| `EU GB`    | 159.8.149.208/28 </br>159.122.210.168/29 </br>158.175.75.160/28 </br>158.175.98.200/29 </br>141.125.73.112/29 </br>141.125.73.80/28 |
| `JP TOK`   | 169.56.51.232/29 </br>169.56.11.208/28 </br>128.168.75.32/28 </br>128.168.75.8/29 </br>165.192.84.8/29 </br>165.192.83.144/28       |
| `US East`  | 169.55.109.112/29 </br>169.55.122.192/28 </br>169.60.82.240/28 </br>169.60.112.72/29 </br>169.62.28.160/28 </br>169.62.3.80/29      | 
| `AU SYD`   | 168.1.213.72/29 </br>168.1.41.96/28 </br>130.198.80.152/29 </br>130.198.66.144/28 </br>135.90.73.96/29 </br>135.90.78.192/28        |
{: caption="Table 4. Source Subnets for Webhook notifications from {{site.data.keyword.mon_full_notm}}" caption-side="top"}
