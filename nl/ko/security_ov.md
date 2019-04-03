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


# 보안
{: #security_ov}

사용자가 수행할 수 있는 {{site.data.keyword.monitoringshort}} 서비스 조치를 제어하기 위해 사용자에게 하나 이상의 조치를 지정할 수 있습니다. UAA 토큰, IAM 토큰 또는 API 키를 사용하여 메트릭 및 경보에 대해 작업하도록 사용자를 인증할 수 있습니다. 
{:shortdesc}





## 인증 모델
{: #auth}

영역에 대해 {{site.data.keyword.monitoringshort}} 서비스에 저장된 메트릭에 대해 작업하려면 인증 토큰 또는 API 키가 필요합니다. 

보안 토큰을 가져오려면 다음을 참조하십시오.

* [UAA 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa)
* [IAM 토큰 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)

API 키를 가져오려면 [API 키 생성](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)을 참조하십시오. API 키가 보안 위험에 노출된 경우에는 이를 삭제하여 취소할 수 있습니다. 그 후에는 새 키를 다시 작성할 수 있습니다. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} UI를 사용하여 API 키 취소](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#revoke_ui)를 참조하십시오. 

UAA 토큰 및 IAM 토큰은 일정 기간이 경과하면 만료됩니다. API 키는 만료되지 않습니다. 

다음 표에는 각 도메인 유형에 대해 지원되는 보안 모델이 나열되어 있습니다.

<table>
  <caption>표 1. 각 도메인에 대해 지원되는 보안 모델</caption>
  <tr>
    <th></th>
	<th align="right">계정</th>
    <th align="right">조직</th>
    <th align="right">영역</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">아니오</td>
	<td align="center">예</td>
	<td align="center">예</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">예</td>
	<td align="center">예</td>
	<td align="center">예</td>
  </tr>
</table>

{{site.data.keyword.monitoringshort}} 서비스는 IAM 액세스 제어 기능을 사용하여 사용자가 도메인에 대해 수행할 수 있는 조치 또는 오퍼레이션을 제어합니다. 예를 들면, 사용자가 도메인에 대해 대시보드를 작성하고 전송하는 것은 허용하지만, 도메인으로부터 메트릭을 검색하는 것은 허용하지 않는 IAM 정책을 정의할 수 있습니다.



## Cloud Foundry 역할
{: #bmx_roles}

다음 표에는 {{site.data.keyword.monitoringshort}} 서비스에 대해 작업하는 데 필요한 각 Cloud Foundry 역할의 권한이 나열되어 있습니다.

<table>
  <caption>표 2. {{site.data.keyword.monitoringshort}} 서비스에 대해 작업하는 데 필요한 Cloud Foundry 역할 및 권한</caption>
  <tr>
    <th>역할</th>
	<th>도메인</th>
	<th>액세스 권한</th>
  </tr>
  <tr>
    <td>관리자</td>
	<td>조직 <br>영역</td>
	<td>모든 RESTful API</td>
  </tr>
  <tr>
    <td>개발자</td>
	<td>영역</td>
	<td>모든 RESTful API</td>
  </tr>
  <tr>
    <td>감사자</td>
	<td>조직 <br>영역</td>
	<td>메트릭 조회와 같은 읽기 전용 오퍼레이션을 수행하는 RESTful API 한정</td>
  </tr>
</table>

UI로 사용자 역할을 지정하는 데 대한 정보는 [Cloud Foundry 액세스 관리](/docs/iam?topic=iam-mngcf#mngcf)를 참조하십시오.



## IAM 역할
{: #iam_roles}

다음 표에는 메트릭에 대해 작업할 때 {{site.data.keyword.monitoringshort}} 서비스 조치와 사용자에게 이러한 태스크를 실행할 수 있는 권한을 부여하는 IAM 역할이 나열되어 있습니다.

<table>
  <caption>표 3. 메트릭에 대한 작업 </caption>
  <tr>
	<th>조치</th>
	<th>IAM 역할</th>
  </tr>
  <tr>
    <td>도메인에 메트릭 전송</td>
	<td>관리자, 편집자, 운영자</td>
  </tr>
  <tr>
    <td>메트릭 검색/조회</td>
	<td>관리자, 편집자, 뷰어</td>
  </tr>
  <tr>
    <td>도메인에서 메트릭 검색</td>
	<td>관리자, 편집자</td>
  </tr>
</table>

다음 표에는 경보에 대해 작업할 때 {{site.data.keyword.monitoringshort}} 서비스 조치와 사용자에게 이러한 태스크를 실행할 수 있는 권한을 부여하는 IAM 역할이 나열되어 있습니다.

<table>
  <caption>표 4. 경보에 대한 작업 </caption>
  <tr>
	<th>조치</th>
	<th>IAM 역할</th>
  </tr>
  <tr>
    <td>경보 규칙 작성, 편집 및 삭제</td>
	<td>관리자, 편집자</td>
  </tr>
  <tr>
    <td>경보 보기</td>
	<td>관리자, 편집자, 뷰어</td>
  </tr>
  <tr>
    <td>경보 알림 작성, 편집 및 삭제</td>
	<td>관리자, 편집자</td>
  </tr>
  <tr>
    <td>알림 보기</td>
	<td>관리자, 편집자, 뷰어</td>
  </tr>
  <tr>
    <td>트리거된 경보 히스토리 레코드 보기</td>
	<td>관리자, 편집자, 뷰어</td>
  </tr>
</table>

UI로 사용자 역할을 지정하는 데 대한 정보는 [IAM 액세스 관리](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)를 참조하십시오.

