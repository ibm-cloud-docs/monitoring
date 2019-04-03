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



# {{site.data.keyword.messagehub}}
{: #monitoring_mh_ov}

{{site.data.keyword.Bluemix}} では、{{site.data.keyword.messagehub}} メトリックは自動的に収集されます。 トピックに送受信されたバイト数が収集されます。 収集のチェックポイントは 15 分ごとです。 Grafana を使用して、これらのメトリックを視覚化できます。 
{:shortdesc}


**注:** {{site.data.keyword.messagehub}} メトリックは、米国南部、英国、およびシドニーにおける {{site.data.keyword.messagehub}} 標準プランでのみ使用可能です。 




## メトリックの表示および分析
{: #view}

{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.messagehub}} のパフォーマンスをモニターするには、Grafana を使用します。 {{site.data.keyword.messagehub}} は、トピックのパフォーマンスを表示およびモニターするために使用できるダッシュボードを提供します。

{{site.data.keyword.monitoringlong}} サービスは、Grafana を使用します。Grafana は、さまざまなグラフ (例えば、チャートや表) でメトリックをモニター、検索、分析、および視覚化するために使用できる、分析および視覚化のためのオープン・ソース・プラットフォームです。 

Grafana は以下のいずれかの方法で起動できます。

* {{site.data.keyword.Bluemix_notm}} コンソールの {{site.data.keyword.messagehub}} ダッシュボードの**「Grafana」**ボタンをクリックすることができます。

    Grafana は、{{site.data.keyword.messagehub}} が実行されている {{site.data.keyword.Bluemix_notm}} のスペースのコンテキスト内で開きます。
    
* Web ブラウザーから直接 Grafana を起動することができます。

    {{site.data.keyword.messagehub}} インスタンスが実行されている正しい組織およびスペースにあることを確認します。
    
    詳しくは、[Web ブラウザーから Grafana ダッシュボードへのナビゲート](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)を参照してください。
    

以下の情報を考慮してください。

* Grafana は、{{site.data.keyword.messagehub}} インスタンスが実行されているのと同じ {{site.data.keyword.Bluemix_notm}} 地域で起動する必要があります。
* デフォルトで提供されている Grafana ダッシュボードを使用して、{{site.data.keyword.messagehub}} インスタンスのモニターを開始します。
* カスタム Grafana ダッシュボードを作成して、随時ダッシュボードをビルドします。 Grafana ダッシュボードで 1 つ以上のメトリック照会を定義して、{{site.data.keyword.messagehub}} インスタンスをモニターできます。 詳しくは、[Grafana でのメトリック照会の構成](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query#define_query)を参照してください。
* また、照会にアラートを定義することもできます。 詳しくは、[アラートの構成](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)を参照してください。


## Kafka トピックのメトリック
{: #kafka_topic_metrics}

定義されている各 Kafka トピックについて、以下のメトリックが収集されます。


<table>
  <caption>Kafka トピックごとのメトリック</caption>
  <tr>
    <th>メトリック</th>
    <th>説明</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Kafka クライアント・アプリケーションによってトピックに送信された単位時間あたりのバイト数。</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Kafka クライアント・アプリケーションによってトピックから受信された単位時間あたりのバイト数。</td>
  </tr>
</table>



## Kafka パーティションのメトリック
{: #kafka_partition_metrics}

メッセージをコンシュームするクラウド・ストレージ・ブリッジがある Kafka パーティションごとに、以下のメトリックが収集されます。


<table>
  <caption>Kafka パーティションのメトリック</caption>
  <tr>
    <th>メトリック</th>
    <th>説明</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>クラウド・ストレージ・ブリッジによって処理される最後の Kafka レコードのオフセット。</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>クラウド・ストレージ・ブリッジによって処理される Kafka レコードのコミット済みオフセット。</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Kafka トピックからクラウド・ストレージ・ブリッジ・インスタンスによって受信されるメッセージの数。 ブリッジで処理できない有効な JSON を含むメッセージのみをカウントします。</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Kafka トピックからクラウド・ストレージ・ブリッジ・インスタンスによって受信されるメッセージの数。 データが有効な JSON ドキュメントではないため、解析できなかったデータを含むメッセージのみをカウントします。</td>
  </tr>
</table>




## 参照
{: #mhlinks}

* [Message Hub の開始](/docs/services/EventStreams?topic=eventstreams-getting_started#getting_started)
* [モニタリングとロギング](/docs/services/EventStreams/messagehub072.html#monitoring)

