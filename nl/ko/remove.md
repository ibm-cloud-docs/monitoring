---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# 인스턴스 제거
{: #remove}

명령행을 통해 또는 {{site.data.keyword.Bluemix}} UI에서 {{site.data.keyword.mon_full_notm}} 서비스의 인스턴스를 제거할 수 있습니다.
{:shortdesc}

{{site.data.keyword.cloud_notm}}에서 인스턴스를 제거할 때는 다음 정보의 정리를 고려하십시오.

1. 제거할 {{site.data.keyword.mon_full_notm}} 인스턴스에 메트릭을 전달하는 소스의 목록을 기록해 두십시오. 각 소스에서 Sysdig 에이전트를 제거해야 합니다.
2. 인스턴스 관련 작업을 위해 사용자에게 부여된 권한을 제거하십시오. 

    액세스 그룹을 사용하여 인스턴스에 대한 액세스를 관리하는 경우에는 액세스 그룹을 제거해야 합니다.

    액세스 그룹을 사용하여 서로 다른 서비스 인스턴스에 대한 액세스를 관리하는 경우에는 제거할 인스턴스에 대한 권한을 부여하는 정책을 제거해야 합니다.
    
    사용자에게 개별 정책을 부여한 경우에는 액세스 권한을 지닌 각 사용자의 정보를 수집하고 삭제할 인스턴스와 관련된 정책을 하나씩 제거해야 합니다.


그리고 {{site.data.keyword.cloud_notm}} 대시보드에서 인스턴스를 삭제하십시오.


## {{site.data.keyword.cloud_notm}} UI를 통해 인스턴스 제거
{: #remove_ui}

{{site.data.keyword.cloud_notm}} UI를 사용하여 {{site.data.keyword.mon_full_notm}}의 인스턴스를 제거하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.cloud_notm}} 계정에 로그인하십시오.

    [{{site.data.keyword.cloud_notm}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/login){:new_window}를 클릭하여 {{site.data.keyword.cloud_notm}} 대시보드를 실행하십시오.

	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.cloud_notm}} UI가 열립니다.

2. **식별성**을 선택하십시오. 

3. **모니터링**을 선택하십시오. 인스턴스의 목록이 표시됩니다.

4. 삭제할 인스턴스를 선택하십시오.

5. *조치* 메뉴에서 **제거**를 선택하십시오.


## CLI를 통해 인스턴스 제거
{: #remove_cli}

명령행을 통해 {{site.data.keyword.mon_full_notm}}의 인스턴스를 제거하려면 다음 단계를 완료하십시오.

1. [전제조건] {{site.data.keyword.cloud_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.cloud_notm}} CLI 설치](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)를 참조하십시오.

   CLI가 설치되면 다음 단계를 계속하십시오.

2. 인스턴스를 프로비저닝할 {{site.data.keyword.cloud_notm}}의 지역에 로그인하십시오. [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) 명령을 실행하십시오.

3. 인스턴스가 프로비저닝된 리소스 그룹을 설정하십시오. [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) 명령을 실행하십시오.

    기본적으로 `기본` 리소스 그룹이 설정됩니다.

4. 인스턴스를 제거하십시오. [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete) 명령을 실행하십시오.

    ```
    ibmcloud resource service-instance-delete NAME
    ```
    {: codeblock}

    여기서 NAME은 인스턴스의 이름입니다.

    예를 들어, 인스턴스를 제거하려면 다음 명령을 실행하십시오.

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
