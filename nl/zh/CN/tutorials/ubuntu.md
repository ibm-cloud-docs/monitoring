---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# 分析 Ubuntu 主机的度量值
{: #ubuntu}

使用本教程可了解如何配置 Ubuntu 主机以将度量值转发到 {{site.data.keyword.cloud_notm}} 中的 {{site.data.keyword.mon_full_notm}} 服务。
{:shortdesc}

要将 Ubuntu 服务器配置为转发度量值，必须安装 Sysdig 代理程序。该代理程序使用访问密钥（令牌）向 {{site.data.keyword.mon_full_notm}} 实例进行认证。Sysdig 代理程序充当数据收集器。它会自动收集度量值。

可以通过 Sysdig 的基于 Web 的用户界面来查看度量值。

![{{site.data.keyword.cloud_notm}} 上的组件概览图](../images/ubuntu.png "{{site.data.keyword.cloud_notm}} 上的组件概览图")



## 开始之前
{: #ubuntu_prereqs}

在美国南部区域中工作。 

请阅读有关 {{site.data.keyword.mon_full_notm}} 的信息。有关更多信息，请参阅[关于](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)。

使用作为 {{site.data.keyword.cloud_notm}} 帐户的成员或所有者的用户标识。要获取 {{site.data.keyword.cloud_notm}} 用户标识，请转至：[注册 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window}。

您的 {{site.data.keyword.IBM_notm}} 标识必须分配有针对以下每个资源的 IAM 策略： 

|资源|访问策略的作用域|角色|区域|信息|
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
|资源组 **Default**|资源组|查看者|us-south|要允许用户查看 Default 资源组中的服务实例，此策略是必需的。|
|{{site.data.keyword.mon_full_notm}} 服务|资源组|编辑者|us-south|要允许用户在 Default 资源组中供应和管理 {{site.data.keyword.mon_full_notm}} 服务，此策略是必需的。|
{: caption="表 1. 完成教程所需的 IAM 策略的列表" caption-side="top"} 

安装 {{site.data.keyword.cloud_notm}} CLI。有关更多信息，请参阅[安装 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。


## 步骤 1：供应 {{site.data.keyword.mon_full_notm}} 实例
{: #ubuntu_step1}

要通过 {{site.data.keyword.cloud_notm}} UI 供应 {{site.data.keyword.mon_full_notm}} 的实例，请完成以下步骤：

1. 登录到 {{site.data.keyword.cloud_notm}} 帐户。

    单击 [{{site.data.keyword.cloud_notm}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window} 以启动 {{site.data.keyword.cloud_notm}}“仪表板”。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}} UI 将打开。

2. 单击**目录**。这将打开 {{site.data.keyword.cloud_notm}} 中可用的服务的列表。

3. 要过滤显示的服务列表，请选择 **Developer Tools** 类别。

4. 单击 **{{site.data.keyword.mon_full_notm}}** 磁贴。将打开*可观察性*仪表板。

5. 选择**创建实例**。 

6. 输入服务实例的名称。

7. 选择 **Default** 资源组。 

    缺省情况下，已设置 **Default** 资源组。

8. 选择**轻量**服务套餐。 

    缺省情况下，已设置**轻量**套餐。

    有关其他服务套餐的更多信息，请参阅[价格套餐](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。

9. 要在您登录到的 {{site.data.keyword.cloud_notm}} 资源组中供应 {{site.data.keyword.mon_full_notm}} 服务，请单击**创建**。

供应实例后，将打开*可观察性*仪表板。 


**注：**要通过 CLI 来供应实例，请参阅[通过 {{site.data.keyword.cloud_notm}} CLI 供应实例](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)。


## 步骤 2：配置 Ubuntu 服务器以将度量值发送到实例
{: #ubuntu_step2}

要配置 Ubuntu 服务器以将度量值发送到 {{site.data.keyword.mon_full_notm}} 实例，必须安装 Sysdig 代理程序。 

通过命令行完成以下步骤：

1. 打开终端。然后，登录到 {{site.data.keyword.cloud_notm}}。运行以下命令并遵循提示进行操作：

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    选择已供应 {{site.data.keyword.mon_full_notm}} 实例的帐户。

2. 获取 Sysdig 访问密钥。有关更多信息，请参阅[通过 {{site.data.keyword.cloud_notm}} UI 获取访问密钥](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

3. 获取采集 URL。有关更多信息，请参阅 [Sysdig 收集器端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

4. 部署 Sysdig 代理程序。运行以下命令：

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是实例的采集密钥。

    * COLLECTOR_ENDPOINT 是监视实例在其中可用的区域的采集 URL。

    * TAG_DATA 是格式为 *TAG_NAME:TAG_VALUE* 的逗号分隔标记。可以将一个或多个标记与 Sysdig 代理程序相关联。例如：*role:serviceX,location:us-south*。稍后，可以使用这些标记来识别来自运行代理程序的环境中的度量值。

    * 将 **sysdig_capture_enabled** 设置为 *false* 以禁用 Sysdig 捕获功能。缺省情况下，此值设置为 *true*。有关更多信息，请参阅[使用捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

如果 Sysdig 代理程序未能正确安装，请手动安装内核头文件。选择分发版，并对该分发版运行该命令。然后，重试部署 Sysdig 代理程序。

* **对于 Debian 和 Ubuntu Linux 分发版**，请运行以下命令：

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **对于 RHEL、CentOS 和 Fedora Linux 分发版**，请运行以下命令：

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## 步骤 3：启动 Sysdig Web UI
{: #ubuntu_step3}

要启动 Web UI，请完成以下步骤：

1. 登录到 {{site.data.keyword.cloud_notm}} 帐户。

    单击 [{{site.data.keyword.cloud_notm}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window} 以启动 {{site.data.keyword.cloud_notm}}“仪表板”。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}}“仪表板”将打开。

2. 在导航菜单中，选择**可观察性**。 

3. 选择**监视**。 

    这将显示 {{site.data.keyword.cloud_notm}} 上可用的实例的列表。

4. 选择实例。然后，单击**查看 Sysdig**。

如果已成功配置 Sysdig 代理程序，那么会打开*探索*视图。

但是，如果 Sysdig 代理程序未成功安装，指向错误的采集端点，或者访问密钥不正确，那么打开的页面会通知您下一步要执行的操作。

每个浏览器只能打开一个 Web UI 会话。
{: tip}


## 步骤 4：监视 Ubuntu 服务器
{: #ubuntu_step4}

可以在通过 Web UI 提供的**探索**视图中监视 Ubuntu 服务器。此视图是对基础架构进行故障诊断和监视的起点。它是用户的 Web UI 的缺省主页。

在*主机和容器*部分中，可以找到 Ubuntu 服务器的条目。单击**主机和容器** ![主机和容器](../images/switch_hosts.png) 以切换数据源。然后，选择 Ubuntu 服务器。显示的数据对应于所选择的 Ubuntu 服务器。

例如，要配置列的颜色编码，请完成以下步骤：

1. 选择列。将鼠标悬停在该列的标题上。然后，选择“画笔”图标。
2. 切换栏以启用颜色编码。
3. 设置不同阈值的值。



## 后续步骤
{: #ubuntu_next_steps}

创建定制仪表板。有关更多信息，请参阅[使用仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)。

您还可以了解有关警报的信息。有关更多信息，请参阅[使用警报](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)。 






