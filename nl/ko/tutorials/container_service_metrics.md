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


# Kubernetes 클러스터에 대한 Grafana에서 메트릭 분석
{: #container_service_metrics}

이 튜토리얼을 통해 {{site.data.keyword.monitoringlong}} 서비스를 사용하여 컨테이너의 성능을 모니터링하는 방법을 배울 수 있습니다. 
{:shortdesc}


## 목표
{: #ks_objectives}

Kubernetes 클러스터에 배치된 앱에 대한 컨테이너 메트릭을 검색하고 분석하는 방법을 학습하십시오.

1. 클러스터에서 수집된 메트릭이 {{site.data.keyword.monitoringshort}} 서비스로 전달되는 위치를 식별하십시오. 
2. Grafana를 실행하고 클러스터 메트릭을 볼 수 있는 {{site.data.keyword.monitoringshort}} 도메인을 설정하십시오.
3. {{site.data.keyword.Bluemix_notm}}에서 Kubernetes 클러스터에 배치된 앱에 대한 컨테이너 메트릭을 검색하고 분석하십시오.

이 튜토리얼은 {{site.data.keyword.Bluemix_notm}}에서 작동하고 클러스터를 프로비저닝하고 클러스터가 {{site.data.keyword.Bluemix_notm}}의 {{site.data.keyword.monitoringshort}} 서비스에 메트릭을 전송하는 위치를 식별하고 클러스터에서 앱을 배치하고 Grafana를 사용하여 해당 클러스터에 대한 클러스터 메트릭을 보고 필터링하는 다음과 같은 엔드 투 엔드 시나리오를 가져오는 데 필요한 단계를 수행합니다.


**참고:** 이 튜토리얼을 완료하려면 전제조건 및 다른 단계에서 링크된 튜토리얼을 완료해야 합니다.


## 전제조건
{: #ks_prereqs}

1. Kubernetes 표준 클러스터를 작성하고 클러스터에 앱을 배치하고 Grafana에서 모니터링하기 위해 {{site.data.keyword.Bluemix_notm}}에서 메트릭을 조회할 수 있는 권한이 있는 {{site.data.keyword.Bluemix_notm}} 계정의 구성원 또는 소유자여야 합니다.

    {{site.data.keyword.Bluemix_notm}}에 대한 사용자 ID에는 다음과 같은 정책이 지정되어 있어야 합니다.
    
    * {{site.data.keyword.containershort}}에 대한 IAM 정책(*운영자* 또는 *관리자* 권한의 경우)
    
    자세한 정보는 [IBM Cloud UI를 통해 사용자에게 IAM 정책 지정](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui)을 참조하십시오.

2. Kubernetes 클러스터를 관리하고 명령행에서 앱을 배치할 수 있는 터미널 세션이 있어야 합니다. 이 튜토리얼의 경우, Ubuntu Linux 시스템에 대한 예입니다.

3. Ubuntu 시스템에서 {{site.data.keyword.containershort}}에 대해 작업할 수 있도록 CLI를 설치하십시오.

    * {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오. 
    * {{site.data.keyword.containershort}} CLI를 설치하여 {{site.data.keyword.containershort}}에서 Kubernetes 클러스터를 작성 및 관리하고 컨테이너화된 앱을 클러스터에 배치하십시오.
    
    자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 설치](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)를 참조하십시오.
    
    

    
 

## 1단계: Kubernetes 클러스터 프로비저닝
{: #ks_step1}

다음 단계를 완료하십시오.

1. 표준 Kubernetes 클러스터를 작성하십시오. 자세한 정보는 [Kubernetes 표준 클러스터 작성](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial)을 참조하십시오.

2. 터미널에서 클러스터 컨텍스트를 설정하십시오. 컨텍스트가 설정된 후에는 Kubernetes 클러스터를 관리하고 Kubernetes 클러스터에 애플리케이션을 배치할 수 있습니다.

    작성한 클러스터와 연관된 {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login)을 참조하십시오.

	{{site.data.keyword.containershort}} 서비스 플러그인을 초기화하십시오.

	```
	ibmcloud cs init
	```
	{: codeblock}

    클러스터에 터미널 컨텍스트를 설정하십시오.
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    이 명령 실행의 출력은 구성 파일에 대한 경로를 설정하기 위해 터미널에서 실행해야 하는 명령을 제공합니다. 예를 들어 다음과 같습니다.

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    명령을 복사하고 붙여넣는 방법으로 터미널에서 환경 변수를 설정한 다음 **Enter**를 누르십시오.



## 2단계: 사용자에게 계정 도메인에서 메트릭을 볼 수 있는 권한 부여
{: #ks_step2}

사용자에게 계정 도메인에서 메트릭을 볼 수 있는 권한을 부여하려면 **뷰어** 역할이 있는 {{site.data.keyword.monitoringshort}} 서비스에 대한 IAM 정책을 사용자에게 지정해야 합니다.

사용자에게 {{site.data.keyword.monitoringshort}} 서비스에 대해 작업할 수 있는 권한을 부여하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드: [http://bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}을 실행하십시오.
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오. 

    *사용자* 창에 사용자의 목록이 현재 선택된 계정에 대한 해당 이메일 주소와 함께 표시됩니다.
	
3. 사용자가 계정의 구성원이면 목록에서 사용자 이름을 선택하거나 *조치* 메뉴에서 **사용자 관리**를 클릭하십시오.

    사용자가 계정의 구성원이 아닌 경우 [사용자 초대](/docs/iam?topic=iam-iamuserinv#iamuserinv)를 참조하십시오.

4. **정책 액세스 > 액세스 지정 > 리소스에 대한 액세스 지정**을 선택하십시오.

5. **{{site.data.keyword.monitoringlong}}** 서비스를 선택하고 클러스터가 사용 가능한 지역을 선택하십시오. 이 튜토리얼의 경우 **미국 남부**입니다. 그런 다음 **뷰어** 역할을 선택하십시오.



## 3단계: {{site.data.keyword.containershort_notm}} 키 소유자 권한 부여
{: #ks_step3}

클러스터가 메트릭을 계정 도메인에 전달하려면 {{site.data.keyword.containershort}} 키 소유자가 다음 IAM 정책을 보유하고 있어야 합니다.

* {{site.data.keyword.monitoringshort}} 서비스에 대한 **편집기** 권한이 있는 IAM 정책
* {{site.data.keyword.containershort}}에 대한 **관리자** 권한이 있는 IAM 정책


{{site.data.keyword.containershort}} 키 소유자 권한을 부여하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드: [http://bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}을 실행하십시오.
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오. 

    *사용자* 창에 사용자의 목록이 현재 선택된 계정에 대한 해당 이메일 주소와 함께 표시됩니다.
	
3. {{site.data.keyword.containershort}} 키 소유자 사용자 ID를 찾으십시오.

    `ibmcloud cs api-key-info ClusterName` 명령을 실행하여 {{site.data.keyword.containershort}} 키 소유자 사용자 ID를 가져오십시오.

4. **정책 액세스 > 액세스 지정 > 리소스에 대한 액세스 지정**을 선택하십시오.

5. **{{site.data.keyword.monitoringlong}}** 서비스를 선택하고 클러스터가 사용 가능한 지역을 선택하십시오. 이 튜토리얼의 경우 **미국 남부**입니다. 그런 다음 **편집기** 역할을 선택하십시오.	

6. 2 - 4단계를 반복한 후 {{site.data.keyword.containershort}} 서비스를 선택하십시오. **모든 지역**, **관리자** 역할을 선택하십시오.	




## 4단계: Kubernetes 클러스터에 샘플 앱 배치
{: #ks_step4}

Kubernetes 클러스터에 샘플 앱을 배치하고 실행하십시오. 다음 튜토리얼의 단계를 완료하여 샘플 앱을 배치하십시오. [학습 1: Kubernetes 클러스터에 단일 인스턴스 앱 배치](/docs/containers?topic=containers-cs_apps_tutorial#cs_apps_tutorial_lesson1).

이 앱은 Hello World Node.js 앱입니다.

```
var express = require('express')
var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

이 샘플 앱의 경우, 사용자가 브라우저에서 앱을 테스트할 때 앱이 stdout에 다음 메지시를 씁니다. `Sample app is listening on port 8080.`


## 5단계: Grafana 실행 및 메트릭 도메인 설정
{: #ks_step5}

브라우저에서 Grafana를 실행하고 클러스터 메트릭을 볼 수 있는 {{site.data.keyword.monitoringshort}} 도메인을 설정하십시오.

클러스터의 메트릭을 분석하려면 클러스터가 작성된 클라우드 퍼블릭 지역에서 Grafana에 액세스해야 합니다. 자세한 정보는 [웹 브라우저에서 Grafana 대시보드로 이동](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)을 참조하십시오.

1. 브라우저에서 Grafana를 실행하십시오. 

    클러스터를 작성한 지역에 대한 {{site.data.keyword.monitoringshort}} 서비스 URL을 입력하십시오. 
    
    지역별 URL을 가져오려면 [모니터링 서비스에 대한 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)을 참조하십시오.

    예를 들어, 미국 남부 지역의 경우 [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)을 실행하십시오.

2. {{site.data.keyword.monitoringshort}} 도메인을 **계정**으로 설정하십시오.

    Grafana에서 사용자 ID를 선택하십시오. 그런 다음, 올바른 계정인지 확인하고 도메인을 선택하십시오. `Domain = account`를 선택하십시오.

    클러스터가 메트릭을 계정 메트릭 도메인으로 전달합니다. 

## 6단계: Grafana에서 클러스터 모니터링
{: #ks_step6}

{{site.data.keyword.containershort}}에서는 클러스터 메트릭을 모니터링하는 데 사용할 수 있는 Grafana 대시보드를 제공합니다. 

샘플 대시보드를 열려면 다음 단계를 완료하십시오.

1. 측면 메뉴 표시줄 토글 ![Grafana 측면 메뉴 표시줄](images/grafana_settings.gif "Grafana 측면 메뉴 표시줄")을 선택하십시오.
2. **대시보드**를 선택하십시오.
3. **열기**를 클릭하십시오.
4. **ClusterMonitoringDashboard_v1**을 선택하십시오.

샘플 대시보드가 열립니다. 

![Grafana 샘플 대시보드](images/cluster_grafana_sample_dashboard.png "Grafana 샘플 대시보드")



## 다음 단계
{: #ks_next_steps}

메트릭에 대한 경보를 정의하십시오. 자세한 정보는 [경보 구성](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)을 참조하십시오.
