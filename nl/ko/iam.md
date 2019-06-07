---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

 
# {{site.data.keyword.cloud_notm}}에서 사용자 액세스 관리
{: #iam}

{{site.data.keyword.iamlong}}(IAM)를 사용하면 안전하게 사용자를 인증하고 {{site.data.keyword.cloud_notm}}에서 일관적으로 모든 클라우드 리소스에 대한 액세스를 제어할 수 있습니다. 
{:shortdesc}

**계정의 {{site.data.keyword.mon_full_notm}} 서비스에 액세스하는 모든 사용자에게는 IAM 사용자 역할이 정의된 액세스 정책이 지정되어야 합니다.** 정책은 선택된 서비스 또는 인스턴스의 컨텍스트 내에서 사용자가 수행할 수 있는 조치를 판별합니다. 허용되는 조치는 서비스에서 수행될 수 있는 오퍼레이션으로서 사용자 정의 및 정의됩니다. 그리고 조치는 IAM 사용자 역할에 맵핑됩니다.

*정책*을 사용하면 서로 다른 레벨에서 액세스 권한이 부여될 수 있습니다. 일부 옵션에는 다음이 포함됩니다. 

* 계정의 모든 IAM 사용 서비스에 액세스
* 계정의 단일 지역에서 서비스의 모든 인스턴스 간에 액세스
* 계정의 개별 서비스 인스턴스에 액세스
* 리소스 그룹의 컨텍스트 내에서 서비스의 모든 인스턴스에 액세스
* 리소스 그룹의 컨텍스트 내에서 단일 지역의 서비스의 모든 인스턴스에 액세스
* 리소스 그룹의 컨텍스트 내에서 모든 IAM 사용 서비스에 액세스

*역할*은 사용자 또는 serviceID가 실행할 수 있는 조치를 정의합니다. {{site.data.keyword.cloud_notm}}에는 상이한 유형의 역할이 있습니다.
* *플랫폼 관리 역할*을 사용하여 사용자는 플랫폼 레벨에서 서비스 리소스에 대한 태스크를 수행할 수 있습니다(예: 서비스에 대한 사용자 액세스 지정, 서비스 ID 작성 및 삭제, 인스턴스 작성, 기타 사용자에게 서비스에 대한 정책 지정 및 애플리케이션에 인스턴스 바인드).
* *서비스 액세스 역할*을 사용하여 사용자는 서비스의 API를 호출하기 위한 다양한 권한 레벨을 지정받을 수 있습니다.

**IAM 권한 관리가 용이하도록 하는 단일 엔티티로 사용자 및 서비스 ID 세트를 구성하려면 **액세스 그룹*을 사용하십시오.** 개별 사용자 또는 서비스 ID당 여러 번 동일한 액세스를 지정하는 대신 단일 정책을 그룹에 지정할 수 있습니다.
{: tip}


## 액세스 그룹을 사용하여 액세스 관리
{: #iam_groups}

액세스 그룹을 사용하여 사용자에 대한 새 액세스 권한을 지정하거나 액세스 권한을 관리하려면 계정의 모든 ID 및 액세스 사용 서비스에 대한 편집자 또는 관리자, 계정 소유자이거나 IAM 액세스 그룹 서비스에 대한 지정 관리자 또는 편집자여야 합니다. 

{{site.data.keyword.cloud_notm}}에서 액세스 그룹을 관리하려면 다음 조치를 선택하십시오.

* [액세스 그룹 작성](/docs/iam?topic=iam-groups#create_ag).
* [그룹에 액세스 지정](/docs/iam?topic=iam-groups#access_ag).


## 사용자에게 직접 정책을 지정하여 액세스 관리
{: #iam_users}

IAM 정책을 사용하여 사용자에 대한 새 액세스를 지정하거나 액세스를 관리하려면 계정의 모든 서비스에 대한 계정 소유자, 관리자이거나 특정 서비스 또는 서비스 인스턴스에 대한 관리자여야 합니다. 

{{site.data.keyword.cloud_notm}}에서 IAM 정책을 관리하려면 다음 조치를 선택하십시오.

* 사용자의 권한을 수정하려면 [기존 액세스 편집](/docs/iam?topic=iam-iammanidaccser#edit_existing)을 참조하십시오.
* 사용자에게 권한을 부여하려면 [새 액세스 지정](/docs/iam?topic=iam-iammanidaccser#assign_new_access)을 참조하십시오.
* 권한을 취소하려면 [액세스 제거](/docs/iam?topic=iam-iammanidaccser#removing_access)를 참조하십시오.
* 사용자의 권한을 검토하려면 [지정된 액세스 검토](/docs/iam?topic=iam-iammanidaccser#review_your_access)를 참조하십시오.


## {{site.data.keyword.cloud_notm}} 플랫폼 역할
{: #iam_platform}

다음 표를 사용하면 다음의 플랫폼 조치를 실행하기 위해 {{site.data.keyword.cloud_notm}}에서 사용자에게 권한 부여할 수 있는 플랫폼 역할을 식별할 수 있습니다.

| 플랫폼 조치                                                        | {{site.data.keyword.cloud_notm}} 플랫폼 역할    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `기타 계정 구성원에 서비스 관련 작업을 위한 액세스 권한 부여`           | 관리자                                        | 
| `서비스 인스턴스 프로비저닝`                                          | 관리자 </br>편집자                            | 
| `서비스 인스턴스 삭제`                                             | 관리자 </br>편집자                            | 
| `서비스 ID 작성`                                                   | 관리자 </br>편집자                            |
| `서비스 인스턴스의 세부사항 보기`                                    | 관리자 </br>편집자 </br>운영자 </br>뷰어  | 
| `식별성 모니터링 대시보드의 서비스 인스턴스 보기`      | 관리자 </br>편집자 </br>운영자 </br>뷰어  | 
{: caption="표 1. IAM 사용자 역할 및 조치" caption-side="top"}



## Sysdig 역할
{: #iam_sysdig_roles}

다음 표에는 Sysdig 역할 및 역할당 조치가 간략하게 설명되어 있습니다.

| 조치                                                                    | Sysdig 역할                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Sysdig 액세스 키 재설정`                                              | Admin                                                |
| `사용자 관리`                                                             | Admin                                                |
| `팀 작성, 구성 및 삭제`                                      | Admin                                                |
| `알림 채널 구성 및 제거`                              | Admin                                                | 
| `Sysdig 에이전트 구성 및 제거`                                       | Admin                                                |
| `Sysdig 웹 UI에서 컨텐츠 작성, 삭제 및 편집`                    | Admin </br>사용자                                      |  
| `Sysdig 웹 UI를 통해 메트릭 보기`                                   | Admin </br>사용자                                      |  
| `경보 작성 및 삭제`                                                 | Admin </br>사용자                                      | 
| `캡처 작성 및 삭제`                                               | Admin </br>사용자                                      |   
{: caption="표 2. Sysdig 역할 및 조치" caption-side="top"}


## Sysdig 역할을 {{site.data.keyword.cloud_notm}} 역할에 맵핑
{: #iam_sysdig}

다음 표를 사용하여 {{site.data.keyword.cloud_notm}} 역할이 Sysdig 역할에 맵핑되는 방법을 알아볼 수 있습니다.

| 역할 유형        | 역할               | Sysdig 역할                |설명                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| 플랫폼 역할       | 관리자      | Admin                      | 사용자 Sysdig admin 권한을 부여합니다.   | 
| 서비스 역할        | 매니저            | Admin                      | 사용자 Sysdig admin 권한을 부여합니다.   | 
| 서비스 역할        | 작성자             | 사용자                       | 사용자 Sysdig 사용자 권한을 부여합니다.    |
| 서비스 역할        | 독자             |                            | 권한이 부여되지 않습니다.                 |
{: caption="표 3. Sysdig 역할" caption-side="top"}


