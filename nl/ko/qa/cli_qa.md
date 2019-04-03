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



# IBM Cloud CLI 사용에 대한 FAQ
{: #cli_qa}

여기에는 {{site.data.keyword.Bluemix}} CLI를 {{site.data.keyword.monitoringshort}} 서비스와 함께 사용하는 데 대한 일반적인 질문의 답이 제공되어 있습니다. 
{:shortdesc}

* [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa/cli_qa.html#login)
* [{{site.data.keyword.Bluemix_notm}} CLI 설치 방법](/docs/services/cloud-monitoring/qa/cli_qa.html#install_bmx_cli)
* [계정의 GUID를 가져오는 방법](/docs/services/cloud-monitoring/qa/cli_qa.html#account_guid)
* [조직의 GUID를 가져오는 방법](/docs/services/cloud-monitoring/qa/cli_qa.html#org_guid)
* [영역의 GUID를 가져오는 방법](/docs/services/cloud-monitoring/qa/cli_qa.html#space_guid)

## IBM Cloud에 로그인하는 방법
{: #login}

다음 명령을 실행하여 {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오.

```
ibmcloud login -a Endpoint
```
{: codeblock}
	
여기서 *Endpoint*는 {{site.data.keyword.Bluemix_notm}}에 로그인하기 위한 URL입니다. 이 URL은 지역마다 다릅니다.
	
<table>
    <caption>{{site.data.keyword.Bluemix_notm}}에 액세스하기 위한 엔드포인트 목록</caption>
	<tr>
	  <th>지역</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>독일</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>시드니</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>영국</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
	<tr>
	  <td>미국 남부</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
</table>

예를 들어, 미국 남부 지역에 로그인하려면 다음 명령을 실행하십시오.
	
```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

지시사항을 따르십시오. 

그런 다음 조직 및 영역을 설정하십시오. 다음 명령을 실행하십시오.

```
ibmcloud target -o OrgName -s SpaceName
```
{: codeblock}

여기서,

* OrgName은 조직의 이름입니다.
* SpaceName은 영역의 이름입니다.

	
## IBM Cloud CLI 설치 방법
{: #install_bmx_cli}

[{{site.data.keyword.Bluemix_notm}} CLI 다운로드 및 설치](/docs/cli/index.html#overview)를 참조하십시오.

## 계정의 GUID를 가져오는 방법
{: #account_guid}
	
계정의 GUID를 가져오려면 다음 단계를 완료하십시오.
	
1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 다음 명령을 실행하십시오.

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	여기서 *Endpoint*는 {{site.data.keyword.Bluemix_notm}}에 로그인하기 위한 URL입니다. 이 URL은 지역마다 다릅니다.
	
	<table>
	    <caption>{{site.data.keyword.Bluemix_notm}}에 액세스하기 위한 엔드포인트 목록</caption>
		<tr>
		  <th>지역</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>미국 남부</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>영국</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    예를 들어, 미국 남부 지역에 로그인하려면 다음 명령을 실행하십시오.
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    지시사항을 따르십시오. {{site.data.keyword.Bluemix_notm}} 인증 정보를 입력하고 조직 및 영역을 선택하십시오.
	
	**연합 사용자 ID**의 경우 다음 명령을 실행하고 지시사항에 따르십시오.
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. `ibmcloud iam accounts` 명령을 실행하여 계정의 GUID를 가져오십시오.

    ```
	ibmcloud iam accounts
	```
	{: codeblock} 
	
	예를 들어, 사용자 xxx@yyy.com의 모든 계정을 해당 GUID와 함께 검색하려면 다음 명령을 실행하십시오.
	
	```
	ibmcloud iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## 조직의 GUID를 가져오는 방법
{: #org_guid}

조직의 GUID를 가져오려면 다음 단계를 완료하십시오.
	
1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 다음 명령을 실행하십시오.

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	여기서 *Endpoint*는 {{site.data.keyword.Bluemix_notm}}에 로그인하기 위한 URL입니다. 이 URL은 지역마다 다릅니다.
	
	<table>
	    <caption>{{site.data.keyword.Bluemix_notm}}에 액세스하기 위한 엔드포인트 목록</caption>
		<tr>
		  <th>지역</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>미국 남부</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>영국</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    예를 들어, 미국 남부 지역에 로그인하려면 다음 명령을 실행하십시오.
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    지시사항을 따르십시오. {{site.data.keyword.Bluemix_notm}} 인증 정보를 입력하고 조직 및 영역을 선택하십시오.
	
	연합 사용자 ID의 경우 다음 명령을 실행하고 지시사항에 따르십시오.
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}

2. `ibmcloud iam org` 명령을 실행하여 조직 GUID를 가져오십시오. 

    ```
    ibmcloud iam org NAME --guid
    ```
    {: codeblock}
	
    여기서 NAME은 {{site.data.keyword.Bluemix_notm}} 조직의 이름입니다.        
		
## 영역의 GUID를 가져오는 방법
{: #space_guid}
	
영역의 GUID를 가져오려면 다음 단계를 완료하십시오.
	
1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 다음 명령을 실행하십시오.

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	여기서 *Endpoint*는 {{site.data.keyword.Bluemix_notm}}에 로그인하기 위한 URL입니다. 이 URL은 지역마다 다릅니다.
	
	<table>
	    <caption>{{site.data.keyword.Bluemix_notm}}에 액세스하기 위한 엔드포인트 목록</caption>
		<tr>
		  <th>지역</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>미국 남부</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>영국</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    예를 들어, 미국 남부 지역에 로그인하려면 다음 명령을 실행하십시오.
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    지시사항을 따르십시오. {{site.data.keyword.Bluemix_notm}} 인증 정보를 입력하고 조직 및 영역을 선택하십시오.
	
	연합 사용자 ID의 경우 다음 명령을 실행하고 지시사항에 따르십시오.
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. `ibmcloud iam space` 명령을 실행하여 영역 GUID를 가져오십시오. 

    ```
    ibmcloud iam space NAME --guid
    ```
    {: codeblock}
	
    여기서 NAME은 {{site.data.keyword.Bluemix_notm}} 영역의 이름입니다. 
	
    예를 들어, *dev* 영역의 GUID를 가져오려면 다음 명령을 실행하십시오.
	
    ```
    ibmcloud iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		
