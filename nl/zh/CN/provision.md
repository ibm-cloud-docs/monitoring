---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# 供应实例
{: #provision}

必须先在 {{site.data.keyword.Bluemix}} 中供应 Sysdig 服务的实例，然后才能使用 Sysdig 来监视和管理度量值。
{:shortdesc}

要在公共云区域中供应 Sysdig 实例，必须选择与实例关联的服务套餐、收集其中度量值的区域，以及用于确定可以监视的度量值数及其保留期的套餐。



## 通过目录供应 Sysdig 实例
{: #provision_ui}

要通过 {{site.data.keyword.cloud_notm}}“目录”供应 Sysdig 实例，请完成以下步骤：

1. 登录到 {{site.data.keyword.cloud_notm}} 帐户。

    单击 [{{site.data.keyword.cloud_notm}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window} 以启动 {{site.data.keyword.cloud_notm}}“仪表板”。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}} UI 将打开。

2. 单击**目录**。这将打开 {{site.data.keyword.cloud_notm}} 上可用的服务的列表。

3. 要过滤显示的服务列表，请选择 **Developer Tools** 类别。

4. 单击 **{{site.data.keyword.mon_full_notm}}** 磁贴。将打开*可观察性*仪表板。

5. 选择**创建实例**。 

6. 选择服务套餐。缺省情况下，已设置**试用**套餐。

    有关服务套餐的更多信息，请参阅[服务套餐](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。

7. 选择资源组。缺省情况下，已设置 **Default** 资源组。

8. 单击**创建**。

供应实例后， 

* 将打开*可观察性*仪表板。 
* 将自动创建服务标识。可以使用此服务标识来获取实例的 Sysdig 访问密钥。

接下来，通过添加 Sysdig 代理程序来配置度量源。此代理程序负责收集度量值并将其转发到 Sysdig。 



## 通过 CLI 供应 Sysdig 实例
{: #provision_cli}

要通过命令行供应 Sysdig 的实例，请完成以下步骤：

1. [先决条件] 安装 {{site.data.keyword.cloud_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

   如果 CLI 已安装，请继续执行下一步。

2. 登录到 {{site.data.keyword.cloud_notm}} 中要供应实例的区域。运行以下命令：[`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. 设置要在其中供应实例的资源组。运行以下命令：[`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    缺省情况下，已设置 `default` 资源组。

4. 创建 Sysdig 实例。运行 [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) 命令：

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    其中

    * NAME 是 Sysdig 实例的名称
    
    * *sysdig-monitor* 是 {{site.data.keyword.cloud_notm}} 中 {{site.data.keyword.mon_full_notm}} 服务的名称
    
    * SERVICE_PLAN_NAME 是套餐的类型。有效值为：*lite* 和 *graduated-tier*
    
    * LOCATION 是在其中创建实例的区域

    例如，要为实例供应付费套餐，请运行以下命令：

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

