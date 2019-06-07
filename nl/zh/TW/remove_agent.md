---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

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

# 移除 Sysdig 代理程式
{: #remove_agent}

當您刪除 {{site.data.keyword.mon_full_notm}} 實例時，或如果想要停止從來源收集度量值，則必須解除安裝 Sysdig 代理程式。
{:shortdesc}


## 從 Kubernetes 叢集移除 Sysdig 代理程式
{: #remove_agent_kube}

請完成下列步驟，從 Kubernetes 叢集移除 Sysdig 代理程式：

1. 設定叢集環境。請執行下列指令：

    首先，取得指令來設定環境變數，並下載 Kubernetes 配置檔。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置檔下載完成之後，會顯示一個指令，可讓您用來將本端 Kubernetes 配置檔的路徑設為環境變數。

    然後，複製並貼上終端機中顯示的指令，以設定 KUBECONFIG 環境變數。

2. 移除叢集角色連結。請執行下列指令：

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. 移除服務帳戶。請執行下列指令：

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. 移除 `daemonset`。請執行下列指令：

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. 移除密碼。請執行下列指令：

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## 在 Linux 上移除 Sysdig 代理程式
{: #remove_agent_linux}

請完成下列步驟，在 Linux 上移除 Sysdig 代理程式：

* 若要從 **Debian 和 Ubuntu Linux 發行套件**中解除安裝代理程式，請從終端機以 **sudo** 使用者身分執行下列指令：

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* 若要從 **RHEL、CentOS 和 Fedora Linux 發行套件**中解除安裝代理程式，請從終端機以 **sudo** 使用者身分執行下列指令：

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


