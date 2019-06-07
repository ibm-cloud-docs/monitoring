---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.mon_full_notm}}의 문제점 해결
{: #troubleshoot}

{{site.data.keyword.mon_full_notm}} 서비스를 사용할 때 발생할 수 있는 몇 가지 일반적인 문제점에 대해 알아봅니다. 대부분 몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다.
{:shortdesc}

## 캡처를 작성할 때 오류가 발생합니까?
{: #troubleshoot-entry-1}

인프라의 호스트에 대한 [캡처 파일](/docs/services/Monitoring-with-Sysdig/captures.html#captures) 작성에 실패합니다. 

웹 UI의 *캡처* 섹션에서 호스트에 대한 캡처 파일을 작성하는 중에 오류가 발생합니다.
{: tsSymptoms}

호스트에서 실행 중인 Sysdig 에이전트의 **sysdig_capture_enabled** 기능이 *false*로 설정되어 있습니다.
{: tsCauses}

호스트에서 실행 중인 Sysdig 에이전트의 **sysdig_capture_enabled** 기능을 사용으로 설정하십시오.
{: tsResolve}


## 캡처 파일의 상태가 *요청됨*으로 설정되어 있으며 *업로드됨* 상태로 변경되지 않습니까?
{: #troubleshoot-entry-2}

[캡처 파일](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)의 상태가 *요청됨*으로 설정되어 있으며 *업로드됨* 상태로 변경되지 않습니다. 분석을 위해 캡처 파일이 사용 가능할 때까지 대기 중입니다.

웹 UI의 *캡처* 섹션에서 호스트에 대한 캡처 파일의 상태가 *업로드됨*으로 변경되지 않습니다.
{: tsSymptoms}

호스트의 TCP 포트 6443이 사용 안함으로 설정되어 있습니다.
{: tsCauses}


6443 포트가 열려 있는지 확인하십시오. 자세한 정보는 [네트워크 트래픽 관리](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send)를 참조하십시오.
{: tsResolve}


