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



# 경보 구성
{: #config_alerts_ov}

{{site.data.keyword.monitoringshort}} 서비스는 조회 기반 경보 시스템을 제공합니다. {{site.data.keyword.monitoringshort}} API를 사용하거나 Grafana를 통해 경보를 구성할 수 있습니다. 경보를 구성하려면 모니터링할 각 메트릭 조회에 대해 규칙 및 알림 방법을 설정해야 합니다. 알림은 이메일을 발송하거나, 웹훅을 트리거하거나 PagerDuty에 경보를 전송하여 수행할 수 있습니다.
{:shortdesc}

메트릭에 대한 알림을 트리거하는 경보를 정의할 수 있습니다. 경보는 모니터되는 메트릭 조회, 임계값, 임계값을 초과하는 경우 취할 조치, 하나 이상의 알림 방법을 나타내는 규칙으로 정의합니다.  

다음 표에는 경보에 대해 작업할 때 사용할 수 있는 다양한 방법 및 지원되는 조치가 나열되어 있습니다.

<table>
  <caption>경보에 대해 작업하는 방법</caption>
	<tr>
    <th>방법</th>
		<th>경보 정의</th>
		<th>경보 업데이트</th>
		<th>경보 삭제</th>
	</tr>
	<tr>
    <td>경보 API</td>
		<td>예</td>
		<td>예</td>
		<td>예</td>
	</tr>
	<tr>
    <td>Grafana</td>
		<td>예</td>
		<td>예</td>
		<td>예</td>
	</tr>
</table>

**참고:** 경보 API를 사용하여 정의하는 경보는 Grafana 대시보드에 표시되지 않습니다.


다음 그림은 알림을 수신하기 위해 {{site.data.keyword.monitoringshort}} 서비스에 구성할 수 있는 다양한 알림 유형을 보여줍니다.

![{{site.data.keyword.monitoringlong}} 서비스에서 사용 가능한 알림 유형에 대한 상위 레벨 컴포넌트 개요](images/alerts_ov_f1.gif)

하나의 인스턴스 또는 여러 인스턴스에 대한 경보를 정의할 수 있습니다. 경보 규칙을 통해 모니터링하는 조회가 와일드카드를 포함하는 경우 이 와일드카드는 여러 대상, 즉 여러 서비스 인스턴스 또는 애플리케이션 인스턴스를 식별합니다. {{site.data.keyword.monitoringshort}} 서비스는 5분마다 경보 규칙에 구성된 조회를 실행하고 각 인스턴스 또는 여러 인스턴스에 대해 리턴된 마지막 데이터 점을 확인합니다. {{site.data.keyword.monitoringshort}} 서비스는 각 인스턴스의 마지막 상태 업데이트를 계속해서 추적하며, 경보의 상태가 변경되면 새 경보를 생성합니다. 



## 경보 API를 사용하여 경보에 대한 작업 수행
{: #api}

경보 API를 사용하여 경보를 정의, 업데이트 또는 삭제할 수 있습니다.

경보 API를 사용하여 메트릭 조회에 대한 경보를 정의하려면 다음을 수행해야 합니다.

1. Grafana 대시보드에서 하나 이상의 메트릭 조회를 정의하십시오. 

    **참고:** 템플리트 변수를 사용하는 Grafana 대시보드에서는 경보를 정의할 수 없습니다.

2. Grafana 대시보드에서 정의된 메트릭 조회에 대한 경보를 구성하십시오.

    * [이메일을 발송하는 경보 구성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-configure_email_alert#configure_email_alert).
    * [PagerDuty 알림을 발송하는 경보 구성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-configure_pagerduty_alert#configure_pagerduty_alert).
    * [웹훅 알림을 발송하는 경보 구성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-configure_webhook_alert#configure_webhook_alert).

    **참고:** 계정 메트릭 도메인에서 정의된 메트릭 조회에 대해서만 이메일 알림을 정의할 수 있습니다.



## Grafana를 사용하여 경보에 대한 작업 수행
{: #grafana}

Grafana 대시보드에서 직접 경보를 정의하고 삭제할 수 있습니다. 규칙 정의도 업데이트할 수 있습니다. 단, 알림 채널 변경은 경보 API를 사용하여 수행해야 합니다.

Grafana에서 경보에 대해 작업할 때 다음 정보를 고려하십시오.

* 규칙에 지정된 알림 채널을 수정하려면 경보 API를 사용해야 합니다.
* 영역 도메인에서 알림 채널을 삭제할 때 해당 채널이 구성된 규칙은 업데이트되지 않습니다. 경보 API를 사용하여 규칙을 수정하고 해당 알림 채널을 제거해야 합니다. 

Grafana 대시보드에서 직접 메트릭 조회에 대한 경보를 정의하려면 다음을 수행해야 합니다.

1. Grafana 대시보드에서 하나 이상의 메트릭 조회를 정의하십시오. 

    **참고:** 템플리트 변수를 사용하는 Grafana 대시보드에서는 경보를 정의할 수 없습니다.

2. Grafana 대시보드에서 정의된 메트릭 조회에 대한 경보를 구성하십시오.

    자세한 정보는 [Grafana에서 경보 구성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-config_alerts_grafana#config_alerts_grafana)을 참조하십시오.


## 경보 상태
{: #status}

규칙이 사용으로 설정된 경우 경보의 상태는 다음 중 하나일 수 있습니다.

* *OK*: 규칙의 상태는 다음 경우에 *OK*로 설정됩니다.
    
	* 규칙과 연관된 메트릭 조회에 대해 {{site.data.keyword.monitoringshort}} 서비스에 데이터가 있습니다. 사용자가 경고 임계값 및 오류 임계값을 설정했습니다. 데이터의 값이 임계값을 초과하지 않았습니다.
	 
	* 규칙과 연관된 메트릭 조회에 대해 {{site.data.keyword.monitoringshort}} 서비스에 데이터가 없으며 규칙 특성 `allow_no_data`를 *true*로 설정했습니다.           
	 
* *WARNING*: 규칙과 연관된 메트릭 조회에 대해 {{site.data.keyword.monitoringshort}} 서비스에 데이터가 있으며 다음 조건을 만족하는 경우 규칙의 상태가 *WARNING*으로 설정됩니다. 사용자가 경고 임계값 및 오류 임계값을 설정했습니다. 데이터의 값이 경고 임계값과 오류 임계값의 사이입니다.
	
* *ERROR*: 규칙과 연관된 메트릭 조회에 대해 {{site.data.keyword.monitoringshort}} 서비스에 데이터가 있으며 다음 조건을 만족하는 경우 규칙의 상태가 *ERROR*로 설정됩니다. 사용자가 경고 임계값 및 오류 임계값을 설정했습니다. 데이터의 값이 오류 임계값에 도달했습니다.  

* *UNKNOWN*: 규칙과 연관된 메트릭 조회에 대해 {{site.data.keyword.monitoringshort}} 서비스에 데이터가 없는 경우 규칙의 상태가 *UNKNOWN*으로 설정됩니다. 규칙에 대해 구성하는 특성 `allow_no_data`에 따른 알림 수신 여부를 구성할 수 있습니다. 이 특성을 `false`로 설정하면 규칙에 대해 데이터를 찾지 못했다는 알림을 수신합니다.



	
## 경보 히스토리
{: #history}

경보의 상태가 변경될 때마다 해당 경보의 히스토리 레코드가 업데이트됩니다. 경보 API(*/v1/alert/history*)를 사용하여 메트릭의 히스토리에 대한 정보를 검색할 수 있습니다.

경보의 상태는 다음 시나리오의 상태를 정의하는 데 사용됩니다.

* 규칙이 알림을 트리거하기 전의 조회 상태.
* 규칙이 트리거된 후의 조회 상태. 

예를 들어, 경고 임계값이 초과된 경우에는 *OK*에서 *WARNING*으로의 상태 전이를 기록하는 히스토리 레코드가 생성됩니다. 마찬가지로, 값이 다시 임계값 미만으로 내려가면 *WARNING*에서 *OK*로의 상태 전이를 기록하는 히스토리 레코드가 생성됩니다.

자세한 정보는 [규칙의 히스토리 검색](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#retrieve_history)을 참조하십시오.


## 규칙
{: #rules1}

규칙은 모니터되는 메트릭 조회, 임계값, 임계값을 초과하는 경우 취할 조치를 나타냅니다. 

* 경보 API를 사용하여 규칙을 작성하거나, 삭제하거나, 업데이트하거나, 규칙의 세부사항을 표시하거나, 모든 규칙을 나열할 수 있습니다. 자세한 정보는 [규칙에 대한 작업](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#rules)을 참조하십시오.

    * 규칙을 작성하려면 [규칙 작성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#create)을 참조하십시오.
	* 규칙을 삭제하려면 [규칙 삭제](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#delete)를 참조하십시오.
	* 규칙을 업데이트하려면 [규칙 업데이트](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#update)를 참조하십시오.
	* 모든 규칙을 나열하려면 [모든 규칙 나열](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#list)을 참조하십시오.
	* 규칙에 대한 정보를 표시하려면 [규칙의 세부사항 표시](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#showing-the-details-of-a-rule)를 참조하십시오.

* 경보 시스템은 영역에서 사용으로 설정된 규칙을 5분마다 확인합니다.

* 기본적으로 규칙은 작성 시 사용으로 설정됩니다. 그러나 규칙을 정의하고 필드 *enable*을 `false`로 구성하여 이를 사용 안함으로 설정할 수 있습니다.

* 규칙 매개변수 *comparison*이 below로 설정된 경우 error_level 값은 warning_level 값보다 낮아야 합니다. 규칙 매개변수 *comparison*이 above로 설정된 경우 error_level 값은 warning_level 값보다 높아야 합니다.

* 기본적으로 규칙은 필드 *allow_no_data*가 `true`로 설정되어 작성됩니다. 데이터 점이 없는 경우, 알림은 규칙 조건이 트리거되지 않는 한 전송되지 않습니다. 규칙 X에 대해 데이터를 찾지 못했다는 알림을 수신하려면 필드 *allow_no_data*를 `false`로 설정해야 합니다. 

**팁:** 경보 규칙을 통해 모니터링하는 조회를 Grafana에서 확인하십시오. 제한시간을 초과하지 않는지 확인하십시오. 예를 들어, 긴 기간을 구성하거나 와일드카드를 포함하는 조회를 정의하는 경우, 조회가 제한시간을 초과할 수 있습니다. 조회가 Grafana에서 제한시간을 초과하는 경우 해당 조회에 대해 구성된 경보가 트리거되지 않는다는 점을 참고하십시오.

규칙을 정의하려면 다음 필드가 필요합니다.

<table>
  <caption>표 1. 규칙을 정의하는 데 사용되는 필드의 목록</caption>
  <tr>
    <th>필드 이름</th>
	<th>설명</th>
  </tr>
  <tr>
    <td>이름</td>
	<td>규칙의 이름입니다. 이 이름은 고유해야 합니다.</td>
  </tr>
  <tr>
    <td>description</td>
	<td>규칙의 요약입니다.</td>
  </tr>
  <tr>
    <td>expression</td>
	<td>모니터하고 임계값이 초과되는 경우 경보를 전송할 메트릭 조회입니다. <br>유효한 표현식은 단일 메트릭 이름, 와일드카드로 식별되는 복수 메트릭 또는 데이터를 집계하기 위한 함수입니다. <br>**팁:** Grafana로부터 확인된 조회를 복사할 수 있습니다.</td>
  </tr>
  <tr>
    <td>enabled</td>
	<td>규칙의 상태를 나타냅니다. <br>규칙을 사용으로 설정하려면 `true`로 설정하십시오. <br>규칙을 사용 안함으로 설정하려면 `false`로 설정하십시오. <br>기본적으로 이는 `true`로 설정됩니다.</td>
  </tr>
  <tr>
    <td>from</td>
	<td>expression 필드에 정의한 조회에 대해 설정한 임계값을 기반으로 데이터를 분석하는 데 사용되는 초기 시점입니다. 예: `"from": "-5min"`</td>
  </tr>
  <tr>
    <td>until</td>
	<td>expression 필드에 정의한 조회에 대해 설정한 임계값을 기반으로 데이터를 분석하는 데 사용되는 종료 시점입니다. 예: `"until": "now"`</td>
  </tr>
  <tr>
    <td>comparison</td>
	<td>어떤 유형의 확인을 수행할지 식별하는 데 사용되는 비교 오퍼레이션입니다. 올바른 값은 *below* 및 *above*입니다. </td>
  </tr>
  <tr>
    <td>comparison_scope</td>
	<td>분석되는 데이터의 범위를 정의합니다. <br>계열(조회에서 사용 가능한 데이터)의 마지막 값을 살펴보려면 *last*로 설정하십시오.</td>
  </tr>
  <tr>
    <td>error_level</td>
	<td>오류 경보를 트리거하기 위해 설정하는 임계값을 정의합니다. <br>도달하는 경우 오류 경보가 생성되는 값을 설정하십시오. 예: `"error_level" : 27.94`</td>
  </tr>
  <tr>
    <td>warning_level</td>
	<td>경고 경보를 트리거하기 위해 설정하는 임계값을 정의합니다. <br>도달하는 경우 경고 경보가 생성되는 값을 설정하십시오. 예: `"warning_level" : 24`</td>
  </tr>
  <tr>
    <td>frequency</td>
	<td>확인 수행 빈도를 정의합니다. <br>이는 5min, 1h, 7d와 같이 분, 시간 또는 일로 측정됩니다. <br>예를 들어, 1분마다 확인하려는 경우에는 `"frequency": "1min"`을 설정할 수 있습니다. <br>**참고:** 현재 이 빈도는 5분으로 고정되어 있습니다.</td>
  </tr>
  <tr>
    <td>dashboard_url</td>
	<td>모니터되는 조회가 정의된 Grafana 대시보드에 대한 URL을 정의합니다.</td>
  </tr>
    <tr>
    <td>allow_no_data</td>
	<td>데이터 점이 없는 경우 알림을 전송하는 조건을 정의합니다. <br>기본적으로 이는 `true`로 설정됩니다. <br>규칙 X에 대해 데이터를 찾지 못했다는 알림을 수신하려면 `false`로 설정하십시오.</td>
  </tr>
  <tr>
    <td>notifications</td>
	<td>규칙에 대해 트리거할 조치를 정의하는 알림의 이름입니다. <br>**참고:** 알림 이름을 쉼표로 구분하여 나열함으로써 규칙당 하나 이상의 알림을 정의할 수 있습니다.</td>
  </tr>
</table>

예를 들면, 다음 항목은 규칙의 샘플입니다.

```
{
  "name": "checkbytesin1",
  "description": "MH check Bytes In per second",
  "expression": "movingAverage(messagehub.65ad9211-1234-5678-a751-c82123411eee.1.kafka-java-console-sa
mple-topic.BytesInPerSec.15MinuteRate,\"5min\")",
  "enabled": true,
  "from": "-5min",
  "until": "now",
  "comparison": "below",
  "comparison_scope": "last",
  "error_level" : 22.94,
  "warning_level" : 25,
  "frequency": "1min",
  "dashboard_url": "https://metrics.ng.bluemix.net",
  "notifications": [
    "emailXXX"
  ]
}
```
{: screen}



## 알림
{: #alert_notifications}

알림은 경보가 트리거된 경우 알리는 데 사용되는 방법 및 세부사항을 나타냅니다. 예를 들어, 메트릭에 대한 경고 알림 및 오류 알림을 받으려면 경고 임계값을 모니터링하는 규칙 및 오류 임계값을 모니터링하는 규칙을 정의하십시오. 

* 알림은 메트릭에 대한 경보의 상태가 "OK"에서 "ERROR"로, 또는 "ERROR"에서 "WARNING"으로 변경되는 경우와 같이 경보의 상태가 변경되는 경우에만 전송됩니다. 

    **참고:** 경보 규칙 상태가 *OK*, *WARNING*, *ERROR* 또는 *UNKNOWN*에서 변경되지 않는 경우 이는 다음 반복 시에 다시 트리거되지 않습니다.

* 알림은 24시간 이벤트로 간주됩니다. 알림이 트리거될 수 있는 시간 간격을 지정할 수는 없습니다.

* 알림 이름을 쉼표로 구분하여 나열함으로써 규칙당 하나 이상의 알림 방법을 구성할 수 있습니다. 

* [Alerts REST API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window}를 사용하여 알림을 작성하거나, 삭제하거나, 업데이트하거나, 알림의 세부사항을 표시하거나, 영역에 정의된 알림을 나열하십시오.

    * 알림을 작성하려면 [알림 작성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#notifications_create)을 참조하십시오.
	* 알림을 삭제하려면 [알림 삭제](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#notifications_delete)를 참조하십시오.
	* 알림을 업데이트하려면 [알림 업데이트](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#notifications_update)를 참조하십시오.
	* 모든 알림을 나열하려면 [모든 알림 나열](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#notifications_list)을 참조하십시오.
	* 알림에 대한 정보를 표시하려면 [알림의 세부사항 표시](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#show)를 참조하십시오.

* 이메일 알림, PagerDuty 구성 및 웹훅 알림을 구성할 수 있습니다. 

**참고:** 여러 규칙에 대해 알림을 재사용할 수 있도록 규칙과 별개로 알림을 정의할 수 있습니다.

	
## 알림 - JSON 템플리트
{: #notification_template}
	
알림은 JSON 파일입니다. 

다음 표에는 알림 방법의 유형에 대한 알림 템플리트가 포함되어 있습니다.

<table>
  <caption>표 3. 알림 템플리트</caption>
  <tr>
    <th>Type</th>
	<th>템플리트</th>
	<th>샘플</th>
  </tr>
  <tr>
    <td>이메일</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Email",
	"description" : "Description",
	"detail": "EmailAddress"
	}
	```
	{: screen}
	</td>
	<td>
	```
	{
	"name": "my-email",
	"type": "Email",
	"description" : "Send email notification when there is an infrastructure problem.",
	"detail": "xxx@yyy.com"
	}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>웹훅</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Webhook",
	"description" : "Description",
	"detail": "Endpoint"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-webhook",
	"type": "Webhook",
	"description" : "Fire a webhook when there is an infrastructure problem..",
	"detail": "https://myendpoint.bluemix.net?key=abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>PagerDuty</td>
	<td>
	```
	"name": "Template_Name",
	"type": "PagerDuty",
	"description" : "Description",
	"detail": "Pagerduty_APIkey"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-pagerduty",
	"type": "PagerDuty",
	"description" : "Fire a PagerDuty alert when there is an infrastructure problem..",
	"detail": "abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
</table>

여기서,

* *Template_Name*은 알림 템플리트의 이름을 정의합니다.
* *Description*은 이 유형의 알림을 사용하는 경우를 설명합니다.
* *EmailAddress*는 알림 수신자의 이메일 주소를 정의합니다.
* *Endpoint*는 POST를 수행해야 하는 URL을 정의합니다. 
* *Pagerduty_APIkey*는 고유 API 키를 정의합니다. 이 API 키는 PagerDuty 계정 관리자 또는 소유자가 생성합니다.



## 규칙-JSON 템플리트
{: #rules_template}

규칙은 JSON 파일을 사용하여 설명됩니다. 

다음 코드는 규칙의 템플리트입니다.

```
{
"name": "Enter rule name",
"description": "Desccribe rule",
"expression": "Add metric query",
"enabled": true,
"from": "-5min",
"until": "now",
"comparison": "below",
"comparison_scope": "last",
"error_level" : xxxx,
"warning_level" : xxxx,
"frequency": "1min",
"dashboard_url": "https://metrics.ng.bluemix.net",
"notifications": [
 "List of Notifications by name. Include all the motification methods for this rule separated by commas."
 ]
}
```
{: screen}



