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



# 경보 삭제
{: #delete_alerts}

[경보 API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window}를 사용하여 {{site.data.keyword.monitoringshort}} 서비스에서 경보를 삭제할 수 있습니다.
{:shortdesc}


[{{site.data.keyword.Bluemix_notm}}의 지역에 로그인](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)한 후에 다음 단계를 완료하여 알림을 삭제하십시오.


## 1단계: 보안 토큰 가져오기
{: #step1_delete_alerts}

UAA 토큰, IAM 토큰 또는 API 키를 사용할 수 있습니다. 

다음 방법 중 하나를 선택하여 보안 토큰을 얻으십시오.
	
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
IAM token:  Bearer djn.._l_HWtlNTibmcloudsl0qjBI9GqCnuQ
UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
그런 다음 *Token* 변수를 내보내십시오.
	
```
export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
```
{: screen}
	
**참고:** 토큰에서 *Bearer*가 제외됩니다.
	

## 2단계: 영역 ID 가져오기 
{: #step2_delete_alerts}

이 단계는 영역 도메인에서 사용 가능한 경보를 삭제하려는 경우에만 적용됩니다.

영역 GUID를 가져오려면 다음 명령을 실행하십시오.
	
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
	
그런 다음 *Space* 변수를 내보내십시오. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다.
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## 3단계: 규칙 나열
{: #step3_delete_alerts}


영역 도메인에 정의되어 있는 규칙을 나열하려면 다음 cURL 명령을 실행하십시오.

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules

```
{: screen}

계정 도메인에서 알림을 나열하려면 다음 cURL 명령을 실행하십시오.

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules
```
{: screen}

여기서,
	
* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

    * *apikey*는 토큰이 API 키임을 식별합니다.
	* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
	* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 
	
* Token은 UAA 또는 IAM 토큰이거나 API 키입니다.
	
* Space는 영역의 GUID입니다. 
	
* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.


## 4단계: 경보 규칙 삭제
{: #step4_delete_alerts}
  

영역 도메인의 규칙을 삭제하려면 다음 cURL 명령을 실행하십시오.

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

계정 도메인에서 규칙을 삭제하려면 다음 cURL 명령을 실행하십시오.

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

	
여기서,
	
* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

    * *apikey*는 토큰이 API 키임을 식별합니다.
	* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
	* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 
	
* Token은 UAA 또는 IAM 토큰이거나 API 키입니다.
	
* Space는 영역의 GUID입니다. 
	
* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.

* *name*은 삭제하려는 규칙의 이름입니다.
	
