---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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


# コンプライアンス
{: #compliance}

[{{site.data.keyword.Bluemix}} は、IBM の厳格なセキュリティー標準に組み込まれたクラウド・プラットフォームとサービスを提供します。](/docs/security/compliance.html#compliance) {{site.data.keyword.monitoringlong}} サービスは、{{site.data.keyword.Bluemix_notm}} 用にビルドされた DevOps サービスです。 
{:shortdesc}


## 一般的なデータ保護規則

一般データ保護規則 (GDPR、General Data Protection Regulation) は、EU 全体で調和のとれたデータ保護法の枠組みの作成に努め、世界のどこでも、これらのデータをホスティングし、「処理する」上で厳格なルールを課す一方、市民に自分の個人データの制御を取り戻すことを目指しています。 規制はまた、EU 内外の個人データの自由な動きに関連するルールを導入します。 

**特記事項:** {{site.data.keyword.monitoringshort}} サービスは、{{site.data.keyword.Bluemix_notm}} のアカウントで実行されるクラウド・リソースのメトリックと、{{site.data.keyword.Bluemix_notm}} の外部から送信する可能性のあるメトリックを格納して表示します。 個人情報 (PI、Personal Information ) は、{{site.data.keyword.monitoringshort}} に格納されているメトリック・エントリーのいずれにも含まれていないため、このデータは、企業内の他のユーザーがアクセスできると同時に、{{site.data.keyword.IBM_notm}} に対してもクラウド・サービスをサポートできるようにする必要があります。

### 地域
{: #regions}

{{site.data.keyword.monitoringshort}} サービスは、サービスが使用可能な {{site.data.keyword.Bluemix_notm}} パブリック地域の GDPR に準拠しています。


### データ保存
{: #data_retention}

{{site.data.keyword.monitoringshort}} サービスは、標準サービス・プランまたはライト・サービス・プランの 15 日間、およびプレミアム・プランの 45 日間のメトリックを保管します。


### データ削除
{: #data_deletion}

以下の情報を考慮してください。

* {{site.data.keyword.monitoringshort}} サービスの標準サービス・プランまたはライト・サービス・プランの場合、メトリックは 15 日後に自動的に削除されます。
* {{site.data.keyword.monitoringshort}} サービスのプレミアム・サービス・プランの場合、メトリックは 45 日後に自動的に削除されます。
* アクティブではないメトリックは、7 日後に自動的に削除されます。


 メトリックは、メトリック API を使用して、いつでも削除できます。 



### 詳細情報
{: #info}

詳しくは、以下を参照してください。

[{{site.data.keyword.Bluemix_notm}} セキュリティー・コンプライアンス](/docs/security/compliance.html#compliance)

[GDPR - {{site.data.keyword.IBM_notm}} 公式ページ](https://www.ibm.com/data-responsibility/gdpr/)



