---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring

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

# 监视环境
{: #monitoring}

您可以使用 {{site.data.keyword.mon_full_notm}} 服务来监视基础架构以及在其上运行的应用程序。还可以请求捕获以分析在某一时间范围内某个节点中发生的事件。
{:shortdesc}

首先，在 {{site.data.keyword.cloud_notm}} 中供应 {{site.data.keyword.mon_full_notm}} 服务的实例。然后，为度量源配置 Sysdig 代理程序。配置源之后，您可以通过服务的 Web UI 查看、监视和管理数据。

缺省度量值的数据会自动收集。可以配置定制度量值，并向这些度量值添加标签以描述其特征。另外还会自动收集这些定制度量值的数据。

可以在 Web UI 的*探索*选项卡和*仪表板*选项卡中分析数据。您可通过度量值视图和仪表板来监视数据。 

* 使用度量值视图可监视单个度量值。
* 使用仪表板可通过多个面板监视数据，以获取对网络数据、应用程序数据、拓扑、服务、主机和容器的专业洞察。在仪表板中，面板显示一个度量值或一组度量值。

对于每个度量值视图和仪表板，可以定义数据作用域、数据聚集方式以及要应用于数据的时间和组过滤器。有关更多信息，请参阅[管理数据](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)。

在*探索*选项卡中，可以使用缺省度量值和缺省仪表板来监视数据。可以使用标签来定义新的基础架构组，然后可以使用这些组以不同方式聚集数据并监视环境。您还可以使用通过*仪表板*选项卡定义的定制仪表板。

在*仪表板*选项卡中，可以使用任一缺省仪表板或通过创建新仪表板来监视数据。

可以将缺省仪表板配置为团队的缺省入口点，以统一团队的体验，并允许用户立即关注与其最相关的信息。
{: tip}

可以使用警报通过一个或多个通知通道来通知用户需要注意的问题。
* Web UI 中的*警报*部分显示预定义警报的列表。在此视图中，可以启用和禁用预定义的警报，可以修改现有警报，还可以创建新警报。
* Web UI 中的*设置*部分是配置通知通道的位置。
 
可以请求对节点的捕获，以分析在某一时间范围内该节点中发生的事件。例如，可以将其用于分析瓶颈或组件交互。

## 度量值
{: #monitoring_metrics}

度量值是一种定量度量，具有一个或多个标签用于定义其特征。使用度量值可通过统计方式分析具有数字值的数据。 

度量值由时间序列表示。时间序列是一段时间内的一组数字数据点。 

度量值分类为两个组： 

* [缺省度量值](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [定制度量值](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

标签分类为基础架构标签和度量值描述符标签。每个度量值都有一组预定义的标签。对于定制度量值，可以配置更多标签。 

可以使用标签来标识和区分度量值的特征，例如：
* 可以将基础架构对象分组为逻辑层次结构。 
* 可以过滤掉数据。 
* 可以将聚集的数据拆分成分段。 

有关更多信息，请参阅[标签](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels)。

## 面板
{: #monitoring_panels}

在仪表板中，面板显示一个度量值或一组度量值。 

可以使用以下任一面板类型来对度量值进行可视化：

|类型|描述|
|------|-------------|
| `折线图` |使用此面板可查看一个或多个度量值随时间变化的趋势。|
| `面积图` |使用此面板可查看一个或多个度量值随时间变化的趋势。|
| `排名靠前的列表` |使用此面板可在多组实体之间比较度量值。条形图会按降序排序。|
|`直方图` |使用此面板可查看存储区中某个度量值的频率分布。|
| `拓扑图` |使用此面板可将基础架构可视化为拓扑映射，并可对映射中实体之间的关系进行可视化。|
| `数字` |使用此面板可查看表示一个或多个实体一段时间内聚集度量值的单个数字。|
| `表格` |使用此面板可根据度量值和分段来显示基础架构的数字数据。|
| `文本` |使用此面板可添加文本。请使用 Markdown 来添加文本。|
{: caption="表 1. 面板类型" caption-side="top"} 

可以复制和更改作用域，还可以复制、删除、导出和探索面板。

可以从面板中导出数据。导出数据时，请考虑以下信息：

* 可以将折线图中的数据导出为 **JSON 文件**。
* 可以将表图表或折线图中的数据导出为 **CSV 文件**。


下表列出了可以使用面板运行的任务：

| 任务|描述|
|------|-------------|
|[复制面板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy)|将面板复制到新仪表板中。|
|[更改作用域](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope)|更改面板的作用域。|
|[复制面板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate)|在同一仪表板中复制面板。|
|[删除面板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete)|从仪表板中删除面板。|
|[导出数据](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export)|将面板中的数据导出为 CSV 文件或 JSON 文件。|
|[创建警报](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert)|定义有关度量值的警报。|
{: caption="表 2. 面板任务" caption-side="top"} 


## 仪表板
{: #monitoring_dashboards}

**仪表板**显示多组度量值，用于报告一个主机或一组主机的基础架构、应用程序和服务的运行状况、性能和状态。仪表板提供了对网络数据、应用程序数据、拓扑、服务、主机和容器的专业洞察。使用仪表板可监视基础架构、应用程序和服务。


在 Web UI 的**仪表板**部分中，仪表板分为三个主要组：

* **我的仪表板**：这些是当前登录的用户创建的仪表板。
* **我共享的仪表板**：这些是当前登录的用户创建并与其他用户共享的仪表板。
* **与我共享的仪表板**：这些是由其他用户创建并与当前用户共享的仪表板。

在 Web UI 的**探索**部分中，仪表板分为两组：
* **缺省仪表板**：这些是预定义仪表板。
* **我的仪表板**：这些是当前登录的用户创建的仪表板。

您可以使用预定义仪表板。还可以通过 Web UI 或以编程方式创建定制仪表板。可以使用 Python 脚本或 Sysdig REST API 来备份和复原仪表板。


还可以通过 Web UI 来复制和共享仪表板。 

下表概述了可以通过 UI 运行以使用仪表板的任务：

| 任务|描述|
|------|-------------|
|[创建仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create)|在 Web UI 中创建定制仪表板。|
|[复制仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy)|在仪表板可用的当前团队中创建该仪表板的副本，或者将仪表板复制到其他团队。|
|[更改作用域](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope)|更改仪表板的作用域。|
|[删除仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete)|删除仪表板。|
|[共享仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share)|通过配置仪表板的公共 URL，在团队中的用户之间以及在外部共享仪表板。|
{: caption="表 1. 可在 Web UI 中运行的仪表板任务" caption-side="top"} 

下表概述了可通过编程方式运行以使用仪表板的任务：

|任务                    |	使用 REST API|
|-------------------------|-------------------------------|
|创建仪表板|[使用 API 创建仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard)|
|删除仪表板|[使用 API 删除仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard)|
|保存仪表板|[使用 API 保存团队的仪表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="表 4. 用于以编程方式管理仪表板的任务" caption-side="top"} 



## 事件
{: #monitoring_events}

事件是一种通知，用于通知在将数据转发到 {{site.data.keyword.mon_full_notm}} 实例的任何节点中发生的活动。使用事件可复查、跟踪和解决问题。 

以下列表概述了不同类型的事件： 

* *警报事件*是由用户配置的警报触发的事件。有关更多信息，请参阅[使用警报](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)。
* *基于基础架构的事件*是从 Docker 和 Kubernetes 节点收集的事件。缺省情况下，Sysdig 代理程序会自动从精选事件组中发现并收集数据。可以编辑代理程序配置文件来启用更多事件。
* *定制事件*是通过以下任一集成配置的事件：Slackbot、预构建的 Python 脚本、用户创建的定制 Python 脚本或 cURL 请求。

缺省情况下，事件具有状态： 
* **活动**：此状态指示触发事件的情况仍然存在，例如节点一直停止运行。
* **正常**：此状态指示情境已恢复正常，例如节点已启动并在运行。

可在 Web UI 的*事件*部分中管理事件。 
* 可以通过*警报事件*选项卡来查看警报事件。
* 可以通过*定制事件*选项卡来查看基于基础架构的事件。
* 可以通过*定制事件*选项卡来查看定制事件。
* 可以使用任一[团队的 API 令牌](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token)向该团队发送定制事件。有关更多信息，请参阅 [Custom Events ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}。
* 您可以将事件设置为**已解决**，以通知其他用户问题已解决，而不需要等待状态设置为**正常**。
{: #tip}



## 警报
{: #monitoring_alerts}

警报是一种通知事件，可用于发出有关需要注意的情境的警告。每个警报都具有严重性状态。此状态会通知您所报告信息的重要程度。 

定义警报时，您必须定义触发通知的条件、要借以获得通知的一个或多个通知通道。您还必须定义警报的严重性以及警报的类型。 

可以为以下任一警报类型定义警报：

|类型|描述|
|-------------------|-------------|
|异常检测|用于根据主机的历史行为监视主机，并在发生偏移时发出警报。|
|停机时间|用于监视任何类型的实体（例如，主机、容器、进程或服务），并在实体停止运行时发出警报。|
|事件|用于监视特定事件的发生，并在发生总数违反阈值时发出警报。例如，可将其用于发出有关容器重新启动和部署、编排和服务事件的警报。|
|组界外值|用于监视一组主机，并在某个主机的行为与其余主机不同时获得通知。|
|度量值|用于监视时间序列度量值，并在它们违反用户定义的阈值时发出警报。|
{: caption="表 5. 警报类型" caption-side="top"} 

缺省情况下，严重性设置为*警告*。可以将警报的严重性设置为以下任一值：*紧急*、*警报*、*严重*、*错误*、*警告*、*通知*、*参考*和*调试*。 

可以为以下任一通知集成定义一个或多个通知通道：
* 电子邮件通知
* PagerDuty 通知
* Slack 通知
* VictorOps 通知
* OpsGenie 通知
* 配置 Webhook 通道

有关更多信息，请参阅[配置通知通道](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create)。


可以在 Web UI 中以及使用 Sysdig API 来启用预定义警报，修改警报和创建定制警报。

可在 Web UI 的*警报*视图中管理警报。可以配置*警报*视图中显示的表列。有效列选项为：*名称*、*作用域*、*警报条件*、*分段依据*、*通知*、*已启用*、*已修改*、*捕获*、*通道*、*已创建*、*描述*、*电子邮件收件人*、*至少针对*、*OpsGenie*、*PagerDuty*、*严重性*、*Slack*、*WebHook*、*SNS 主题*、*类型*和 *VictorOps*。

以下列表概述了使用警报时的主要任务：
* [配置警报 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [启用或禁用警报 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [搜索警报 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [修改警报 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [将警报复制到同一团队 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [将警报复制到其他团队 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [导出警报 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [删除警报 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [将警报阈值定义为定制布尔表达式 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## 捕获
{: #monitoring_captures}

捕获是一种跟踪文件，您可以生成该文件来分析在某一时间范围内某个节点中发生的事件。捕获文件大小限制为 100 MB。例如，可以将其用于分析瓶颈或组件交互。 

捕获包含系统调用以及其他操作系统事件，例如系统级别的等待时间、批处理作业持续时间、部署中断时间、自动缩放等待时间、容器启动时间或应用程序事务时间。捕获包括节点上每个容器中的详细信息。 

请根据组织的准则，考虑禁用捕获。缺省情况下，在节点中配置 Sysdig 代理程序时捕获已启用。
{: tip}

可以针对各个节点创建、探索、下载和删除*捕获*。节点可以是主机、容器、虚拟机、裸机或安装 Sysdig 代理程序的任何度量源。 

* 在 Web UI 中，可以在*探索*部分中创建捕获，然后通过*捕获*部分来管理捕获文件。
* 可以使用 *Csysdig*（Sysdig 的基于 curses 的命令行 UI）或开放式源代码 Sysdig 实用程序来分析捕获中的数据，从而对捕获中的数据进行可视化。
* 可以使用过滤器来搜索捕获中的数据。
* 可以使用凿子（脚本）来处理捕获中的数据。 

为团队启用捕获功能时，捕获文件仅可供该团队的成员查看。

以下列表概述了使用捕获时的主要任务：
* [创建捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [删除捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [探索捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [下载捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

有关更多信息，请参阅[使用捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。


