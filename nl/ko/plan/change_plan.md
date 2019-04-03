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


# 플랜 변경
{: #change_plan}

{{site.data.keyword.monitoringlong_notm}} 대시보드를 사용하거나 `cf update-service` 명령을 실행하여 {{site.data.keyword.monitoringshort}} 서비스를 변경할 수 있습니다. 플랜은 언제든지 업그레이드하거나 다운그레이드할 수 있습니다.
{:shortdesc}

## UI를 통한 서비스 플랜 변경
{: #change_plan_ui}

{{site.data.keyword.monitoringlong_notm}} 대시보드에서 서비스 플랜을 변경하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 다음 대시보드에서 {{site.data.keyword.monitoringshort}} 서비스를 클릭하십시오. 

    {{site.data.keyword.monitoringshort}} 서비스 대시보드가 열립니다.
    
2. **플랜** 탭을 선택하십시오.

    현재 플랜에 대한 정보가 표시됩니다.
	
3. 플랜을 업그레이드하거나 다운그레이드할 새 플랜을 선택하십시오. 

4. **저장**을 클릭하십시오.



## CLI를 통한 서비스 플랜 변경
{: #change_plan_cli}

CLI를 통해 {{site.data.keyword.Bluemix_notm}}의 서비스 플랜을 변경하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa/cli_qa.html#login)을 참조하십시오.
	
2. `ibmcloud service list` 명령을 사용하여 현재 플랜을 확인하고, 서비스 목록으로부터 영역에서 사용 가능한 {{site.data.keyword.loganalysisshort}} 서비스 이름을 가져오십시오. 

    필드 **name**의 값이 플랜을 변경하기 위해 사용해야 하는 값입니다. 

    예를 들어 다음과 같습니다.
	
	```
	$ ibmcloud service list
	Getting services in org MyOrg / space dev as xxx@yyy.com...
	OK
	name            service      plan   bound apps   last operation
	Monitoring-0c   Monitoring   premium             create succeeded
    ```
	{: screen}
    
3. 플랜을 업그레이드하거나 다운그레이드하십시오. `ibmcloud service update` 명령을 실행하십시오.
    
	```
	ibmcloud service update service_name [-p new_plan]
	```
	{: codeblock}
	
	여기서, 
	
	* *service_name*은 서비스의 이름입니다. 
	* *new_plan*은 플랜의 이름입니다.
	
	다음 표에는 다양한 플랜과 해당 지원되는 값이 나열되어 있습니다.
	
	<table>
	  <caption>표 1. 플랜 목록</caption>
	  <tr>
	    <th>플랜</th>
		<th>기능</th>
	    <th>이름</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>무료 모니터링 기능입니다.</td>
		<td>lite</td>
	  </tr>
	  <tr>
	    <td>프리미엄</td>
	    <td>프리미엄 모니터링 기능입니다.</td>
		<td>premium</td>
	  </tr>
	</table>
	
	예를 들어, 플랜을 *Lite* 플랜으로 다운그레이드하려면 다음 명령을 실행하십시오.
	
	```
	ibmcloud service update "Monitoring-0c" -p lite
    Updating service instance Monitoring-0c as xxx@yyy.com...
    OK
	```
	{: screen}

4. 새 플랜으로 변경되었는지 확인하십시오. `ibmcloud service list` 명령을 실행하십시오.

    ```
	ibmcloud service list
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service       plan   bound apps   last operation
    Monitoring-0c     Monitoring    lite                create succeeded
	```
	{: screen}






