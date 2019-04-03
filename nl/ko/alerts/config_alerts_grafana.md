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

# Grafana에서 경보 구성
{: #config_alerts_grafana}

{{site.data.keyword.monitoringshort}} 서비스는 조회 기반 경보 시스템을 제공합니다. 템플리트 변수가 없는 대시보드에서 Grafana의 경보를 구성할 수 있습니다. 
{:shortdesc}

Grafana UI를 통해 메트릭 조회에 대한 경보를 구성하려면 다음 단계를 완료하십시오.

1. Grafana를 실행하십시오.
2. 하나 이상의 알림 채널을 정의하십시오.
3. 그래프 및 하나 이상의 조회 메트릭을 포함하는 Grafana 대시보드를 작성하십시오. 
4. Grafana 그래프에서 **경보** 탭을 통해 경보를 구성하십시오.

## 1단계: Grafana 실행
{: #step1_cag1}

브라우저에서 Grafana를 실행하십시오. 예를 들어, 다음 URL을 입력하여 미국 남부 지역에서 Grafana를 여십시오. [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

지역별 Grafana URL 목록을 보려면 [{{site.data.keyword.monitoringshort}} 서비스 URL](/docs/services/cloud-monitoring/monitoring_ov.html#region)을 참조하십시오.

## 2단계: 하나 이상의 알림 채널 정의
{: #step2_cag2}

다음 단계를 완료하십시오.

1. Grafana에서 측면 메뉴 표시줄을 선택하십시오.

2. **경보 > 알림 채널 > 새 채널**을 선택하십시오.

3. 새 채널에 대한 데이터를 입력하십시오. 예를 들어, 이메일 알림 채널을 추가하십시오.

<table>
  <caption>새 채널을 작성하기 위해 반드시 입력해야 하는 이메일 알림 방법 및 데이터</caption>
  <tr>
     <th>필드</th>
     <th>설명</th>
  </tr>
  <tr>
    <td>이름</td>
    <td>알림 채널의 이름. 이 값은 고유해야 합니다.</td>
  </tr>
  <tr>
    <td>설명</td>
    <td>사용자가 문서화하기 위해 포함하려는 추가 정보가 있습니다.</td>
  </tr>
  <tr>
    <td>Type</td>
    <td>선택: **이메일**</td>
  </tr>
  <tr>
    <td>이메일 ID</td>
    <td>수신자의 이메일 주소를 입력하십시오. </br>쉼표로 구분된 다중 이메일 주소를 입력할 수 있습니다.</td>
  </tr>
</table>

<table>
  <caption>새 채널을 작성하기 위해 반드시 입력해야 하는 웹훅 알림 방법 및 데이터</caption>
  <tr>
     <th>필드</th>
     <th>설명</th>
  </tr>
  <tr>
    <td>이름</td>
    <td>알림 채널의 이름. 이 값은 고유해야 합니다.</td>
  </tr>
  <tr>
    <td>설명</td>
    <td>사용자가 문서화하기 위해 포함하려는 추가 정보가 있습니다.</td>
  </tr>
  <tr>
    <td>Type</td>
    <td>선택: **웹훅**</td>
  </tr>
  <tr>
    <td>웹훅 POST URL</td>
    <td>POST를 수행해야 하는 URL을 입력하십시오.</td>
  </tr>
  <tr>
    <td>웹훅 헤더</td>
    <td>임의의 헤더를 입력하십시오.</td>
  </tr>
  <tr>
    <td>웹훅 조회 매개변수</td>
    <td>임의의 조회 매개변수를 입력하십시오.</td>
  </tr>
</table>

<table>
  <caption>새 채널을 작성하기 위해 반드시 입력해야 하는 PagerDuty 알림 방법 및 데이터</caption>
  <tr>
     <th>필드</th>
     <th>설명</th>
  </tr>
  <tr>
    <td>이름</td>
    <td>알림 채널의 이름. 이 값은 고유해야 합니다.</td>
  </tr>
  <tr>
    <td>설명</td>
    <td>사용자가 문서화하기 위해 포함하려는 추가 정보가 있습니다.</td>
  </tr>
  <tr>
    <td>Type</td>
    <td>선택: **PagerDuty**</td>
  </tr>
  <tr>
    <td>PagerDuty API 키</td>
    <td>PagerDuty 키를 입력하십시오.</td>
  </tr>
</table>

## 3단계: 메트릭 정의
{: #step3_cag3}

새 대시보드를 작성하려면 다음 단계를 완료하십시오.

1. 측면 메뉴 표시줄 토글 ![Grafana 측면 메뉴 표시줄](images/grafana_settings.gif "Grafana 측면 메뉴 표시줄")을 선택하십시오.
2. **대시보드**를 선택하십시오.
3. **새로 작성**을 클릭하십시오.

대시보드가 열립니다. 이 대시보드는 구성할 준비가 된 비어 있는 행을 포함하고 있습니다. 

다음으로, 메트릭 조회를 추가하십시오.

1. *그래프* 패널을 추가하십시오.
2. **그래프**를 선택하십시오.
3. 그래프 제목을 클릭한 후 **편집**을 선택하십시오.
    
    *메트릭* 탭이 열립니다. 여기서는 기본 데이터 소스를 볼 수 있습니다.
    
4. 그래프에 표시되는 데이터를 필터링하는 메트릭 조회를 정의하십시오. 


## 4단계: 경보 정의
{: #step4_cag4}

Grafana UI에서 경보를 정의하려면 다음 단계를 완료하십시오.

1. **경보** 탭을 선택하십시오.
2. **경보 구성** 섹션에서 경보 알림이 생성되는 조건을 정의하는 규칙을 정의하십시오.

    **항상 평가** 필드 및 **조건** 섹션을 구성하십시오.

3. **알림** 섹션에서 하나 이상의 알림 채널을 선택하십시오.

**참고:** 

* 조건이 설정되면 그래프에서 빨간 선을 보고 임계값 세트를 정의할 수 있습니다. 이를 그래프로 끌어 변경할 수 있습니다.
* 일단 경보가 작성되고 나면 수정이 필요한 경우에 반드시 경보 API를 사용하여 수정해야 합니다.
* **삭제**를 선택하면 경보가 삭제됩니다.

## 다음: 경보 생성 여부 확인
{: #next_cag5}

예를 들어, 이메일 알림 채널을 작성한 경우, 이메일을 확인하십시오.

**IBM Cloud Monitoriing**이라는 송신자로 이메일을 찾으십시오.

이메일에는 격상된 경보에 대한 정보 및 상황을 볼 수 있는 Grafana 대시보드에 대한 링크가 포함됩니다.

예를 들어 다음과 같습니다.

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level :
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


