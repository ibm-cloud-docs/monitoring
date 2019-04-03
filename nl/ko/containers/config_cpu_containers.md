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


# Grafana에서 컨테이너에 대한 CPU 메트릭 구성
{: #config_cpu_containers}

{{site.data.keyword.Bluemix}}에서 컨테이너에 대해 선택된 CPU 메트릭이 자동으로 수집됩니다. {{site.data.keyword.monitoringlong}}을 통해 모니터링하려면 Grafana 조회를 정의해야 합니다. 
{:shortdesc}

자동으로 수집되는 CPU 메트릭에 대한 목록을 보려면 [컨테이너에 대한 CPU 메트릭](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers)을 참조하십시오.


## 1단계: 모니터링할 컨테이너에 대한 데이터 수집
{: #step15}

모니터링할 컨테이너에 대해 다음 정보를 얻으십시오.

* 클러스터가 실행 중인 **지역**
* 컨테이너가 실행 중인 **클러스터 이름** 	
* 컨테이너가 배치된 **네임스페이스** 

    네임스페이스는 클러스터 리소스를 그룹화하는 데 사용됩니다.
	
* 모니터링할 컨테이너와 연관된 **팟(Pod) 이름** 

    팟(Pod)은 스토리지 및 네트워크를 공유하고 클러스터 내에서 컨테이너를 실행하는 방법에 대한 세부사항이 있는 하나 이상의 컨테이너 그룹을 정의합니다.
	
* 모니터링할 컨테이너의 **컨테이너 이름**

메트릭이 영역 도메인 또는 계정 도메인에 전달되는지 여부를 확인하십시오.

클러스터가 메트릭을 전달하는 위치를 식별하려면 다음 명령을 실행하십시오.

```
$ ibmcloud cs cluster-get ClusterName --json
```
{: codeblock}

여기서, *ClusterName*은 클러스터의 이름입니다.

출력에서 다음 필드가 메트릭이 전달되는 위치에 대한 정보를 표시합니다.

* **logOrg**는 CF 조직의 ID를 정의합니다.
* **logOrgName**은 CF 조직의 이름을 정의합니다.
* **logSpace**는 CF 영역의 ID를 정의합니다.
* **logSpaceName**은 CF 영역의 이름을 정의합니다.

필드가 비어 있으면 메트릭이 계정 도메인으로 전달됩니다.
필드에 CF 조직 및 CF 영역 세트가 있는 경우, 메트릭이 이 영역과 연관된 영역 도메인으로 전달됩니다.

## 2단계: Grafana 실행
{: #step24}

브라우저에서 Grafana를 실행하십시오. 자세한 정보는 [웹 브라우저에서 Grafana 대시보드로 이동](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)을 참조하십시오.

Grafana에서 클러스터가 실행 중인 계정에 로그인되어 있는지 확인하십시오. 

1. 브라우저에서 Grafana를 실행하십시오. 

    클러스터를 작성한 지역에 대한 {{site.data.keyword.monitoringshort}} 서비스 URL을 입력하십시오. 
    
    지역별 URL을 가져오려면 [모니터링 서비스에 대한 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)을 참조하십시오.

    예를 들어, 미국 남부 지역의 경우 [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)을 실행하십시오.

2. 클러스터 메트릭을 볼 수 있는 {{site.data.keyword.monitoringshort} 도메인을 설정하십시오.

    Grafana에서 사용자 ID를 선택하십시오. 그런 다음, 올바른 계정인지 확인하고 도메인을 선택하십시오.

    연관된 CF 영역이 있는 클러스터가 메트릭을 영역 메트릭 도메인으로 전달합니다. `Domain = space`, 조직 및 클러스터와 연관된 영역을 선택하십시오.

    계정 레벨에서 작성된 클러스터가 메트릭을 계정 메트릭 도메인으로 전달합니다. `Domain = account`을 선택하십시오.




## 3단계: CPU 메트릭에 대한 Grafana에서 조회 정의
{: #step33}

다음 단계를 완료하여 Grafana 대시보드를 작성하고 컨테이너의 CPU 사용량을 모니터링할 조회를 정의하십시오.

1. 새 대시보드를 작성하십시오.

    * 측면 메뉴 표시줄 토글 ![Grafana 측면 메뉴 표시줄](images/grafana_settings.gif "Grafana 측면 메뉴 표시줄")을 선택하십시오.
    * **대시보드**를 선택하십시오.
    * **새로 작성**을 클릭하십시오.

    대시보드가 열립니다. 이 대시보드는 구성할 준비가 된 비어 있는 행을 포함하고 있습니다.

2. *그래프* 패널을 추가하여 팟(Pod)에 대한 CPU 메트릭을 모니터링하십시오.

    1. **그래프**를 선택하십시오.

    2. 그래프 제목을 클릭한 후 **편집**을 선택하십시오.

        *메트릭* 탭이 열립니다. 여기서는 기본 데이터 소스를 볼 수 있습니다.

3. 그래프에 표시되는 데이터를 필터링하는 조회를 정의하십시오. 

    조회의 형식에 대한 정보는 [컨테이너에 대해 수집된 CPU 메트릭의 조회 형식](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers)을 참조하십시오.

    *메트릭* 탭에서 **조회 추가**를 선택하십시오. </br>조회 항목이 추가됩니다. 각 조회는 하나의 문자로 레이블 지정됩니다.
	
	조회를 정의하려면 다음 단계를 완료하십시오.
	
    1. **메트릭 선택**을 클릭하여 소스를 지정한 후 `ibmcloud`를 선택하십시오.
    
    2. **메트릭 선택**을 클릭하여 클라우드 유형을 지정한 후 `public`을 선택하십시오.
    
    3. **메트릭 선택**을 클릭하여 서비스 이름을 지정한 후 `containers-kubernetes`를 선택하십시오.
	
    4. **메트릭 선택**을 클릭하여 지역을 지정한 후 클러스터가 실행 중인 지역을 선택하십시오. 예를 들어, `us-south`입니다.
    
    5. **메트릭 선택**을 클릭하여 클러스터 이름을 지정한 후 컨테이너가 실행 중인 클러스터의 이름을 선택하십시오.
		
	6. **메트릭 선택**을 클릭하여 메트릭 소스를 지정하십시오. **컨테이너**를 선택하십시오.
		
	7. **메트릭 선택**을 클릭하여 네임스페이스를 지정하십시오. 그런 다음 컨테이너와 연관된 클러스터의 네임스페이스 이름을 입력하십시오.
		
	8. **메트릭 선택**을 클릭하여 팟(Pod) 이름을 지정하십시오.
	
	9. **메트릭 선택**을 클릭하여 모니터링할 컨테이너의 컨테이너 이름을 지정하십시오.
	
	10. **메트릭 선택**을 클릭하여 메트릭 유형을 지정한 다음 **메트릭 선택**을 클릭하여 메트릭 하위 유형을 지정하십시오.
	
	    CPU 메트릭 목록은 [컨테이너에 대한 CPU 메트릭](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers)을 참조하십시오.
	
	11. 더하기 이미지 ![추가 아이콘](images/grafana_plus_image.gif "더하기 이미지")를 클릭하고 함수를 선택하십시오. 함수를 추가하여 메트릭에 대해 사용 가능한 데이터를 변환하거나, 결합하거나, 이에 대한 계산을 수행할 수 있습니다.

        예를 들면, **alias(newName)** 함수를 추가하여 메트릭에 대해 별명을 추가할 수 있습니다. 이 별명은 그래프에 표시되는 범례에 메트릭 이름 대신 문자열을 인쇄하는 데 사용됩니다.

        메트릭에 대해 별명을 추가하려면 다음 단계를 완료하십시오.

        1. 더하기 기호를 클릭하십시오.
        2. **특수**를 선택하십시오.
        3. **별명**을 선택하십시오.
        4. 문자열(예: `My sample metric`)을 입력하십시오.


## 4단계: 나중에 재사용할 수 있도록 대시보드 저장
{: #step43}

다음 단계를 완료하십시오.

1. 대시보드 저장 이미지 ![대시보드 저장 이미지](images/grafana_save_image.gif "대시보드 저장 이미지")를 클릭하십시오.
2. 대시보드의 이름을 입력하십시오.
3. **저장**을 클릭하십시오.

