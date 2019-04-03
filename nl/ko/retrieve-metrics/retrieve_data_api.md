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

# 메트릭 검색
{: #retrieve_data_api}

[메트릭 API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}를 사용하여 {{site.data.keyword.monitoringshort}} 서비스에서 메트릭을 검색할 수 있습니다.
{:shortdesc}


## 영역에서 메트릭 검색
{: #uaa}

영역에서 메트릭을 검색하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.

2. 보안 토큰 또는 API 키를 설정하십시오.
  
    보안 토큰 또는 API 키를 사용하여 **X-Auth-User-Token** 필드를 설정해야 합니다. UAA 토큰, IAM 토큰 또는 API 키를 사용할 수 있습니다.

    먼저, 다음 방법 중 하나를 선택하여 메트릭을 전송하는 데 필요한 보안 토큰을 얻으십시오.
	
    * UAA 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 UAA 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)를 참조하십시오.
    
	* IAM 토큰을 가져오려면 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)를 참조하십시오.
    
	* API 키를 가져오려면 [API 키 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)를 참조하십시오. 

    토큰 또는 API 키에는 `apikey`, `iam` 또는 `uaa` 값 중 하나로 접두부가 지정되어야 합니다. 

    여기서, 

    * *apikey*는 토큰이 API 키임을 식별합니다.
    * *iam*은 지정된 토큰이 IAM 생성 토큰임을 식별합니다.
    * *uaa*는 지정된 토큰이 UAA 생성 토큰임을 식별합니다.

    예를 들어, API 키에 대해 `X-Auth-User-Token: apikey SomeIAMGeneratedKey` 헤더를 설정할 수 있습니다.
	
	그런 다음, {{site.data.keyword.Bluemix_notm}}에 로그인한 것과 동일한 터미널에서 토큰에 대한 Token 변수를 설정하십시오.

    예를 들어, UAA 토큰을 설정하고 토큰 값에서 *Bearer* 파트를 제거하십시오.

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. 영역 ID를 가져오십시오.

    메트릭을 검색하려면 헤더 필드 **X-Auth-Scope-Id**가 필요하며 영역 GUID로 설정되어야 합니다. 

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

4. 메트릭을 전송하려면 다음 cURL 명령을 실행하십시오.

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	여기서,
	
	* *X-Auth-User-Token*은 {{site.data.keyword.Bluemix_notm}} UAA 토큰을 전달하는 매개변수입니다.
	
	* Auth_Type은 토큰 유형을 정의하는 접두부입니다. 올바른 값은 UAA 토큰의 경우 *uaa*, IAM 토큰의 경우 *iam* 및 API 키의 경우 *api*입니다.
	
	* *X-Auth-Scope-Id*는 영역 GUID를 전달하는 매개변수입니다. 이 GUID에는 영역임을 식별하기 위해 접두부 *s-*가 지정되어야 합니다. 이 헤더는 UAA 인증을 사용하는 경우에만 필요합니다. IAM 인증 토큰을 사용하는 경우 이 헤더는 선택사항이며, 토큰에 바인드된 도메인 정보가 사용됩니다.
	
	* *Token*은 보안 토큰을 나타냅니다.
	
	* *Space*는 영역의 GUID를 나타냅니다. 
	
	* *Start_Time*은 요청의 시작을 정의합니다. 이 정보는 상대 또는 절대 시간을 계산하는 데 사용됩니다. *End_Time*은 요청의 시작을 정의합니다. 이 정보는 상대 또는 절대 시간을 계산하는 데 사용됩니다. 자세한 정보는 [기간 설정](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#time)을 참조하십시오.
	
	* *Path*는 하나 또는 몇 가지 메트릭을 식별합니다. 선택적으로 각 메트릭에 함수를 적용할 수 있습니다. 경로는 하나의 경로에서 둘 이상의 메트릭을 식별할 수 있게 해 주는 와일드카드 또한 지원합니다. 자세한 정보는 [메트릭 정의](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#metrics)를 참조하십시오.
	
	* *METRICS_ENDPOINT*는 서비스에 대한 시작점을 나타냅니다. 각 지역의 URL은 서로 다릅니다. 지역별 엔드포인트 목록을 가져오려면 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하십시오.
	

	
## 메트릭 정의
{: #metrics}

메트릭에 대한 데이터를 검색하려면 메트릭 트리의 루트에서 메트릭으로 메트릭의 경로를 지정해야 하며, 각 단계를 마침표(.)로 구분해야 합니다.

이 경로는 **Target** 매개변수에 지정됩니다. 요청당 최대 5개의 대상을 지정할 수 있습니다.  

선택적으로 메트릭에 함수를 적용할 수 있습니다. 지원되는 함수에 대한 자세한 정보는 [Graphite 0.9.15 함수 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://graphite.readthedocs.io/en/latest/functions.html)를 참조하십시오.

경로를 정의하는 데 와일드카드를 사용할 수 있습니다. 와일드카드를 사용하면 하나의 경로에서 둘 이상의 메트릭을 식별할 수 있습니다. 

* **별표**: 별표(*)를 사용하여 0개 이상의 문자를 비교할 수 있습니다. 

    하나의 경로 요소에 둘 이상의 별표를 포함시킬 수 있으며, 예를 들면 `servers.sp*aeg*r.cpu.total.*`와 같습니다. 이 예는 패턴과 일치하는 모든 서버의 총 CPU에 대한 데이터를 리턴합니다.

* **문자 목록 또는 범위**: 문자를 대괄호([...]) 안에 정의하여 경로 문자열 내에 하나의 문자 위치를 지정할 수 있습니다. 

    하이픈(-)으로 구분된 두 문자를 지정하여 경계 문자를 포함하는 범위를 설정할 수 있습니다. 이러한 두 문자 사이의 범위에 포함되는 모든 문자는 일치 항목으로 간주됩니다. 
	
	대괄호로 묶인 하나 이상의 문자 범위를 정의할 수 있습니다. 
	
	대괄호 세트 내의 문자를 하나의 범위로 읽을 수 없는 경우 해당 문자는 값 목록으로 취급됩니다. 
	
	대괄호 내의 시작 또는 끝 부분에 하이픈(-)을 삽입하여 이를 값 목록 내의 문자로 포함시킬 수 있습니다.

* **값 목록**: 중괄호 내에 쉼표로 구분된 값을 설정하여 값 목록을 정의할 수 있습니다. 

    예를 들어, `servers.myserver.cpu.total.user` 및 `servers.myserver.cpu.total.system` 경로에 대한 메트릭을 다운로드하려는 경우에는 두 유형 모두에 대해 단일 경로 `servers.myserver.cpu.total.{user,system}`을 설정할 수 있습니다.



## 기간 설정
{: #time}

선택적으로 상대 시간 또는 절대 시간을 사용하여 기간을 지정할 수 있습니다. 조회 매개변수 **From** 및 **Until**을 정의해야 합니다.  

* 기간의 시작 시간이 생략되는 경우의 기본값은 24시간 전입니다. 

* 기간의 종료 시간이 생략되는 경우의 기본값은 현재 시간인 *now*입니다.

**상대 시간** 앞에는 항상 빼기 기호(-)가 오며 그 뒤에는 시간 단위가 옵니다. 

다음 표에는 사용할 수 있는 다양한 상대 시간 약어가 나열되어 있습니다.


|약어 |설명 |
|--------------|-------------|
| s            | 초     |
| min          | 분     |
| h            | 시간       |
| d            | 일        |
| w            | 주       |
| mon          | 월      |
| now          | 현재 시간 |


`HH:MM_YYMMDD`, `YYYYMMDD`, `MM/DD/YY` 중 하나의 형식을 사용하여 **절대 시간**을 정의할 수 있습니다.

|약어 |설명 |
|--------------|-------------|
| YYYY         | 네 자리 연도 |
| MM           | 두 자리 월(01=1월 등) |
| DD           | 두 자리 날짜(01 - 31) |
| hh           | 두 자리 시간(00 - 23) |
| mm           | 두 자리 분(00 - 59) |
| ss           | 두 자리 초(00 - 59) |

**예**

다음 표는 *from* 및 *until* 매개변수를 설정하여 다양한 기간을 설정하는 방법에 대한 여러 예제를 보여줍니다.

<table>
  <caption>표 1. *from* 및 *until* 매개변수를 설정하여 다양한 기간을 설정하는 방법을 보여주는 여러 예제</caption>
  <tr>
    <th>예</th>
	<th>설명</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>마지막 월요일부터 지금까지의 데이터를 포함하는 기간</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>월(예: 11월)로 설정된 기간 </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>2017월 7월 1일의 02:00 - 14:00와 같이, 24시간 주기 내의 데이터를 표시합니다.</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>주(예: 지난 주)의 동일한 요일을 표시합니다.</td>
  </tr>
  
</table>


