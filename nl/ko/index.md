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


# 시작하기 튜토리얼
{: #getting-started-with-ibm-cloud-monitoring}

이 튜토리얼을 통해 {{site.data.keyword.Bluemix}}에서 {{site.data.keyword.monitoringlong}} 서비스를 사용하여 작업을 시작하는 방법을 배울 수 있습니다.
{:shortdesc}

기본적으로 {{site.data.keyword.Bluemix_notm}}에서는 선택된 서비스에 대한 통합 모니터링 기능을 제공합니다. {{site.data.keyword.monitoringlong_notm}} 서비스를 사용하여 메트릭에 대해 작업할 때의 수집 및 보존 기능을 확장하고 주의가 필요한 상태에 대해 알려주는 규칙 및 경보를 정의할 수 있습니다. {{site.data.keyword.monitoringshort}} 서비스는 앱이 리소스를 수행하고 이용하는 방법에 대한 인사이트를 키울 수 있는 기능을 제공하며 신속하게 (상태)동향을 식별하고 문제점을 발견 및 진단할 수 있도록 지원하며 즉각적인 가치실현시간 및 낮은 총소유비용이라는 이점을 제공합니다. Grafana를 통해 환경을 모니터링합니다. 

## 시작하기 전에
{: #cm_prereqs}

{{site.data.keyword.Bluemix_notm}} 계정의 구성원 또는 소유자인 사용자 ID가 있어야 합니다. {{site.data.keyword.Bluemix_notm}} 사용자 ID를 얻으려면 [등록 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/registration/){:new_window}으로 이동하십시오.

## 1단계: 모니터링할 클라우드 리소스 선택
{: #cm_step1}

{{site.data.keyword.Bluemix_notm}}의 경우, {{site.data.keyword.containershort}}에서 실행되는 CF 앱, 컨테이너 및 선택된 서비스는 자동으로 메트릭 시리즈 데이터를 수집하여 이를 {{site.data.keyword.monitoringshort}} 서비스로 전달합니다.

다음 표에는 다양한 클라우드 리소스가 나열되어 있습니다. {{site.data.keyword.monitoringshort}} 서비스를 사용하여 작업을 시작하려면 리소스에 대한 튜토리얼을 완료하십시오.

<table>
  <caption>{{site.data.keyword.monitoringshort}} 서비스를 시작하기 위한 튜토리얼 </caption>
  <tr>
    <th>리소스</th>
    <th>튜토리얼</th>
    <th>클라우드 환경</th>
    <th>시나리오</th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containershort}}에서 실행 중인 컨테이너</td>
    <td>[Kubernetes 클러스터에 배치된 앱에 대한 Grafana에서 메트릭 분석](/docs/services/cloud-monitoring/tutorials/container_service_metrics.html#container_service_metrics)</td>
    <td>퍼블릭 </br>데디케이티드</td>
    <td>![Kubernetes 클러스터에 배치된 컨테이너에 대한 상위 레벨 컴포넌트 개요](containers/images/containers_kube_metrics_dedicated.png "Kubernetes 클러스터에 배치된 컨테이너에 대한 상위 레벨 컴포넌트 개요")</td>
  </tr>
  <tr>
    <td>CF 앱</td>
    <td>[CF 앱에 대한 Grafana에서 메트릭 분석](/docs/services/cloud-monitoring/tutorials/cfapps_metrics.html#cfapps_metrics)</td>
    <td>퍼블릭</td>
    <td>![{{site.data.keyword.Bluemix_notm}}의 CF 앱 모니터링에 대한 상위 레벨 보기](cf/images/cfapp_metrics_ov.png "{{site.data.keyword.Bluemix_notm}}의 CF 앱 모니터링에 대한 상위 레벨 보기")</td>
  </tr>
</table>



## 2단계: 메트릭을 볼 사용자에 대한 권한 설정
{: #cm_step2}

사용자가 수행할 수 있는 {{site.data.keyword.monitoringshort}} 조치를 제어하기 위해 사용자에게 역할 및 정책을 지정할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}}에는 사용자가 {{site.data.keyword.monitoringshort}} 서비스를 사용하여 작업할 때 수행할 수 있는 조치를 제어하는 두 가지 유형의 보안 권한이 있습니다.

* CF(Cloud Foundry) 역할: 사용자가 영역에서 메트릭을 보아야 하는 권한을 정의하려면 사용자에게 CF 역할을 부여하십시오.
* IAM 역할: 사용자가 계정 도메인에서 메트릭을 보아야 하는 권한을 정의하려면 사용자에게 IAM 정책을 부여하십시오.


다음 단계를 완료하여 사용자에게 영역에서 메트릭을 볼 수 있는 권한을 부여하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드: [http://bluemix.net ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}을 실행하십시오.
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오. 

    *사용자* 창에 사용자의 목록이 현재 선택된 계정에 대한 해당 이메일 주소와 함께 표시됩니다.
	
3. 사용자가 계정의 구성원이면 목록에서 사용자 이름을 선택하거나 *조치* 메뉴에서 **사용자 관리**를 클릭하십시오.

    사용자가 계정의 구성원이 아닌 경우 [사용자 초대](/docs/iam/iamuserinv.html#iamuserinv)를 참조하십시오.

4. **Cloud Foundry 액세스**를 선택한 다음 조직을 선택하십시오.

    해당 조직에서 사용 가능한 영역 목록이 나열됩니다.

5. {{site.data.keyword.monitoringshort}} 서비스를 프로비저닝한 영역을 선택하십시오. 그런 다음 메뉴 조치에서 **영역 역할 편집**을 선택하십시오.

6. *감사자*를 선택하십시오. 

    하나 이상의 영역 역할을 선택할 수 있습니다. *관리자*, *개발자* 및 *감사자* 역할은 모두 사용자에게 로그를 볼 수 있도록 허용합니다.
	
7. **역할 저장**을 클릭하십시오.


자세한 정보는 [권한 부여](/docs/services/cloud-monitoring/security/assign_policy.html#grant_permissions)를 참조하십시오.

사용자가 메트릭 데이터를 볼 수 있는지 확인하려면 튜토리얼 중 하나를 완료한 클라우드 지역에서 Grafana를 실행하십시오. 예를 들어, 미국 남부 지역의 경우, 웹 브라우저를 열고 [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)이라는 URL을 입력하십시오.


다른 지역에서 Grafana를 실행하는 방법에 대한 자세한 정보는 [웹 브라우저에서 Grafana로 이동](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#navigating_grafana)을 참조하십시오.

**참고:** Grafana를 실행할 때 *bearer 토큰이 유효하지 않음*을 나타내는 메시지를 수신한 경우, 영역에서 권한을 확인하십시오. 이 메시지는 사용자 ID에 메트릭을 볼 수 있는 권한이 없음을 표시합니다.
    

## 다음 단계 
{: #cm_next_steps}

메트릭에 대한 경보를 정의하십시오. 자세한 정보는 [경보 구성](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov)을 참조하십시오.
