---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# 캡처 관리
{: #captures}

캡처는 시간 범위 중에 호스트에서 발생하는 사항을 분석하기 위해 생성할 수 있는 추적 파일입니다. 예를 들어, 이를 사용하여 병목현상 또는 컴포넌트 상호작용을 분석할 수 있습니다. {{site.data.keyword.mon_full_notm}} 서비스에서 개별 노드에 대한 *캡처*를 작성, 탐색, 다운로드 및 삭제할 수 있습니다. 
{:shortdesc}

자세한 정보는 [캡처](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)를 참조하십시오.


## 캡처 작성
{: #captures_create}

사용자는 *탐색* 보기에서 캡처를 작성합니다.

캡처 파일을 작성하려면 다음 단계를 완료하십시오.

1. 웹 UI에서 *탐색* 섹션으로 이동하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. 호스트 전환 아이콘 ![호스트 전환 아이콘](images/switch_hosts.png)을 클릭하십시오.

3. 호스트 또는 컨테이너를 선택하십시오.

4. 조치 아이콘 ![세 점 아이콘](images/actions.png)을 클릭하고 **Sysdig 캡처**를 선택하십시오.

    *Sysdig 캡처* 창이 열립니다.

5. *Sysdig 캡처* 창에서 다음 매개변수를 정의하십시오.

    1. *캡처 경로 및 이름* 필드에서 캡처 파일의 이름을 입력하십시오. 기본값을 그대로 두거나 이를 수정할 수 있습니다. 기본 이름에는 캡처 작성 시의 날짜와 시간소인이 포함됩니다. 

    2. 데이터 수집 시간(초)을 지정하려면 *시간 범위*를 설정하십시오. 기본 캡처 시간은 15초입니다. 최대 캡처 시간은 86400초(24시간)입니다. 

    3. (선택사항) 수집되는 추적 정보의 양을 제한하려면 필터를 추가하십시오. 

6. **캡처 시작**을 클릭하십시오. 캡처 시작 신호가 Sysdig 에이전트에 전달되며 이는 결과 추적 파일을 되돌려줍니다. 

7. **캡처 페이지로 이동**을 클릭하여 웹 UI의 *캡처* 섹션에서 캡처의 목록을 표시하십시오. 

*캡처* 페이지는 캡처 파일 이름, 캡처가 검색된 호스트, 시간 범위 및 캡처 크기를 나열하는 테이블을 표시합니다. 

캡처 파일의 상태 값은 다음과 같을 수 있습니다.
* `요청됨`: 파일을 생성 중입니다.
* `업로드됨`: 파일을 다운로드 및 분석할 수 있습니다.
* `오류`: 제한시간 초과, 데이터 미수신 또는 에이전트 오류 때문에 파일을 사용할 수 없습니다.



## 캡처 삭제
{: #captures_delete}

캡처 파일을 삭제하려면 다음 단계를 완료하십시오.

1. 웹 UI에서 *캡처* 섹션으로 이동하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. 삭제할 캡처 파일을 식별하고 선택하십시오.
3. **삭제**를 클릭하십시오.



## 캡처 탐색
{: #captures_explore}

캡처 파일을 탐색하려면 다음 단계를 완료하십시오.

1. 웹 UI에서 *캡처* 섹션으로 이동하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. 분석할 호스트에 대한 데이터가 포함된 캡처 파일을 식별하고 선택하십시오.
3. **탐색**을 클릭하십시오.



## 캡처 다운로드
{: #captures_download}

캡처 파일을 다운로드하려면 다음 단계를 완료하십시오.

1. 웹 UI에서 *캡처* 섹션으로 이동하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. 다운로드할 데이터가 포함된 캡처 파일을 식별하고 선택하십시오.
3. **다운로드**를 클릭하십시오.


## 치즐
{: #captures_chisels}

Sysdig 치즐은 스크립팅 언어인 Lua로 작성된 스크립트입니다. 이를 사용하여 캡처 파일의 데이터를 분석할 수 있습니다. 

자세한 정보는 [Chisels User Guide ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}를 참조하십시오.



## Csysdig
{: #captures_csysdig}

Csysdig는 모니터링 및 디버깅을 위해 설계된 Linux용 오픈 소스 도구입니다. 이를 사용하여 캡처 파일을 분석할 수 있습니다. 

자세한 정보는 다음 리소스를 참조하십시오.
* [Csysdig 블로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Csysdig 동영상 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


