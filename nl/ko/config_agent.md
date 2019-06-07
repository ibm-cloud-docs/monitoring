---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

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

# Sysdig 에이전트 구성
{: #config_agent}

{{site.data.keyword.cloud_notm}}에서 {{site.data.keyword.mon_full_notm}} 서비스의 인스턴스를 프로비저닝한 후에는 모니터하고자 하는 각 환경에서 Sysdig 에이전트를 구성해야 합니다. Sysdig 에이전트는 사전 정의된 메트릭을 자동으로 수집하고 이에 대해 보고합니다. 사용자는 각 환경에서 모니터할 메트릭을 구성할 수 있습니다.
{:shortdesc}

하나 이상의 태그를 각 Sysdig 에이전트에 연관시킬 수 있습니다. 태그는 **TAG_NAME:TAG_VALUE** 형식의 쉼표로 구분된 값입니다. 환경을 모니터할 때 이러한 태그를 사용하여 에이전트에서 사용 가능한 메트릭을 식별할 수 있습니다. 예를 들어, 이 에이전트가 수집하는 모든 메트릭과 함께 서비스 이름과 위치에 대한 정보를 포함할 수 있습니다.
{: tip}

## Linux의 Sysdig 에이전트 구성
{: #config_agent_linux}

메트릭을 수집하고 이를 {{site.data.keyword.mon_full_notm}} 서비스의 인스턴스에 전달하도록 Linux의 Sysdig 에이전트를 구성하려면 다음 단계를 완료하십시오.

1. Sysdig 액세스 키를 가져오십시오. 자세한 정보는 [{{site.data.keyword.cloud_notm}} UI를 통해 액세스 키 가져오기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)를 참조하십시오.

2. 수집 URL을 가져오십시오. 자세한 정보는 [Sysdig 콜렉터 엔드포인트](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)를 참조하십시오.

3. Sysdig 에이전트를 배치하십시오. 터미널에서 다음 명령을 실행하십시오.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    여기서

    * SYSDIG_ACCESS_KEY는 인스턴스에 대한 수집 키입니다.

    * COLLECTOR_ENDPOINT는 모니터링 인스턴스가 사용 가능한 지역에 대한 수집 URL입니다.

    * TAG_DATA는 *TAG_NAME:TAG_VALUE* 형식의 쉼표로 구분된 태그입니다. 사용자는 하나 이상의 태그를 자신의 Sysdig 에이전트에 연관시킬 수 있습니다. 예를 들어, *role:serviceX,location:us-south*입니다.  

    * Sysdig 캡처 기능을 사용 안함으로 설정하려면 **sysdig_capture_enabled**를 *false*로 설정하십시오. 기본적으로는 *true*로 설정됩니다. 자세한 정보는 [캡처 관련 작업](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)을 참조하십시오.

    * 통신에서 SSL을 사용하려면 **secure**를 *true*로 설정하십시오.

Sysdig 에이전트가 올바른 설치에 실패하는 경우에는 커널 헤더를 수동으로 설치하십시오. 배포를 선택하고 해당 배포에 대한 명령을 실행하십시오. 그리고 Sysdig 에이전트의 배치를 재시도하십시오.

* **Debian 및 Ubuntu Linux 배포의 경우에는** 다음 명령을 실행하십시오.

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **RHEL, CentOS 및 Fedora Linux 배포의 경우에는** 다음 명령을 실행하십시오.

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Docker 컨테이너의 Sysdig 에이전트 구성
{: #config_agent_docker}

메트릭을 수집하고 이를 {{site.data.keyword.mon_full_notm}} 서비스의 인스턴스에 전달하도록 Docker 컨테이너의 Sysdig 에이전트를 구성하려면 다음 단계를 완료하십시오.

1. Sysdig 액세스 키를 가져오십시오. 자세한 정보는 [{{site.data.keyword.cloud_notm}} UI를 통해 액세스 키 가져오기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)를 참조하십시오.

2. 수집 URL을 가져오십시오. 자세한 정보는 [Sysdig 콜렉터 엔드포인트](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)를 참조하십시오.

3. Sysdig 에이전트를 배치하십시오. 다음 명령을 실행하십시오.

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    여기서

    * SYSDIG_ACCESS_KEY는 인스턴스에 대한 수집 키입니다.

    * COLLECTOR_ENDPOINT는 모니터링 인스턴스가 사용 가능한 지역에 대한 수집 URL입니다.

    * TAG_DATA는 *TAG_NAME:TAG_VALUE* 형식의 쉼표로 구분된 태그입니다. 사용자는 하나 이상의 태그를 자신의 Sysdig 에이전트에 연관시킬 수 있습니다. 예를 들어, *role:serviceX,location:us-south*입니다.  

    * Sysdig 캡처 기능을 사용 안함으로 설정하려면 **sysdig_capture_enabled**를 *false*로 설정하십시오. 기본적으로는 *true*로 설정됩니다. 자세한 정보는 [캡처 관련 작업](/docs/services/Monitoring-with-Sysdig/captures.html#captures)을 참조하십시오.

    * 통신에서 SSL을 사용하려면 **SECURE**를 *true*로 설정하십시오.

    컨테이너는 분리 모드에서 실행됩니다. 컨테이너의 출력을 보려면 *-d*를 제거하십시오.
    {: note}




## 스크립트를 사용하여 Kubernetes 클러스터의 Sysdig 에이전트 구성
{: #config_agent_kube_script}

{{site.data.keyword.containerlong_notm}}에서 실행되는 Kubernetes 클러스터의 Sysdig 에이전트를 구성하려면 다음 단계를 완료하십시오.

1. Sysdig 액세스 키를 가져오십시오. 자세한 정보는 [{{site.data.keyword.cloud_notm}} UI를 통해 액세스 키 가져오기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)를 참조하십시오.

2. 수집 URL을 가져오십시오. 자세한 정보는 [Sysdig 콜렉터 엔드포인트](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)를 참조하십시오.

3. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

4. Sysdig 에이전트를 배치하십시오. 다음 명령을 실행하십시오.

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    여기서

    * SYSDIG_ACCESS_KEY는 인스턴스에 대한 수집 키입니다.

    * COLLECTOR_ENDPOINT는 모니터링 인스턴스가 사용 가능한 지역에 대한 수집 URL입니다.

    * TAG_DATA는 *TAG_NAME:TAG_VALUE* 형식의 쉼표로 구분된 태그입니다. 사용자는 하나 이상의 태그를 자신의 Sysdig 에이전트에 연관시킬 수 있습니다. 예: *role:serviceX,location:us-south*. 

    * Sysdig 캡처 기능을 사용 안함으로 설정하려면 **sysdig_capture_enabled**를 *false*로 설정하십시오. 기본적으로는 *true*로 설정됩니다. 자세한 정보는 [캡처 관련 작업](/docs/services/Monitoring-with-Sysdig/captures.html#captures)을 참조하십시오.



## 수동으로 Kubernetes 클러스터의 Sysdig 에이전트 구성
{: #config_agent_kube_manually}

{{site.data.keyword.containerlong_notm}}에서 실행되는 Kubernetes 클러스터의 Sysdig 에이전트를 구성하려면 다음 단계를 완료하십시오.

1. Sysdig 액세스 키를 가져오십시오. 자세한 정보는 [{{site.data.keyword.cloud_notm}} UI를 통해 액세스 키 가져오기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)를 참조하십시오.

2. 수집 URL을 가져오십시오. 자세한 정보는 [Sysdig 콜렉터 엔드포인트](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)를 참조하십시오.

3. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

4. kubernetes 클러스터를 모니터하기 위한 **sysdig-agent**라고 하는 서비스 계정을 작성하십시오. 다음 명령을 실행하십시오.

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Kubernetes 클러스터에 시크릿을 추가하십시오. 다음 명령을 실행하십시오.

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY는 인스턴스에 대한 수집 키입니다.

    Kubernetes 시크릿에는 {{site.data.keyword.mon_full_notm}} 서비스에서 Sysdig 에이전트를 인증하는 데 사용되는 수집 키가 포함되어 있습니다. 이를 사용하여 모니터링 백엔드 시스템의 수집 서버에 대한 보안 웹 소켓을 열 수 있습니다.

6. 클러스터 역할 및 클러스터 역할 바인딩을 작성하십시오. 

    [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml)을 다운로드하십시오.
    
    클러스터 역할을 추가하려면 다음 명령을 실행하십시오.
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    클러스터 역할 바인딩을 추가하려면 다음 명령을 실행하십시오.

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. **sysdig-agent-configmap.yaml**을 편집하여 {{site.data.keyword.cloud_notm}}에서 작업할 에이전트의 구성을 위한 필수 매개변수를 추가하십시오.

    [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml)를 다운로드하십시오.

    편집기를 사용하여 sysdig-agent-configmap.yaml 파일을 여십시오. 그리고 다음 매개변수를 추가하십시오.

    * **k8s_cluster_name**: 이 매개변수는 메트릭 레이블로서 클러스터 이름을 지정합니다. *kubernetes.cluster.name* 레이블을 사용하여 클러스터 이름으로 Kubernetes 대시보드를 탐색하고 클러스터와 연관된 메트릭을 필터링하여 걸러낼 수 있습니다.

    * **collector**: 이 매개변수는 모니터링 인스턴스가 사용 가능한 지역에 대한 수집 URL을 지정합니다. 

    * **collector_port**: 이 매개변수는 콜렉터가 청취하는 포트를 표시합니다. 값은 *6443*으로 설정되어야 합니다.
    
    * **ssl**: 이 매개변수는 *true*로 설정되어야 합니다.
    
    * **ssl_verfiy_certificate**: 이 매개변수는 *true*로 설정되어야 합니다.
    
    * **new_k8s**: kube 상태 메트릭을 캡처하려면 이 매개변수는 *true*로 설정되어야 합니다.

    * **sysdig_capture_enabled**: 이 매개변수는 Sysdig 캡처 기능을 사용 또는 사용 안함으로 설정합니다. 기본적으로는 *true*로 설정됩니다. 자세한 정보는 [캡처 관련 작업](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)을 참조하십시오.

    예제 Yaml 파일은 다음과 같습니다.

    ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: ingest.us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

8. 클러스터에 구성 맵을 적용하십시오. 다음 명령을 실행하십시오.

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. daemonset를 적용하여 Sysdig 에이전트를 클러스터에 배치하십시오. 다음 명령을 실행하십시오.

    [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml)을 다운로드하십시오.

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




