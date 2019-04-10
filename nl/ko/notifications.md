---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# 알림 채널 관련 작업
{: #notifications}

경보가 트리거될 때 알림을 받으려면 알림 채널을 구성하십시오. 알림 채널은 웹 UI의 *설정* 패널을 통해 관리됩니다.
{:shortdesc}
 

## 알림 채널 구성
{: #notifications_create}

알림 채널을 추가하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. 웹 UI 실행 방법에 대한 자세한 정보는 [웹 UI로 이동](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)을 참조하십시오. 
    
2. 탐색줄의 *선택기* 단추에서 **설정**을 선택하십시오.

3. **알림 채널**을 선택하십시오.

4. **내 채널** ![추가 아이콘](../images/add.png)을 클릭하십시오. 그리고 채널을 선택하십시오.

    **참고:** 처음으로 알림 채널을 구성하는 경우에는 채널을 클릭하십시오.

5. 알림 채널을 구성하십시오.

    * 채널의 이름을 입력하십시오.

    * 경보 조건이 더 이상 트리거되지 않을 때 알림을 수신하려면 *정상 시에 알림* 필드를 사용으로 설정하십시오.

    * 사용자가 경보를 수동으로 분석할 때 알림을 수신하려면 *분석 시에 알림* 조건을 사용으로 설정하십시오.

    * **이메일** 알림 채널의 경우 쉼표로 분리된 수신인의 목록을 추가하십시오.

    * **slack** 알림 채널의 경우 *Slack 채널*의 이름을 추가하십시오.

    * **웹훅** 알림 채널의 경우 *웹훅 URL*을 추가하십시오. **참고:** 경보가 트리거되면 알림이 웹훅 엔드포인트에 JSON 형식의 POST로 전송됩니다. 자세한 정보는 [웹훅 채널 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}을 참조하십시오. 예를 들어, Sysdig는 사용자 정의 웹훅을 사용하여 ServiceNow와 통합될 수 있습니다. ServiceNow의 Sysdig 구성에 대해 알아보려면 [ServiceNow 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}을 참조하십시오.

    * **VictorOps** 알림 채널의 경우 *API 키* 및 *라우팅 키*를 추가하십시오.

    * **OpsGenie** 알림 채널의 경우 *OpsGenie API 키*를 추가하십시오. 참고로, OpsGenie에서 Sysdig와의 통합을 구성해야 합니다. 자세한 정보는 [Opsgenie에서 Sysdig 클라우드 통합 추가 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}를 참조하십시오.

    * **PagerDuty** 알림 채널의 경우에는 우선 계정과의 통합을 위해 Sysdig에 권한을 부여해야 합니다. PagerDuty를 선택하면 Sysdig와의 통합을 구성하기 위한 마법사가 열립니다. PagerDuty에 권한을 부여하려면 **통합에 권한 부여** 또는 **ID 제공자를 사용하여 사인인**을 클릭하십시오. Sysdig 통합에 대해 기존 서비스를 선택하거나 새 서비스를 설정한 후에 **통합 완료**를 클릭하십시오. Sysdig 인시던트에 사용할 에스컬레이션 정책을 선택하십시오. 그리고 *알림* 탭에서 PagerDuty 계정, 서비스 이름, 서비스 키를 확인하십시오. 

    * (선택사항) 테스트를 허용하는 통합의 경우 테스트 알림 수신을 위해 *테스트 알림* 조건을 사용으로 설정하십시오. 10분 안에 테스트 알림이 수신되지 않으면 채널 구성을 검토하십시오. 

6. **채널 작성**을 클릭하십시오. 



## 알림 채널 수정
{: #notifications_update}

알림 채널을 수정하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. 웹 UI 실행 방법에 대한 자세한 정보는 [웹 UI로 이동](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)을 참조하십시오. 
    
2. 탐색줄의 *선택기* 단추에서 **설정**을 선택하십시오.

3. **알림 채널**을 선택하십시오.

4. 수정할 대상 채널을 식별하고 **편집**을 클릭하십시오.

5. 변경을 마치면 **변경사항 저장**을 클릭하십시오.



## 알림 채널 테스트
{: #notifications_test}

알림 채널을 테스트하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. 웹 UI 실행 방법에 대한 자세한 정보는 [웹 UI로 이동](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)을 참조하십시오. 
    
2. 탐색줄의 *선택기* 단추에서 **설정**을 선택하십시오.

3. **알림 채널**을 선택하십시오.

4. 수정할 대상 채널을 식별하고 **테스트**를 클릭하십시오.



## 알림 채널 사용 안함
{: #notifications_disable}

알림 채널을 잠시 사용 안함으로 설정하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. 웹 UI 실행 방법에 대한 자세한 정보는 [웹 UI로 이동](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)을 참조하십시오. 
    
2. 탐색줄의 *선택기* 단추에서 **설정**을 선택하십시오.

3. **알림 채널**을 선택하십시오.

4. *알림* 섹션에서 *작동 중지 시간*을 사용으로 설정하여 잠시 경보 사용 안함을 설정하고 모든 알림을 차단하십시오.

## 알림 채널 삭제
{: #notifications_delete}

알림 채널을 삭제하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. 웹 UI 실행 방법에 대한 자세한 정보는 [웹 UI로 이동](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)을 참조하십시오. 
    
2. 탐색줄의 *선택기* 단추에서 **설정**을 선택하십시오.

3. **알림 채널**을 선택하십시오.

4. 수정할 대상 채널을 식별하고 **편집**을 클릭하십시오.

5. **채널 삭제**를 클릭하십시오.

6. 채널 삭제를 확인하십시오. **변경사항 저장**을 클릭하십시오.




