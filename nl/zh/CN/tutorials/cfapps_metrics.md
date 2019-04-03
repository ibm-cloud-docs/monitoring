---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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


# 在 Grafana 中分析 CF 应用程序的度量值
{: #cfapps_metrics}

使用本教程可了解如何使用 {{site.data.keyword.monitoringlong}} 服务来监视在 {{site.data.keyword.Bluemix_notm}} Public 中运行的 Cloud Foundry (CF) 应用程序的性能。
{:shortdesc}


## 目标
{: #objectives}

了解如何搜索和分析 CF 应用程序的度量值：

1. 部署 CF 应用程序。
2. 启动 Grafana 并设置可以在其中查看 CF 应用程序度量值的 {{site.data.keyword.monitoringshort}} 域。
3. 搜索和分析在 {{site.data.keyword.Bluemix_notm}} 空间中运行的 CF 应用程序的度量值。

本教程假定您在美国南部区域工作。


## 先决条件
{: #cfapps_prereqs}

1. 您是 {{site.data.keyword.Bluemix_notm}} 帐户的成员或所有者，并有权供应空间中的服务、部署 CF 应用程序以及通过 {{site.data.keyword.monitoringshort}} 服务查询 {{site.data.keyword.Bluemix_notm}} 中的度量值。

    {{site.data.keyword.Bluemix_notm}} 的用户标识必须具有在其中供应 {{site.data.keyword.monitoringshort}} 服务和 CF 应用程序的空间的 CF 角色。所需的角色是*开发者*。
    
    有关更多信息，请参阅[使用 IBM Cloud UI 授予用户 CF 角色](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#grant_permissions_ui_space)。

2. 在您有权在美国南部区域供应服务的空间内供应 {{site.data.keyword.monitoringshort}} 服务。

    有关更多信息，请参阅[供应 {{site.data.keyword.monitoringshort}} 服务](/docs/services/cloud-monitoring/how-to?topic=cloud-monitoring-provision#provision)。

## 步骤 1：授予用户使用 CF 应用程序和 {{site.data.keyword.monitoringshort}} 服务的许可权
{: #cfapps_step1}

要授予用户在空间中部署 CF 应用程序或查看空间域中度量值的许可权，您必须为该用户分配 CF 角色，该角色描述此用户可对空间中以及 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.monitoringshort}} 服务执行的操作。 

**注：**本教程假定您是帐户所有者或具有将角色添加到用户标识的许可权。如果您没有相应的许可权，请向所有者请求完成此步骤。

要授予用户完成本教程的许可权，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。


    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}}“仪表板”：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 从菜单栏中，单击**管理 > 帐户 > 用户**。 

    *用户*窗口将显示一个用户列表，其中包含当前选定帐户的电子邮件地址。
	
3. 从列表中找到您的用户名，然后从*操作*菜单中单击**管理用户**。

4. 选择 **Cloud Foundry 访问权**，然后选择**分配组织**。

5. 输入以下值： 

    <table>
      <caption>要选择的值列表</caption>
      <tr>
        <th>字段</th>
        <th>值</th>
      </tr>
      <tr>
        <td>组织</td>
        <td>MyOrg</td>
      </tr>
      <tr>
        <td>组织角色</td>
        <td>无组织角色</td>
      </tr>
      <tr>
        <td>区域</td>
        <td>美国南部</td>
      </tr>
      <tr>
        <td>空间</td>
        <td>dev</td>
      </tr>
      <tr>
        <td>空间角色</td>
        <td>开发者</td>
      </tr>
    </table>
	
6. 单击**保存角色**。
 

## 步骤 2：部署 CF 应用程序
{: #cfapps_step2}

在 {{site.data.keyword.Bluemix_notm}} 控制台中，完成以下步骤：

1. 单击 {{site.data.keyword.Bluemix_notm}} 工具栏中的**目录**。

2. 单击 **Cloud Foundry 应用程序 > Liberty for Java**。 

3. 输入以下信息：

    * **应用程序名称**：应用程序的名称。必须唯一。
    * **区域**：选择美国南部。
    * **组织**：选择已供应 {{site.data.keyword.monitoringshort}} 服务的组织。
    * **空间**：选择已供应 {{site.data.keyword.monitoringshort}} 服务的空间。

3. 单击**创建**。

CF 应用程序运行后，系统会立即收集度量值并将其转发到 {{site.data.keyword.monitoringshort}} 服务。

## 步骤 3：启动 Grafana 并设置度量值域
{: #cfapps_step3}

通过浏览器启动 Grafana，并设置可以在其中查看 CF 应用程序度量值的 {{site.data.keyword.monitoringshort}} 域。

1. 通过浏览器启动 Grafana。 

    输入供应 {{site.data.keyword.monitoringshort}} 服务的区域的 {{site.data.keyword.monitoringshort}} 服务 URL。
    
    要获取每个区域的 URL，请参阅 [Monitoring 服务的 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)。

    例如，对于美国南部区域，请启动：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

2. 设置可以在其中查看集群度量值的 {{site.data.keyword.monitoringshort}} 域。

    在 Grafana 中，选择您的标识。接着，检查您是否位于正确的帐户中，然后选择 `Domain = space`。

    验证组织名称和空间名称是否与部署了 CF 应用程序并供应了 {{site.data.keyword.monitoringshort}} 服务的组织和空间相对应。


## 步骤 4：创建 Grafana 仪表板来监视度量值
{: #cfapps_step4}


要在 Grafana 中创建新仪表板，请完成以下步骤：

1. 选择侧菜单栏切换 ![Grafana 侧菜单栏](images/grafana_settings.gif "Grafana 侧菜单栏")。
2. 选择**仪表板**。
3. 单击**新建**。

这将打开仪表板。仪表板包含一个空行，可随时用于配置。

![Grafana 仪表板](images/grafana4_f1.gif "Grafana 仪表板")

在 Grafana 中，通过添加行可将仪表板分成不同部分。一行可将一个或多个面板分组在一起。在一行内，面板是最小的可视化单元，可以配置为显示度量值的数据，例如可以选择图形面板或表面板。您可以通过拖放面板在仪表板中重新排列面板。面板显示的数据可通过查询进行配置。可以在一个面板中定义一个或多个查询。每个查询表示一组不同的数据。还可以设置面板的时间范围。通常，时间范围由*仪表板*时间选取器进行设置。

定义用于过滤图形中所显示数据的查询。此查询监视趋近于容器限制的 CPU 利用率的百分比。

有关查询格式的信息，请参阅 [Grafana 的 CF 应用程序查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-cfapps_metrics_format#cfapps_metrics_format)。
    
1. 添加*图形*面板以针对容器监视所有核心中 CPU 时间的纳秒数。
    
    1. 选择**图形**。
    
    2. 单击图形标题，然后选择**编辑**。
    
        这将打开*度量值*选项卡。在此可以看到缺省数据源。
    
        ![包含配置选项卡的图形面板](images/grafana4_f2.gif "包含配置选项卡的图形面板")
    
2. 定义用于过滤图形中所显示数据的查询。 
    
    在*度量值*选项卡中，选择**添加查询**。<br>这将添加一个查询条目。每个查询都会使用一个字母进行标记。
    
    ![新建查询条目](images/grafana4_query_f1.gif "新建查询条目")
        
    1. 单击**选择度量值**，然后选择源：`ibmcloud`。
    
    2. 单击**选择度量值**，然后选择云类型：`public`。
    
    3. 单击**选择度量值**，然后选择 `cloud-foundry`。
    
    4. 单击**选择度量值**，然后选择您在其中工作的区域，例如 `us-south` 表示美国南部区域。
    
    5. 单击**选择度量值**，然后选择 CF 应用程序名称，例如 `logtester`。
    
    6. 单击**选择度量值**，然后选择 CF 应用程序实例索引，例如 `0`。

    7. 单击**选择度量值**，然后选择 `container`。
    
    9. 单击**选择度量值**，然后选择度量值。要监视容器的 *CPU 使用率百分比*，请选择 `cpu-utilization`。

    10. 单击加号图像 ![“添加”图标](images/grafana_plus_image.gif "加号图像")，然后选择函数。可以添加函数来对可用于度量值的数据执行变换、组合和计算。
        
        例如，可以添加 **alias(newName)** 函数来为度量值添加别名。此别名用于在图形中所显示的图注中显示字符串，而不显示度量值名称。
        
        要为度量值添加别名，请完成以下步骤：
        
        1. 单击加号。
        2. 选择**特殊**。
        3 选择**别名**。
        4. 输入字符串，例如 `My sample metric`。
        

## 步骤 5：保存仪表板
{: #cfapps_step5}

保存仪表板以供将来复用。

1. 单击保存仪表板图像 ![保存仪表板图像](images/grafana_save_image.gif "保存仪表板图像")。

    ![保存仪表板](images/grafana_save_dashboard.gif "保存仪表板")

2. 输入仪表板的名称。
3. 单击**保存**。


## 后续步骤
{: #cfapps_next_steps}

为度量值定义警报。有关更多信息，请参阅[配置警报](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)。
