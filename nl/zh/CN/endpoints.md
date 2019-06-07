---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, regions, endpoints

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


# 区域和端点
{: #endpoints}

{{site.data.keyword.mon_full_notm}} 服务的受支持区域和端点的列表：
{:shortdesc}

## 区域
{: #endpoints_regions}

{{site.data.keyword.mon_full_notm}} 服务在以下区域中可用：

|区域|位置| 
|-----------------------|-----------|
| `US SOUTH`            |达拉斯| 
|`EU-DE`|法兰克福| 
| `EU-GB`               |伦敦| 
| `JP-TOK`              |东京|
{: caption="表 1. 服务在其中可用的区域的列表" caption-side="top"} 

目前，**法兰克福**和 **EU GB** 是**非**欧盟管理的位置。有关更多信息，请参阅[启用欧盟支持设置](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported)。
{: important}


## Sysdig 收集器端点
{: #endpoints_ingestion}

**Sysdig 收集器**端点是采集端点，可用于发送数据。

下表列出了每个区域可用的 **Sysdig 收集器端点**：

|区域|端点|端口|
|---------------|-----------------------------------------------------------|------|
|`US South`|`ingest.us-south.monitoring.cloud.ibm.com`|TCP 6443|
|`EU DE`|`ingest.eu-de.monitoring.cloud.ibm.com`|TCP 6443| 
| `EU GB`     | `ingest.eu-gb.monitoring.cloud.ibm.com`                   |TCP 6443| 
| `JP TOK`      | `ingest.jp-tok.monitoring.cloud.ibm.com`                  |TCP 6443| 
{: caption="表 2. 采集端点的列表" caption-side="top"} 



## Sysdig 端点
{: #endpoints_sysdig}

下表列出了每个区域可用的 **Sysdig 端点**：

|区域|端点|端口|
|--------------|-----------------------------------------------------------|-----------------|
|`US South`|`https://us-south.monitoring.cloud.ibm.com `| HTTPS (TLS) 443 |  
|`EU DE`| `https://eu-de.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `EU GB`     | `https://eu-gb.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `JP TOK`     | `https://jp-tok.monitoring.cloud.ibm.com`                 | HTTPS (TLS) 443 |
{: caption="表 3. Sysdig 端点的列表" caption-side="top"} 


