---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# 定制 Linux Sysdig 代理程序
{: #change_linux_agent}

缺省情况下，Sysdig 代理程序会从一系列平台和应用程序收集数据。您可以编辑代理程序配置文件以更改其缺省行为，还可以包含或排除数据。可以定制 Sysdig 代理程序配置文件以包含定制度量值，例如 JMX、StatsD 和 Prometheus。还可以过滤掉度量值和容器。
{:shortdesc}

Sysdig 代理程序使用两个配置文件来指定要自动收集的数据：

|文件|描述|位置|
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
|`dragent.default.yaml`|主配置文件</br>**注：**** 请勿编辑此文件。|`/opt/draios/etc/dragent.default.yaml`|
|`dragent.yaml`|用于定制 Sysdig 代理程序的配置文件。|`/opt/draios/etc/dragent.yaml`|
{: caption="表 1. Sysdig 代理程序配置文件" caption-side="top"} 

可以编辑 *dragent.yaml* 文件来定制收集的数据。更改将在保存文件后立即生效。代理程序检测到更改后，会自动重新启动。您可以在 *dragent.default.yaml* 文件中找到 Sysdig 代理程序检查的频率和检查的文件。

例如，*dragent.default.yaml* 包含以下信息：

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## 编辑 dragent yaml 文件
{: #change_linux_agent_edit_agent}

该 YAML 文件位于 */opt/draios/etc/* 中。

要编辑该文件并应用更改，请完成以下步骤：

1. 直接访问 *dragent.yaml*。该文件位于 `/opt/draios/etc/dragent.yaml`。
2. 编辑该文件。请使用有效的 YAML 语法。
3. 重新启动代理程序。运行以下命令：

    ```
    service dragent restart
    ```
    {: codeblock}


## 阻止端口
{: #change_linux_agent_block_ports}

要阻止来自网络端口的网络流量和度量值，必须定制 *dragent.yaml* 文件中的 **blacklisted_ports** 部分。必须列出要从中过滤掉任何数据的端口。

**注：**端口 53 (DNS) 始终列入黑名单。 

例如，以下样本显示了如何设置 Sysdig 代理程序的 *blacklisted_ports* 部分，以排除来自端口 6666 和 6379 的数据：

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## 包含和排除度量值
{: #change_linux_agent_inc_exc_metrics}

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
{: #change_linux_agent_log_level}

要配置日志级别，必须定制 *dragent.yaml* 文件中的 **log** 部分。 

Sysdig 代理程序在 */opt/draios/logs/draios.log* 中生成日志条目。 
* 日志文件在大小达到 10 MB 时会循环。
* 将保留 10 个最近的日志文件。附加到文件名的日期戳记用于确定要保留的文件。
* 有效日志级别为：*none*、*error*、*warning*、*info*、*debug* 和 *trace*
* 缺省日志级别为 *info*，其中除了用于任何警告和错误的条目外，每次向后端服务器传输聚集的度量值时（每秒一次），都会创建一个条目。
* 可以通过配置 Sysdig 代理程序配置文件 **/opt/draios/etc/dragent.yaml** 来定制日志的类型和收集的条目。编辑该文件后，必须在 shell 中使用 `service dragent restart` 重新启动代理程序以使更改生效。

|用例|Log 部分条目|
|-----------------------------------------------|-----------------------------|
|对代理程序行为进行故障诊断|`file_priority: debug`|
|减少容器控制台输出|`console_priority: warning`|
|按严重性过滤事件|`event_priority: warning`|
|验证包含或排除的度量值|`metrics_excess_log: true`|
{: caption="表 2. Log 部分条目" caption-side="top"} 
