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

# 메트릭 API를 사용하여 데이터 전송
{: #send_data_api}

메트릭 API를 사용하여 메트릭을 {{site.data.keyword.monitoringshort}} 서비스에 전송할 수 있습니다. 
{:shortdesc}


{{site.data.keyword.Bluemix_notm}} Docker 컨테이너의 경우, 기본 시스템 메트릭은 자동으로 수집됩니다. Cloud Foundry 애플리케이션, 그리고 가상 머신(VM)에서 실행 중인 앱의 경우에는 [메트릭 API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}를 사용하여 앱에서 바로 메트릭을 전송해야 합니다. 



## 영역 도메인에 메트릭 전송
{: #space_uaa}

cURL을 사용하여 메트릭을 영역에 전송하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.

2. 보안 토큰을 가져오십시오. UAA 토큰, IAM 토큰 또는 API 키를 사용할 수 있습니다.

    다음 방법 중 하나를 선택하여 메트릭을 전송하는 데 필요한 보안 토큰을 얻으십시오.
	
	* UAA 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 UAA 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)를 참조하십시오.
	
	* IAM 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)를 참조하십시오.
	
	* API 키를 가져오려면 [API 키 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)를 참조하십시오.
	
	{{site.data.keyword.Bluemix_notm}}에 로그인한 것과 동일한 터미널에서 토큰에 대한 *Token* 변수를 설정하십시오.

    예를 들어, UAA 토큰을 설정하고 토큰 값에서 *Bearer* 파트를 제거하십시오.

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
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
	
5. 메트릭을 전송하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	여기서,
	
	* Metrics_File은 {{site.data.keyword.monitoringshort}} 서비스로 전송되는 메트릭의 정의를 포함하는 JSON 파일을 나타냅니다.
	
	* *X-Auth-User-Token*은 보안 토큰을 전달하는 매개변수입니다.
	
	* *Auth_Type*은 토큰 유형을 정의하는 접두부입니다. 올바른 값은 UAA 토큰의 경우 *uaa*, IAM 토큰의 경우 *iam* 및 API 키의 경우 *api*입니다.
	
	* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다.
	
	* Token은 보안 토큰 또는 API 키를 나타냅니다.
	
	* Space는 영역의 GUID를 나타냅니다. 
	
	* Endpoint는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	
	예를 들어, 2개의 메트릭 `myhost.cpu.idle` 및 `myapp.login.attempts`를 {{site.data.keyword.monitoringshort}} 서비스에 전송하려는 경우에는 다음 명령을 실행하십시오.
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	샘플 파일 *metric.json*은 다음과 같이 정의되어 있습니다.

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
