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

 
# Managing network traffic for custom firewall configurations
{: #network}

When you have an extra firewall set up, or you customize the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure, you need to allow outgoing network traffic to the {{site.data.keyword.mon_full_notm}} service. 
{:shortdesc}


## Ingestion endpoints
{: #network_send}

To send metric data to the {{site.data.keyword.mon_full_notm}} service, you must define the following firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses                                     | Ports    |
|-------------|---------------------------------------------------|---------------------------------------------------------|----------|
| `US South`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | TCP 6443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | TCP 6443 | 
| `US East`   | ingest.us-east.monitoring.cloud.ibm.com           | 169.60.112.74</br> 169.55.109.114 </br> 169.62.3.82     | TCP 6443 | 
{: caption="Table 1. IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}


## Web UI endpoints
{: #network_ui}

To access the {{site.data.keyword.mon_full_notm}} web UI, you must define the following firewall rule in your host:

| Region      | Web UI endpoint                        | Public IP addresses                                       | Ports   |
|-------------|----------------------------------------|-----------------------------------------------------------|---------|
| `US South`  | us-south.monitoring.cloud.ibm.com      | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70        | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com         | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38     | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com         | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
| `JP TOK`    | jp-tok.monitoring.cloud.ibm.com        | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238       | https (TLS) 443 |
| `US East`   | us-east.monitoring.cloud.ibm.com       | 169.60.112.74</br> 169.55.109.114 </br> 169.62.3.82       | https (TLS) 443 | 
{: caption="Table 2. IP addresses to access the {{site.data.keyword.mon_full_notm}} web UI" caption-side="top"}


