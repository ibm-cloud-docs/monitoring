---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# Kubernetes Sysdig 에이전트의 사용자 정의
{: #change_kube_agent}

{{site.data.keyword.mon_full_notm}}에서 사용자는 로그 레벨 설정, 포트 차단, 메트릭 데이터 포함/제외, 이벤트 추가/제거 및 필터링으로 컨테이너 걸러내기를 수행하도록 Sysdig 에이전트 구성을 사용자 정의할 수 있습니다. 
{:shortdesc}

Kubernetes Sysdig 에이전트를 사용자 정의하려면 다음 파일의 섹션을 구성해야 합니다.

| 파일 이름                        | 조치       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` |로그 레벨을 수정합니다. |
| `sysdig-agent-configmap.yaml`    | 포트를 차단합니다. </br>메트릭 데이터를 포함 또는 제외합니다. </br>이벤트를 추가하거나 제거합니다. </br>컨테이너를 필터링합니다. |
{: caption="표 1. Kubernetes Sysdig 에이전트 구성 파일" caption-side="top"} 

Kubernetes Sysdig 에이전트를 편집하려면 *sysdig-agent-configmap.yaml*, *sysdig-agent-daemonset-v2.yaml* 또는 두 파일을 모두 편집해야 합니다.
{: tip}

구성 파일의 수정에 사용할 수 있는 두 가지 방법이 있습니다.
* 방법 1: 에이전트가 실행되는 클러스터에서 직접 파일을 수정합니다.
* 방법 2: 로컬로 파일을 수정하고 변경사항을 클러스터에 적용합니다.

## kubectl edit을 사용하여 Kubernetes Sysdig 에이전트 구성 편집
{: #change_kube_agent_edit_kube_agent_method1}

Kubernetes Sysdig 에이전트 구성을 편집하려면 다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-configmap.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    변경을 수행하십시오. **참고:** 변경하는 방법을 알아보려면 `vi` 편집기 지시사항을 참조하십시오.

    변경사항을 저장하십시오. 변경사항이 자동으로 적용됩니다. 

3. *sysdig-agent-daemonset-v2.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오. 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    변경을 수행하십시오. **참고:** 변경하는 방법을 알아보려면 `vi` 편집기 지시사항을 참조하십시오.

    변경사항을 저장하십시오. 변경사항이 자동으로 적용됩니다.

## kubectl apply를 사용하여 Kubernetes Sysdig 에이전트 구성 편집
{: #change_kube_agent_edit_kube_agent_method2}

소스 제어 시스템에서 저장 및 관리되는 구성 yaml 파일이 있는 경우에는 이 방법을 사용하십시오.

Kubernetes Sysdig 에이전트 구성을 편집하려면 다음 단계를 완료하십시오.

1. 소스 제어기에서 각 파일의 최신 사본을 가져오십시오. 

    클러스터에 배치된 구성으로 로컬 파일을 작성하기 위해 다음 명령을 실행할 수도 있습니다.
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    또는 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. 구성을 편집하십시오.

3. 다음 명령을 사용하여 변경사항을 적용하십시오.

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    또는
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

실행 에이전트는 Kubernetes가 클러스터의 모든 노드에서 변경사항을 푸시한 이후 새 구성을 자동으로 선정합니다.


## Kubernetes Sysdig 에이전트에서 수집된 데이터에 태그를 더 추가
{: #change_kube_agent_add_tags}

이미 배치된 Kubernetes Sysdig 에이전트 구성에 태그를 더 추가하려면 다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-configmap.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. **참고:** 변경하는 방법을 알아보려면 `vi` 편집기 지시사항을 참조하십시오.

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 

제공된 샘플의 경우 **agent.tag.cluster_version** 및 **agent.tag.region** 태그를 가져옵니다. 이를 사용하여 경보를 정의하고 범위 등을 사용자 정의할 수 있습니다.



## Kubernetes 이벤트 세트 수집
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}}에서는 Kubernetes와의 이벤트 통합을 지원합니다. Sysdig 에이전트는 이러한 서비스를 자동 검색하고 이로부터 이벤트 데이터를 수집합니다. 사용자는 에이전트 구성 파일을 편집하여 기본 작동을 변경하고 이벤트 데이터를 포함 또는 제외할 수 있습니다. 

기본적으로는 한정된 세트의 이벤트만 수집됩니다. 기본적으로 수집되는 이벤트에 대한 자세한 정보는 [Kubernetes 이벤트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}를 참조하십시오.

이벤트를 추가 또는 제거하려면 *sysdig-agent-configmap.yaml* 파일을 사용자 정의하여 포함할 이벤트와 필터링하여 걸러낼 이벤트를 지정해야 합니다. **참고:** *sysdig-agent-configmap.yaml*에 있는 섹션의 항목은 기본 구성의 전체 섹션을 대체합니다.
{: tip}

Kubernetes 팟(Pod)에서 이벤트를 필터링하려면 다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-configmap.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *events* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

    **참고:** 변경하는 방법을 알아보려면 `vi` 편집기 지시사항을 참조하십시오.

    예를 들어, Kubernetes 팟(Pod) 풀링 이벤트는 수집하지만 기본적으로 수집되는 기타 팟(Pod) 이벤트는 필터링하여 걸러내고자 할 수 있습니다. replicationController 및 노드에 대한 기본 Kubernetes 이벤트는 여전히 수집하고자 합니다.

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 


Kubernetes 이벤트의 서브세트를 수집하는 방법을 볼 수 있는 다른 예제: 팟(Pod)에 대해 풀링 중, 풀링된 및 실패한 이벤트만 모니터하고자 합니다.

* 옵션 1: 글머리 기호 목록으로 항목의 시퀀스 정의:

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* 옵션 2: 대괄호로 묶인 단일 행에 항목의 시퀀스 정의:

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

사용자 정의 이벤트 관련 작업 방법에 대한 자세한 정보는 [사용자 정의 이벤트 관련 작업 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}을 참조하십시오.


## 이벤트 수집 사용 안함
{: #change_kube_agent_disable_events}

Sysdig 에이전트가 Kubernetes 이벤트를 수집하지 못하도록 하려면 *sysdig-agent-configmap.yaml* 파일을 수정해야 합니다. **events** 섹션의 **Kubernetes** 항목을 *none*으로 설정하십시오. 

다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-configmap.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *events* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 






## 메트릭 포함 및 제외
{: #change_kube_agent_inc_exc_metrics}

사용자 정의 메트릭을 필터링하려면 *sysdig-agent-configmap.yaml* 파일의 **metrics_filter** 섹션을 사용자 정의해야 합니다. **include** 및 **exclude** 필터링 매개변수를 구성하여 포함할 메트릭과 필터링하여 제외할 메트릭을 지정할 수 있습니다.

<p class="important">필터링 규칙 순서의 설정: 메트릭과 일치하는 첫 번째 규칙이 적용됩니다. 해당 메트릭에 대한 후속 규칙은 무시됩니다.</p>

다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-configmap.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *metrics_filter* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

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

4. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 




## 데이터가 수집되는 kubernetes 오브젝트 및 컨테이너 필터링
{: #change_kube_agent_filter_data}

Kubernetes Sysdig 에이전트는 Prometheus, StatsD, JMX, app-check 및 기본 제공 메트릭을 포함하여 클러스터에서 발견된 *모든 컨테이너*에서 자동으로 메트릭을 수집합니다.
 
메트릭 수집에서 컨테이너를 제외하도록 Sysdig 에이전트를 사용자 정의할 수 있습니다. 

컨테이너를 제외할 때는 다음 정보를 고려하십시오.
* 에이전트 및 백엔드 로드를 경감합니다.
* 모니터하고자 하는 컨테이너의 데이터만 수집합니다.
* 중요한 컨테이너에 대해서는 보고하고 불필요한 또는 중요치 않은 컨테이너는 필터링하여 걸러내어 비용을 통제할 수 있습니다.

Sysdig 에이전트가 컨테이너를 필터링하는 기능을 사용으로 설정하려면 *sysdig-agent-configmap.yaml* 파일을 사용자 정의해야 합니다. **containers** 섹션의 **use_container_filter** 항목을 *true*로 설정하십시오. **참고:** 기본적으로 이 기능은 꺼져 있습니다. 그 다음에는 하나 이상의 조건이 포함되며 적용하고자 하는 규칙을 정의하십시오.

다음 표에는 클러스터에서 필터링 규칙의 설정을 위해 정의할 수 있는 매개변수가 간략하게 설명되어 있습니다.

|매개변수                          |조건                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | 컨테이너 이미지 이름                           |
| `container.name`                   | 컨테이너 이름                                 |
| `container.label.*`                | 컨테이너 레이블                                |
| `kubernetes.object.*`             | Kubernetes 오브젝트. 오브젝트는 팟(Pod), 네임스페이스 등일 수 있습니다.   |
| `kubernetes.object.annotation.*`  | Kubernetes 오브젝트 어노테이션                   |
| `kubernetes.object.label.*`       | Kubernetes 오브젝트 레이블                        |
| `all`                              | 모든 오브젝트를 지정하기 위한 기본 규칙            |
{: caption="표 2. 컨테이너의 상태를 정의하기 위한 매개변수" caption-side="top"} 

Sysdig 에이전트가 **container_filter** 섹션에 정의된 규칙을 적용하는 방법에 대해 다음 정보를 고려하십시오.
* **include** 및 **exclude** 필터링 매개변수로 구성하여 조건을 정의합니다. 
* 목록의 첫 번째 일치 규칙은 컨테이너의 포함 또는 제외 여부를 판별합니다.
* 조건은 키 이름 및 값으로 구성됩니다. 컨테이너에 대한 해당 키가 값과 일치하면 규칙이 적용됩니다.
* 규칙에 여러 조건이 포함되어 있으면 적용되는 규칙에 대해 `모든 조건`이 일치해야 합니다.

Sysdig 에이전트가 클러스터에서 모니터하는 컨테이너를 필터링하여 걸러내려면 다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-configmap.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *metrics_filter* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

    예를 들어, 구성 맵의 다음 추출을 참조하십시오.

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 


## 포트 차단
{: #change_kube_agent_block_ports}

네트워크 포트에서 네트워크 트래픽 및 메트릭을 차단하려면 *sysdig-agent-configmap.yaml* 파일의 **blacklisted_ports** 섹션을 사용자 정의해야 합니다. 사용자는 해당 데이터를 필터링하여 걸러내고자 하는 포트를 나열해야 합니다.

**참고:** 포트 53(DNS)은 항상 블랙리스트에 있습니다. 

다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-configmap.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *metrics_filter* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

    예를 들어, 다음 샘플은 포트 6666 및 6379에서 유입되는 데이터를 제외하도록 Sysdig 에이전트의 *blacklisted_ports* 섹션을 설정하는 방법을 보여줍니다.

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 



## 로그 레벨 변경
{: #change_kube_agent_log_level}

로그 레벨을 구성하려면 *sysdig-agent-daemonset-v2.yaml* 파일의 **log** 섹션을 사용자 정의해야 합니다. 

Sysdig 에이전트는 */opt/draios/logs/draios.log*의 로그 항목을 생성합니다. 
* 로그 파일은 10MB 크기에 도달하면 순환됩니다.
* 10개의 최근 로그 파일이 보관됩니다. 파일 이름에 추가된 날짜 소인은 보관할 파일을 판별하는 데 사용됩니다.
* 유효한 로그 레벨은 *없음*, *오류*, *경고*, *정보*, *디버그*, *추적*입니다.
* 기본 로그 레벨은 *정보*이며, 여기서는 경고 및 오류에 대한 항목과 함께 백엔드 서버로의 집계된 메트릭 전송 각각에 대해 항목이 작성됩니다.
* Sysdig 에이전트 구성 파일 **/opt/draios/etc/dragent.yaml**을 구성하여 수집된 항목과 로그의 유형을 사용자 정의할 수 있습니다. 파일 편집을 마치면 변경사항을 적용하기 위해 `service dragent restart`로 쉘에서 에이전트를 다시 시작해야 합니다.

다음 표에는 일부 공통 시나리오 및 이들 각각에서 사용자가 설정해야 하는 값이 나열되어 있습니다.

| 유스 케이스                                     | 로그 섹션 항목           |
|-----------------------------------------------|-----------------------------|
| 에이전트 작동의 문제점 해결                   | `file_priority: debug`      |
| 컨테이너 콘솔 출력 감소               | `console_priority: warning` |
| 심각도별 이벤트 필터링                  | `event_priority: warning`   |
| 포함 또는 제외되는 메트릭 확인  | `metrics_excess_log: true`  |
{: caption="표 2. 로그 섹션 항목" caption-side="top"} 

로그 레벨을 구성하려면 다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-daemonset-v2.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *log* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

    예를 들어, 낮은 심각도 이벤트(*알림*, *정보*, *디버그*)를 필터링하여 걸러내려면 **log** 섹션의 **metrics_excess_log** 항목을 *true*로 설정해야 합니다.

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 


## 심각도별 Kubernetes 이벤트 필터링
{: #change_kube_agent_filterby_severity}

심각도별로 이벤트를 필터링하려면 *sysdig-agent-daemonset-v2.yaml* 파일을 수정해야 합니다. **log** 섹션의 **event_priority** 항목을 *none*으로 설정하십시오. 

기본 로그 레벨은 **정보**입니다. 이는 경고 이상의 심각도 이벤트만 전송됨을 의미합니다.

유효한 레벨은 *긴급*, *경보*, *심각*, *오류*, *경고*, *알림*, *정보*, *디버그* 및 *없음*입니다. **참고**: 값은 높은 우선순위에서 낮은 우선순위 순으로 나열되어 있습니다.

다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-daemonset-v2.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *log* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

    예를 들어, 낮은 심각도 이벤트(*알림*, *정보*, *디버그*)를 필터링하여 걸러내려면 로그 섹션 **event_priority**를 *warning*으로 설정해야 합니다.

    ```
    log:
      event_priority: warning
    ```
    {: codeblock}

6. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 

## 포함 또는 제외되는 메트릭을 파일에 로깅
{: #change_kube_agent_log_metrics}

포함될 사용자 정의 메트릭과 제외될 사용자 정의 메트릭에 대한 정보를 파일에 로깅하려면 *sysdig-agent-daemonset-v2.yaml* 파일을 사용자 정의해야 합니다. **log** 섹션에서 **metrics_excess_log** 항목을 **true**로 설정하십시오.

* 로깅은 기본적으로 사용 안함으로 설정되어 있습니다. 
* 로깅은 30초마다 정보 레벨에서 발생하며 10초간 지속됩니다. 
* 로그 파일은 */opt/draios/logs/draios.log*에서 사용 가능합니다.
* 로깅 데이터의 형식은 다음과 같습니다.

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-*는 메트릭의 포함 또는 제외 여부를 표시하는 기호입니다. 더하기(*+*)는 메트릭이 포함됨을 표시합니다. 빼기(*-*)는 메트릭이 제외됨을 표시합니다. 

    * *[type]*은 메트릭 유형(예:*statsd*)을 지정합니다.
    
    * *[metric included/excluded]*는 사용자 판독 가능 방식으로 메트릭의 포함/제외 여부를 표시합니다.

    *  *metric.name*은 메트릭 이름을 표시합니다.

    * *(filter: +/-[metric.filter])*는 *sysdig-agent-daemonset-v2.yaml* 파일의 **metrics_filter** 섹션에 정의된 필터에 대한 정보를 제공합니다.

샘플 항목은 다음과 같습니다.

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. *sysdig-agent-daemonset-v2.yaml* 파일을 편집하십시오. 

    다음 명령을 실행하십시오.

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 변경을 수행하십시오. *log* 섹션을 추가하거나 해당 섹션을 업데이트하십시오.

    예를 들어, 낮은 심각도 이벤트(*알림*, *정보*, *디버그*)를 필터링하여 걸러내려면 **log** 섹션의 **metrics_excess_log** 항목을 *true*로 설정해야 합니다.

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. 변경사항을 저장하십시오. 

변경사항이 자동으로 적용됩니다. 


## 샘플 configmap yaml 파일
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:    
      kubernetes:
        node: 
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter: 
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## 샘플 daemonset yaml 파일
{: #change_kube_agent_sample_daemonset}

```
 Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

