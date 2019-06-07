---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# Linux Sysdig 에이전트의 사용자 정의
{: #change_linux_agent}

기본적으로 Sysdig 에이전트는 다양한 플랫폼 및 애플리케이션에서 데이터를 수집합니다. 사용자는 에이전트 구성 파일을 편집하여 기본 작동을 변경하고 데이터를 포함 또는 제외할 수 있습니다. 또한 Sysdig 에이전트 구성 파일을 사용자 정의하여 JMX, StatsD 및 Prometheus 등의 사용자 정의 메트릭을 포함시킬 수 있습니다. 메트릭 및 컨테이너를 필터링하여 걸러낼 수도 있습니다.
{:shortdesc}

Sysdig 에이전트는 자동으로 수집할 데이터를 지정하는 두 개의 구성 파일을 사용합니다.

|파일                   |설명                                                     |위치                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | 기본 구성 파일 </br>**참고:****이 파일은 편집하지 마십시오. | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Sysdig 에이전트를 사용자 정의하기 위해 편집하는 구성 파일입니다. | `/opt/draios/etc/dragent.yaml`          |
{: caption="표 1. Sysdig 에이전트 구성 파일" caption-side="top"} 

사용자는 *dragent.yaml* 파일을 편집하여 수집되는 데이터를 사용자 정의할 수 있습니다. 변경사항은 파일을 저장하는 즉시 적용됩니다. 에이전트는 변경사항을 감지하고 자동으로 다시 시작됩니다. 사용자는 Sysdig 에이전트가 *dragent.default.yaml* 파일에서 확인하는 파일 및 빈도를 찾을 수 있습니다.

예를 들어, *dragent.default.yaml*에는 다음 정보가 포함되어 있습니다.

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## dragent yaml 파일 편집
{: #change_linux_agent_edit_agent}

yaml 파일은 */opt/draios/etc/*에 있습니다.

파일을 편집하고 변경사항을 적용하려면 다음 단계를 완료하십시오.

1. *dragent.yaml*에 직접 액세스하십시오. 파일은 `/opt/draios/etc/dragent.yaml`에 있습니다.
2. 파일을 편집하십시오. 올바른 YAML 구문을 사용하십시오.
3. 에이전트를 다시 시작하십시오. 다음 명령을 실행하십시오.

    ```
    service dragent restart
    ```
    {: codeblock}


## 포트 차단
{: #change_linux_agent_block_ports}

네트워크 포트에서 네트워크 트래픽 및 메트릭을 차단하려면 *dragent.yaml* 파일의 **blacklisted_ports** 섹션을 사용자 정의해야 합니다. 사용자는 해당 데이터를 필터링하여 걸러내고자 하는 포트를 나열해야 합니다.

**참고:** 포트 53(DNS)은 항상 블랙리스트에 있습니다. 

예를 들어, 다음 샘플은 포트 6666 및 6379에서 유입되는 데이터를 제외하도록 Sysdig 에이전트의 *blacklisted_ports* 섹션을 설정하는 방법을 보여줍니다.

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## 메트릭 포함 및 제외
{: #change_linux_agent_inc_exc_metrics}

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
{: #change_linux_agent_log_level}

로그 레벨을 구성하려면 *dragent.yaml* 파일의 **log** 섹션을 사용자 정의해야 합니다. 

Sysdig 에이전트는 */opt/draios/logs/draios.log*의 로그 항목을 생성합니다. 
* 로그 파일은 10MB 크기에 도달하면 순환됩니다.
* 10개의 최근 로그 파일이 보관됩니다. 파일 이름에 추가된 날짜 소인은 보관할 파일을 판별하는 데 사용됩니다.
* 유효한 로그 레벨은 *없음*, *오류*, *경고*, *정보*, *디버그*, *추적*입니다.
* 기본 로그 레벨은 *정보*이며, 여기서는 경고 및 오류에 대한 항목과 함께 백엔드 서버로의 집계된 메트릭 전송 각각에 대해 항목이 작성됩니다.
* Sysdig 에이전트 구성 파일 **/opt/draios/etc/dragent.yaml**을 구성하여 수집된 항목과 로그의 유형을 사용자 정의할 수 있습니다. 파일 편집을 마치면 변경사항을 적용하기 위해 `service dragent restart`로 쉘에서 에이전트를 다시 시작해야 합니다.

| 유스 케이스                                     | 로그 섹션 항목           |
|-----------------------------------------------|-----------------------------|
| 에이전트 작동의 문제점 해결                   | `file_priority: debug`      |
| 컨테이너 콘솔 출력 감소               | `console_priority: warning` |
| 심각도별 이벤트 필터링                  | `event_priority: warning`   |
| 포함 또는 제외되는 메트릭 확인  | `metrics_excess_log: true`  |
{: caption="표 2. 로그 섹션 항목" caption-side="top"} 
