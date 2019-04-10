---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 定制 Sysdig 代理程序以控制数据
{: #customize_agent}

缺省情况下，Sysdig 代理程序会从一系列平台和应用程序收集数据。您可以编辑代理程序配置文件以更改其缺省行为，还可以包含或排除数据。可以定制 Sysdig 代理程序配置文件以包含定制度量值，例如 JMX、StatsD 和 Prometheus。还可以过滤掉度量值、事件数据和容器。
{:shortdesc}

## 定制 Kubernetes Sysdig 代理程序
{: #kube}

Kubernetes Sysdig 代理程序使用两个配置文件来指定要自动收集的数据：

|文件名|操作|
|----------------------------------|-------------------|
|`sysdig-agent-daemonset-v2.yaml`|修改日志级别。|
|`sysdig-agent-configmap.yaml`|阻止端口。</br>包含或排除度量值数据。</br>添加或除去事件。</br>过滤掉容器。|
{: caption="表 1. Kubernetes Sysdig 代理程序配置文件" caption-side="top"} 

要编辑 Kubernetes Sysdig 代理程序，您可能需要编辑 *sysdig-agent-configmap.yaml* 和/或 *sysdig-agent-daemonset-v2.yaml*。


可以使用两种方法来修改配置文件：
* 方法 1：直接在运行代理程序的集群上修改文件。有关更多信息，请参阅[使用 kubectl edit 编辑 Kubernetes Sysdig 代理程序配置](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1)。
* 方法 2：本地修改文件，然后将更改应用于集群。有关更多信息，请参阅[使用 kubectl apply 编辑 Kubernetes Sysdig 代理程序配置](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2)。

可以向代理程序收集的数据添加标记。 
* 使用这些标记可帮助您管理监视的数据。 

    * 使用标签可将基础架构资源分组为逻辑层次结构，过滤掉数据以及将聚集的数据拆分成分段。 
    
    * 定制在配置图形或为度量值创建警报时聚集数据的方式。 
    
    * 设置仪表板、面板或警报的作用域，以过滤掉数据点。 
    
    * 通过团队管理用户的数据访问权，从而限制对数据的访问权。 
    
    * 有关如何管理数据的更多信息，请参阅[管理数据](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)。

* 有关如何添加标记的信息，请参阅[向通过 Kubernetes Sysdig 代理程序收集的数据添加更多标记](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags)。 


**可以定制 Sysdig 代理程序收集的数据。** 

排除事件、度量值和容器时，请考虑以下信息：
* 可以降低代理程序和后端负载。
* 仅从要监视的容器收集数据。
* 可以通过只报告重要容器，而过滤掉不必要或不重要的容器，从而控制成本。
* 可以配置要监视的 Kubernetes 事件。有关更多信息，请参阅[收集一组 Kubernetes 事件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events)。

以下列表概述了可以执行以控制 Sysdig 代理程序所收集数据的操作：
* [禁用事件收集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [包含和排除度量值](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [过滤从中收集数据的 Kubernetes 对象和容器](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [阻止端口](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [按严重性过滤 Kubernetes 事件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

还可以定制日志的类型以及收集的条目。有关更多信息，请参阅[更改日志级别](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level)。

还可以记录代理程序报告其数据的度量值的列表。有关更多信息，请参阅[将包含或排除的度量值记录到日志文件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics)。

Sysdig 代理程序在 */opt/draios/logs/draios.log* 中生成日志条目。 
* 日志文件在大小达到 10 MB 时会循环。
* 将保留 10 个最近的日志文件。附加到文件名的日期戳记用于确定要保留的文件。
* 有效日志级别为：*none*、*error*、*warning*、*info*、*debug* 和 *trace*
* 缺省日志级别为 *info*，其中除了用于任何警告和错误的条目外，每次向后端服务器传输聚集的度量值时（每秒一次），都会创建一个条目。

下表列出了一些常见场景以及必须在其中每个场景中设置的值：

|用例|Log 部分条目|
|-----------------------------------------------|-----------------------------|
|对代理程序行为进行故障诊断|`file_priority: debug`|
|减少容器控制台输出|`console_priority: warning`|
|按严重性过滤事件|`event_priority: warning`|
|验证包含或排除的度量值|`metrics_excess_log: true`|

## 容器 Sysdig 代理程序
{: #container}


以下列表概述了可以执行以控制 Sysdig 代理程序所收集数据的操作：
* [禁用事件收集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [包含和排除度量值](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [过滤从中收集数据的容器](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [阻止端口](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [按严重性过滤事件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

还可以定制日志的类型以及收集的条目。有关更多信息，请参阅[更改日志级别](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level)。



## Linux Sysdig 代理程序
{: #linux}

Linux Sysdig 代理程序使用两个配置文件来指定要自动收集的数据：

|文件|描述|位置|
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
|`dragent.default.yaml`|主配置文件</br>**注：**** 请勿编辑此文件。|`/opt/draios/etc/dragent.default.yaml`|
|`dragent.yaml`|用于定制 Sysdig 代理程序的配置文件。|`/opt/draios/etc/dragent.yaml`|
{: caption="表 1. Sysdig 代理程序配置文件" caption-side="top"} 

可以编辑 *dragent.yaml* 文件来定制收集的数据。更改将在保存文件后立即生效。代理程序检测到更改后，会自动重新启动。您可以在 *dragent.default.yaml* 文件中找到 Sysdig 代理程序检查的频率和检查的文件。有关更多信息，请参阅[编辑 dragent yaml 文件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent)。

例如，*dragent.default.yaml* 包含以下信息：

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

以下列表概述了可以执行以控制 Sysdig 代理程序所收集数据的操作：
* [包含和排除度量值](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [阻止端口](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

还可以定制日志的类型以及收集的条目。有关更多信息，请参阅[更改日志级别](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level)。


