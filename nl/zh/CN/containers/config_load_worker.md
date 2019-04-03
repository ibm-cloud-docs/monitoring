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



# 为 Grafana 中的工作程序配置负载度量值
{: #config_load_worker}

在 {{site.data.keyword.Bluemix}} 中，会自动收集工作程序的所选负载度量值。要通过 {{site.data.keyword.monitoringlong}} 监视这些度量值，必须定义 Grafana 查询。
{:shortdesc}

有关自动收集的负载度量值的列表，请参阅[工作程序的负载度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#load_metrics_workers)。


## 步骤 1：收集要监视的工作程序的数据
{: #step16}

获取要监视的工作程序的以下信息：

* **区域** - 运行集群的区域。
* **集群名称** - 运行容器的集群的名称。 
* **工作程序名称** - 要监视的工作程序的名称。 

确定度量值是会转发到空间域还是帐户域。

要确定集群将度量值转发到的位置，请运行以下命令：

```
$ ibmcloud cs cluster-get ClusterName --json
```
{: codeblock}

其中，*ClusterName* 是集群的名称。

在输出中，以下字段提供有关度量值转发位置的信息：

* **logOrg** 定义 CF 组织的标识。
* **logOrgName** 定义 CF 组织的名称。
* **logSpace** 定义 CF 空间的标识。
* **logSpaceName** 定义 CF 空间的名称。

如果这些字段为空，那么度量值会转发到帐户域。如果字段设置了 CF 组织和 CF 空间，那么会将度量值转发到与此空间关联的空间域。

## 步骤 2：启动 Grafana
{: #step25}

通过浏览器启动 Grafana。有关更多信息，请参阅[通过 Web 浏览器导航至 Grafana 仪表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。

确保在 Grafana 中登录到运行集群的帐户。 

1. 通过浏览器启动 Grafana。 

    输入创建集群的区域的 {{site.data.keyword.monitoringshort}} 服务 URL。 
    
    要获取每个区域的 URL，请参阅 [Monitoring 服务的 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)。

    例如，对于美国南部区域，请启动：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

2. 设置可以在其中查看集群度量值的 {{site.data.keyword.monitoringshort}} 域。

    在 Grafana 中，选择您的标识。接着，检查您是否位于正确的帐户中，然后选择一个域。

    关联有 CF 空间的集群会将度量值转发到空间度量值域。选择 `Domain = space`，然后选择与集群关联的组织和空间。

    在帐户级别创建的集群会将度量值转发到帐户度量值域。选择 `Domain = account`。



## 步骤 3：在 Grafana 中定义针对 CPU 度量值的查询
{: #step34}

要创建 Grafana 仪表板并定义查询来监视工作程序的 CPU 使用率，请完成以下步骤：

1. 创建新的仪表板。

    * 选择侧菜单栏切换 ![Grafana 侧菜单栏](images/grafana_settings.gif "Grafana 侧菜单栏")。
    * 选择**仪表板**。
    * 单击**新建**。

    这将打开仪表板。仪表板包含一个空行，可随时用于配置。

2. 添加*图形*面板以监视 pod 的 CPU 度量值。

    1. 选择**图形**。

    2. 单击图形标题，然后选择**编辑**。

        这将打开*度量值*选项卡。在此可以看到缺省数据源。

3. 定义用于过滤图形中所显示数据的查询。 

    有关查询格式的信息，请参阅[为工作程序收集的负载度量值的查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#load_workers)。

    在*度量值*选项卡中，选择**添加查询**。<br>这将添加一个查询条目。每个查询都会使用一个字母进行标记。
	
	要定义查询，请完成以下步骤：

    1. 单击**选择度量值**以指定源，然后选择 `ibmcloud`。
    
    2. 单击**选择度量值**以指定云类型，然后选择 `public`。
    
    3. 单击**选择度量值**以指定服务名称，然后选择 `containers-kubernetes`。
	
    4. 单击**选择度量值**以指定区域，然后选择运行集群的区域。例如，`us-south`。
    
    5. 单击**选择度量值**以指定集群名称，然后选择运行容器的集群的名称。
		
	6. 单击**选择度量值**以指定要监视的工作程序的工作程序名称。
	
	7. 单击**选择度量值**以指定度量值类型，然后单击**选择度量值**以指定度量值子类型。
	
	    有关 CPU 度量值的列表，请参阅[工作程序的 CPU 度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#load_metrics_workers)。
	
	10. 单击加号图像 ![“添加”图标](images/grafana_plus_image.gif "加号图像")，然后选择函数。可以添加函数来对可用于度量值的数据执行变换、组合和计算。

        例如，可以添加 **alias(newName)** 函数来为度量值添加别名。此别名用于在图形中所显示的图注中显示字符串，而不显示度量值名称。

        要为度量值添加别名，请完成以下步骤：

        1. 单击加号。
        2. 选择**特殊**。
        3 选择**别名**。
        4. 输入字符串，例如 `My sample metric`。

4. 保存仪表板以供将来复用。

    1. 单击保存仪表板图像 ![保存仪表板图像](images/grafana_save_dashboard.gif "保存仪表板图像")。
    2. 输入仪表板的名称。
    3. 单击**保存**。

