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


# API 키에 대한 작업
{: #auth_api_key}

{{site.data.keyword.Bluemix}} CLI 또는 {{site.data.keyword.Bluemix_notm}} UI를 사용하여 API를 가져올 수 있습니다. API 키는 만료되지 않습니다. API가 보안 위험에 노출된 경우에는 이를 취소하고 새 API를 생성할 수 있습니다.
{:shortdesc}

## IBM Cloud CLI를 사용하여 IAM API 키 생성
{: #iam_apikey_cli}

{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 API 키를 생성하려면 다음 단계를 완료하십시오.

1. (전제조건) {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 설치](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa)를 참조하십시오.
   
   CLI가 설치되어 있는 경우에는 다음 단계를 진행하십시오.
	
2. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.
 
3. `ibmcloud iam api-key-create` 명령을 실행하여 API 키를 작성하십시오.

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	여기서,
	
	* NAME은 작성되는 API 키의 이름입니다.
	* DESCRIPTION은 API 키를 설명하는 데 사용되는 텍스트입니다.
	* FILE은 키가 저장되는 파일의 이름입니다.
	
    예를 들어, *MyKey*라는 API 키를 작성하려는 경우에는 다음 명령을 실행하십시오.
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## IBM Cloud UI를 사용하여 IAM API 키 생성
{: #iam_apikey_ui}

{{site.data.keyword.Bluemix_notm}} UI를 통해 API 키를 생성하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드 [http://console.bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}을 실행하십시오.
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 콘솔 메뉴 표시줄에서 **관리 > 보안 > IBM Cloud API 키**를 클릭하십시오.

3. **API 키 작성**을 클릭하십시오.

4. API 키의 이름 및 설명을 입력하십시오. 그런 다음 **API 키 작성**을 클릭하십시오.

5. API 키를 저장하십시오. **API 키 다운로드**을 클릭하십시오.

    API 키를 표시하려면 **표시**를 클릭하십시오.  

**참고:** API 키는 작성 시에만 표시하거나 다운로드할 수 있습니다. API 키를 유실한 경우에는 새 API 키를 작성해야 합니다.  


	
## BM Cloud UI를 사용하여 API 키 취소
{: #revoke_ui}
	
{{site.data.keyword.Bluemix_notm}} UI를 통해 IAM API 키를 취소하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드 [http://console.bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}을 실행하십시오.
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 콘솔 메뉴 표시줄에서 **관리 > 보안 > IBM Cloud API 키**를 클릭하십시오.

3. **조치**를 클릭하고 **키 삭제**를 클릭하십시오.





	

	
	
	
	
	
	
