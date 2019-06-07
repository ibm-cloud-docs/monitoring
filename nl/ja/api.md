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


# Sysdig REST API の管理
{: #api}

Sysdig REST API を使用して、ルーチン・タスクを自動化し、通知をモニターします。
{:shortdesc}

カスタム・スクリプトまたはカスタム・プログラムから API を使用する場合は、Sysdig トークンを使用して {{site.data.keyword.mon_full_notm}} インスタンスで認証する必要があります。 
{: tip}

## API を使用したダッシュボードの作成
{: #api_create_dashboard}

既存のダッシュボードを複製することによって、ダッシュボードを作成できます。  

ダッシュボードを作成するには、以下のステップを実行します。

1. ダッシュボードを保存するチームの Sysdig API トークンを取得します。 詳しくは、[Sysdig API トークンの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)を参照してください。

2. ダッシュボードが記述される json ファイルを作成します。 以下のように各フィールドを設定してください。

    * `name`: ダッシュボードの名前を入力します。

    * `id`: *null* に設定します。

    * `version`: *null* に設定します。

    * `username`: IBMid と関連付けた E メールに設定します。

    * `isShared`: true に設定して他のチーム・メンバーとダッシュボードを共有します。

    * `isPublic`: ダッシュボードをパブリックに使用可能にする場合は true に設定します。

    * ダッシュボードの有効範囲を定義するフィルターを構成します。
    
3. ダッシュボードを作成します。 次の cURL コマンドを実行します。

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    説明

    * *ENDPOINT* は、モニタリング・インスタンスが使用可能な地域の URL です。 詳しくは、[Sysdig エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)を参照してください。

    * *SYSDIG_API_TOKEN* は、前のステップで取得した API トークンです。

    * *dashboard.json* は、パネルやメトリックを含め、新しいダッシュボードが記述されるファイルです。

例えば、ダッシュボードを作成するサンプルの json ファイルは以下のようになります。
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



## API を使用したチームのダッシュボードの保存
{: #api_save_dashboard}

チームが使用できるダッシュボードをダウンロードするには、以下のステップを実行します。

1. ダッシュボードを保存するチームの Sysdig API トークンを取得します。 詳しくは、[Sysdig API トークンの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)を参照してください。

2. 次の cURL コマンドを実行します。

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    説明

    * *ENDPOINT* は、モニタリング・インスタンスが使用可能な地域の URL です。 詳しくは、[Sysdig エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)を参照してください。

    * *SYSDIG_API_TOKEN* は、前のステップで取得した API トークンです。

例えば、米国南部地域で作業するチームのダッシュボードをダウンロードするには、以下のコマンドを実行します。

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

出力は、各ダッシュボードが **id** フィールドで開始される JSON ファイルです。 ダッシュボードの名前は、**name** フィールドに指定されます。


## API を使用したダッシュボードの削除
{: #api_delete_dashboard}

チームが使用可能なダッシュボードのリストからダッシュボードを削除するには、以下のステップを実行します。

1. ダッシュボードを保存するチームの Sysdig API トークンを取得します。 詳しくは、[Sysdig API トークンの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)を参照してください。

2. チームが使用可能なすべてのダッシュボードを取得します。 詳しくは、[API を使用したダッシュボードの保存](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard)を参照してください。

3. 削除するダッシュボードの ID を見つけます。 削除するダッシュボードの **name** に関連付けられている **id** 値を探します。

4. 次の cURL コマンドを実行します。

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    説明

    * *ID* は、削除するダッシュボードの ID です。

    * *ENDPOINT* は、モニタリング・インスタンスが使用可能な地域の URL です。 詳しくは、[Sysdig エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)を参照してください。

    * *SYSDIG_API_TOKEN* は、前のステップで取得した API トークンです。

例えば、米国南部地域で作業するチームのダッシュボードのリストから ID が *391* のダッシュボードを削除するには、以下のコマンドを実行します。

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




