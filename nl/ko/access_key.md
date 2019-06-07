---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, access key

subcollection: Sysdig

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

# 액세스 키 관리
{: #access_key}

**액세스 키**는 {{site.data.keyword.cloud_notm}}의 {{site.data.keyword.mon_full_notm}} 인스턴스에 데이터를 성공적으로 전달하도록 Sysdig 에이전트를 구성하는 데 사용해야 하는 토큰입니다.   
{:shortdesc}


## {{site.data.keyword.cloud_notm}} UI를 통해 액세스 키 가져오기
{: #access_key_ibm_cloud_ui}

{{site.data.keyword.cloud_notm}} UI를 통해 {{site.data.keyword.mon_full_notm}} 인스턴스에 대한 액세스 키를 가져오려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.cloud_notm}} 계정에 로그인하십시오.

    [{{site.data.keyword.cloud_notm}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/login){:new_window}를 클릭하여 {{site.data.keyword.cloud_notm}} 대시보드를 실행하십시오.

	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.cloud_notm}} UI가 열립니다.

2. 탐색 메뉴에서 **식별성**을 선택하십시오. 

3. **모니터링**을 선택하십시오. {{site.data.keyword.mon_full_notm}} 대시보드가 열립니다. {{site.data.keyword.cloud_notm}}에서 사용 가능한 모니터링 인스턴스의 목록을 볼 수 있습니다.

3. 해당 액세스 키를 가져올 인스턴스를 식별하고 **액세스 키 보기**를 클릭하십시오.

4. 열리는 팝업 창에서 **표시**를 클릭하면 액세스 키를 볼 수 있습니다.



## CLI를 통해 액세스 키 가져오기
{: #access_key_cli}

명령행을 통해 Sysdig 인스턴스에 대한 액세스 키를 가져오려면 다음 단계를 완료하십시오.

1. [전제조건] {{site.data.keyword.cloud_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.cloud_notm}} CLI 설치](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)를 참조하십시오.

   CLI가 설치되면 다음 단계를 계속하십시오.

2. Sysdig 인스턴스가 실행 중인 {{site.data.keyword.cloud_notm}}의 지역에 로그인하십시오. [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) 명령을 실행하십시오.

3. Sysdig 인스턴스가 실행 중인 리소스 그룹을 설정하십시오. [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) 명령을 실행하십시오.

    기본적으로 `기본` 리소스 그룹이 설정됩니다.

4. 인스턴스 이름를 가져오십시오. [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) 명령을 실행하십시오.

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Sysdig 인스턴스와 연관된 API 키의 이름을 가져오십시오. [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) 명령을 실행하십시오.

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    여기서 INSTANCE_NAME은 이전 단계에서 가져온 인스턴스의 이름입니다.

6. 액세스 키를 가져오십시오. [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) 명령을 실행하십시오.

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    여기서 APIKEY_NAME은 API 키의 이름입니다.
 
    이 명령의 출력에는 인스턴스에 대한 액세스 키가 포함된 **Sysdig 액세스 키** 필드가 포함됩니다.


예를 들어, 다음 명령은 샘플 서비스 ID의 출력을 보여줍니다.

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## 액세스 키 재설정 
{: #access_key_reset}

액세스 키가 손상되었거나 며칠 후에 이를 갱신하는 정책을 보유 중인 경우에는 새 키를 생성하고 이전 키를 삭제할 수 있습니다.

{{site.data.keyword.mon_full_notm}} 인스턴스에 대한 액세스 키를 갱신하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.mon_full_notm}} 웹 UI를 실행하십시오. 자세한 정보는 [웹 UI로 이동](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)을 참조하십시오.

2. 탐색줄의 *선택기* 단추에서 **설정**을 선택하십시오.

2. *비밀번호 관리* 섹션에서 **비밀번호 재설정**을 클릭하십시오.

**참고:** Sysdig 액세스 키를 재설정한 후 메트릭을 이 {{site.data.keyword.mon_full_notm}} 인스턴스에 전달하는 로그 소스에 대한 액세스 키를 업데이트해야 합니다.
