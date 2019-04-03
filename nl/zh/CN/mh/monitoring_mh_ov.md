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



# {{site.data.keyword.messagehub}}
{: #monitoring_mh_ov}

在 {{site.data.keyword.Bluemix}} 中，系统会自动收集 {{site.data.keyword.messagehub}} 度量值。 还会收集出入主题的字节数。 每 15 分钟进行一次检查。 您可以通过 Grafana 使这些度量值可视化。 
{:shortdesc}


**注：**{{site.data.keyword.messagehub}} 度量值仅在美国南部、英国和悉尼的 {{site.data.keyword.messagehub}} 标准套餐中可用。 




## 查看和分析度量值
{: #view}

要监视 {{site.data.keyword.Bluemix_notm}} 中 {{site.data.keyword.messagehub}} 的性能，请使用 Grafana。 {{site.data.keyword.messagehub}} 提供了一个仪表板，可用于查看和监视主题的性能。

{{site.data.keyword.monitoringlong}} 服务使用 Grafana（一种开放式源代码分析和可视化平台）通过各种图形（例如，图表和表）来对度量值进行监视、搜索、分析和可视化表示。 

您可以使用以下任何一种方法来启动 Grafana：

* 您可以在 {{site.data.keyword.Bluemix_notm}} 控制台的 {{site.data.keyword.messagehub}} 仪表板上单击 **Grafana** 按钮。

    Grafana 在运行 {{site.data.keyword.messagehub}} 的 {{site.data.keyword.Bluemix_notm}} 的空间上下文中打开。
    
* 您可以直接从 Web 浏览器启动 Grafana。

    检查您是否位于运行 {{site.data.keyword.messagehub}} 实例的同一组织和空间。
    
    有关更多信息，请参阅[通过 Web 浏览器导航至 Grafana 仪表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。
    

请考虑以下信息：

* 您必须在运行 {{site.data.keyword.messagehub}} 实例的同一 {{site.data.keyword.Bluemix_notm}} 区域中启动 Grafana。
* 使用缺省情况下提供的 Grafana 仪表板来开始监视您的 {{site.data.keyword.messagehub}} 实例。
* 通过创建定制的 Grafana 仪表板来构建特别的仪表板。 您可以在 Grafana 仪表板中定义一个或多个度量值查询，以监视 {{site.data.keyword.messagehub}} 实例。 有关更多信息，请参阅[在 Grafana 中配置度量值查询](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query#define_query)。
* 您还可以针对查询定义警报。 有关更多信息，请参阅[配置警报](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)。


## Kafka 主题的度量值
{: #kafka_topic_metrics}

对于所定义的每个 Kafka 主题，将收集以下度量值：


<table>
  <caption>每个 Kafka 主题的度量值</caption>
  <tr>
    <th>度量值</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Kafka 客户机应用程序向主题发送字节的速度。</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Kafka 客户机应用程序从主题接收字节的速度。</td>
  </tr>
</table>



## Kafka 分区的度量值
{: #kafka_partition_metrics}

对于拥有可消耗消息的 Cloud Storage 网桥的每个 Kafka 分区，收集以下度量值：


<table>
  <caption>Kafka 分区度量值</caption>
  <tr>
    <th>度量值</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>Cloud Storage 网桥处理的最后一个 Kafka 记录的偏移量。</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>Cloud Storage 网桥处理的 Kafka 记录的已落实偏移量。</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Cloud Storage 网桥实例从 Kafka 主题接收的消息数。 仅统计包含该网桥无法处理的有效 JSON 的消息。</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Cloud Storage 网桥实例从 Kafka 主题接收的消息数。 仅统计包含因为不是有效 JSON 文档而无法解析的数据的消息。</td>
  </tr>
</table>




## 参考
{: #mhlinks}

* [Message Hub 入门](/docs/services/EventStreams?topic=eventstreams-getting_started#getting_started)
* [监视和记录](/docs/services/EventStreams/messagehub072.html#monitoring)

