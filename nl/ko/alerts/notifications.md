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


# CRUD 알림
{: #notifications}

경보 API를 사용하여 알림을 작성하거나 삭제하거나 업데이트하거나 알림의 세부사항을 표시하거나 영역에 정의된 알림을 나열하십시오.
{:shortdesc}

## 알림 작성
{: #notifications_create}

알림을 작성하려면 다음 단계를 완료하십시오.

1. 알림 파일을 작성하십시오.

    1. 알림 템플리트를 사용하여 알림 파일을 작성하십시오. 자세한 정보는 [알림 템플리트](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template)를 참조하십시오.
	
	2. 파일을 업데이트하십시오.
	
	    * 필드 *name*에 고유 이름을 입력하십시오. 이 필드의 값은 나중에 알림의 세부사항을 업데이트하거나, 삭제하거나 표시하는 데 사용됩니다.
		* 설명을 입력하십시오.
		* 유효한 이메일 주소, URL 엔드포인트 또는 PagerDuty 키를 입력하십시오.
		
	3. 파일을 저장하십시오. 예를 들어, 영역에서 실행되는 조회에 대해 정의하는 알림에 *s-*와 같은 접두부를 사용하십시오.
	
	    **팁:** {{site.data.keyword.monitoringshort_notm}} 서비스의 리소스를 그룹화하려면 디렉토리 *~/cloud-monitoring/notifications/*에서 알림 파일을 작성하십시오. 
	
	4. *NOTIFICATION_FILE* 변수를 내보내십시오.
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.

3. 보안 토큰을 가져오십시오. UAA 토큰, IAM 토큰 또는 API 키를 사용할 수 있습니다. 다음 방법 중 하나를 선택하여 보안 토큰을 얻으십시오.
	
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
	
4. 영역 GUID를 가져오십시오. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다.

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
	
5. {{site.data.keyword.monitoringshort}} 서비스에 알림을 등록하십시오.

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	여기서,
	
	* NOTIFICATION_FILE은 알림을 정의하는 JSON 파일입니다.
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
	* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 이 헤더는 UAA 토큰 인증을 사용하는 경우 필요합니다. IAM 인증 토큰을 사용하는 경우 이 헤더는 선택사항이며, 토큰에 바인드된 도메인 정보가 사용됩니다.
	
	* Token은 UAA 토큰, IAM 토큰 또는 API 키입니다.
	
	* Space는 영역의 GUID입니다. 
	
	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
    예를 들어 다음과 같습니다. 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## 알림 삭제
{: #notifications_delete}

알림을 삭제하려면 다음 단계를 완료하십시오.

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
	
	그런 다음 *Space* 변수를 내보내십시오.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 알림을 삭제하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	여기서,
	
	* *X-Auth-User-Token*은 UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다. 토큰 또는 API 키에는 *apikey*, *iam* 또는 *uaa* 값 중 하나로 접두부가 지정되어야 합니다. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
		
	* Token은 UAA 토큰, IAM 토큰 또는 API 키입니다.
	
	* Space는 영역의 GUID입니다. 
	
	* Notification_Name은 알림의 이름, 즉 알림의 특성을 나열했을 때 필드 *name*의 값입니다.
	
	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	


## 알림 모두 나열
{: #notifications_list}

알림을 모두 나열하려면 다음 단계를 완료하십시오.

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
	
	그런 다음 *Space* 변수를 내보내십시오.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 모든 알림을 나열하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	여기서,
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
		
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다. 토큰 또는 API 키에는 *apikey*, *iam* 또는 *uaa* 값 중 하나로 접두부가 지정되어야 합니다. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
		
	* Token은 UAA 토큰, IAM 토큰 또는 API 키입니다.
	
	* Space는 영역의 GUID입니다. 
	
	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.

			

## 알림 세부사항 표시
{: #show}


알림에 대한 정보를 표시하려면 다음 단계를 완료하십시오.

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
	
	그런 다음 *Space* 변수를 내보내십시오.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 알림의 세부사항을 표시하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	여기서,
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
		
	* Token은 UAA 토큰, IAM 토큰 또는 API 키입니다.
	
	* Space는 영역의 GUID입니다. 
	
	* NOTIFICATION_NAME은 알림의 이름, 즉 알림의 특성을 나열했을 때 필드 *name*의 값입니다.
	
	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
     
		

			
## 알림 테스트
{: #test}	
			
알림을 테스트하려면 다음 단계를 완료하십시오.

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
	
	그런 다음 *Space* 변수를 내보내십시오.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 알림을 테스트하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	여기서,
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다. 토큰 또는 API 키에는 *apikey*, *iam* 또는 *uaa* 값 중 하나로 접두부가 지정되어야 합니다. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
		
	* Token은 UAA 토큰, IAM 토큰 또는 API 키입니다.
	
	* Space는 영역의 GUID입니다. 
	
	* NOTIFICATION_NAME은 알림의 이름, 즉 알림의 특성을 나열했을 때 필드 *name*의 값입니다.
	
	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	


## 알림 업데이트
{: #notifications_update}

알림을 업데이트하려면 다음 단계를 완료하십시오.

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
	
	그런 다음 *Space* 변수를 내보내십시오.
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 알림을 업데이트하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	여기서,
	
	* NOTIFICATION_FILE은 알림을 정의하는 JSON 파일입니다.
	
	* *Auth_Type*은 토큰 또는 API 키의 유형을 정의하는 접두부입니다. 다음 목록에는 올바른 값이 간략하게 설명되어 있습니다: *apikey*, *iam*, *uaa*. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
	
	* *X-Auth-User-Token*은 bluemix UAA 토큰, IAM 토큰 또는 API 키를 전달하는 매개변수입니다. 토큰 또는 API 키에는 *apikey*, *iam* 또는 *uaa* 값 중 하나로 접두부가 지정되어야 합니다. 여기서,

        * *apikey*는 토큰이 API 키임을 식별합니다.
		* *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
		* *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.
		
	* Token은 UAA 토큰, IAM 토큰 또는 API 키입니다.
	
	* Space는 영역의 GUID입니다. 

	* METRICS_ENDPOINT는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
        

