---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring

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

# 환경 모니터링
{: #monitoring}

{{site.data.keyword.mon_full_notm}} 서비스를 사용하여 사용자의 인프라 및 여기서 실행되는 애플리케이션을 모니터할 수 있습니다. 시간 범위 중에 노드에서 발생하는 사항을 분석하기 위해 캡처를 요청할 수 있습니다.
{:shortdesc}

먼저 {{site.data.keyword.cloud_notm}}에서 {{site.data.keyword.mon_full_notm}} 서비스의 인스턴스를 프로비저닝합니다. 그런 다음 메트릭 소스에 대한 Sysdig 에이전트를 구성합니다. 소스가 구성된 후 서비스의 웹 UI를 통해 데이터를 보고 모니터하며 관리할 수 있습니다.

기본 메트릭에 대한 데이터는 자동으로 수집됩니다. 사용자는 사용자 정의 메트릭을 구성하고 레이블을 해당 메트릭에 추가하여 해당 특성을 기술할 수 있습니다. 이러한 사용자 정의 메트릭에 대한 데이터 역시 자동으로 수집됩니다.

웹 UI의 *대시보드* 탭과 *탐색* 탭에서 데이터를 분석할 수 있습니다. 메트릭 보기 및 대시보드를 통해서는 데이터를 모니터합니다. 

* 메트릭 보기를 사용하여 개별 메트릭을 모니터할 수 있습니다.
* 대시보드를 사용하여 패널을 통해 데이터를 모니터링함으로써 네트워크 데이터, 애플리케이션 데이터, 토폴로지, 서비스, 호스트 및 컨테이너에 대한 전문적 인사이트를 얻을 수 있습니다. 패널은 대시보드에서 메트릭 또는 메트릭 그룹을 표시합니다.

각각의 메트릭 보기 및 대시보드의 경우, 사용자는 데이터의 범위, 데이터 집계 방법 및 데이터에 적용할 시간과 그룹 필터를 정의할 수 있습니다. 자세한 정보는 [데이터 관리](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)를 참조하십시오.

*탐색* 탭에서는 기본 메트릭 및 기본 대시보드를 사용하여 데이터를 모니터할 수 있습니다. 레이블을 사용하여 새 인프라 그룹을 정의할 수 있으며, 나중에 이를 사용하여 데이터를 다른 방식으로 집계하고 사용자 환경을 모니터할 수 있습니다. 또한 *대시보드* 탭을 통해 정의된 사용자 정의 대시보드를 사용할 수도 있습니다.

*대시보드* 탭에서는 기본 대시보드를 사용하거나 새 대시보드를 작성하여 데이터를 모니터할 수 있습니다.

기본 대시보드를 팀의 기본 시작점으로 구성하여 팀의 경험을 통합하고 사용자가 가장 관련성이 높은 정보에 즉각적인 주의를 기울이도록 할 수 있습니다.
{: tip}

경보를 사용하여 하나 이상의 알림 채널을 통해 주의를 요하는 문제점에 대해 사용자에게 알릴 수 있습니다.
* 웹 UI의 *경보* 섹션은 사전 정의된 경보의 목록을 표시합니다. 이 보기에서 사전 정의된 경보를 사용 및 사용 안함으로 설정하고 기존 경보를 수정하며 새 경보를 작성할 수 있습니다.
* 웹 UI의 *설정* 섹션은 사용자가 알림 채널을 구성하는 위치입니다.
 
시간 범위 중에 해당 노드에서 발생하는 사항을 분석하기 위해 노드의 캡처를 요청할 수 있습니다. 예를 들어, 이를 사용하여 병목현상 또는 컴포넌트 상호작용을 분석할 수 있습니다.

## 메트릭
{: #monitoring_metrics}

메트릭은 해당 특성을 정의하기 위한 하나 이상의 레이블이 있는 정량적 측정값입니다. 메트릭을 사용하여 숫자 값을 지닌 데이터를 통계적으로 분석할 수 있습니다. 

메트릭은 시계열에 의해 표시됩니다. 시계열은 일정 기간 동안의 숫자 데이터 점 세트입니다. 

메트릭은 두 개의 그룹으로 분류됩니다. 

* [기본 메트릭](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [사용자 정의 메트릭](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

레이블은 인프라 레이블 및 메트릭 디스크립터 레이블로 분류됩니다. 각 메트릭에는 사전 정의된 레이블 세트가 있습니다. 사용자 정의 메트릭의 경우에는 추가 레이블을 구성할 수 있습니다. 

레이블을 사용하여 메트릭의 특성을 식별하고 구분할 수 있습니다, 예를 들어, 다음을 수행할 수 있습니다.
* 인프라 오브젝트를 논리 계층 구조로 그룹화할 수 있습니다. 
* 데이터를 필터링하여 걸러낼 수 있습니다. 
* 집계된 데이터를 세그먼트로 분할할 수 있습니다. 

자세한 정보는 [레이블](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels)을 참조하십시오.

## 패널
{: #monitoring_panels}

패널은 대시보드에서 메트릭 또는 메트릭 그룹을 표시합니다. 

다음의 패널 유형을 사용하여 메트릭을 시각화할 수 있습니다.

|유형 |설명 |
|------|-------------|
| `라인` | 이 패널을 사용하여 하나 이상의 메트릭에 대해 시간의 흐름에 따른 상태동향을 볼 수 있습니다.  |
| `영역` | 이 패널을 사용하여 하나 이상의 메트릭에 대해 시간의 흐름에 따른 상태동향을 볼 수 있습니다.  |
| `최상위 목록` | 이 패널을 사용하여 엔티티 그룹 간에 메트릭을 비교할 수 있습니다. 막대형 차트는 내림차순으로 정렬됩니다.  |
| `히스토그램` | 이 패널을 사용하여 버킷에서 메트릭의 빈도 분포를 볼 수 있습니다.  |
| `토폴로지` | 이 패널을 사용하여 맵의 엔티티 간의 관계 및 토폴로지 맵으로서 인프라를 시각화할 수 있습니다.  |
| `숫자` | 이 패널을 사용하여 하나 이상의 엔티티에 대해 시간의 흐름에 따른 집계 메트릭 값을 표시하는 단일 숫자를 볼 수 있습니다.  |
| `테이블` | 이 패널을 사용하여 메트릭 및 세그먼트를 기반으로 인프라에 대한 숫자 데이터를 표시할 수 있습니다.  |
| `텍스트` | 이 패널을 사용하여 텍스트를 추가할 수 있습니다. 텍스트를 추가하려면 마크다운을 사용하십시오.  |
{: caption="표 1. 패널 유형" caption-side="top"} 

범위의 복사, 변경 및 패널의 복제, 삭제, 내보내기, 탐색을 수행할 수 있습니다.

패널에서 데이터를 내보낼 수 있습니다. 데이터를 내보낼 때는 다음 정보를 고려하십시오.

* 선형 차트에서 **json 파일**로 데이터를 내보낼 수 있습니다.
* 테이블 차트 또는 선형 차트에서 **csv 파일**로 데이터를 내보낼 수 있습니다.


다음 표에는 패널에서 실행할 수 있는 태스크가 나열되어 있습니다.

| 태스크 |설명 |
|------|-------------|
| [패널 복사](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | 패널을 새 대시보드로 복사합니다.  |
| [범위 변경](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | 패널의 범위를 변경합니다. |
| [패널 복제](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | 동일한 대시보드에서 패널을 복사합니다.  |
| [패널 삭제](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | 대시보드에서 패널을 삭제합니다.  |
| [데이터 내보내기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | 패널의 데이터를 csv 파일이나 json 파일로 내보냅니다.  |
| [경보 작성](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | 메트릭에 대한 경보를 정의합니다. |
{: caption="표 2. 패널 태스크" caption-side="top"} 


## 대시보드
{: #monitoring_dashboards}

**대시보드**는 단일 호스트 또는 호스트 그룹에 대한 서비스와 인프라, 애플리케이션의 상태 및 안전성, 성능에 대해 보고하는 메트릭 그룹을 표시합니다. 대시보드는 네트워크 데이터, 애플리케이션 데이터, 토폴로지, 서비스, 호스트 및 컨테이너에 대한 전문적 인사이트를 제공합니다. 대시보드를 사용하여 모니터, 애플리케이션 및 서비스를 모니터할 수 있습니다.


웹 UI의 **대시보드** 섹션에서 대시보드는 세 개의 기본 그룹으로 구성되어 있습니다.

* **내 대시보드**: 현재 로그인한 사용자가 작성한 대시보드입니다.
* **내 공유 대시보드**: 현재 로그인한 사용자가 작성했으며 다른 사용자와 공유되는 대시보드입니다.
* **나와 공유되는 대시보드**: 다른 사용자가 작성했으며 현재 사용자와 공유되는 대시보드입니다.

웹 UI의 **탐색** 섹션에서 대시보드는 두 개의 기본 그룹으로 구성되어 있습니다.
* **기본 대시보드**: 이러한 대시보드는 사전 정의된 대시보드입니다.
* **내 대시보드**: 현재 로그인한 사용자가 작성한 대시보드입니다.

사전 정의된 대시보드를 사용할 수 있습니다. 웹 UI를 통해 또는 프로그래밍 방식으로 사용자 정의 대시보드를 작성할 수도 있습니다. Python 스크립트 또는 Sysdig REST API를 사용하여 대시보드를 백업 및 복원할 수 있습니다.

웹 UI를 통해 대시보드를 복사 및 공유할 수도 있습니다. 

다음 표에는 UI에서 대시보드 관련 작업을 위해 실행할 수 있는 태스크가 간략하게 설명되어 있습니다.

| 태스크 |설명 |
|------|-------------|
| [대시보드 작성](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | 웹 UI에서 사용자 정의 대시보드를 작성합니다. |
| [대시보드 복사](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | 대시보드가 사용 가능한 현재 팀에서 대시보드의 사본을 작성하거나 대시보드를 다른 팀에 복사합니다. |
| [범위 변경](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | 대시보드의 범위를 변경합니다.       |
| [대시보드 삭제](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) | 대시보드를 삭제합니다. |
| [대시보드 공유](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | 대시보드에 대한 공용 URL을 구성하여 외부적으로 및 팀의 사용자 간에 대시보드를 공유합니다. |
{: caption="표 3. 웹 UI에서 실행할 수 있는 대시보드 태스크" caption-side="top"} 

다음 표에는 대시보드 관련 작업을 위해 프로그래밍 방식으로 실행할 수 있는 태스크가 간략하게 설명되어 있습니다.

| 태스크                    |	 REST API 사용                |
|-------------------------|-------------------------------|
| 대시보드 작성      |[API를 사용하여 대시보드 작성](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| 대시보드 삭제      |[API를 사용하여 대시보드 삭제](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| 대시보드 저장       | [API를 사용하여 팀의 대시보드 저장](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="표 4. 프로그래밍 방식의 대시보드 관리를 위한 태스크" caption-side="top"} 



## 이벤트
{: #monitoring_events}

이벤트는 {{site.data.keyword.mon_full_notm}} 인스턴스에 데이터를 전달하는 노드에서 발생하는 사항에 대해 알리는 알림입니다. 이벤트를 사용하여 문제를 검토, 추적 및 해결할 수 있습니다. 

다음 목록에는 여러 가지 유형의 이벤트가 설명되어 있습니다. 

* *경보 이벤트*는 사용자 구성된 경보에 의해 트리거되는 이벤트입니다. 자세한 정보는 [경보 관련 작업](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)을 참조하십시오.
* *인프라 기반 이벤트*는 Docker 및 Kubernetes 노드에서 수집된 이벤트입니다. 기본적으로 Sysdig 에이전트는 선택된 이벤트 그룹에서 데이터를 자동으로 검색하고 수집합니다. 에이전트 구성 파일을 편집하여 추가 이벤트를 사용으로 설정할 수 있습니다.
* Slackbot, 사전 빌드된 Python 스크립트, 사용자 정의 사용자 작성된 Python 스크립트 또는 cURL 요청 등의 통합을 통해 구성하는 *사용자 정의 이벤트*.

기본적으로 이벤트의 상태는 다음과 같습니다. 
* **활성**: 이 상태는 이벤트를 트리거한 상황이 계속 유지됨을 표시합니다(예: 노드가 계속 작동 중지 상태임).
* **정상**: 이 상태는 상황이 다시 정상으로 돌아왔음을 표시합니다(예: 노드가 시작되어 실행 중임).

웹 UI의 *이벤트* 섹션에서 이벤트를 관리할 수 있습니다. 
* *경보 이벤트* 탭을 통해 경보 이벤트를 볼 수 있습니다.
* *사용자 정의 이벤트* 탭을 통해 인프라 기반 이벤트를 볼 수 있습니다.
* *사용자 정의 이벤트* 탭을 통해 사용자 정의 이벤트를 볼 수 있습니다.
* [팀에 대한 API 토큰](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token)을 사용하여 해당 팀에 사용자 정의 이벤트를 전송할 수 있습니다. 자세한 정보는 [사용자 정의 이벤트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}를 참조하십시오.
* 상태가 **정상**으로 설정될 때까지 대기하는 대신 이벤트를 **해결됨**으로 설정하여 다른 사용자에게 문제가 해결되었음을 알릴 수 있습니다.
{: #tip}



## 경보
{: #monitoring_alerts}

경보는 주의를 요하는 상황에 대해 경고하는 데 사용할 수 있는 알림 이벤트입니다. 각 경보에는 심각도 상태가 있습니다. 이 상태는 보고되는 정보의 심각도에 대해 알려줍니다. 

경보를 정의할 때 알림을 트리거하는 조건 및 알림을 받을 하나 이상의 알림 채널을 정의해야 합니다. 또한 경보의 심각도 및 경보의 유형도 정의해야 합니다. 

다음의 경보 유형의 경보를 정의할 수 있습니다.

|유형              |설명 |
|-------------------|-------------|
| 이상 항목 발견 | 일탈 시에 경보 및 히스토리 동작을 기반으로 호스트를 모니터하는 데 사용됩니다. |
| 작동 중지 시간          | 엔티티 작동 중지 시에 경보 및 호스트, 컨테이너, 프로세스 또는 서비스 등의 엔티티 유형을 모니터하는 데 사용됩니다. |
| 이벤트             | 총 발생 수의 임계값 위반 시에 경보 및 특정 이벤트의 발생을 모니터하는 데 사용됩니다. 예를 들어, 이를 사용하여 컨테이너, 오케스트레이션 및 서비스 이벤트의 배치 및 재시작에 대해 경보할 수 있습니다.|
| 그룹 아웃라이어(outlier)     | 하나가 나머지와 달리 작동 시에 알림을 받고 호스트 그룹을 모니터하는 데 사용됩니다. |
| 메트릭            | 사용자 정의된 임계값 위반 시에 경보 및 시계열 메트릭을 모니터하는 데 사용됩니다. |
{: caption="표 5. 경보 유형" caption-side="top"} 

기본적으로 심각도는 *경고*로 설정됩니다. 경보의 심각도를 다음 값으로 설정할 수 있습니다. *긴급*, *경보*, *심각*, *오류*, *경고*, *알림*, *정보*, 디버그* 

다음의 알림 통합에 대해 하나 이상의 알림 채널을 정의할 수 있습니다.
* 이메일 알림
* PagerDuty 알림
* Slack 알림
* VictorOps 알림
* OpsGenie 알림
* 웹훅 채널 구성

자세한 정보는 [알림 채널 구성](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create)을 참조하십시오.


웹 UI에서 및 Sysdig API를 사용하여 사전 정의된 경보를 사용으로 설정하고 경보를 수정하며 사용자 정의 경보를 작성할 수 있습니다.

사용자는 웹 UI의 *경보* 보기에서 경보를 관리합니다. 또한 *경보* 보기에 표시되는 테이블 열을 구성할 수 있습니다. 유효한 열 옵션은 *이름*, *범위*, *경보 시기*, *세그먼트 기준*, *알림*, *사용*, *수정일*, *캡처*, *채널*, *작성일*, *설명*, *이메일 수신인*, *최소 기간*, *OpsGenie*, *PagerDuty*, *심각도*, *Slack*, *웹훅*, *SNS 주제*, *유형*, *VictorOps*입니다.

다음 목록에는 경보 관련 작업 시의 기본 태스크가 간략하게 설명되어 있습니다.
* [경보 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [경보 사용 또는 사용 안함 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [경보 검색 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [경보 수정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [동일 팀에 경보 복사 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [다른 팀에 경보 복사 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [경보 내보내기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [경보 삭제 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [사용자 정의 부울 표현식으로 경보 임계값 정의 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## 캡처
{: #monitoring_captures}

캡처는 시간 범위 중에 노드에서 발생하는 사항을 분석하기 위해 생성할 수 있는 추적 파일입니다. 캡처 파일 크기 한계는 100MB입니다. 예를 들어, 이를 사용하여 병목현상 또는 컴포넌트 상호작용을 분석할 수 있습니다. 

캡처에는 시스템 호출 및 기타 OS 이벤트(예: 시스템 레벨 대기 시간, 일괄처리 작업 지속 기간, 배치 인터럽트 시간, Auto-Scaling 대기 시간, 컨테이너 스타트업 시간 또는 애플리케이션 트랜잭션 시간)가 포함되어 있습니다. 캡처에는 노드의 모든 컨테이너의 상세 정보가 포함되어 있습니다. 

조직의 가이드라인에 따라 캡처 사용 안함을 고려하십시오. 기본적으로, 캡처는 노드에서 Sysdig 에이전트 구성 시에 사용으로 설정되어 있습니다.
{: tip}

개별 노드에 대한 *캡처*를 작성, 탐색, 다운로드 및 삭제할 수 있습니다. 노드는 Sysdig 에이전트가 설치되는 메트릭 소스 또는 호스트, 컨테이너, 가상 머신, 베어메탈일 수 있습니다. 

* 웹 UI에서 사용자는 *탐색* 섹션에서 캡처를 작성하고 *캡처* 섹션을 통해 캡처 파일을 관리합니다.
* *Csysdig*(sysdig용 curses 기반 명령행 UI)를 사용하여 캡처에서 데이터를 시각화하거나 오픈 소스 Sysdig 유틸리티를 사용하여 캡처의 데이터를 분석할 수 있습니다.
* 필터를 사용하여 캡처의 데이터를 검색할 수 있습니다.
* 치즐(스크립트)을 사용하여 캡처의 데이터를 조작할 수 있습니다. 

팀에 대해 캡처 기능을 사용으로 설정하는 경우 캡처 파일은 해당 팀의 구성원만 볼 수 있습니다.

다음 목록에는 캡처 관련 작업 시의 기본 태스크가 간략하게 설명되어 있습니다.
* [캡처 작성](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [캡처 삭제](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [캡처 탐색](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [캡처 다운로드](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

자세한 정보는 [캡처 관련 작업](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)을 참조하십시오.


