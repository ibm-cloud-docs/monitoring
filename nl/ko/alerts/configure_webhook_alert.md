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


# {{site.data.keyword.monitoringshort}} API를 사용하여 웹훅 경보 구성
{: #configure_webhook_alert}

메트릭에 대한 웹훅 경보를 구성하려면 규칙과 웹훅 알림을 정의하십시오. 그런 다음, 규칙과 알림 방법을 {{site.data.keyword.monitoringshort}} 서비스에 등록하십시오.
{:shortdesc}

다음 단계를 완료하십시오.

## 1단계: 규칙 작성
{: #cwa_step1}

Grafana에서 정의한 메트릭 조회에 대한 규칙을 작성하십시오. 자세한 정보는 [규칙 작성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#create)을 참조하십시오.

예를 들어, 규칙 파일 `s-rule-1.json`을 `~/cloud-monitoring/rules/` 디렉토리에 작성하십시오. 

```
{
    "name": "RULE_NAME",
    "description": "MH check Bytes In per second",
    "expression": "movingAverage(messagehub.65qser11-8034-1234-5678-c82fb42wdfgh.1.kafka-java-console-sample-topic.BytesInPerSec.15MinuteRate,\"5min\")",
    "enabled": true,
    "from": "-5min",
    "until": "now",
    "comparison": "above",
    "comparison_scope": "last",
    "error_level" : 27,
    "warning_level" : 25,
    "frequency": "1min",
    "dashboard_url": "https://metrics.ng.bluemix.net",
    "notifications": [
      "NOTIFICATION_NAME"
    ]
}
```
{: screen}

그 후 *RULE_FILE* 변수를 내보내십시오.
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## 2단계: Monitoring 서비스에서 규칙 등록
{: #cwa_step2}
	
터미널에서 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.

2. 보안 토큰을 가져오십시오. UAA 토큰, IAM 토큰 또는 API 키를 사용할 수 있습니다. 다음 방법 중 하나를 선택하여 보안 토큰을 얻으십시오.
	
	* UAA 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 UAA 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)를 참조하십시오.
	
	* IAM 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)를 참조하십시오.
	
	* API 키를 가져오려면 [API 키 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)를 참조하십시오.
	
	예를 들어, IAM 토큰을 사용하려면 다음 명령을 실행하십시오.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	이 명령의 결과는 다음과 같습니다.
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	그런 다음 *Token* 변수를 내보내십시오.
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**참고:** 토큰에서 *Bearer*가 제외됩니다.
	
3. 영역 GUID를 가져오십시오. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다.

    다음 명령을 실행하십시오.
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	여기서, *SpaceName*은 알림을 정의하는 영역의 이름입니다.
	
	예를 들어, 이름이 *dev*인 영역의 GUID를 가져오려면 다음 명령을 실행하십시오.
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	이 명령의 결과는 다음과 같습니다.
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	그런 다음 *Space* 변수를 내보내십시오.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 규칙을 등록하려면 다음 cURL 명령을 실행하십시오.
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	여기서,
	
	* RULE_FILE은 경보 규칙을 정의하는 JSON 파일입니다.
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
	* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 이 헤더는 UAA 토큰 인증을 사용하는 경우 필요합니다. IAM 인증 토큰을 사용하는 경우 이 헤더는 선택사항이며, 토큰에 바인드된 도메인 정보가 사용됩니다.
	
	* Token은 UAA 또는 IAM 토큰이거나 API 키입니다.
	
	* Space는 영역의 GUID입니다. 
	
	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
	규칙이 작성되었는지 확인하려면 다음 명령을 실행하십시오.
	
	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	예를 들어 다음과 같습니다.

    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## 3단계: 웹훅 알림 작성
{: #cwa_step3}


알림 파일을 작성하려면 다음 정보를 고려하십시오.

* 웹훅 경보에 대한 알림 템플리트를 사용하십시오. 자세한 정보는 [알림 템플리트](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template)를 참조하십시오.
* 로컬 디렉토리에 파일을 작성하십시오(예: `~/cloud-monitoring/notifications`).

예를 들어, vi 편집기를 사용하여 **webhook.json** 파일을 작성하십시오. 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "Webhook",
"description" : "Fire this webhook when ....",
"detail": "https://myendpoint.bluemix.net?key=abcd1234"
}
```
{: codeblock}	

웹훅을 호출하려면 필드 *detail*을 POST를 수행해야 하는 URL로 설정해야 합니다. https 엔드포인트에 대한 웹훅을 구성하고 매개변수를 추가하십시오.
	
자세한 정보는 [알림 작성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#notifications_create)을 참조하십시오.
	
## 4단계: Monitoring 서비스에서 알림 메소드 등록
{: #cwa_step4}
	
터미널에서 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.

2. 보안 토큰을 가져오십시오. UAA 토큰, IAM 토큰 또는 API 키를 사용할 수 있습니다. 다음 방법 중 하나를 선택하여 보안 토큰을 얻으십시오.
	
	* UAA 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 UAA 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)를 참조하십시오.
	
	* IAM 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)를 참조하십시오.
	
	* API 키를 가져오려면 [API 키 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)를 참조하십시오.
	
	예를 들어, IAM 토큰을 사용하려면 다음 명령을 실행하십시오.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	이 명령의 결과는 다음과 같습니다.
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	그런 다음 *Token* 변수를 내보내십시오.
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**참고:** 토큰에서 *Bearer*가 제외됩니다.
	
3. 영역 GUID를 가져오십시오. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다.

    다음 명령을 실행하십시오.
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	여기서, *SpaceName*은 알림을 정의하는 영역의 이름입니다.
	
	예를 들어, 이름이 *dev*인 영역의 GUID를 가져오려면 다음 명령을 실행하십시오.
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	이 명령의 결과는 다음과 같습니다.
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	그런 다음 *Space* 변수를 내보내십시오.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 알림을 등록하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	여기서,
	
	* NOTIFICATION_FILE은 알림을 정의하는 JSON 파일입니다.
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
	* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 이 헤더는 UAA 토큰 인증을 사용하는 경우 필요합니다. IAM 인증 토큰을 사용하는 경우 이 헤더는 선택사항이며, 토큰에 바인드된 도메인 정보가 사용됩니다.
	
	* Token은 UAA 또는 IAM 토큰이거나 API 키입니다.
	
	* Space는 영역의 GUID입니다. 
	
	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
    알림이 작성되었는지 확인하려면 다음 명령을 실행하십시오.

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
