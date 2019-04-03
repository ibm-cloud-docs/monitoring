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

在 {{site.data.keyword.Bluemix}} 中，會自動收集 {{site.data.keyword.messagehub}} 度量值。進出主題的位元組數都會收集。每 15 分鐘會取得一個檢查點。您可以使用 Grafana 將這些度量值視覺化。
{:shortdesc}


**附註**：{{site.data.keyword.messagehub}} 度量值可用於 {{site.data.keyword.messagehub}} 標準方案，且僅限美國南部、英國及雪梨。 




## 檢視及分析度量值
{: #view}

若要在 {{site.data.keyword.Bluemix_notm}} 中監視 {{site.data.keyword.messagehub}} 的效能，請使用 Grafana。{{site.data.keyword.messagehub}} 提供一個儀表板，以用來檢視及監視您的主題的效能。

{{site.data.keyword.monitoringlong}} 服務使用 Grafana（一種開放程式碼分析與視覺化平台），可用來以各種圖形（例如圖表和表格）監視、搜尋、分析及視覺化您的度量值。 

您可以使用下列任何方式來啟動 Grafana：

* 您可以在 {{site.data.keyword.Bluemix_notm}} 主控台中，按一下 {{site.data.keyword.messagehub}} 儀表板上的 **Grafana** 按鈕。

    Grafana 會在 {{site.data.keyword.messagehub}} 執行所在之處，{{site.data.keyword.Bluemix_notm}} 的空間環境定義內開啟。
    
* 您可以從 Web 瀏覽器直接啟動 Grafana。

    確認您位於 {{site.data.keyword.messagehub}} 實例執行所在的正確組織及空間。
    
    如需相關資訊，請參閱[從 Web 瀏覽器導覽至 Grafana 儀表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。
    

請考量下列資訊：

* 您必須在 {{site.data.keyword.messagehub}} 實例執行所在的相同 {{site.data.keyword.Bluemix_notm}} 地區中啟動 Grafana。
* 使用依預設提供的 Grafana 儀表板來開始監視您的 {{site.data.keyword.messagehub}} 實例。
* 建立自訂的 Grafana 儀表板，以建置特定儀表板。您可以在 Grafana 儀表板中定義一個以上的度量值查詢，以監視 {{site.data.keyword.messagehub}} 實例。如需相關資訊，請參閱[在 Grafana 中配置度量值查詢](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query#define_query)。
* 您也可以定義查詢的警示。如需相關資訊，請參閱[配置警示](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)。


## Kafka 主題的度量值
{: #kafka_topic_metrics}

針對每個已定義的 Kafka 主題，會收集下列度量值：


<table>
  <caption>每個 Kafka 主題的度量值</caption>
  <tr>
    <th>度量值</th>
    <th>說明</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Kafka 用戶端應用程式傳送至主題的位元組速率。</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Kafka 用戶端應用程式從主題收到的位元組速率。</td>
  </tr>
</table>



## Kafka 分割區的度量值
{: #kafka_partition_metrics}

針對具有耗用訊息之 Cloud Storage 橋接器的每個 Kafka 分割區，會收集下列度量值：


<table>
  <caption>Kafka 分割區度量值</caption>
  <tr>
    <th>度量值</th>
    <th>說明</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>Cloud Storage 橋接器所處理的最後一個 Kafka 記錄的偏移。</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>Cloud Storage 橋接器所處理的 Kafka 記錄的已確定偏移。</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Cloud Storage 橋接器從 Kafka 主題收到的訊息數。只會計算包含有效 JSON 且無法由橋接器處理的訊息。</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Cloud Storage 橋接器從 Kafka 主題收到的訊息數。只會計算包含因為資料不是有效 JSON 文件而無法剖析之資料的訊息。</td>
  </tr>
</table>




## 參考資料
{: #mhlinks}

* [開始使用 Message Hub](/docs/services/EventStreams?topic=eventstreams-getting_started#getting_started)
* [監視及記載](/docs/services/EventStreams/messagehub072.html#monitoring)

