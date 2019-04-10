---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# 웹 UI로 이동
{: #launch}

{{site.data.keyword.Bluemix}}에서 {{site.data.keyword.mon_full_notm}} 서비스의 인스턴스를 프로비저닝하고 메트릭 소스에 대한 Sysdig 에이전트를 구성한 후에는 {{site.data.keyword.mon_full_notm}} 웹 UI를 통해 메트릭을 보고 모니터하며 관리할 수 있습니다.
{:shortdesc}


## 사용자에게 데이터 보기를 위한 IAM 정책 부여 
{: #launch_step1}

**참고:** {{site.data.keyword.mon_full_notm}} 서비스의 관리자, {{site.data.keyword.mon_full_notm}} 인스턴스의 관리자이거나 기타 사용자 정책을 부여하기 위한 계정 IAM 권한이 있어야 합니다.

다음 표에는 {{site.data.keyword.mon_full_notm}} 웹 UI를 실행하고 데이터를 보기 위해 사용자가 보유해야 하는 최소 정책이 나열되어 있습니다.

| 서비스                        | 역할                      | 부여된 권한     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | 플랫폼 역할: 뷰어     | 사용자가 식별성 모니터링 대시보드에서 서비스 인스턴스의 목록을 볼 수 있도록 허용합니다. |
| `{{site.data.keyword.mon_full_notm}}` | 서비스 역할: 작성자      |사용자가 웹 UI를 실행하고 웹 UI에서 메트릭을 볼 수 있도록 허용합니다.  |
{: caption="표 1. IAM 정책" caption-side="top"} 

사용자에 대해 이러한 정책을 구성하는 방법에 대한 자세한 정보는 [사용자에게 메트릭 보기 권한 부여](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig)를 참조하십시오.


## {{site.data.keyword.cloud_notm}} UI를 통해 웹 UI 실행
{: #launch_step2}

{{site.data.keyword.cloud_notm}} UI에서, {{site.data.keyword.mon_full_notm}} 인스턴스의 컨텍스트 내에서 웹 UI를 실행하십시오. 

웹 UI를 실행하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.cloud_notm}} 계정에 로그인하십시오.

    [{{site.data.keyword.cloud_notm}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/login){:new_window}를 클릭하여 {{site.data.keyword.cloud_notm}} 대시보드를 실행하십시오.

	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.cloud_notm}} 대시보드가 열립니다.

2. 탐색 메뉴에서 **식별성**을 선택하십시오. 

3. **모니터링**을 선택하십시오. 

    {{site.data.keyword.cloud_notm}}에서 사용 가능한 인스턴스의 목록이 표시됩니다.

4. 하나의 인스턴스를 선택하십시오. 그리고 **Sysdig 보기**를 클릭하십시오.

웹 UI가 열립니다.


