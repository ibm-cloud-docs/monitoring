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


# UAA 토큰 가져오기
{: #auth_uaa}

{{site.data.keyword.Bluemix}} UAA 모델을 사용하여 {{site.data.keyword.monitoringshort}} 서비스에 대해 작업하는 데 사용할 수 있는 인증 토큰을 가져오십시오. {{site.data.keyword.Bluemix_notm}} CLI를 사용하여 인증 토큰을 얻을 수 있습니다.
{:shortdesc}

토큰에는 만기 시간이 있습니다. 
		
## IBM Cloud CLI를 사용하여 UAA 토큰 가져오기
{: #uaa_cli}


UAA 토큰을 가져오려면 다음 단계를 완료하십시오.

1. (전제조건) {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 설치](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa)를 참조하십시오.
   
   CLI가 설치되어 있는 경우에는 다음 단계를 진행하십시오.
    
2. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.
	
3. `ibmcloud iam oauth-tokens` 명령을 실행하여 UAA 토큰을 가져오십시오.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	출력에 UAA 토큰이 리턴됩니다.

**참고:** 토큰을 사용할 때는 API 호출에 전달하는 토큰의 값에서 *Bearer*를 제거하십시오.
	


	
