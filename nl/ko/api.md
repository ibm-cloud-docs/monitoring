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


# Sysdig REST API 관련 작업
{: #api}

Sysdig REST API를 사용하여 일상적인 태스크를 자동화하고 알림을 모니터할 수 있습니다.
{:shortdesc}

사용자 정의 스크립트나 프로그램에서 API를 사용할 때는 Sysdig 토큰을 사용하여 {{site.data.keyword.mon_full_notm}} 인스턴스를 인증해야 합니다. 
{: tip}

## API를 사용하여 대시보드 작성
{: #api_create_dashboard}

기존 대시보드를 복제하여 대시보드를 작성할 수 있습니다.  

대시보드를 작성하려면 다음 단계를 완료하십시오.

1. 해당 대시보드를 저장하고자 하는 팀에 대한 Sysdig API 토큰을 가져오십시오. 자세한 정보는 [Sysdig API 토큰 가져오기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)를 참조하십시오.

2. 대시보드를 기술하는 json 파일을 작성하십시오. 표시된 대로 다음 필드를 설정해야 합니다.

    * *이름*: 대시보드의 이름을 입력하십시오．

    * *id*: *null*로 설정하십시오.

    * *버전*: *null*로 설정하십시오.

    * 사용자 이름: IBM ID와 연관된 이메일로 설정하십시오.

    * *isShared*: 기타 팀 구성원과 대시보드를 공유하려면 true로 설정하십시오.

    * *isPublic*: 대시보드가 공개적으로 사용 가능하도록 하려면 true로 설정하십시오.

    * 대시보드 범위를 정의하기 위한 필터를 구성하십시오.
    
3. 대시보드를 작성하십시오. 다음 cURL 명령을 실행하십시오.

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    여기서

    * *ENDPOINT*는 모니터링 인스턴스가 사용 가능한 지역의 URL입니다. 자세한 정보는 [Sysdig 엔드포인트](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)를 참조하십시오.

    * *SYSDIG_API_TOKEN*은 이전 단계에서 가져온 API 토큰입니다.

    * *dashboard.json*은 패널 및 메트릭을 포함하여 새 대시보드를 기술하는 파일입니다.

예를 들어, 대시보드를 작성하기 위한 샘플 json 파일은 다음과 같습니다.
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



## API를 사용하여 팀의 대시보드 저장
{: #api_save_dashboard}

팀에서 사용할 수 있는 대시보드를 다운로드하려면 다음 단계를 완료하십시오.

1. 해당 대시보드를 저장하고자 하는 팀에 대한 Sysdig API 토큰을 가져오십시오. 자세한 정보는 [Sysdig API 토큰 가져오기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)를 참조하십시오.

2. 다음 cURL 명령을 실행하십시오.

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    여기서

    * *ENDPOINT*는 모니터링 인스턴스가 사용 가능한 지역의 URL입니다. 자세한 정보는 [Sysdig 엔드포인트](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)를 참조하십시오.

    * *SYSDIG_API_TOKEN*은 이전 단계에서 가져온 API 토큰입니다.

예를 들어, 미국 남부 지역에서 작업 중인 팀의 대시보드를 다운로드하려면 다음 명령을 실행할 수 있습니다.

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

출력은 각 대시보드가 **id** 필드로 시작하는 JSON 파일입니다. 대시보드의 이름은 **이름** 필드에 지정되어 있습니다.


## API를 사용하여 대시보드 삭제
{: #api_delete_dashboard}

팀에서 사용할 수 있는 대시보드의 목록에서 대시보드를 삭제하려면 다음 단계를 완료하십시오.

1. 해당 대시보드를 저장하고자 하는 팀에 대한 Sysdig API 토큰을 가져오십시오. 자세한 정보는 [Sysdig API 토큰 가져오기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get)를 참조하십시오.

2. 팀에서 사용할 수 있는 모든 대시보드를 가져오십시오. 자세한 정보는 [API를 사용하여 대시보드 저장](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard)을 참조하십시오.

3. 삭제할 대시보드의 ID를 찾으십시오. 삭제할 대시보드 **이름**과 연관된 **id** 값을 찾으십시오.

4. 다음 cURL 명령을 실행하십시오.

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    여기서

    * *ID*는 삭제할 대시보드의 ID입니다.

    * *ENDPOINT*는 모니터링 인스턴스가 사용 가능한 지역의 URL입니다. 자세한 정보는 [Sysdig 엔드포인트](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints)를 참조하십시오.

    * *SYSDIG_API_TOKEN*은 이전 단계에서 가져온 API 토큰입니다.

예를 들어, 미국 남부 지역에서 작업 중인 팀의 대시보드 목록에서 ID *391*의 대시보드를 삭제하려면 다음 명령을 실행할 수 있습니다.

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




