---

copyright:
  years: 2018, 2019
lastupdated: "2018-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 定制容器 Sysdig 代理程序
{: #change_agent}

在 {{site.data.keyword.mon_full_notm}} 中，可以定制 Sysdig 代理程序配置以设置日志级别，阻止端口，包含或排除度量值数据，添加或除去事件以及过滤掉容器。
{:shortdesc}




## 编辑 dragent yaml 文件
{: #edit_agent}

该 YAML 文件位于 */opt/draios/etc/* 中。

要编辑该文件并应用更改，请完成以下步骤：

1. 直接在 `/opt/draios/etc/dragent.yaml` 处访问 *dragent.yaml*。
2. 编辑该文件。请使用有效的 YAML 语法。
3. 重新启动代理程序。运行以下命令：

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## 阻止端口
{: #ports}

要阻止来自网络端口的网络流量和度量值，必须定制 *dragent.yaml* 文件中的 **blacklisted_ports** 部分。必须列出要从中过滤掉任何数据的端口。

**注：**端口 53 (DNS) 始终列入黑名单。 

例如，以下样本显示了如何设置 Sysdig 代理程序的 *blacklisted_ports* 部分，以排除来自端口 6666 和 6379 的数据：

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## 收集一组 Docker 事件
{: #docker}

{{site.data.keyword.mon_full_notm}} 支持与 Docker 的事件集成。Sysdig 代理程序会自动发现 Docker 源并从中收集事件数据。您可以编辑代理程序配置文件以更改其缺省行为，还可以包含或排除事件数据。 

缺省情况下，只收集一组有限的事件。缺省设置配置文件 */opt/draios/etc/dragent.default.yaml* 包含收集的事件。有关缺省情况下收集的事件的更多信息，请参阅 [Docker Events ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}。

要添加或除去事件，必须定制 *dragent.yaml* 文件，并指定要包含的事件和要过滤掉的事件。**注：**更改 *dragent.yaml* 某个部分中的条目会覆盖缺省配置中该部分的整个内容。
{: tip}

例如，要过滤掉 Docker 映像事件并仅收集 attach、commit 和 copy 操作的事件，那么必须如下所示设置 *docker* 部分：

* 选项 1：将条目中的序列定义为项目符号列表：

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* 选项 2：将条目中的序列定义为用方括号括起的一行：

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## 禁用事件收集
{: #disable}

要禁止 Sysdig 代理程序收集事件，请修改 *dragent.default.yaml* 文件。在 *dragent.yaml* 文件中，将 **events** 部分设置为 *none*。

例如，要过滤掉 Docker 事件，必须在 *dragent.yaml* 文件中设置 *events* 部分，如下所示：

```
events:
  docker: none
```
{: codeblock}



## 按严重性过滤事件
{: #severity}

要按严重性过滤事件，还可以更改 *dragent.yaml* 文件中事件的日志条目类型。 

缺省日志级别为 **information**。这表示仅传输警告和更高严重性的事件。

有效级别为：*emergency*、*alert*、*critical*、*error*、*warning*、*notice*、*information*、*debug* 和 *none*。**注**：值按优先级从高到低列出。

例如，要过滤掉低严重性的事件（*notice*、*information* 和 *debug*），必须将 log 部分的 **event_priority** 设置为 *warning*：

```
log:
  event_priority: warning
```
{: codeblock}


要阻止收集事件，必须将 log 部分的 **event_priority** 设置为 *none*：

```
log:
  event_priority: none
```
{: codeblock}




## 包含和排除度量值
{: #params}

要过滤定制度量值，必须定制 *dragent.yaml* 文件中的 **metrics_filter** 部分。通过配置 **include** 和 **exclude** 过滤参数，可以指定要包含的度量值以及要过滤掉的度量值。

**注：**过滤规则顺序的设置如下所示：将应用与度量值匹配的第一个规则。

例如，如果 Sysdig 代理程序的 *metrics_filter* 部分如下所示：

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* 您将 Sysdig 代理程序配置为从以 *metricA*、*metricB* 和 *haproxy.backend* 开头的度量值收集所有数据。 
* 您将过滤掉以 *metricC* 开头的度量值以及以 *haproxy* 开头的其他度量值。 
* `exclude: metricA.*` 条目将被忽略。


## 更改日志级别
{: #log_level}

要配置日志级别，必须定制 *dragent.yaml* 文件中的 **log** 部分。 

Sysdig 代理程序在 */opt/draios/logs/draios.log* 中生成日志条目。 
* 日志文件在大小达到 10 MB 时会循环。
* 将保留 10 个最近的日志文件。附加到文件名的日期戳记用于确定要保留的文件。
* 有效日志级别为：*none*、*error*、*warning*、*info*、*debug* 和 *trace*
* 缺省日志级别为 *info*，其中除了用于任何警告和错误的条目外，每次向后端服务器传输聚集的度量值时（每秒一次），都会创建一个条目。
* 可以通过配置 Sysdig 代理程序配置文件 **/opt/draios/etc/dragent.yaml** 来定制日志的类型和收集的条目。编辑该文件后，必须在 shell 中使用 `docker restart sysdig-agent` 重新启动代理程序以使更改生效。

|用例|Log 部分条目|
|-----------------------------------------------|-----------------------------|
|对代理程序行为进行故障诊断|`file_priority: debug`|
|减少容器控制台输出|`console_priority: warning`|
|按严重性过滤事件|`event_priority: warning`|
|验证包含或排除的度量值|`metrics_excess_log: true`|
{: caption="表 2. Log 部分条目" caption-side="top"} 


