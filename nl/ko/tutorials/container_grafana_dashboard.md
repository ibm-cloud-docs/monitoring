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


# Kubernetes 클러스터를 모니터링하기 위해 Grafana 대시보드 작성
{: #container_grafana_dashboard}


이 튜토리얼을 통해 {{site.data.keyword.monitoringlong}} 서비스에서 Grafana 대시보드를 작성하여 클러스터의 성능을 모니터링하는 방법을 배울 수 있습니다. 
{:shortdesc}


## 목표
{: #cgd_objectives}

Kubernetes 클러스터에 배치된 앱에 대한 컨테이너 메트릭을 검색하고 분석하는 방법을 학습하십시오.

1. Grafana를 실행하고 클러스터 메트릭을 볼 수 있는 {{site.data.keyword.monitoringshort}} 도메인을 설정하십시오.
2. Grafana 대시보드를 작성하고 컨테이너의 CPU 사용률을 모니터링하는 메트릭을 정의하십시오.


## 가정사항
{: #cgd_assumptions}

튜토리얼에서는 다음을 가정합니다.

* 클러스터가 미국 남부 지역에서 사용 가능합니다. 
* 사용자 ID에는 **뷰어** 권한이 있는 {{site.data.keyword.monitoringshort}} 서비스에 대한 IAM 정책이 있습니다.

이 튜토리얼을 완료하려면 [Kubernetes 클러스터에 배치된 앱에 대한 Grafana에서 메트릭 분석](/docs/services/cloud-monitoring/tutorials/container_service_metrics.html#container_service_metrics)을 완료하거나 하나 이상의 애플리케이션이 배치되어 프로비저닝된 클러스터가 있어야 합니다.



## 1단계: Grafana 실행
{: #cgd_step1}

브라우저에서 Grafana를 실행하고 클러스터 메트릭을 볼 수 있는 {{site.data.keyword.monitoringshort}} 도메인을 설정하십시오.

클러스터의 메트릭을 분석하려면 클러스터가 작성된 클라우드 퍼블릭 지역에서 Grafana에 액세스해야 합니다. 자세한 정보는 [웹 브라우저에서 Grafana 대시보드로 이동](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser)을 참조하십시오.

1. 브라우저에서 Grafana를 실행하십시오. 

    클러스터를 작성한 지역에 대한 {{site.data.keyword.monitoringshort}} 서비스 URL을 입력하십시오. 
    
    지역별 URL을 가져오려면 [모니터링 서비스에 대한 URL](/docs/services/cloud-monitoring/monitoring_ov.html#region)을 참조하십시오.

    예를 들어, 미국 남부 지역의 경우 [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)을 실행하십시오.

2. {{site.data.keyword.monitoringshort}} 도메인을 **계정**으로 설정하십시오.

    Grafana에서 사용자 ID를 선택하십시오. 그런 다음, 올바른 계정인지 확인하고 `Domain = account`를 선택하십시오.


## 2단계: Grafana 대시보드 작성
{: #cgd_step2}

새 대시보드를 작성하려면 다음 단계를 완료하십시오.

1. 측면 메뉴 표시줄 토글 ![Grafana 측면 메뉴 표시줄](images/grafana_settings.gif "Grafana 측면 메뉴 표시줄")을 선택하십시오.
2. **대시보드**를 선택하십시오.
3. **새로 작성**을 클릭하십시오.

대시보드가 열립니다. 이 대시보드는 구성할 준비가 된 비어 있는 행을 포함하고 있습니다.

![Grafana 대시보드](images/grafana4_f1.gif "Grafana 대시보드")

Grafana에서는 행을 추가하여 대시보드를 섹션으로 나눕니다. 하나의 행은 1개 이상의 패널을 그룹화합니다. 패널은 행 내에서 메트릭에 대한 데이터를 표시하기 위해 구성할 수 있는 가장 작은 시각화 단위로, 예를 들면 그래프 패널 또는 표 패널을 선택할 수 있습니다. 패널을 끌어서 놓아 대시보드에서 패널을 다시 배치할 수 있습니다. 패널이 표시하는 데이터는 조회를 통해 구성됩니다. 패널에는 하나 이상의 조회를 정의할 수 있습니다. 각 조회는 서로 다른 데이터 세트를 나타냅니다. 패널의 시간 범위를 설정할 수도 있습니다. 일반적으로 시간 범위는 *대시보드* 시간 선택도구로 설정됩니다.

## 3단계: 대시보드에 그래프를 추가하여 메트릭 모니터링
{: #cgd_step3}

다음 단계를 완료하십시오.

1. **그래프**를 선택하십시오.

2. 그래프 제목을 클릭한 후 **편집**을 선택하십시오.

    *메트릭* 탭이 열립니다. 여기서는 기본 데이터 소스를 볼 수 있습니다.


![구성 탭을 포함한 그래프 패널](images/grafana4_f2.gif "구성 탭을 포함한 그래프 패널")


## 4단계: 메트릭 조회 정의
{: #cgd_step4}

그래프에 표시되는 데이터를 필터링하는 조회를 정의하십시오. 이 조회는 컨테이너의 모든 코어의 CPU 시간(나노초(ns))을 모니터링합니다.

조회의 형식에 대한 정보는 [컨테이너에 대해 수집된 CPU 메트릭의 조회 형식](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers)을 참조하십시오.
 
*메트릭* 탭에서 **조회 추가**를 선택하십시오. <br>조회 항목이 추가됩니다. 각 조회는 하나의 문자로 레이블 지정됩니다. 

![새 조회 항목](images/grafana4_query_f1.gif "새 조회 항목") 
	
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
	
    예를 들어, 컨테이너의 모든 코어의 CPU 시간(나노초(ns))을 모니터링하려면 유형으로 **cpu**를 선택하고 하위 유형으로 **사용량**을 선택하십시오.
		
	CPU 메트릭 목록은 [컨테이너에 대한 CPU 메트릭](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#cpu_metrics_containers)을 참조하십시오.
    
11. 더하기 이미지 ![추가 아이콘](images/grafana_plus_image.gif "더하기 이미지")를 클릭하고 함수를 선택하십시오. 함수를 추가하여 메트릭에 대해 사용 가능한 데이터를 변환하거나, 결합하거나, 이에 대한 계산을 수행할 수 있습니다.

    예를 들면, **alias(newName)** 함수를 추가하여 메트릭에 대해 별명을 추가할 수 있습니다. 이 별명은 그래프에 표시되는 범례에 메트릭 이름 대신 문자열을 인쇄하는 데 사용됩니다.

    메트릭에 대해 별명을 추가하려면 다음 단계를 완료하십시오.

    1. 더하기 기호를 클릭하십시오.
    2. **특수**를 선택하십시오.
    3. **별명**을 선택하십시오.
    4. 문자열(예: `My sample metric`)을 입력하십시오.

## 5단계: 대시보드 저장
{: #cgd_step5}

나중에 재사용할 수 있도록 대시보드를 저장하십시오.

1. 대시보드 저장 이미지 ![대시보드 저장 이미지](images/grafana_save_image.gif "대시보드 저장 이미지")를 클릭하십시오.

    ![대시보드 저장](images/grafana_save_dashboard.gif "대시보드 저장")

2. 대시보드의 이름을 입력하십시오.
3. **저장**을 클릭하십시오.



## 다음 단계
{: #cgd_next_steps}

메트릭에 대한 경보를 정의하십시오. 자세한 정보는 [경보 구성](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov)을 참조하십시오.
