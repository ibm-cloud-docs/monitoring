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

 
# カスタム・ファイアウォール構成に対するネットワーク・トラフィックの管理
{: #network}

追加ファイアウォールをセットアップしたか、{{site.data.keyword.cloud_notm}} インフラストラクチャー (SoftLayer) のファイアウォール設定をカスタマイズした場合は、{{site.data.keyword.mon_full_notm}} サービスへの発信ネットワーク・トラフィックを許可する必要があります。 
{:shortdesc}


## 取り込みエンドポイント
{: #network_send}

メトリック・データを {{site.data.keyword.mon_full_notm}} サービスに送信するには、ホスト内で次のファイアウォール・ルールを定義する必要があります。

| 地域      | 取り込みエンドポイント                                | パブリック IP アドレス               | ポート    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `US South`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | TCP 6443 | 
{: caption="表 1. メトリックを送信するための IP アドレス" caption-side="top"}



## Web UI エンドポイント
{: #network_ui}

{{site.data.keyword.mon_full_notm}} Web UI にアクセスするには、ホスト内で次のファイアウォール・ルールを定義する必要があります。

| 地域      | Web UI エンドポイント                                   | パブリック IP アドレス                                    | ポート   |
|-------------|---------------------------------------------------|--------------------------------------------------------|---------|
| `US South`  | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
{: caption="表 2. {{site.data.keyword.mon_full_notm}} Web UI にアクセスするための IP アドレス" caption-side="top"}


