---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, metrics

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

# 使用度量值
{: #metrics}

在 {{site.data.keyword.Bluemix}} 中供应 {{site.data.keyword.mon_full_notm}} 服务的实例，并为度量源配置了 Sysdig 代理程序后，可以通过 {{site.data.keyword.mon_full_notm}} Web UI 来查看、监视和管理度量值。使用度量值可通过统计方式分析具有数字值的数据。
{:shortdesc}


**度量值是一种定量度量，具有一个或多个标签用于定义其特征。**

度量值由时间序列表示。 

时间序列是一段时间内的一组数字数据点。 

度量值分类为两个组： 

* 缺省度量值 
* 定制度量值


## 标签
{: #metrics_labels}

**标签定义度量值的特征。**

标签分类为基础架构标签和度量值描述符标签。每个度量值都有一组预定义的标签。对于定制度量值，可以配置更多标签。 

可以使用标签来标识和区分度量值的特征，例如：
* 可以将基础架构对象分组为逻辑层次结构。 
* 可以过滤掉数据。 
* 可以将聚集的数据拆分成分段。 


## 缺省度量值 
{: #metrics_default}

**有关系统、编排器和网络基础架构的缺省度量值报告。**

监视服务会自动向每个度量值添加标签。


## 定制度量值
{: #metrics_custom}

**定制度量值根据基础架构类型以及受监视的应用程序而有所不同。一些示例包括 JMX、Prometheus 和 StatsD。**

这些度量值具有一组预定义的标签。可以添加其他定制标签。

监视服务会维护最近 14 天所报告数据的所有定制度量值和定制标签的索引。可以使用这些度量值来配置仪表板、作用域和警报。

请考虑以下有关监视服务如何管理索引条目的信息：
*  发生以下任一情况时，将自动从监视服务索引中除去度量值并将其标记为缺失：
    
    * 监视服务超过 14 天未收到某个度量值或标签的任何数据。
    
    * 某个度量值或标签从未报告过数据。

* 无法在度量值缺失或标签缺失的情况下配置新工件。 
* 从当前配置中删除缺失的度量值和标签之前，无法更新现有工件。
* 无法在数据查询和图表上使用缺失的度量值或缺失的标签。 
* 包含缺失度量值或缺失标签的现有工件不受影响。
* 收到缺失的度量值或标签的数据时，会将该度量值或标签添加回索引。



