---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# 除去实例
{: #remove}

您可以通过 {{site.data.keyword.Bluemix}} UI 或命令行来除去 {{site.data.keyword.mon_full_notm}} 服务的实例。
{:shortdesc}

从 {{site.data.keyword.cloud_notm}} 中除去实例时，请考虑要整理的以下信息：

1. 记下将度量值转发到要除去的 {{site.data.keyword.mon_full_notm}} 实例的源的列表。必须从每个源中除去 Sysdig 代理程序。
2. 除去向用户授予的使用该实例的许可权。 

    如果是使用访问组来管理访问实例的许可权，那么必须除去该访问组。

    如果是使用访问组来管理访问不同服务实例的许可权，那么必须除去针对要除去的实例授予许可权的策略。
    
    如果已向用户授予了单个策略，那么必须收集有权访问该实例的每个用户的信息。然后逐一除去与要删除的实例相关的策略。


接下来，从 {{site.data.keyword.cloud_notm}}“仪表板”中删除该实例。


## 通过 {{site.data.keyword.cloud_notm}} UI 除去实例
{: #remove_ui}

要使用 {{site.data.keyword.cloud_notm}} UI 来除去 {{site.data.keyword.mon_full_notm}} 的实例，请完成以下步骤：

1. [登录到 {{site.data.keyword.cloud_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window}。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}} UI 将打开。

2. 选择**可观察性**。 

3. 选择**监视**。这将显示实例的列表。

4. 选择要删除的实例。

5. 从*操作*菜单中，选择**除去**。


## 通过 CLI 除去实例
{: #remove_cli}

要通过命令行除去 {{site.data.keyword.mon_full_notm}} 的实例，请完成以下步骤：

1. [先决条件] 安装 {{site.data.keyword.cloud_notm}} CLI。如果 CLI 已安装，请继续执行下一步。

   有关更多信息，请参阅[安装 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

2. 登录到 {{site.data.keyword.cloud_notm}} 中要供应实例的区域。运行以下命令：[`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. 设置在其中供应实例的资源组。运行以下命令：[`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    缺省情况下，已设置 `default` 资源组。

4. 除去实例。运行 [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete) 命令：

    ```
    ibmcloud resource service-instance-delete NAME
    ```
    {: codeblock}

    其中 NAME 是实例的名称

    例如，要除去实例，请运行以下命令：

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
