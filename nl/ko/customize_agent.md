---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 데이터 제어를 위한 Sysdig 에이전트의 사용자 정의
{: #customize_agent}

기본적으로 Sysdig 에이전트는 다양한 플랫폼 및 애플리케이션에서 데이터를 수집합니다. 사용자는 에이전트 구성 파일을 편집하여 기본 작동을 변경하고 데이터를 포함 또는 제외할 수 있습니다. 또한 Sysdig 에이전트 구성 파일을 사용자 정의하여 JMX, StatsD 및 Prometheus 등의 사용자 정의 메트릭을 포함시킬 수 있습니다. 메트릭, 이벤트 데이터 및 컨테이너를 필터링하여 걸러낼 수도 있습니다.
{:shortdesc}

## Kubernetes Sysdig 에이전트의 사용자 정의
{: #kube}

Kubernetes Sysdig 에이전트는 자동으로 수집할 데이터를 지정하는 두 개의 구성 파일을 사용합니다.

| 파일 이름                        | 조치           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` |로그 레벨을 수정합니다. |
| `sysdig-agent-configmap.yaml`    | 포트를 차단합니다. </br>메트릭 데이터를 포함 또는 제외합니다. </br>이벤트를 추가 또는 제거합니다. </br>컨테이너를 필터링하여 걸러냅니다. |
{: caption="표 1. Kubernetes Sysdig 에이전트 구성 파일" caption-side="top"} 

Kubernetes Sysdig 에이전트를 편집하려면 *sysdig-agent-configmap.yaml*, *sysdig-agent-daemonset-v2.yaml* 또는 두 파일을 모두 편집해야 합니다.

구성 파일의 수정에 사용할 수 있는 두 가지 방법이 있습니다.
* 방법 1: 에이전트가 실행되는 클러스터에서 직접 파일을 수정합니다. 자세한 정보는 [kubectl edit을 사용하여 Kubernetes Sysdig 에이전트 구성 편집](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1)을 참조하십시오.
* 방법 2: 로컬로 파일을 수정하고 변경사항을 클러스터에 적용합니다. 자세한 정보는 [kubectl apply를 사용하여 Kubernetes Sysdig 에이전트 구성 편집](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2)을 참조하십시오.

에이전트가 수집하는 데이터에 태그를 추가할 수 있습니다. 
* 이러한 태그를 사용하면 모니터 중인 데이터를 관리하는 데 도움이 됩니다. 

    * 레이블을 사용하여 인프라 리소스를 논리 계층 구조로 그룹화하고 데이터를 필터링하여 걸러내며 집계된 데이터를 세그먼트로 분할할 수 있습니다. 
    
    * 그래프를 구성하거나 메트릭에 대한 경보를 작성할 때 데이터 집계 방법을 사용자 정의하십시오. 
    
    * 데이터 점을 필터링하여 걸러내기 위한 경보 또는 패널, 대시보드의 범위를 설정하십시오. 
    
    * 팀을 통한 사용자의 데이터 액세스를 관리하여 데이터에 대한 액세스를 제한하십시오. 
    
    * 데이터 관리 방법에 대한 자세한 정보는 [데이터 관리](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)를 참조하십시오.

* 태그 추가 방법에 대한 정보는 [Kubernetes Sysdig 에이전트에서 수집된 데이터에 태그를 더 추가](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags)를 참조하십시오. 


**Sysdig 에이전트가 수집하는 데이터를 사용자 정의할 수 있습니다. ** 

이벤트, 메트릭 및 컨테이너를 제외할 때는 다음 정보를 고려하십시오.
* 에이전트 및 백엔드 로드를 줄일 수 있습니다.
* 모니터하고자 하는 컨테이너의 데이터만 수집합니다.
* 중요한 컨테이너에 대해서는 보고하고 불필요한 또는 중요치 않은 컨테이너는 필터링하여 걸러내어 비용을 통제할 수 있습니다.
* 모니터하고자 하는 Kubernetes 이벤트를 구성할 수 있습니다. 자세한 정보는 [Kubernetes 이벤트 세트 수집](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events)을 참조하십시오.

다음 목록에는 Sysdig 에이전트가 수집하는 데이터를 제어하기 위해 수행할 수 있는 조치가 간략하게 설명되어 있습니다.
* [이벤트 수집 사용 안함](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [메트릭 포함 및 제외](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [데이터가 수집되는 kubernetes 오브젝트 및 컨테이너 필터링](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [포트 차단](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [심각도별 Kubernetes 이벤트 필터링](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

수집된 항목과 로그의 유형 역시 사용자 정의할 수 있습니다. 자세한 정보는 [로그 레벨 변경](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level)을 참조하십시오.

또한 에이전트가 데이터를 보고하는 메트릭의 목록을 로깅할 수도 있습니다. 자세한 정보는 [포함 또는 제외되는 메트릭을 파일에 로깅](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics)을 참조하십시오.

Sysdig 에이전트는 */opt/draios/logs/draios.log*의 로그 항목을 생성합니다. 
* 로그 파일은 10MB 크기에 도달하면 순환됩니다.
* 10개의 최근 로그 파일이 보관됩니다. 파일 이름에 추가된 날짜 소인은 보관할 파일을 판별하는 데 사용됩니다.
* 유효한 로그 레벨은 *없음*, *오류*, *경고*, *정보*, *디버그*, *추적*입니다.
* 기본 로그 레벨은 *정보*이며, 여기서는 경고 및 오류에 대한 항목과 함께 백엔드 서버로의 집계된 메트릭 전송 각각에 대해 항목이 작성됩니다.

다음 표에는 일부 공통 시나리오 및 이들 각각에서 사용자가 설정해야 하는 값이 나열되어 있습니다.

| 유스 케이스                                     | 로그 섹션 항목           |
|-----------------------------------------------|-----------------------------|
| 에이전트 작동의 문제점 해결                   | `file_priority: debug`      |
| 컨테이너 콘솔 출력 감소               | `console_priority: warning` |
| 심각도별 이벤트 필터링                  | `event_priority: warning`   |
| 포함 또는 제외되는 메트릭 확인  | `metrics_excess_log: true`  |

## 컨테이너 Sysdig 에이전트
{: #container}


다음 목록에는 Sysdig 에이전트가 수집하는 데이터를 제어하기 위해 수행할 수 있는 조치가 간략하게 설명되어 있습니다.
* [이벤트 수집 사용 안함](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [메트릭 포함 및 제외](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [데이터가 수집되는 컨테이너 필터링](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [포트 차단](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [심각도별 이벤트 필터링](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

수집된 항목과 로그의 유형 역시 사용자 정의할 수 있습니다. 자세한 정보는 [로그 레벨 변경](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level)을 참조하십시오.



## Linux Sysdig 에이전트
{: #linux}

Linux Sysdig 에이전트는 자동으로 수집할 데이터를 지정하는 두 개의 구성 파일을 사용합니다.

|파일                   |설명                                                     |위치                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | 기본 구성 파일 </br>**참고:****이 파일은 편집하지 마십시오.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Sysdig 에이전트를 사용자 정의하기 위해 편집하는 구성 파일입니다. | `/opt/draios/etc/dragent.yaml`          |
{: caption="표 1. Sysdig 에이전트 구성 파일" caption-side="top"} 

사용자는 *dragent.yaml* 파일을 편집하여 수집되는 데이터를 사용자 정의할 수 있습니다. 변경사항은 파일을 저장하는 즉시 적용됩니다. 에이전트는 변경사항을 감지하고 자동으로 다시 시작됩니다. 사용자는 Sysdig 에이전트가 *dragent.default.yaml* 파일에서 확인하는 파일 및 빈도를 찾을 수 있습니다. 자세한 정보는 [dragent yaml 파일 편집](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent)을 참조하십시오.

예를 들어, *dragent.default.yaml*에는 다음 정보가 포함되어 있습니다.

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

다음 목록에는 Sysdig 에이전트가 수집하는 데이터를 제어하기 위해 수행할 수 있는 조치가 간략하게 설명되어 있습니다.
* [메트릭 포함 및 제외](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [포트 차단](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

수집된 항목과 로그의 유형 역시 사용자 정의할 수 있습니다. 자세한 정보는 [로그 레벨 변경](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level)을 참조하십시오.


