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


# 사용자 권한 부여
{: #grant_permissions}

{{site.data.keyword.Bluemix}}에서는 사용자에게 하나 이상의 역할을 지정할 수 있습니다. 이러한 역할은 해당 사용자가 {{site.data.keyword.monitoringshort}} 서비스에 대해 작업할 수 있도록 사용으로 설정되는 태스크를 정의합니다. 
{:shortdesc}

사용자에게 메트릭에 대해 작업할 수 있는 권한을 부여하려면 이 사용자가 계정에서 {{site.data.keyword.monitoringshort}} 서비스에 대해 수행할 수 있는 조치를 설명하는 해당 사용자의 정책을 추가해야 합니다. 계정 소유자만 개별 정책을 사용자에게 지정할 수 있습니다.


## IBM Cloud UI를 통해 사용자에게 IAM 정책 지정 
{: #assign_policy_ui}

사용자에게 {{site.data.keyword.monitoringshort}} 서비스에 대해 작업할 수 있는 권한을 부여하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드 [http://console.bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}을 실행하십시오.
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오. 

    *사용자* 창에 사용자의 목록이 현재 선택된 계정에 대한 해당 이메일 주소와 함께 표시됩니다.
	
3. 사용자가 계정의 구성원이면 목록에서 사용자 이름을 선택하거나 *조치* 메뉴에서 **사용자 관리**를 클릭하십시오.

    사용자가 계정의 구성원이 아닌 경우 [사용자 초대](/docs/iam?topic=iam-iamuserinv#iamuserinv)를 참조하십시오.

4. **서비스 정책 지정**을 클릭하십시오.

5. 정책에 대한 정보를 입력하십시오. 다음 표에는 정책을 정의하는 데 필수이거나 선택사항인 필드가 나열되어 있습니다. 

    <table>
	  <caption>IAM 정책을 구성하기 위한 필드 목록</caption>
	  <tr>
	    <th>필드</th>
		<th>값</th>
		<th>상태</th>
	  </tr>
	  <tr>
	    <td>서비스</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>필수</td>
	  </tr>
	  <tr>
	    <td>역할</td>
		<td>하나 이상의 IAM 역할을 선택하십시오. <br>올바른 역할은 *관리자*, *운영자*, *편집자* 및 *뷰어*입니다. <br>역할별로 허용되는 조치에 대한 자세한 정보는 [IAM 역할](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#iam_roles)을 참조하십시오.</td>
		<td>필수</td>
	  </tr>
	  <tr>
	    <td>지역</td>
		<td>사용자에게 메트릭에 대해 작업할 수 있는 액세스 권한이 부여될 지역을 지정할 수 있습니다. **선택적 서비스 컨텍스트 지정**을 선택하십시오. 그런 다음, 하나 이상의 지역을 개별적으로 추가하거나 **모든 현재 지역**을 선택하여 모든 지역에 액세스 권한을 부여하십시오.</td>
		<td>선택사항</td>
	  </tr>
	</table>
	
6. **정책 지정**을 클릭하십시오.
	
사용자가 구성하는 정책이 선택한 지역에 적용됩니다. 

## 명령행을 사용하여 사용자에게 IAM 정책 지정
{: #assign_policy_commandline}

명령행을 사용하여 메트릭을 볼 수 있는 액세스 권한을 사용자에게 부여하려면 다음 단계를 완료하십시오.

1. (전제조건) {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 설치](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)를 참조하십시오.
   
   CLI가 설치되어 있는 경우에는 다음 단계를 진행하십시오.
	
2. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.
	
3. 계정 ID를 가져오십시오. 

    다음 명령을 실행하여 계정 ID를 가져오십시오.

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	계정의 목록이 해당 GUID와 함께 표시됩니다.
	
	사용자에게 권한을 부여하려는 계정의 ID를 내보내십시오. `$acct_id`와 같은 쉘 변수를 구성하십시오. 예를 들어, 다음과 같습니다.
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. 권한을 부여하려는 사용자의 {{site.data.keyword.IBM_notm}} ID를 가져오십시오.

    1. 계정과 연관된 사용자를 표시하십시오. 다음 명령을 실행하십시오.
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. 사용자의 GUID를 가져오십시오. **참고: 권한을 부여하려는 사용자가 이 단계를 완료해야 합니다.**
	
	    예를 들어, 사용자에게 다음 명령을 실행하여 자신의 사용자 ID를 가져오도록 요청하십시오.
		
		IAM 토큰을 가져오십시오. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli)를 참조하십시오.

        IAM 토큰의 처음 2개 점 사이에 있는 데이터를 IAM 토큰에서 가져오십시오. `$user_data`와 같은 쉘 변수로 데이터를 내보내십시오. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		예를 들어, 다음 명령을 실행하여 사용자 ID를 가져오십시오. 이 명령은 이 샘플의 jq를 사용하여 정보를 JSON 형식의 텍스트로 디코드합니다.
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		이 명령을 실행한 출력은 다음과 같습니다.
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		*id* 필드의 값인 사용자 ID를 계정 소유자에게 전송하십시오. 
		
	3. `$user_ibm_id`와 같은 쉘 변수로 사용자 ID를 내보내십시오.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. 아직 구성원이 아닌 경우 사용자를 계정에 초대하십시오. 자세한 정보는 [사용자 초대](/docs/iam?topic=iam-iamuserinv#iamuserinv)를 참조하십시오.

    예를 들어, xxx@yyy.com 사용자를 zzz@ggg.com 계정에 초대하려면 다음 명령을 실행하십시오.
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. 정책 파일 이름을 작성하십시오. 

    예를 들어, 미국 남부 지역에서 보기 권한을 부여하려면 다음 템플리트를 사용하십시오.
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor"
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	정책 파일의 이름을 `policy.json`으로 지정하십시오.
	
5. 사용자 ID에 대한 IAM 토큰을 가져오십시오.

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli)를 참조하십시오.

    IAM 토큰을 `$iam_token`과 같은 쉘 변수로 내보내십시오. 예를 들어, 다음과 같습니다.
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. 사용자에게 {{site.data.keyword.monitoringshort}} 서비스에 대해 작업할 수 있는 권한을 부여하십시오. 

   미국 남부 지역에서 권한을 부여하려면 다음 cURL 명령을 실행하십시오.
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	영국 지역에서 권한을 부여하려면 다음 cURL 명령을 실행하십시오.
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## IBM Cloud UI를 통해 사용자에게 CF 역할 권한 부여 
{: #grant_permissions_ui_space}


영역 도메인 또는 조직 도메인에서 메트릭에 대해 작업하려면 사용자에게 {{site.data.keyword.Bluemix_notm}}에서 지정된 CF(Cloud Foundry) 역할이 있어야 합니다. CF 역할은 사용자가 영역 또는 조직에서 {{site.data.keyword.monitoringshort}} 서비스에 대해 수행할 수 있는 조치에 대해 설명합니다. 

사용자에게 {{site.data.keyword.monitoringshort}} 서비스에 대해 작업할 수 있는 권한을 부여하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드: [http://bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}을 실행하십시오.
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오. 

    *사용자* 창에 사용자의 목록이 현재 선택된 계정에 대한 해당 이메일 주소와 함께 표시됩니다.
	
3. 사용자가 계정의 구성원이면 목록에서 사용자 이름을 선택하거나 *조치* 메뉴에서 **사용자 관리**를 클릭하십시오.

    사용자가 계정의 구성원이 아닌 경우 [사용자 초대](/docs/iam?topic=iam-iamuserinv#iamuserinv)를 참조하십시오.

4. **조직 지정**을 클릭하십시오.

5. 정책에 대한 정보를 입력하십시오. 다음 표에는 정책을 정의하는 데 필수이거나 선택사항인 필드가 나열되어 있습니다. 

    <table>
	  <caption>CF 정책을 구성하기 위한 필드 목록</caption>
	  <tr>
	    <th>필드</th>
		<th>값</th>
	  </tr>
	  <tr>
	    <td>조직</td>
		<td>목록에서 조직을 선택하십시오.</td>
	  </tr>
	  <tr>
	    <td>조직 역할</td>
		<td>**조직 역할 없음**을 선택하십시오. 그러나 사용자에게 조직 역할이 있는 경우 목록에서 조직 역할을 선택하십시오. <br>올바른 값은 **청구 관리자**, **감사자**, **관리자**입니다.</td>
	  </tr>
	  <tr>
	    <td>Region</td>
		<td>목록에서 지역을 선택하십시오. <br>올바른 값은 **모든 현재 지역**, **미국 남부**, **영국**입니다.</td>
	  </tr>
	  <tr>
	    <td>영역</td>
		<td>*지역* 필드가 **모든 현재 지역**으로 설정된 경우 기본적으로 **모든 현재 영역**이 사전 정의됩니다. 개별 영역에 권한을 부여하려면 특정 지역을 선택한 후 목록에서 영역을 선택하십시오.</td>
	  </tr>
	  <tr>
	    <td>영역 역할</td>
		<td>목록에서 영역 역할을 선택하십시오. <br>올바른 값은 **관리자**, **감사자**, **개발자** 및 **영역 역할이 없음**입니다. 자세한 정보는 [Cloud Foundry 역할](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#bmx_roles)을 참조하십시오.</td>
	  </tr>
	</table>
	
6. **정책 지정**을 클릭하십시오.
	
사용자가 구성하는 정책이 선택한 지역에 적용됩니다. 


