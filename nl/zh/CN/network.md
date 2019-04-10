---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-22"

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

 
# 管理定制防火墙配置的网络流量
{: #network}

如果设置了其他防火墙，或者在 {{site.data.keyword.cloud_notm}} Infrastructure (SoftLayer) 中定制了防火墙设置，那么需要允许流至 {{site.data.keyword.mon_full_notm}} 服务的所有出局网络流量。
{:shortdesc}


## 采集端点
{: #network_send}

要将度量数据发送到 {{site.data.keyword.mon_full_notm}} 服务，必须在主机中定义以下防火墙规则：

|区域|采集端点|公共 IP 地址|端口|
|-------------|---------------------------------------------------|-----------------------------------|----------|
|`US South`|ingest.us-south.monitoring.cloud.ibm.com|169.60.151.174</br>169.46.0.70</br>169.48.214.70|TCP 6443| 
|`EU DE`|ingest.eu-de.monitoring.cloud.ibm.com|149.81.77.78</br>161.156.102.206</br>159.122.102.38|TCP 6443| 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   |TCP 6443| 
{: caption="表 1. 用于发送度量值的 IP 地址" caption-side="top"}



## Web UI 端点
{: #network_ui}

要访问 {{site.data.keyword.mon_full_notm}} Web UI，必须在主机中定义以下防火墙规则：

|区域|Web UI 端点|公共 IP 地址|端口|
|-------------|---------------------------------------------------|--------------------------------------------------------|---------|
|`US South`|us-south.monitoring.cloud.ibm.com|169.60.151.174</br>169.46.0.70</br>169.48.214.70|https (TLS) 443| 
|`EU DE`|eu-de.monitoring.cloud.ibm.com|149.81.77.78</br>161.156.102.206</br>159.122.102.38|https (TLS) 443| 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   |https (TLS) 443| 
{: caption="表 2. 用于访问 {{site.data.keyword.mon_full_notm}} Web UI 的 IP 地址" caption-side="top"}


