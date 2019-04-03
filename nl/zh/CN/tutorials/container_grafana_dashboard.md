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


# 创建 Grafana 仪表板以监视 Kubernetes 集群
{: #container_grafana_dashboard}


使用本教程可了解如何在 {{site.data.keyword.monitoringlong}} 服务中创建 Grafana 仪表板，以监视集群的性能。
{:shortdesc}


## 目标
{: #cgd_objectives}

了解如何对部署在 Kubernetes 集群中的应用程序进行容器度量值的搜索和分析：

1. 启动 Grafana 并设置可以在其中查看集群度量值的 {{site.data.keyword.monitoringshort}} 域。
2. 创建 Grafana 仪表板并定义度量值来监视容器的 CPU 使用率。


## 假定
{: #cgd_assumptions}

教程假定：

* 集群在美国南部区域中可用。 
* 您的用户标识采用了具有 {{site.data.keyword.monitoringshort}} 服务的**查看者**许可权的 IAM 策略。

要完成本教程，您必须完成[在 Grafana 中分析部署在 Kubernetes 集群中的应用程序的度量值](/docs/services/cloud-monitoring/tutorials?topic=cloud-monitoring-container_service_metrics#container_service_metrics)教程，或者已供应集群并至少部署了 1 个应用程序。



## 步骤 1：启动 Grafana
{: #cgd_step1}

通过浏览器启动 Grafana，并设置可以在其中查看集群度量值的 {{site.data.keyword.monitoringshort}} 域。

要分析集群的度量值，您必须在创建集群的云公共区域中访问 Grafana。有关更多信息，请参阅[通过 Web 浏览器导航至 Grafana 仪表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。

1. 通过浏览器启动 Grafana。 

    输入创建集群的区域的 {{site.data.keyword.monitoringshort}} 服务 URL。 
    
    要获取每个区域的 URL，请参阅 [Monitoring 服务的 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)。

    例如，对于美国南部区域，请启动：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

2. 将 {{site.data.keyword.monitoringshort}} 域设置为**帐户**。

    在 Grafana 中，选择您的标识。接着，检查您是否位于正确的帐户中，然后选择 `Domain = account`。


## 步骤 2：创建 Grafana 仪表板
{: #cgd_step2}

要创建新仪表板，请完成以下步骤：

1. 选择侧菜单栏切换 ![Grafana 侧菜单栏](images/grafana_settings.gif "Grafana 侧菜单栏")。
2. 选择**仪表板**。
3. 单击**新建**。

这将打开仪表板。仪表板包含一个空行，可随时用于配置。

![Grafana 仪表板](images/grafana4_f1.gif "Grafana 仪表板")

在 Grafana 中，通过添加行可将仪表板分成不同部分。一行可将一个或多个面板分组在一起。在一行内，面板是最小的可视化单元，可以配置为显示度量值的数据，例如可以选择图形面板或表面板。您可以通过拖放面板在仪表板中重新排列面板。面板显示的数据可通过查询进行配置。可以在一个面板中定义一个或多个查询。每个查询表示一组不同的数据。还可以设置面板的时间范围。通常，时间范围由*仪表板*时间选取器进行设置。

## 步骤 3：向仪表板添加图形以监视度量值
{: #cgd_step3}

请完成以下步骤：

1. 选择**图形**。

2. 单击图形标题，然后选择**编辑**。

    这将打开*度量值*选项卡。在此可以看到缺省数据源。


![包含配置选项卡的图形面板](images/grafana4_f2.gif "包含配置选项卡的图形面板")


## 步骤 4：定义度量值查询
{: #cgd_step4}

定义用于过滤图形中所显示数据的查询。此查询监视容器的所有核心中 CPU 时间的纳秒数。

有关查询格式的信息，请参阅[为容器收集的 CPU 度量值的查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers)。
 
在*度量值*选项卡中，选择**添加查询**。<br>这将添加一个查询条目。每个查询都会使用一个字母进行标记。 

![新建查询条目](images/grafana4_query_f1.gif "新建查询条目") 
	
要定义查询，请完成以下步骤：
        
1. 单击**选择度量值**以指定源，然后选择 `ibmcloud`。
    
2. 单击**选择度量值**以指定云类型，然后选择 `public`。
    
3. 单击**选择度量值**以指定服务名称，然后选择 `containers-kubernetes`。
	
4. 单击**选择度量值**以指定区域，然后选择运行集群的区域。例如，`us-south`。
    
5. 单击**选择度量值**以指定集群名称，然后选择运行容器的集群的名称。
		
6. 单击**选择度量值**以指定度量源。选择**容器**。
		
7. 单击**选择度量值**以指定名称空间。然后，输入集群中与容器关联的名称空间的名称。
		
8. 单击**选择度量值**以指定 pod 名称。
	
9. 单击**选择度量值**以指定要监视的容器的容器名称。
	
10. 单击**选择度量值**以指定度量值类型，然后单击**选择度量值**以指定度量值子类型。
	
    例如，要监视容器的所有核心中 CPU 时间的纳秒数，对于类型，请选择 **cpu**，对于子类型，请选择 **usage**。
		
	有关 CPU 度量值的列表，请参阅[容器的 CPU 度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers)。
    
11. 单击加号图像 ![“添加”图标](images/grafana_plus_image.gif "加号图像")，然后选择函数。可以添加函数来对可用于度量值的数据执行变换、组合和计算。

    例如，可以添加 **alias(newName)** 函数来为度量值添加别名。此别名用于在图形中所显示的图注中显示字符串，而不显示度量值名称。

    要为度量值添加别名，请完成以下步骤：

    1. 单击加号。
    2. 选择**特殊**。
        3 选择**别名**。
    4. 输入字符串，例如 `My sample metric`。

## 步骤 5：保存仪表板
{: #cgd_step5}

保存仪表板以供将来复用。

1. 单击保存仪表板图像 ![保存仪表板图像](images/grafana_save_image.gif "保存仪表板图像")。

    ![保存仪表板](images/grafana_save_dashboard.gif "保存仪表板")

2. 输入仪表板的名称。
3. 单击**保存**。



## 后续步骤
{: #cgd_next_steps}

为度量值定义警报。有关更多信息，请参阅[配置警报](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)。
