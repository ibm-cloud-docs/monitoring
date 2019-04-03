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


# 경보 API를 사용하여 경보의 히스토리 검색
{: #retrieve_history}

경보 API를 사용하여 경보의 히스토리를 검색하십시오. 
{:shortdesc}


경보 API를 사용하여 경보의 히스토리를 검색하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.

2. 보안 토큰을 가져오십시오. UAA 토큰, IAM 토큰 또는 API 키를 사용할 수 있습니다. 다음 방법 중 하나를 선택하여 보안 토큰을 얻으십시오.
	
	* UAA 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 UAA 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)를 참조하십시오.
	
	* IAM 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)를 참조하십시오.
	
	* API 키를 가져오려면 [API 키 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)를 참조하십시오.
	
	{{site.data.keyword.Bluemix_notm}}에 로그인한 것과 동일한 터미널에서 토큰에 대한 Token 변수를 설정하십시오.

    예를 들어, IAM 토큰을 사용하려면 다음 명령을 실행하십시오.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	이 명령의 결과는 다음과 같습니다.
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	그런 다음 *Token* 변수를 내보내십시오.
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
	그런 다음 *Space* 변수를 내보내십시오. **참고:** 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다.
	
	예를 들어 다음과 같습니다.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 규칙의 히스토리 검색

    * 해당 이름을 사용하여 규칙의 히스토리를 검색하려면 [해당 이름을 사용하여 규칙의 히스토리 검색](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_name)을 참조하십시오.
	* 일정 기간 동안의 규칙 히스토리를 검색하려면 [최근 48시간 동안의 규칙 히스토리 검색](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_time)을 참조하십시오.
	* 규칙의 히스토리에서 여러 항목을 검색하려면 [규칙의 히스토리에서 최근 3개의 항목 검색](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#number)을 참조하십시오.
	
	
## 규칙 이름을 사용하여 규칙의 히스토리 검색
{: #by_name}
	
경보의 히스토리를 가져오려면 다음 cURL 명령을 실행하십시오.

```
curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/history?rule_name=RULE_NAME
```
{: codeblock}
	
여기서,
	
* *X-Auth-User-Token*은 UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

    * *apikey*는 토큰이 API 키임을 식별합니다.
	* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
	* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 이 헤더는 UAA 토큰 인증을 사용하는 경우 필요합니다. IAM 인증 토큰을 사용하는 경우 이 헤더는 선택사항이며, 토큰에 바인드된 도메인 정보가 사용됩니다.
	
* *Token*은 UAA 또는 IAM 토큰이거나 API 키입니다.
	
* *Space*는 영역의 GUID입니다. 
	
* *RULE_NAME*은 이 경보를 트리거하는 데 사용되는 규칙의 이름입니다. 이 값은 *name* 필드에 지정된 값입니다.
	
* *METRICS_ENDPOINT*는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
    
예를 들어, 규칙 `highNginxCPU`의 히스토리는 다음과 같습니다.

```
curl -XGET --header "X-Auth-User-Token: iam ${Token}" --header "X-Auth-Scope-Id: ${Space}" https://metrics.ng.bluemix.net/v1/alert/history?rule_name=highNginxCPU
```
{: screen}

```
[
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T22.23.21.000",
 "value": 99.5,
 "from_level": "OK",
 "to_level": "ERROR"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.11.12.123",
 "value": 98.5,
 "from_level" : "OK",
 "to_level": "WARN"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.12.14.000",
 "value": 97.0,
 "from_level" : "WARN",
 "to_level": "OK"
 }
]
```
{: screen}


## 최근 48시간 동안의 규칙 히스토리 검색
{: #by_time}

최근 48시간 동안의 경보 히스토리를 가져오려면 다음 cURL 명령을 실행하십시오.

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?start=-48h
```
{: codeblock}

여기서,
	
* *X-Auth-User-Token*은 UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

    * *apikey*는 토큰이 API 키임을 식별합니다.
	* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
	* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 이 헤더는 UAA 토큰 인증을 사용하는 경우 필요합니다. IAM 인증 토큰을 사용하는 경우 이 헤더는 선택사항이며, 토큰에 바인드된 도메인 정보가 사용됩니다.
	
* *Token*은 UAA 또는 IAM 토큰이거나 API 키입니다.
	
* *Space*는 영역의 GUID입니다. 
	
* *RULE_NAME*은 이 경보를 트리거하는 데 사용되는 규칙의 이름입니다. 이 값은 *name* 필드에 지정된 값입니다.
	
* *METRICS_ENDPOINT*는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	

## 규칙의 히스토리에서 최근 3개의 항목 검색
{: #number}

경보의 히스토리에서 최근 3개의 항목을 가져오려면 다음 cURL 명령을 실행하십시오.

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?max_results=3
```
{: codeblock}

여기서,
	
* *X-Auth-User-Token*은 UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

    * *apikey*는 토큰이 API 키임을 식별합니다.
	* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
	* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 이 헤더는 UAA 토큰 인증을 사용하는 경우 필요합니다. IAM 인증 토큰을 사용하는 경우 이 헤더는 선택사항이며, 토큰에 바인드된 도메인 정보가 사용됩니다.
	
* *Token*은 UAA 또는 IAM 토큰이거나 API 키입니다.
	
* *Space*는 영역의 GUID입니다. 
	
* *RULE_NAME*은 이 경보를 트리거하는 데 사용되는 규칙의 이름입니다. 이 값은 *name* 필드에 지정된 값입니다.
	
* *METRICS_ENDPOINT*는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
