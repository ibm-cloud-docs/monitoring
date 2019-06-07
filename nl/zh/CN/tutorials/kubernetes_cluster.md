---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-10"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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


# 分析在 Kubernetes 集群中部署的应用程序的度量值
{: #kubernetes_cluster}

使用本教程了解如何配置 {{site.data.keyword.containerlong}} 集群以将度量值转发到 {{site.data.keyword.mon_full}} 服务。
{:shortdesc}

要将集群配置为转发度量值，必须使用[守护程序集 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) 将 Sysdig 代理程序安装到 Kubernetes 集群中的每个工作程序节点上。Sysdig 代理程序使用访问密钥（令牌）向 {{site.data.keyword.mon_full_notm}} 实例进行认证。Sysdig 代理程序充当数据收集器。它会自动收集度量值，例如*工作程序节点 CPU* 和*工作程序节点内存*使用情况、
*进出容器的 HTTP 流量*以及若干基础架构组件的相关数据。此外，该代理程序还可以使用兼容 Prometheus 的提取器或 StatsD 外观来收集定制的应用程序度量值。 

可以通过 Sysdig 的基于 Web 的用户界面来查看度量值。

![{{site.data.keyword.cloud_notm}} 上的组件概览图](../images/kube.png "{{site.data.keyword.cloud_notm}} 上的组件概览图")

## 目标
{: #kubernetes_cluster_objectives}

在本教程中，您使用 {{site.data.keyword.containerlong}} 集群中的 Sysdig 配置度量值。尤其是：
*  供应 {{site.data.keyword.mon_full_notm}} 实例。
*  配置您集群中的 Sysdig 代理程序，以将度量值发送至 Sysdig。
*  使用 Sysdig Web UI 分析集群度量值。


## 开始之前
{: #kubernetes_cluster_prereqs}

1. 请阅读有关 {{site.data.keyword.mon_full_notm}} 的信息。有关更多信息，请参阅[关于](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)。

2. 使用作为 {{site.data.keyword.cloud_notm}} 帐户的成员或所有者的用户标识。要获取 {{site.data.keyword.cloud_notm}} 用户标识，请转至：[注册 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window}。

3. 安装 {{site.data.keyword.cloud_notm}} CLI 和 Kubernetes CLI 插件。有关更多信息，请参阅[安装 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

4. [创建集群](/docs/containers?topic=containers-clusters#clusters)或使用现有的 {{site.data.keyword.containerlong_notm}} 集群。
    *  集群必须运行 Kubernetes V1.10 或更高版本。
    *  集群不必位于**达拉斯**位置，但可以位于任何 [{{site.data.keyword.containerlong_notm}} 区域](/docs/containers/cs_regions.html#regions-and-zones)。

5. 确保您的用户标识分配有以下 {{site.data.keyword.iamlong}} 策略：

|资源|访问策略的作用域|角色|区域|信息|
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
|资源组 **Default**           |资源组|查看者|美国南部|要允许用户查看 Default 资源组中的服务实例，此策略是必需的。|
|{{site.data.keyword.mon_full_notm}} 服务|资源组|编辑者|美国南部|要允许用户在 Default 资源组中供应和管理 {{site.data.keyword.mon_full_notm}} 服务，此策略是必需的。|
|Kubernetes 集群实例|资源|编辑者|美国南部|要在 Kubernetes 集群中配置私钥和 Sysdig 代理程序，此策略是必需的。|
{: caption="表 1. 完成教程所需的 IAM 策略的列表" caption-side="top"}

有关 {{site.data.keyword.containerlong}} IAM 角色的更多信息，请参阅[用户访问许可权](/docs/containers?topic=containers-access_reference#access_reference)。



## 步骤 1. 供应 {{site.data.keyword.mon_full_notm}} 实例
{: #kubernetes_cluster_step1}

在本入门教程中，提供了在美国南部区域中供应 {{site.data.keyword.mon_full_notm}} 实例的指示信息。有关支持的区域的更多信息，请参阅
[区域](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints)。

要通过 {{site.data.keyword.cloud_notm}} UI 供应 {{site.data.keyword.mon_full_notm}} 的实例，请完成以下步骤：

1. [登录到 {{site.data.keyword.cloud_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window}。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}} UI 将打开。

2. 单击**目录**。这将打开 {{site.data.keyword.cloud_notm}} 中可用的服务的列表。

3. 要过滤显示的服务列表，请选择 **Developer Tools** 类别。

4. 单击 **{{site.data.keyword.mon_full_notm}}** 磁贴。将打开*可观察性*仪表板。

5. 选择**创建实例**。 

6. 输入服务实例的名称。

7. 选择 **Default** 资源组。 

    您可以在您有创建资源的许可权的任何资源组中供应实例。

    缺省情况下，已设置 **Default** 资源组。

8. 选择**试用**服务套餐。 

    缺省情况下，已设置**试用**套餐。

    有关其他服务套餐的更多信息，请参阅[价格套餐](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。

9. 单击**创建**。

    供应实例后，*可观察性*仪表板将打开并显示**监视**实例的详细信息。 


要通过 CLI 供应实例，请参阅[通过 {{site.data.keyword.cloud_notm}} CLI 供应实例](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)。
{: note}


## 步骤 2. 配置 Kubernetes 集群以将度量值发送到实例
{: #kubernetes_cluster_step2}

要配置 Kubernetes 集群以将度量值发送到 {{site.data.keyword.mon_full_notm}} 实例，必须在集群的每个节点上安装 Sysdig 代理程序 pod。Sysdig 代理程序是通过守护程序集安装的，用于确保每个工作程序节点上都有一个代理程序实例在运行。Sysdig 代理程序会从安装了该代理程序的 pod 收集度量值，并将这些数据转发到您的实例。

为了提供整套系统度量值，Sysdig 代理程序需要具有特权状态。
{: note}

要配置 Kubernetes 集群以将度量值转发到 {{site.data.keyword.mon_full_notm}} 实例，请通过命令行完成以下步骤：

1. 打开终端。然后，登录到 {{site.data.keyword.cloud_notm}}。运行以下命令并遵循提示进行操作：

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    选择集群可用的帐户。

2. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。复制并粘贴终端中显示的命令，以设置 `KUBECONFIG` 环境变量。

    每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，必须运行这些命令以将集群配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。{: tip}

3. 获取 Sysdig 访问密钥。有关更多信息，请参阅[通过 {{site.data.keyword.cloud_notm}} UI 获取访问密钥](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

4. 从 [Sysdig 收集器端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)获取采集 URL。

5. 部署 Sysdig 代理程序。运行以下命令：

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: pre}

    其中

    * **SYSDIG_ACCESS_KEY** 是先前检索的实例的采集密钥。

    * **COLLECTOR_ENDPOINT** 是先前所检索监视实例在其中可用的区域的采集 URL。

    * **TAG_DATA** 是格式为 *TAG_NAME:TAG_VALUE* 的逗号分隔标记。可以将一个或多个标记与 Sysdig 代理程序相关联。例如：*role:serviceX,location:us-south*。稍后，可以使用这些标记来识别来自运行代理程序的环境中的度量值。

    * 将 **sysdig_capture_enabled** 设置为 *false* 以禁用 Sysdig 捕获功能。缺省情况下，此值设置为 *true*。有关更多信息，请参阅[使用捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

6. 验证是否已成功创建 Sysdig 代理程序并验证其状态。运行以下命令：

    ```
    kubectl get pods -n ibm-observe
    ```
    {: codeblock}

    当您看到一个或多个 `sysdig-agent` pod 时，表明部署成功完成。`sysdig-agent` pod 的数量与集群中工作程序节点的数量相同。所有 pod 都必须处于`运行`状态。


## 步骤 3. 启动 Sysdig Web UI
{: #kubernetes_cluster_step3}

要通过 {{site.data.keyword.cloud_notm}} 控制台启动 Sysdig Web UI，请完成以下步骤。

每个浏览器只能打开一个 Web UI 会话。
{: imp}

1. [登录到 {{site.data.keyword.cloud_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window}。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}}“仪表板”将打开。

2. 从菜单 ![外部链接图标](../../../icons/icon_hamburger.svg "“菜单”图标") 中，选择**可观察性**。 

3. 选择**监视**。这将显示 {{site.data.keyword.cloud_notm}} 上可用的实例的列表。

4. 找到您的实例，并单击**查看 Sysdig**。

    * **首次使用**：因为您已经安装了 Sysdig 代理程序，您可以跳过安装向导，开始操作，完成登录。
    
    * **后续使用**：将打开**探索**视图。


如果 Sysdig 代理程序未成功安装，指向错误的采集端点，或者访问密钥不正确，那么打开的页面会通知您下一步要执行的操作。

例如，如果未成功安装 Sysdig 代理程序，那么无法跳过安装向导，您可能看到与以下内容类似的消息：
    
```
Waiting for the first node to connect... Go ahead and follow the instructions below.
```
{: screen}
    
您可以尝试以下操作：
*  验证您使用的是否为 `ingest` [端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)，而不是 Sysdig 端点。 
*  验证[访问密钥](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key)是否正确。
*  遵循任何其他指示信息，并重复本教程中的步骤。



## 步骤 4. 监视集群
{: #kubernetes_cluster_step4}

可以在通过 Sysdig UI 提供的**探索**视图中监视集群。此视图是缺省主页以及您对集群基础架构和资源进行故障诊断和监视的起点。

在*主机和容器*部分中，可以查看*探索表*，这是集群中正在将度量值转发到监视实例的工作程序的列表。每个工作程序条目表示该工作程序的一组相关基础架构对象。

单击**主机和容器** ![主机和容器](../images/switch_hosts.png) 以切换数据源。然后，选择工作程序。显示的数据对应于所选择的工作程序。如果单击**返回至探索表**，那么将显示*探索表*。 

**定制_探索表_**

您可以定制*探索表*。 

* 每列显示不同的度量值。 
* 可以分别配置每个度量值。 
* 您可以更改列的顺序。 

    请注意，更改现有列的顺序时，在您处于登录状态时，更改会在不同分组之间持久存储。如果添加或除去列，那么该更改会持久存储。 

* 还可以配置颜色，以突出显示值并提高可读性。 

例如，要配置列的颜色编码，请完成以下步骤：

1. 选择列。将鼠标悬停在该列的标题上。然后，选择“画笔”图标。
2. 切换栏以启用颜色编码。
3. 设置不同阈值的值。


**定制仪表板**

要查看有关某个特定工作程序节点的更多详细信息，请单击相应基础架构条目，然后表格中将打开*概述（按主机）*仪表板。您可以通过单击 ![切换仪表板](../images/switch_dashboards_1.png) 图标来探索其他仪表板和度量值。请注意，您只能选择与所选工作程序节点相关的度量值和仪表板。

要返回完整的_探索表_，请单击 **X（返回探索表）**按钮。


有关更多信息，请查看 [Sysdig 文档](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822446/The+Explore+Table)。



## 后续步骤
{: #kubernetes_cluster_next_steps}

创建定制仪表板。有关更多信息，请参阅[使用仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)。

您还可以了解有关警报的信息。有关更多信息，请参阅[使用警报](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)。 






