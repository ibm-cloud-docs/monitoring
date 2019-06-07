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


# 地區與端點
{: #endpoints}

{{site.data.keyword.mon_full_notm}} 服務支援之地區與端點的清單：
{:shortdesc}

## 地區
{: #endpoints_regions}

下列地區提供 {{site.data.keyword.mon_full_notm}} 服務：

| 地區                | 位置  | 
|-----------------------|-----------|
| `US SOUTH`            | 達拉斯    | 
| `EU-DE`               | 法蘭克福 | 
| `EU-GB`               | 倫敦| 
| `JP-TOK`              |東京|
{: caption="表 1. 提供服務的地區清單" caption-side="top"} 

目前，**法蘭克福**和 **EU GB** 是**不由**歐盟管理的位置。如需相關資訊，請參閱[啟用歐盟支援設定](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported)。
{: important}


## Sysdig 收集器端點
{: #endpoints_ingestion}

**Sysdig 收集器**端點是您可以用來傳送資料的汲取端點。

下表列出了每個地區可用的 **Sysdig 收集器端點**：

| 地區        | 端點                                                  | 埠 |
|---------------|-----------------------------------------------------------|------|
| `美國南部`          | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU DE`     | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU GB`     | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `JP TOK`     | `ingest.jp-tok.monitoring.cloud.ibm.com`                  | TCP 6443 | 
{: caption="表 2. 汲取端點的清單" caption-side="top"} 



## Sysdig 端點
{: #endpoints_sysdig}

下表列出了每個地區可用的 **Sysdig 端點**：

| 地區        | 端點                                                  | 埠 |
|--------------|-----------------------------------------------------------|-----------------|
| `美國南部`          | `https://us-south.monitoring.cloud.ibm.com `              | HTTPS (TLS) 443 |  
| `EU DE`     | `https://eu-de.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `EU GB`     | `https://eu-gb.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `JP TOK`     | `https://jp-tok.monitoring.cloud.ibm.com`                 | HTTPS (TLS) 443 |
{: caption="表 3. Sysdig 端點的清單" caption-side="top"} 


