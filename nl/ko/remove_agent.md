---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, delete agent

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

# Sysdig 에이전트 제거
{: #remove_agent}

{{site.data.keyword.mon_full_notm}} 인스턴스의 삭제 시에 또는 소스에서 메트릭 수집을 중지하고자 하는 경우에는 Sysdig 에이전트를 설치 제거해야 합니다.
{:shortdesc}


## Kubernetes 클러스터에서 Sysdig 에이전트 제거
{: #remove_agent_kube}

Kubernetes 클러스터에서 Sysdig 에이전트를 제거하려면 다음 단계를 완료하십시오.

1. 클러스터 환경을 설정하십시오. 다음 명령을 실행하십시오.

    우선 환경 변수를 설정하는 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    구성 파일의 다운로드가 완료되면 환경 변수로서 로컬 Kubernetes 구성 파일에 대한 경로 설정에 사용할 수 있는 명령이 표시됩니다.

    그리고 터미널에 표시된 명령을 복사하여 붙여넣어서 KUBECONFIG 환경 변수를 설정하십시오.

    **참고:** 클러스터 관련 작업을 위해 {{site.data.keyword.containerlong}} CLI에 로그인할 때마다 이러한 명령을 실행하여 세션 변수로서 클러스터의 구성 파일에 대한 경로를 설정해야 합니다. Kubernetes CLI는 이 변수를 사용하여 {{site.data.keyword.cloud_notm}}에서 클러스터와 연결하는 데 필요한 로컬 구성 파일과 인증서를 찾습니다.

2. 클러스터 역할 바인딩을 제거하십시오. 다음 명령을 실행하십시오.

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. 서비스 계정을 제거하십시오. 다음 명령을 실행하십시오.

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. daemonset를 제거하십시오. 다음 명령을 실행하십시오.

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. 시크릿을 제거하십시오. 다음 명령을 실행하십시오.

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Linux에서 Sysdig 에이전트 제거
{: #remove_agent_linux}

Linux에서 Sysdig 에이전트를 제거하려면 다음 단계를 완료하십시오.

* **Debian 및 Ubuntu Linux 배포**에서 에이전트를 설치 제거하려면 터미널에서 **sudo** 사용자로 다음 명령을 실행하십시오.

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* **RHEL, CentOS 및 Fedora Linux 배포**에서 에이전트를 설치 제거하려면 터미널에서 **sudo** 사용자로 다음 명령을 실행하십시오.

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


