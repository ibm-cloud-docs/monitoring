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



# 使用 Grafana 的常見問題
{: #grafana_qa}

以下是關於搭配使用 Grafana 與 {{site.data.keyword.monitoringshort}} 服務的常見問題與解答。
{:shortdesc}

* [我看不到在 Grafana 儀表板中使用 Alerts API 所定義的警示](/docs/services/cloud-monitoring/qa/grafana_qa.html#alerts1)
* [嘗試儲存對 Grafana 儀表板進行的變更時收到 BXNMSAL41E](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL41E)
* [將警示新增至 Grafana 儀表板之後，當我嘗試儲存變更時收到 BXNMSAL36E](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL36E)
* [登入監視服務 Web 使用者介面時顯示 404](/docs/services/cloud-monitoring/qa/grafana_qa.html#404)
* [我只上傳了 Grafana 儀表板的 json 資料，為何捲軸消失？](/docs/services/cloud-monitoring/qa/grafana_qa.html#2)


## 我看不到在 Grafana 儀表板中使用 Alerts API 所定義的警示
{: #alerts1}

Grafana 的警示標籤中未顯示使用 Alerts API 所定義的警示。若要查看 Grafana 中的警示，您必須直接在 Grafana 儀表板中定義它們。

如需相關資訊，請參閱[在 Grafana 中配置警示](/docs/services/cloud-monitoring/alerts/config_alerts_grafana.html#config_alerts_grafana)。

## 嘗試儲存對 Grafana 儀表板進行的變更時收到 BXNMSAL41E
{: #BXNMSAL41E}

您可以在 Grafana 中定義通知通道及警示。如果您在 Grafana 中刪除通知通道，而且未更新可移除該通知通道的規則，則會在嘗試儲存 Grafana 儀表板時收到 **BXNMSAL41E** 錯誤。

若要修正問題，請使用 Alerts API 來更新規則，並重試儲存儀表板。當您更新規則時，請移除已刪除的通知通道。

如需相關資訊，請參閱 [Alerts API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction)。

## 將警示新增至 Grafana 儀表板之後，當我嘗試儲存變更時收到 BXNMSAL36E
{: #BXNMSAL36E}

如果您達到在 {{site.data.keyword.monitoringshort}} 服務中監視度量值之網域的配額，則會收到下列錯誤：**BXNMSAL36E**

請升級方案，然後重試。

如需如何升級方案的相關資訊，請參閱[變更方案](/docs/services/cloud-monitoring/plan/change_plan.html#change_plan)。


## 使用 UAA 鑑別模型登入監視服務 Web 使用者介面時顯示 404
{: #404}

當您嘗試登入 {{site.data.keyword.monitoringshort}} 服務 Web 使用者介面 (Grafana) 時，如果顯示 404，請確認該空間存在，並確認您具有其存取權。

使用 [UAA 鑑別模型](/docs/services/cloud-monitoring/security/auth_uaa.html#auth_uaa)來存取 {{site.data.keyword.monitoringshort}} 服務時，您必須使用您用來登入 {{site.data.keyword.Bluemix_notm}} 主控台的相同使用者 ID 及密碼。 

若要驗證您有權可存取要登入的帳戶、組織及空間，請登入 {{site.data.keyword.Bluemix_notm}} 主控台並切換至空間。 

您也可以使用指令行，來驗證您有權可存取該空間。請執行下列指令，以登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間：

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

請遵循指示。輸入您的 {{site.data.keyword.Bluemix_notm}} 認證，選取組織及空間。


## 我只上傳了 Grafana 儀表板的 JSON 資料，為何捲軸會消失？
{: #2}

Grafana 中有一個錯誤，會在您匯入儀表板之後隱藏捲軸。 

若要看到捲軸，請在匯入儀表板之後儲存儀表板。 








