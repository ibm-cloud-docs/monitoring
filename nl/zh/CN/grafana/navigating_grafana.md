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


# 导航至 Grafana 仪表板
{:#navigating_grafana}

在 {{site.data.keyword.Bluemix}} 中，可以使用 Grafana（一种开放式源代码分析和可视化平台）通过各种图形（例如，图表和表）来对度量值进行监视、搜索、分析和可视化表示。 可使用 Grafana 执行高级分析任务。
{:shortdesc}

您可以使用以下任何一种方法来启动 Grafana：

* 在 {{site.data.keyword.Bluemix_notm}} 中

    可以在特定 Docker 容器的上下文中，使用 Grafana 显示该 Docker 容器的度量值。 此功能仅适用于在 {{site.data.keyword.Bluemix_notm}} 管理的基础架构中部署的容器。 
    
    有关更多信息，请参阅[从 {{site.data.keyword.Bluemix_notm}} 仪表板导航至 Grafana 仪表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_bluemix)。

* 通过浏览器链接直接打开

    您可以启动 Grafana，以便您看到的数据从所提供 {{site.data.keyword.Bluemix_notm}} 空间内的服务聚集日志。
    
    有关更多信息，请参阅[通过 Web 浏览器导航至 Grafana 仪表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。
    
有关 Grafana 的更多信息，请参阅 [Grafana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://docs.grafana.org/guides/getting_started/){: new_window}。


##  通过 IBM Cloud 仪表板导航至 Grafana 仪表板
{: #launch_grafana_from_bluemix}

**注：**此功能仅适用于在 {{site.data.keyword.Bluemix_notm}} 管理的基础架构中部署的容器。 

用于过滤 Grafana 中所显示数据的查询会检索从中启动 Grafana 的 {{site.data.keyword.Bluemix_notm}} 容器的数据。 

要在 Grafana 中查看 Docker 容器的度量值，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后在*仪表板*中单击该容器。 
    
2. 在导航栏中，单击**监视和日志**。 这将打开“监视”选项卡。 
    
3. 单击**高级视图**。 这将打开 **Grafana** 仪表板。


##  通过 Web 浏览器导航至 Grafana 仪表板
{: #launch_grafana_from_browser}

用于过滤 Grafana 中所显示数据的查询会检索 {{site.data.keyword.Bluemix_notm}} 组织中空间的数据。 Grafana 显示的度量值信息包括在您登录到的 {{site.data.keyword.Bluemix_notm}} 组织空间内部署的所有资源的记录。

要通过浏览器启动 Grafana，请完成以下步骤：

1. 打开 Web 浏览器。 
2. 输入要监视度量值的区域的 URL。 

    下表列出了每个区域的 URL：
	<table>
      <caption>用于在不同区域启动 Grafana 的 URL</caption>
      <tr>
        <th>区域</th>
	    <th>端点</th>
      </tr>
      <tr>
        <td>德国</td>
	    <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
      </tr>
      <tr>
        <td>英国</td>
	    <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
      </tr>
      <tr>
        <td>美国南部</td>
    	<td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
      </tr>
      <tr>
        <td>英国</td>
	    <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
      </tr>
      
    </table>
	
2. 选择 **Grafana**。
     

