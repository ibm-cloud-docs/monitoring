---

copyright:
  years: 2018, 2019
lastupdated: "2018-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 컨테이너 Sysdig 에이전트의 사용자 정의
{: #change_agent}

{{site.data.keyword.mon_full_notm}}에서 사용자는 로그 레벨 설정, 포트 차단, 메트릭 데이터 포함/제외, 이벤트 추가/제거 및 필터링으로 컨테이너 걸러내기를 수행하도록 Sysdig 에이전트 구성을 사용자 정의할 수 있습니다. 
{:shortdesc}




## dragent yaml 파일 편집
{: #edit_agent}

yaml 파일은 */opt/draios/etc/*에 있습니다.

파일을 편집하고 변경사항을 적용하려면 다음 단계를 완료하십시오.

1. *dragent.yaml*(`/opt/draios/etc/dragent.yaml`)에 직접 액세스하십시오.
2. 파일을 편집하십시오. 올바른 YAML 구문을 사용하십시오.
3. 에이전트를 다시 시작하십시오. 다음 명령을 실행하십시오.

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## 포트 차단
{: #ports}

네트워크 포트에서 네트워크 트래픽 및 메트릭을 차단하려면 *dragent.yaml* 파일의 **blacklisted_ports** 섹션을 사용자 정의해야 합니다. 사용자는 해당 데이터를 필터링하여 걸러내고자 하는 포트를 나열해야 합니다.

**참고:** 포트 53(DNS)은 항상 블랙리스트에 있습니다. 

예를 들어, 다음 샘플은 포트 6666 및 6379에서 유입되는 데이터를 제외하도록 Sysdig 에이전트의 *blacklisted_ports* 섹션을 설정하는 방법을 보여줍니다.

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## Docker 이벤트 세트 수집
{: #docker}

{{site.data.keyword.mon_full_notm}}에서는 Docker와의 이벤트 통합을 지원합니다. Sysdig 에이전트는 Docker 소스를 자동 검색하고 이로부터 이벤트 데이터를 수집합니다. 사용자는 에이전트 구성 파일을 편집하여 기본 작동을 변경하고 이벤트 데이터를 포함 또는 제외할 수 있습니다. 

기본적으로는 한정된 세트의 이벤트만 수집됩니다. 기본 설정 구성 파일 */opt/draios/etc/dragent.default.yaml*에는 수집된 이벤트가 포함됩니다. 기본적으로 수집되는 이벤트에 대한 자세한 정보는 [Docker 이벤트![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}를 참조하십시오.

이벤트를 추가 또는 제거하려면 *dragent.yaml* 파일을 사용자 정의하여 포함할 이벤트와 필터링하여 걸러낼 이벤트를 지정해야 합니다. **참고:** *dragent.yaml*에 있는 섹션의 항목은 기본 구성의 전체 섹션을 대체합니다.
{: tip}

예를 들어, Docker 이미지 이벤트는 필터링하여 걸러내고 접속, 커미트 및 복사 조치에 대한 이벤트만 수집하려면 *docker* 섹션을 다음과 같이 설정해야 합니다.

* 옵션 1: 글머리 기호 목록으로 항목의 시퀀스 정의:

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* 옵션 2: 대괄호로 묶인 단일 행에 항목의 시퀀스 정의:

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## 이벤트 수집 사용 안함
{: #disable}

Sysdig 에이전트가 이벤트를 수집하지 못하도록 하려면 *dragent.default.yaml* 파일을 수정하십시오. *dragent.yaml* 파일에서 **events** 섹션을 *none*으로 설정하십시오.

예를 들어, Docker 이벤트를 필터링하여 걸러내려면 *dragent.yaml* 파일의 *events* 섹션을 다음과 같이 설정해야 합니다.

```
events:
  docker: none
```
{: codeblock}



## 심각도별 이벤트 필터링
{: #severity}

심각도별로 이벤트를 필터링하려면 *dragent.yaml* 파일에서 이벤트에 대한 로그 항목 유형 변경도 필요합니다. 

기본 로그 레벨은 **정보**입니다. 이는 경고 이상의 심각도 이벤트만 전송됨을 의미합니다.

유효한 레벨은 *긴급*, *경보*, *심각*, *오류*, *경고*, *알림*, *정보*, *디버그* 및 *없음*입니다. **참고**: 값은 높은 우선순위에서 낮은 우선순위 순으로 나열되어 있습니다.

예를 들어, 낮은 심각도 이벤트(*알림*, *정보*, *디버그*)를 필터링하여 걸러내려면 로그 섹션 **event_priority**를 *warning*으로 설정해야 합니다.

```
log:
  event_priority: warning
```
{: codeblock}


이벤트 수집을 차단하려면 로그 섹션 **event_priority**를 *none*으로 설정해야 합니다.

```
log:
  event_priority: none
```
{: codeblock}




## 메트릭 포함 및 제외
{: #params}

사용자 정의 메트릭을 필터링하려면 *dragent.yaml* 파일의 **metrics_filter** 섹션을 사용자 정의해야 합니다. **include** 및 **exclude** 필터링 매개변수를 구성하여 포함할 메트릭과 필터링하여 제외할 메트릭을 지정할 수 있습니다.

**참고:** 필터링 규칙 순서의 설정: 메트릭과 일치하는 첫 번째 규칙이 적용됩니다.

예를 들어, Sysdig 에이전트의 *metrics_filter* 섹션은 다음과 같을 수 있습니다.

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* *metricA*, *metricB* 및 *haproxy.backend*로 시작하는 메트릭의 모든 데이터를 수집하도록 Sysdig 에이전트를 구성합니다. 
* *metricC*로 시작하는 메트릭과 *haproxy*로 시작하는 기타 메트릭은 필터링하여 걸러냅니다. 
* `exclude: metricA.*` 항목은 무시합니다.


## 로그 레벨 변경
{: #log_level}

로그 레벨을 구성하려면 *dragent.yaml* 파일의 **log** 섹션을 사용자 정의해야 합니다. 

Sysdig 에이전트는 */opt/draios/logs/draios.log*의 로그 항목을 생성합니다. 
* 로그 파일은 10MB 크기에 도달하면 순환됩니다.
* 10개의 최근 로그 파일이 보관됩니다. 파일 이름에 추가된 날짜 소인은 보관할 파일을 판별하는 데 사용됩니다.
* 유효한 로그 레벨은 *없음*, *오류*, *경고*, *정보*, *디버그*, *추적*입니다.
* 기본 로그 레벨은 *정보*이며, 여기서는 경고 및 오류에 대한 항목과 함께 백엔드 서버로의 집계된 메트릭 전송 각각에 대해 항목이 작성됩니다.
* Sysdig 에이전트 구성 파일 **/opt/draios/etc/dragent.yaml**을 구성하여 수집된 항목과 로그의 유형을 사용자 정의할 수 있습니다. 파일 편집을 마치면 변경사항을 적용하기 위해 `docker restart sysdig-agent`로 쉘에서 에이전트를 다시 시작해야 합니다.

| 유스 케이스                                     | 로그 섹션 항목           |
|-----------------------------------------------|-----------------------------|
| 에이전트 작동의 문제점 해결                   | `file_priority: debug`      |
| 컨테이너 콘솔 출력 감소               | `console_priority: warning` |
| 심각도별 이벤트 필터링                  | `event_priority: warning`   |
| 포함 또는 제외되는 메트릭 확인  | `metrics_excess_log: true`  |
{: caption="표 2. 로그 섹션 항목" caption-side="top"} 


