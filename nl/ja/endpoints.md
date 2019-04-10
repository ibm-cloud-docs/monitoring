---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-22"

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


# 地域とエンドポイント
{: #endpoints}

{{site.data.keyword.mon_full_notm}} サービスでサポートされる地域とエンドポイントのリスト:
{:shortdesc}

## 地域
{: #endpoints_regions}

{{site.data.keyword.mon_full_notm}} サービスは、以下の地域で使用可能です。

| 地域                | ロケーション  | 
|-----------------------|-----------|
| `US South`            | ダラス    | 
| `EU-DE`               | フランクフルト | 
| `EU-GB`               | ロンドン    | 
{: caption="表 1. サービスが使用可能な地域のリスト" caption-side="top"} 

**フランクフルト**および**EU GB**は、現在 EU 管理のロケーションでは **ありません**。詳しくは、[「EU サポート対象」設定の有効化](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported)を参照してください。
{: important}


## Sysdig Collector エンドポイント
{: #endpoints_ingestion}

**Sysdig Collector** エンドポイントは、データの送信に使用できる取り込みエンドポイントです。

以下の表は、使用可能な **Sysdig Collector エンドポイント**を地域ごとに示しています。

| 地域        | エンドポイント                                                  | ポート |
|---------------|-----------------------------------------------------------|------|
| `US South`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU-DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU-GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
{: caption="表 2. 取り込みエンドポイントのリスト" caption-side="top"} 



## Sysdig エンドポイント
{: #endpoints_sysdig}

以下の表は、使用可能な **Sysdig エンドポイント**を地域ごとに示しています。

| 地域       | エンドポイント                                                  | ポート |
|--------------|-----------------------------------------------------------|------|
| `US South`   | `https://us-south.monitoring.cloud.ibm.com `              | https (TLS) 443 |  
| `EU-DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
| `EU-GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
{: caption="表 3. Sysdig エンドポイントのリスト" caption-side="top"} 


