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

# 除去 Sysdig 代理程序
{: #remove_agent}

删除 {{site.data.keyword.mon_full_notm}} 实例时，或者如果要停止从源收集度量值，必须卸载 Sysdig 代理程序。
{:shortdesc}


## 从 Kubernetes 集群中除去 Sysdig 代理程序
{: #remove_agent_kube}

要从 Kubernetes 集群中除去 Sysdig 代理程序，请完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

2. 除去集群角色绑定。运行以下命令：

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. 除去服务帐户。运行以下命令：

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. 除去`守护程序集`。运行以下命令：

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. 除去私钥。运行以下命令：

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## 在 Linux 上除去 Sysdig 代理程序
{: #remove_agent_linux}

要在 Linux 上除去 Sysdig 代理程序，请完成以下步骤：

* 要从 **Debian 和 Ubuntu Linux 分发版**中卸载代理程序，请在终端中以 **sudo** 用户身份运行以下命令：

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* 要从 **RHEL、CentOS 和 Fedora Linux 分发版**中卸载代理程序，请在终端中以 **sudo** 用户身份运行以下命令：

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


