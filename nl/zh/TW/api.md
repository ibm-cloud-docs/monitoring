---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, sysdig rest api

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


# 使用 Sysdig REST API
{: #api}

使用 Sysdig REST API，將例行作業及監視通知自動化。
{:shortdesc}

從您的自訂 Script 或程式中使用 API 時，您必須使用 Sysdig 記號，透過 {{site.data.keyword.mon_full_notm}} 實例進行鑑別。
{: tip}

## 使用 API 來建立儀表板
{: #api_create_dashboard}

您可以複製現有儀表板來建立儀表板。  

請完成下列步驟來建立儀表板：

1. 取得您要儲存其儀表板之團隊的 Sysdig API 記號。如需相關資訊，請參閱[取得 Sysdig API 記號](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)。

2. 建立說明儀表板的 json 檔案。下列欄位必須依指示設定：

    * *名稱*：輸入儀表板的名稱。

    * *ID*：設為*空值*。

    * *版本*：設為*空值*。

    * 使用者名稱：設為與您的 IBM ID 相關聯的電子郵件。

    * *isShared*：設為 true 以與其他團隊成員共用儀表板。

    * *isPublic*：如果您要讓儀表板變成公用，請設為 true。

    * 配置過濾器以定義儀表板範圍。
    
3. 建立儀表板。執行下列 cURL 指令：

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    其中

    * *ENDPOINT* 是可以使用監視實例之地區的 URL。如需相關資訊，請參閱 [Sysdig 端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)。

    * *SYSDIG_API_TOKEN* 是您在前一個步驟中取得的 API 記號。

    * *dashboard.json* 是說明新儀表板的檔案，其中包括畫面及度量。

例如，若要建立儀表板，範例 JSON 檔案如下所示：
```
{
  "dashboard": {
    "filterExpression": null,
    "name": "My new dashboard",
    "items": [
      {
        "customDisplayOptions": {
          "yAxisLeftDomain": {
            "to": null,
            "from": 0
          },
          "yAxisScale": "linear",
          "yAxisRightDomain": {
            "to": null,
            "from": 0
          },
          "valueLimit": {
            "count": 10,
            "direction": "desc"
          },
          "histogram": {
            "numberOfBuckets": 10
          },
          "xAxis": {
            "to": null,
            "from": 0
          }
        },
        "name": "CPU usage",
        "overrideFilter": true,
        "showAsType": "line",
        "showAs": "timeSeries",
        "groupId": "My new cpu dashboardcontainer.namecarboncache1",
        "metrics": [
          {
            "propertyName": "k0",
            "metricId": "timestamp"
          },
          {
            "propertyName": "v0",
            "metricId": "cpu.used.percent",
            "aggregation": "avg",
            "groupAggregation": "avg"
          }
        ],
        "paging": {
          "to": 9,
          "from": 0
        },
        "compareToConfig": null,
        "gridConfiguration": {
          "size_y": 4,
          "size_x": 6,
          "col": 1,
          "row": 1
        },
        "filter": {
          "filters": {
            "filters": [
              {
                "metric": "container.name",
                "filters": null,
                "value": "carboncache",
                "op": "="
              }
            ],
            "logic": "and"
          }
        }
      }
    ],
    "isPublic": false,
    "annotations": {
      "createdByEngine": true
    },
    "username": "ENTER YOUR EMAIL ADDRESS",
    "version": null,
    "layout": [
      {
        "size_y": 4,
        "size_x": 6,
        "col": 1,
        "row": 1
      }
    ],
    "schema": 1,
    "id": null,
    "isShared": false
  }
}
```
{: screen}



## 使用 API 來儲存團隊的儀表板
{: #api_save_dashboard}

請完成下列步驟，以下載可供團隊使用的儀表板：

1. 取得您要儲存其儀表板之團隊的 Sysdig API 記號。如需相關資訊，請參閱[取得 Sysdig API 記號](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)。

2. 執行下列 cURL 指令：

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    其中

    * *ENDPOINT* 是可以使用監視實例之地區的 URL。如需相關資訊，請參閱 [Sysdig 端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)。

    * *SYSDIG_API_TOKEN* 是您在前一個步驟中取得的 API 記號。

例如，若要下載在美國南部地區工作之團隊的儀表板，您可以執行下列指令：

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

輸出是 JSON 檔案，其中每個儀表板都以 **ID** 欄位開始。儀表板的名稱在**名稱**欄位中指定。


## 使用 API 來刪除儀表板
{: #api_delete_dashboard}

請完成下列步驟，從可供團隊使用的儀表板清單中刪除儀表板：

1. 取得您要儲存其儀表板之團隊的 Sysdig API 記號。如需相關資訊，請參閱[取得 Sysdig API 記號](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)。

2. 取得所有可供團隊使用的儀表板。如需相關資訊，請參閱[使用 API 來儲存儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard)。

3. 尋找您要刪除的儀表板 ID。找出 **ID** 值，其與您要刪除的儀表板**名稱**相關聯。

4. 執行下列 cURL 指令：

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    其中

    * *ID* 是您要刪除的儀表板 ID。

    * *ENDPOINT* 是可以使用監視實例之地區的 URL。如需相關資訊，請參閱 [Sysdig 端點](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)。

    * *SYSDIG_API_TOKEN* 是您在前一個步驟中取得的 API 記號。

例如，若要從工作於美國南部地區之團隊的儀表板清單中刪除 ID 為 *391* 的儀表板，您可以執行下列指令：

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




