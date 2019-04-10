---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, pricing

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


# 定价
{: #pricing_plans}

有不同的价格套餐可用于 {{site.data.keyword.mon_full_notm}} 实例。
{:shortdesc}
 

|套餐|层|数据收集|
|------------------|--------------|------------------|
|`试用`|              |收集每个节点最多 20 个容器的数据，或每个节点 200 个定制度量值的数据，但仅支持使用 30 天。|
|`累进层`|`基本`|收集每个节点最多 20 个容器的数据，或每个节点 200 个定制度量值的数据。|
|`累进层`|`专业`|收集每个节点最多 50 个容器的数据，或每个节点 500 个定制度量值的数据。|
|`累进层`|`高级`|收集每个节点最多 110 个容器的数据，或每个节点 1000 个定制度量值的数据。|
{: caption="表 1. 服务套餐列表" caption-side="top"} 


**注：**节点可以是主机、容器、虚拟机、裸机或安装 Sysdig 代理程序的任何度量源。

每个节点的容器数或度量值数在一段时间内超过累进层套餐的阈值限制时，会应用自动层检测。如果计费使用量通知配置中启用了以下警报，那么将触发警报通知：**[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

通过使用 [IBM Cloud 支持 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window} 开具凭单，可以为超过*高级累进层付费价格套餐*上限的任何内容，请求**定制价格报价**。
{: tip}

数据会根据所有套餐中的标准准则进行收集和保留。有关更多信息，请参阅[数据收集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection)和[数据保留](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention)。


## 检查使用情况
{: #pricing_usage}

要监视 {{site.data.keyword.mon_full_notm}} 服务使用情况以及与其使用量关联的成本，请参阅[查看使用情况](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage)。



## 启用用于通知层更改的警报
{: #pricing_alert}

要在发生更改层时收到通知，必须启用以下警报：**[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

要启用警报，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
2. 创建通知通道。有关更多信息，请参阅[配置通知通道](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create)。 
3. 单击**警报**以导航至*警报*部分。
2. 搜索 **[IBM]: Usage Tier Change**。
3. 编辑警报以添加通知通道。
4. 单击**保存**。



## 如何生成服务套餐警报？
{: #pricing_how}

要在发生更改层时收到通知，必须启用以下警报：**[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

**注：**启用此警报时，必须指定要通知的通知通道。

使用量的计算方式是前一小时内以每 10 秒采样一次的频率采样到的节点数和度量值数的平均值。不包括短时间的小幅波动。先前使用量和当前使用量之间的差异将每小时比较一次。

定义的阈值按以下方式进行设置：

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [21, 50]
    Advanced = [51, 100]
  }
  metricDensity {
    Basic = [0, 200]
    Pro = [201, 500]
    Advanced = [501, 1000]
}
```
{: screen}

警报通知的生成如下所示：
1. 每小时如果层中每个节点的容器数增加，将生成一个定制事件。
2. 警报条件会检查是否有任何定制事件通知每个节点的容器数更改。如果发现有事件表明层中的容器数自上次计算使用量后增加，那么会发送通知。

警报频率为每小时一次。对于波动节点，警报频率最多为两小时一次。

请注意，仅当节点从*基本*层移至*专业*层或*高级*层时，才会生成警报。 



### 示例
{: #pricing_examples}

**样本 1** 

如果平均容器计数如下： 

|小时|容器数|描述|是否生成警报？|
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
|10:00|18|层设置为**基本**。|否|
|11:00|21|容器数超过*基本*层。层将移至**专业**。|是|
|12:00|19|容器数低于*基本*层。层将移回**基本**。|否|
|13:00|20|无层更改。层设置为**基本**。|否|
{: caption="表 2. 样本 1" caption-side="top"} 


**样本 2**

如果平均容器计数如下： 

|小时|容器数|描述|是否生成警报？|
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
|10:00|15|层设置为**基本**。|否|
|11:00|19|层设置为**基本**。|否|
|12:00|20|层设置为**基本**。|否|
|13:00|21|容器数超过*基本*层。层将移至**专业**。|是|
{: caption="表 3. 样本 2" caption-side="top"}


**样本 3**

如果平均容器计数如下： 

|小时|容器数|描述|是否生成警报？|
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
|10:00|15|层设置为**基本**。|否|
|11:00|20|层设置为**基本**。|否|
|12:00|21|层设置为**基本**。|是|
|13:00|20|容器数恢复为*基本*层。层将移至**专业**。|否|
{: caption="表 3. 样本 3" caption-side="top"}



