---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, overview

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


# {{site.data.keyword.mon_full_notm}} 정보
{: #about}

{{site.data.keyword.mon_full}}은 {{site.data.keyword.cloud_notm}} 아키텍처의 일부로서 포함할 수 있는 서드파티 클라우드 고유의 컨테이너 인텔리전스 관리 시스템입니다. 이를 사용하여 애플리케이션, 서비스 및 플랫폼의 성능과 상태에 대한 운영상의 가시성을 얻을 수 있습니다. 이는 관리자, DevOps 팀과 개발자에게 모니터링 및 문제점 해결, 경보 정의 및 사용자 정의 대시보드 설계를 위한 고급 기능을 갖춘 풀스택(full-stack) 텔레메트리를 제공합니다. {{site.data.keyword.mon_full_notm}}은 {{site.data.keyword.IBM_notm}}과의 파트너십으로 Sysdig에 의해 운영됩니다.
{:shortdesc}


{{site.data.keyword.cloud_notm}}에서 {{site.data.keyword.mon_full_notm}}의 모니터링 기능을 추가하려면 {{site.data.keyword.mon_full_notm}} 서비스의 인스턴스를 프로비저닝해야 합니다.

인스턴스를 프로비저닝하려면 우선 다음 정보를 고려하십시오.

* 사용자 데이터는 서드파티에 전송됩니다.
* 계정 소유자는 {{site.data.keyword.cloud_notm}}에서 서비스 인스턴스의 작성, 보기 및 삭제를 수행할 수 있으며 {{site.data.keyword.mon_full_notm}} 서비스 관련 작업을 위해 기타 사용자에게 권한을 부여할 수 있습니다.
* `관리자` 또는 `편집자` 권한이 있는 기타 {{site.data.keyword.cloud_notm}} 사용자는 {{site.data.keyword.cloud_notm}}에서 {{site.data.keyword.mon_full_notm}} 서비스를 관리할 수 있습니다. 이러한 사용자에게는 인스턴스를 프로비저닝할 계획인 리소스 그룹의 컨텍스트 내에서 리소스를 작성할 수 있는 플랫폼 권한도 있어야 합니다.

사용자는 리소스 그룹의 컨텍스트 내에서 인스턴스를 프로비저닝합니다. 리소스 그룹을 사용하면 액세스 제어 및 비용 청구 용도로 서비스를 구성할 수 있습니다. *기본* 리소스 그룹 또는 사용자 정의 리소스 그룹에서 {{site.data.keyword.mon_full_notm}} 인스턴스를 프로비저닝할 수 있습니다.

[인스턴스를 프로비저닝](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision)하면 [Sysdig 액세스 키](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key)라고 하는 수집 키를 자동으로 받습니다.

인스턴스를 프로비저닝한 후에는 각 메트릭 소스에 대해 {{site.data.keyword.mon_full_notm}} 에이전트를 구성해야 합니다. 메트릭 소스는 해당 성능과 상태를 모니터하고 제어할 클라우드 리소스입니다. 모니터할 각 환경에서 {{site.data.keyword.mon_full_notm}} 에이전트를 구성해야 합니다. 예를 들어, 메트릭 소스는 Kubernetes 클러스터일 수 있습니다. 액세스 키를 사용하여 메트릭 데이터를 수집하고 이를 인스턴스에 전달하는 일을 담당하는 Sysdig 에이전트를 구성할 수 있습니다.

{{site.data.keyword.mon_full_notm}} 에이전트가 메트릭 소스에 배치되면 메트릭 수집 및 인스턴스에 메트릭 전달이 자동으로 이루어집니다. {{site.data.keyword.mon_full_notm}} 에이전트는 사전 정의된 메트릭을 자동으로 수집하고 이에 대해 보고합니다. 사용자는 환경에서 모니터할 메트릭을 구성할 수 있습니다.

{{site.data.keyword.mon_full_notm}} 웹 UI를 통해 데이터를 [모니터](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring) 및 [관리](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)할 수 있습니다.  

다음 그림은 {{site.data.keyword.cloud_notm}}에서 실행 중인 {{site.data.keyword.mon_full_notm}} 서비스에 대한 컴포넌트 개요를 보여줍니다.

![{{site.data.keyword.cloud_notm}}의 {{site.data.keyword.mon_full_notm}} 컴포넌트 개요](images/components.png "{{site.data.keyword.cloud_notm}}의 {{site.data.keyword.mon_full_notm}} 컴포넌트 개요")



## 데이터 수집
{: #overview_collection}

데이터를 수집하고 이를 {{site.data.keyword.mon_full_notm}} 인스턴스에 전달하도록 Sysdig 에이전트를 구성하는 경우에는 데이터가 자동으로 수집되어 웹 UI를 통한 분석이 가능합니다.

데이터는 10초 빈도로 수집됩니다. 

## 데이터 가용성
{: #overview_availability}

데이터는 최대 15개월 동안 사용이 가능합니다.

호스트 또는 컨테이너에서 Sysdig 에이전트가 제거된 후에 히스토리 데이터는 삭제되지 않습니다. 에이전트가 설치되어 보고 중인 동안에는 웹 UI를 통해 데이터를 분석에 사용할 수 있습니다.

{{site.data.keyword.mon_full_notm}} 서비스의 인스턴스를 삭제한 후에는 데이터를 검색 및 분석에 사용할 수 없습니다.



## 데이터 보관
{: #overview_retention}

데이터는 *롤업* 정책에 따라 각 인스턴스마다 보관됩니다.

시간이 경과되면서 데이터는 3개월이 지나면 미세 입자성에서 거친 입자성으로 롤업됩니다.

롤업 정책은 시간의 흐름에 따른 데이터의 입자성을 기술합니다.

* 데이터는 최소 6시간 동안 10초 간격으로 보관됩니다.
* 데이터는 2일 동안 1분 간격으로 보관됩니다.
* 데이터는 2주 동안 10분 간격으로 보관됩니다.
* 데이터는 3개월 동안 1시간 간격으로 보관됩니다.
* 데이터는 1년 동안 1일 간격으로 보관됩니다.

## 데이터 삭제
{: #overview_data_deletion}

{{site.data.keyword.cloud_notm}}에서 {{site.data.keyword.mon_full_notm}}의 인스턴스를 삭제하는 경우, 데이터의 삭제를 요청하려면 지원 팀을 통해 케이스를 열어야 합니다. 세부사항은 [지원 팀에 문의](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp)를 참조하십시오.

캡처를 삭제하면 해당 캡처에 대한 데이터 파일이 자동으로 삭제됩니다.

**참고: {{site.data.keyword.mon_short}} 인스턴스의 하나의 단일 Sysdig 에이전트에서 수집된 데이터의 삭제는 지원되지 않습니다.**



## 데이터 위치
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}}은 메트릭을 수집하고 집계합니다. 

* 메트릭 데이터는 {{site.data.keyword.cloud_notm}}에서 호스팅됩니다.
* 각 다중 구역 지역(MZR) 위치는 해당 위치에서 실행되는 {{site.data.keyword.mon_full_notm}}의 각 인스턴스에 대해 메트릭을 수집하고 집계합니다.
* 데이터는 {{site.data.keyword.mon_full_notm}} 인스턴스가 프로비저닝된 지역에서 공존합니다. 예를 들어, 미국 남부에서 프로비저닝된 인스턴스의 메트릭 데이터는 미국 남부 지역에서 호스팅됩니다.



## {{site.data.keyword.mon_full_notm}} 에이전트
{: #overview_sysdig_agent}

{{site.data.keyword.mon_full_notm}} 에이전트는 사전 정의된 메트릭을 자동으로 수집하고 이에 대해 보고합니다. 

다음 목록에는 사용 가능한 {{site.data.keyword.mon_full_notm}} 에이전트가 간략하게 나열되어 있습니다.

* Kubernetes, GKE 및 OpenShift용 {{site.data.keyword.mon_full_notm}} 에이전트.
* Docker 컨테이너용 또는 컨테이너화되지 않은 서비스용 {{site.data.keyword.mon_full_notm}} 에이전트.
* Mesos, Marathon 및 DCOS용 {{site.data.keyword.mon_full_notm}} 에이전트.
* 수동 Linux 설치용 {{site.data.keyword.mon_full_notm}} 에이전트.

자세한 정보는 [Sysdig 에이전트 구성](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) 및 [Sysdig 에이전트 제거](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove)를 참조하십시오.


## 사용량 보기
{: #overview_usage}

서비스 사용량 및 비용을 모니터하려면 [사용량 보기](/docs/billing-usage/viewing_usage.html#viewingusage)를 참조하십시오.


## 서비스 플랜
{: #overview_plans}

다양한 가격 플랜을 {{site.data.keyword.mon_full_notm}} 인스턴스에 사용할 수 있습니다. 자세한 정보는 [가격](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)을 참조하십시오.


## 보안 고려사항
{: #overview_security}

**캡처**

캡처는 시간 범위 중에 호스트에서 발생하는 사항을 분석하기 위해 생성할 수 있는 추적 파일입니다. 캡처에는 시스템 호출 및 기타 OS 이벤트가 포함됩니다. 노드에서 메트릭을 수집하는 Sysdig 에이전트를 구성할 때 해당 노드마다 이 기능을 사용 또는 사용 안함으로 설정할 수 있습니다. 기본적으로, Sysdig 에이전트 구성 시에 *캡처*는 사용으로 설정되어 있습니다. 노드는 Sysdig 에이전트가 설치되는 메트릭 소스 또는 호스트, 컨테이너, 가상 머신, 베어메탈일 수 있습니다.

**중요:** 캡처가 사용으로 설정되면 사용자의 오퍼레이션에 대한 Sysdig의 가시성이 강화됨을 유념하십시오. 조직 외부로의 데이터 노출 가능성과 보안 사고를 미연에 방지하려면 노드에서 캡처를 사용으로 설정하기 전에 조직의 보안 정책을 확인하십시오. 모든 Sysdig 에이전트에 대해 *캡처* 기능의 사용 안함 설정을 고려하십시오.
{: tip}

