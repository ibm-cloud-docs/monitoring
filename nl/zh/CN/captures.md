---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# 使用捕获
{: #captures}

捕获是一种跟踪文件，您可以生成该文件来分析在某一时间范围内主机中发生的事件。例如，可以将其用于分析瓶颈或组件交互。在 {{site.data.keyword.mon_full_notm}} 服务中，可以针对各个节点创建、探索、下载和删除*捕获*。
{:shortdesc}

有关更多信息，请参阅[捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。


## 创建捕获
{: #captures_create}

可以在*探索*视图中创建捕获。

要创建捕获文件，请完成以下步骤：

1. 在 Web UI 中，导航至*探索*部分。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。

2. 单击“切换主机”图标 ![“切换主机”图标](images/switch_hosts.png)。

3. 选择主机或容器。

4. 单击“操作”图标 ![三个点图标](images/actions.png) ，然后选择 **Sysdig 捕获**。

    这将打开 *Sysdig 捕获*窗口。

5. 在 *Sysdig 捕获*窗口中，定义以下参数：

    1. 在*捕获路径和名称*字段中，输入捕获文件的名称。您可以保留缺省值，也可以修改缺省值。缺省名称包含创建捕获时的日期和时间戳记。 

    2. 设置*时间范围*以指定用于收集数据的秒数。缺省捕获时间为 15 秒。最大捕获时间为 86400 秒（24 小时）。 

    3. （可选）添加过滤器以限制收集的跟踪信息量。 

6. 单击**开始捕获**。系统会向 Sysdig 代理程序发出信号以开始捕获，并会返回生成的跟踪文件。 

7. 单击**转至捕获页面**以在 Web UI 的*捕获*部分中显示捕获的列表。 

*捕获*页面显示了一个表，其中列出了捕获文件名、从中检索到该文件的主机、时间范围和捕获的大小。 

捕获文件的状态可以是以下任一值：
* **已请求**：正在生成文件。
* **已上传**：文件可供下载和分析。
* **错误**：由于超时、从未收到数据或代理程序错误而导致文件不可用。



## 删除捕获
{: #captures_delete}

要删除捕获文件，请完成以下步骤：

1. 在 Web UI 中，导航至*捕获*部分。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。
2. 识别并选择要删除的捕获文件。
3. 单击**删除**。



## 探索捕获
{: #captures_explore}

要探索捕获文件，请完成以下步骤：

1. 在 Web UI 中，导航至*捕获*部分。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。
2. 识别并选择包含要分析的主机的数据的捕获文件。
3. 单击**探索**。



## 下载捕获
{: #captures_download}

要下载捕获文件，请完成以下步骤：

1. 在 Web UI 中，导航至*捕获*部分。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。
2. 识别并选择包含要下载的数据的捕获文件。
3. 单击**下载**。


## 凿子
{: #captures_chisels}

Sysdig 凿子是一种用 Lua 脚本语言编写的脚本。您可以将其用于分析捕获文件中的数据。 

有关如何使用凿子的更多信息，请参阅以下用户指南：[Chisels User Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}



## Csysdig
{: #captures_csysdig}

Csysdig 是一种面向 Linux 的开放式源代码工具，旨在用于监视和调试。您可以将其用于分析捕获文件。 

有关更多信息，请参阅以下资源：
* [Csysdig 博客 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Csysdig 视频 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


