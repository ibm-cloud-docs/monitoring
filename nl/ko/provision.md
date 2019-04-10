---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# 인스턴스 프로비저닝
{: #provision}

Sysdig에서 메트릭을 모니터하고 관리하려면 우선 {{site.data.keyword.Bluemix}}에서 서비스의 인스턴스를 프로비저닝해야 합니다.
{:shortdesc}

퍼블릭 클라우드 지역에서 Sysdig 인스턴스를 프로비저닝하려면 인스턴스와 연관된 서비스 플랜, 메트릭이 수집되는 지역 및 모니터 가능한 메트릭 수와 이의 보관 기간을 판별하는 플랜을 선택해야 합니다.



## 카탈로그에서 Sysdig 인스턴스 프로비저닝
{: #provision_ui}

{{site.data.keyword.cloud_notm}} 카탈로그에서 Sysdig의 인스턴스를 프로비저닝하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.cloud_notm}} 계정에 로그인하십시오.

    [{{site.data.keyword.cloud_notm}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/login){:new_window}를 클릭하여 {{site.data.keyword.cloud_notm}} 대시보드를 실행하십시오.

	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.cloud_notm}} UI가 열립니다.

2. **카탈로그**를 클릭하십시오. {{site.data.keyword.cloud_notm}}에서 사용 가능한 서비스의 목록이 열립니다.

3. 표시된 서비스의 목록을 필터링하려면 **개발자 도구** 카테고리를 선택하십시오.

4. **{{site.data.keyword.mon_full_notm}}** 타일을 클릭하십시오. *식별성* 대시보드가 열립니다.

5. **인스턴스 작성**을 선택하십시오. 

6. 서비스 플랜을 선택하십시오. 기본적으로 **체험판** 플랜이 설정됩니다.

    서비스 플랜에 대한 자세한 정보는 [서비스 플랜](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)을 참조하십시오.

7. 리소스 그룹을 선택하십시오. 기본적으로 **기본** 리소스 그룹이 설정됩니다.

8. **작성**을 클릭하십시오.

인스턴스를 프로비저닝한 후에는 

* *식별성* 대시보드가 열립니다. 
* 서비스 ID가 자동으로 작성됩니다. 이 서비스 ID를 사용하여 인스턴스에 대한 Sysdig 액세스 키를 가져올 수 있습니다.

그 다음에는 Sysdig 에이전트를 추가하여 메트릭 소스를 구성하십시오. 이 에이전트는 메트릭을 수집하고 이를 Sysdig에 전달하는 일을 담당합니다. 



## CLI를 통해 Sysdig 인스턴스 프로비저닝
{: #provision_cli}

명령행을 통해 Sysdig의 인스턴스를 프로비저닝하려면 다음 단계를 완료하십시오.

1. [전제조건] {{site.data.keyword.cloud_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.cloud_notm}} CLI 설치](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)를 참조하십시오.

   CLI가 설치되면 다음 단계를 계속하십시오.

2. 인스턴스를 프로비저닝할 {{site.data.keyword.cloud_notm}}의 지역에 로그인하십시오. [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) 명령을 실행하십시오.

3. 인스턴스를 프로비저닝할 리소스 그룹을 설정하십시오. [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target) 명령을 실행하십시오.

    기본적으로 `기본` 리소스 그룹이 설정됩니다.

4. Sysdig 인스턴스를 작성하십시오. [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) 명령을 실행하십시오.

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    여기서

    * NAME은 Sysdig 인스턴스의 이름입니다.
    
    * *sysdig-monitor*는 {{site.data.keyword.cloud_notm}}에서 {{site.data.keyword.mon_full_notm}} 서비스 이름의 이름입니다.
    
    * SERVICE_PLAN_NAME은 플랜의 유형입니다. 유효한 값은 *lite*, *graduated-tier*입니다.
    
    * LOCATION은 인스턴스가 작성된 지역입니다.

    예를 들어, 유료 플랜으로 인스턴스를 프로비저닝하려면 다음 명령을 실행하십시오.

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

