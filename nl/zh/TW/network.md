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

 
# 管理自訂防火牆配置的網路資料流量
{: #network}

如果設定了額外的防火牆，或者在 {{site.data.keyword.cloud_notm}} 基礎架構中自訂了防火牆設定，則需要容許流至 {{site.data.keyword.mon_full_notm}} 服務的送出網路資料流量。
{:shortdesc}


## 汲取端點
{: #network_send}

若要將度量值資料傳送至 {{site.data.keyword.mon_full_notm}} 服務，您必須在主機中定義下列防火牆規則：

| 地區      | 汲取端點                                | 公用 IP 位址               | 埠    |
|-------------|---------------------------------------------------|---------------------------------------------------------|----------|
| `US South`    | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | TCP 6443 | 
| `JP TOK`     | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | TCP 6443 | 
{: caption="表 1. 用於將資料傳送到 {{site.data.keyword.mon_full_notm}} 的 IP 位址" caption-side="top"}


## Web 使用者介面端點
{: #network_ui}

若要存取 {{site.data.keyword.mon_full_notm}} Web 使用者介面，您必須在主機中定義下列防火牆規則：

| 地區      | Web 使用者介面端點                                   | 公用 IP 位址                                    | 埠   |
|-------------|---------------------------------------------------|-----------------------------------------------------------|---------|
| `美國南部`          | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | https (TLS) 443 | 
| `JP TOK`     | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | https (TLS) 443 |
{: caption="表 2. 用來存取 {{site.data.keyword.mon_full_notm}} Web 使用者介面的 IP 位址" caption-side="top"}


