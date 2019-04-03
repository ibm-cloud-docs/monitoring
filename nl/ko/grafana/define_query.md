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


# Grafana에서 메트릭 조회 구성
{: #define_query}

{{site.data.keyword.Bluemix}}에서는 선택된 클라우드 서비스의 메트릭이 자동으로 수집됩니다. {{site.data.keyword.monitoringlong}}을 통해 모니터링하려면 Grafana 조회를 정의해야 합니다. 
{:shortdesc}

## 1단계: 모니터링할 CF 앱 또는 서비스에 대한 데이터 수집
{: #step18}

모니터링할 CF 앱 또는 서비스에 대해 다음 정보를 얻으십시오.

* CF 앱이 실행 중인 **지역**
* CF 앱이 실행 중인 **조직** 	
* CF 앱이 실행 중인 **영역** 
* 모니터링할 앱의 **CF 앱 이름** 또는 **서비스 이름** 


## 2단계: Grafana 실행
{: #step27}

브라우저에서 Grafana를 실행하십시오. 자세한 정보는 [웹 브라우저에서 Grafana 대시보드로 이동](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser)을 참조하십시오.

Grafana에서 CF 앱 또는 서비스가 실행 중인 계정, 조직 및 지역에 로그인되어 있는지 확인하십시오. 


## 3단계: Grafana에서 조회 정의
{: #step36}

Grafana 대시보드를 작성하고 조회를 정의하려면 다음 단계를 완료하십시오.

1. 새 대시보드를 작성하십시오.

    * 측면 메뉴 표시줄 토글 ![Grafana 측면 메뉴 표시줄](images/grafana_settings.gif "Grafana 측면 메뉴 표시줄")을 선택하십시오.
    * **대시보드**를 선택하십시오.
    * **새로 작성**을 클릭하십시오.

    대시보드가 열립니다. 이 대시보드는 구성할 준비가 된 비어 있는 행을 포함하고 있습니다.

2. *그래프* 패널을 추가하십시오.

    1. **그래프**를 선택하십시오.

    2. 그래프 제목을 클릭한 후 **편집**을 선택하십시오.

        *메트릭* 탭이 열립니다. 여기서는 기본 데이터 소스를 볼 수 있습니다.

3. 그래프에 표시되는 데이터를 필터링하는 조회를 정의하십시오. 

    *메트릭* 탭에서 **조회 추가**를 선택하십시오. <br>조회 항목이 추가됩니다. 각 조회는 하나의 문자로 레이블 지정됩니다.
    
    ![새 조회 항목](images/grafana4_query_f1.gif "새 조회 항목")
        
    1. **메트릭 선택**을 클릭한 다음 소스: `ibmcloud`를 선택하십시오.
    
    2. **메트릭 선택**을 클릭한 다음 클라우드 유형: `public`을 선택하십시오.
    
    3. **메트릭 선택**을 클릭한 다음 서비스 이름을 선택하십시오. 예를 들어, CF 앱 메트릭의 경우 `cloud-foundry`를 선택하고 {{site.data.keyword.messagehub}} 메트릭의 경우 `message hub`를 선택하십시오.
    
    4. **메트릭 선택**을 클릭한 다음 작업 중인 지역을 선택하십시오. 예를 들어, 미국 남부 지역의 경우, `ng`입니다.
    
    5. 모니터링할 서비스 또는 CF 앱에 적용되는 특정 서비스 필드를 선택하십시오.

        <table>
          <caption>서비스 또는 CF 앱별 메트릭 조회 형식</caption>
          <tr>
            <th>서비스 이름</th>
            <th>메트릭 조회 형식에 대한 링크</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[컨테이너에 대해 수집된 CPU 메트릭의 조회 형식](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers) </br>[작업자에 대해 수집된 로드 메트릭의 조회 형식](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers) </br>[컨테이너에 대해 수집된 메모리 메트릭의 조회 형식](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)</td> 
          </tr>
          <tr>
            <td>CF 앱</td>
            <td>[CF 앱의 조회 형식](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format)</td> 
          </tr>
        </table>

        예를 들어, CF 앱의 경우, 다음을 선택하십시오.
    
        **메트릭 선택**을 클릭한 다음 CF 앱 이름을 선택하십시오. 예를 들어, `logtester`입니다.
    
        **메트릭 선택**을 클릭한 다음 CF 앱 인스턴스 인덱스를 선택하십시오. 예를 들어, `0`입니다.

        **메트릭 선택**을 클릭한 다음 `컨테이너`를 선택하십시오.
    
    9. **메트릭 선택**을 클릭한 다음 메트릭 유형을 선택하십시오. 예를 들어, CPU 메트릭의 경우 **cpu**이며 메모리 메트릭의 경우 **memory**이며 디스크 메모리의 경우 **disk**입니다. 

        **참고:** CF 앱에 대해서는 이 단계를 건너뛰십시오. 

    10. **메트릭 선택**을 클릭한 다음 메트릭을 선택하십시오. 

        <table>
          <caption>서비스 또는 CF 앱별 메트릭 목록</caption>
          <tr>
            <th>서비스 이름</th>
            <th>메트릭에 링크</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[CPU 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[디스크 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[메모리 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>CF 앱</td>
            <td>[CPU 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics)  </br>[디스크 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[메모리 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Kafka 토픽에 대한 메트릭](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_topic_metrics) </br>[Kafka 파티션에 대한 메트릭](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. 더하기 이미지 ![추가 아이콘](images/grafana_plus_image.gif "더하기 이미지")를 클릭하고 함수를 선택하십시오. 함수를 추가하여 메트릭에 대해 사용 가능한 데이터를 변환하거나, 결합하거나, 이에 대한 계산을 수행할 수 있습니다.
        
        예를 들면, **alias(newName)** 함수를 추가하여 메트릭에 대해 별명을 추가할 수 있습니다. 이 별명은 그래프에 표시되는 범례에 메트릭 이름 대신 문자열을 인쇄하는 데 사용됩니다.
        
        메트릭에 대해 별명을 추가하려면 다음 단계를 완료하십시오.
        
        1. 더하기 기호를 클릭하십시오.
        2. **특수**를 선택하십시오. 
        3. **별명**을 선택하십시오.
        4. 문자열(예: `My sample metric`)을 입력하십시오.


## 4단계: 나중에 재사용할 수 있도록 대시보드 저장
{: #step44}

다음 단계를 완료하십시오.

1. 대시보드 저장 이미지 ![대시보드 저장 이미지](images/grafana_save_image.gif "대시보드 저장 이미지")를 클릭하십시오.
2. 대시보드의 이름을 입력하십시오.
3. **저장**을 클릭하십시오.
