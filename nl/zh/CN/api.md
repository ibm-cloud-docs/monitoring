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

使用 Sysdig REST API 可自动执行例程任务和监视通知。
{:shortdesc}

通过定制脚本或程序使用 API 时，必须使用 Sysdig 令牌向 {{site.data.keyword.mon_full_notm}} 实例进行认证。
{: tip}

## 使用 API 创建仪表板
{: #api_create_dashboard}

可以通过复制现有仪表板来创建仪表板。  

要创建仪表板，请完成以下步骤：

1. 获取要保存其仪表板的团队的 Sysdig API 令牌。有关更多信息，请参阅[获取 Sysdig API 令牌](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)。

2. 创建用于描述仪表板的 JSON 文件。以下字段必须如下所示进行设置：

    * *name*：输入仪表板的名称。

    * *id*：设置为 *null*。

    * *version*：设置为 *null*。

    * username：设置为与 IBM 标识关联的电子邮件。

    * *isShared*：设置为 true 可与其他团队成员共享仪表板。

    * *isPublic*：如果希望仪表板公开可用，请设置为 true。

    * 配置过滤器以定义仪表板作用域。
    
3. 创建仪表板。运行以下 cURL 命令：

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    其中

    * *ENDPOINT* 是监视实例在其中可用的区域的 URL。有关更多信息，请参阅 [Sysdig 端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)。

    * *SYSDIG_API_TOKEN* 是上一步中获取的 API 令牌。

    * *dashboard.json* 是描述新仪表板的文件，包括面板和度量值。

例如，要创建仪表板，样本 JSON 文件如下所示：
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



## 使用 API 保存团队的仪表板
{: #api_save_dashboard}

要下载可供团队使用的仪表板，请完成以下步骤：

1. 获取要保存其仪表板的团队的 Sysdig API 令牌。有关更多信息，请参阅[获取 Sysdig API 令牌](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)。

2. 运行以下 cURL 命令：

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    其中

    * *ENDPOINT* 是监视实例在其中可用的区域的 URL。有关更多信息，请参阅 [Sysdig 端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)。

    * *SYSDIG_API_TOKEN* 是上一步中获取的 API 令牌。

例如，要为在美国南部区域工作的团队下载仪表板，可以运行以下命令：

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

输出是一个 JSON 文件，其中每个仪表板均以 **id** 字段开头。仪表板的名称在 **name** 字段中指定。


## 使用 API 删除仪表板
{: #api_delete_dashboard}

要从可供团队使用的仪表板列表中删除仪表板，请完成以下步骤：

1. 获取要保存其仪表板的团队的 Sysdig API 令牌。有关更多信息，请参阅[获取 Sysdig API 令牌](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)。

2. 获取可供团队使用的所有仪表板。有关更多信息，请参阅[使用 API 保存仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard)。

3. 查找要删除的仪表板的标识。查找与要删除的仪表板 **name** 关联的 **id** 值。

4. 运行以下 cURL 命令：

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    其中

    * *ID* 是要删除的仪表板的标识。

    * *ENDPOINT* 是监视实例在其中可用的区域的 URL。有关更多信息，请参阅 [Sysdig 端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)。

    * *SYSDIG_API_TOKEN* 是上一步中获取的 API 令牌。

例如，对于供在美国南部区域工作的团队使用的仪表板列表，要从中删除标识为 *391* 的仪表板，可以运行以下命令：

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




