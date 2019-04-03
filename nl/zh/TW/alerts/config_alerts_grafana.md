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

# 在 Grafana 中配置警示
{: #config_alerts_grafana}

{{site.data.keyword.monitoringshort}} 服務提供以查詢為基礎的警示系統。您可以在沒有範本變數的儀表板上，於 Grafana 中配置警示。
{:shortdesc}

若要透過 Grafana 使用者介面配置度量值查詢的警示，請完成下列步驟：

1. 啟動 Grafana。
2. 定義一個以上的通知通道。
3. 建立 Grafana 儀表板，以包括「圖形」及至少一個查詢度量值。 
4. 透過 Grafana 圖形上的**警示**標籤，以配置警示。

## 步驟 1：啟動 Grafana
{: #step1_cag1}

從瀏覽器啟動 Grafana。例如，輸入下列 URL，以在「美國南部」地區中開啟 Grafana：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

如需每個地區的 Grafana URL 清單，請參閱 [{{site.data.keyword.monitoringshort}} 服務的 URL](/docs/services/cloud-monitoring/monitoring_ov.html#region)。

## 步驟 2：定義一個以上的通知通道
{: #step2_cag2}

請完成下列步驟：

1. 在 Grafana 中，選取側邊功能表列。

2. 選取**警示 > 通知通道 > 新建通道**。

3. 輸入新通道的資料。例如，新增電子郵件通知通道。

<table>
  <caption>您必須輸入以建立新通道的電子郵件通知方法及資料</caption>
  <tr>
     <th>欄位</th>
     <th>說明</th>
  </tr>
  <tr>
    <td>名稱</td>
    <td>通知通道的名稱。此值必須是唯一的。</td>
  </tr>
  <tr>
    <td>說明</td>
    <td>您可能要基於文件用途而包括的其他資訊。</td>
  </tr>
  <tr>
    <td>類型</td>
    <td>選取：**電子郵件**</td>
  </tr>
  <tr>
    <td>電子郵件 ID</td>
    <td>輸入收件者的電子郵件位址。</br>您可以輸入以逗點區隔的多個電子郵件位址。</td>
  </tr>
</table>

<table>
  <caption>您必須輸入以建立新通道的 Webhook 通知方法及資料</caption>
  <tr>
     <th>欄位</th>
     <th>說明</th>
  </tr>
  <tr>
    <td>名稱</td>
    <td>通知通道的名稱。此值必須是唯一的。</td>
  </tr>
  <tr>
    <td>說明</td>
    <td>您可能要基於文件用途而包括的其他資訊。</td>
  </tr>
  <tr>
    <td>類型</td>
    <td>選取：**Webhook**</td>
  </tr>
  <tr>
    <td>Webhook POST URL</td>
    <td>輸入應該進行 POST 的 URL。</td>
  </tr>
  <tr>
    <td>Webhook 標頭</td>
    <td>輸入任何標頭。</td>
  </tr>
  <tr>
    <td>Webhook 查詢參數</td>
    <td>輸入任何查詢參數。</td>
  </tr>
</table>

<table>
  <caption>您必須輸入以建立新通道的 PagerDuty 通知方法及資料</caption>
  <tr>
     <th>欄位</th>
     <th>說明</th>
  </tr>
  <tr>
    <td>名稱</td>
    <td>通知通道的名稱。此值必須是唯一的。</td>
  </tr>
  <tr>
    <td>說明</td>
    <td>您可能要基於文件用途而包括的其他資訊。</td>
  </tr>
  <tr>
    <td>類型</td>
    <td>選取：**PagerDuty**</td>
  </tr>
  <tr>
    <td>PagerDuty API 金鑰</td>
    <td>輸入 PagerDuty 金鑰。</td>
  </tr>
</table>

## 步驟 3：定義度量值
{: #step3_cag3}

請完成下列步驟，以建立新的儀表板：

1. 選取側邊功能表列切換 ![Grafana 側邊功能表列](images/grafana_settings.gif "Grafana 側邊功能表列")。
2. 選取**儀表板**。
3. 按一下**新建**。

即會開啟儀表板。儀表板包括已備妥可進行配置的空白列。 

接下來，新增度量值查詢：

1. 新增*圖形*畫面。
2. 選取**圖形**。
3. 按一下圖形標題，然後選取**編輯**。
    
    即會開啟*度量值*標籤。您可以在這裡看到預設資料來源。
    
4. 定義過濾圖形中所顯示資料的度量值查詢。 


## 步驟 4：定義警示
{: #step4_cag4}

請完成下列步驟，以在 Grafana 使用者介面中定義警示：

1. 選取**警示**標籤。
2. 在**警示配置**區段中，定義規則，以定義用來產生警示通知的條件。

    配置**評估的間隔**欄位及**條件**區段。

3. 在**通知**區段中，選取一個以上的通知通道。

**附註：** 

* 設定條件時，您可以在圖形上看到紅色線條，以定義臨界值集。您可以在圖形上拖曳它，以進行變更。
* 建立警示之後，如果您要進行修改，則必須使用 Alerts API 來執行它。
* 如果您選取**刪除**，則會刪除警示。

## 下一步：驗證已產生警示
{: #next_cag5}

例如，如果您已建立電子郵件通知通道，請檢查電子郵件。

尋找寄件者為 **IBM Cloud Monitoriing** 的電子郵件。

電子郵件包括所發出警示的資訊，以及您可在其中檢視狀況之 Grafana 儀表板的鏈結。

例如：

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


