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

# 在 Grafana 中配置警报
{: #config_alerts_grafana}

{{site.data.keyword.monitoringshort}} 服务提供了基于查询的警报系统。您可以在 Grafana 中没有模板变量的仪表板上配置警报。
{:shortdesc}

要通过 Grafana UI 针对度量值查询配置警报，请完成以下步骤：

1. 启动 Grafana。
2. 定义一条或多条通知通道。
3. 创建包含一个图形和至少一个查询度量值的 Grafana 仪表板。 
4. 通过 Grafana 图形上的**警报**选项卡来配置警报。

## 步骤 1：启动 Grafana
{: #step1_cag}

通过浏览器启动 Grafana。例如，输入以下 URL 以在美国南部区域中打开 Grafana：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

有关每个区域的 Grafana URL 列表，请参阅 [{{site.data.keyword.monitoringshort}} 服务的 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)。

## 步骤 2：定义一条或多条通知通道
{: #step2_cag}

请完成以下步骤：

1. 在 Grafana 中，选择侧菜单栏。

2. 选择**警报 > 通知通道 > 新建通道**。

3. 为新通道输入数据。例如，添加电子邮件通知通道。

<table>
  <caption>为了创建新通道而必须输入的电子邮件通知方法和数据</caption>
  <tr>
     <th>字段</th>
     <th>描述</th>
  </tr>
  <tr>
    <td>名称</td>
    <td>通知通道的名称。此值必须唯一。</td>
  </tr>
  <tr>
    <td>描述</td>
    <td>您出于文档记录目的而可能希望包含的其他信息。</td>
  </tr>
  <tr>
    <td>类型</td>
    <td>选择：**电子邮件**</td>
  </tr>
  <tr>
    <td>电子邮件标识</td>
    <td>输入收件人的电子邮件地址。</br>您可以输入以逗号分隔的多个电子邮件地址。</td>
  </tr>
</table>

<table>
  <caption>为了创建新通道而必须输入的 Webhook 通知方法和数据</caption>
  <tr>
     <th>字段</th>
     <th>描述</th>
  </tr>
  <tr>
    <td>名称</td>
    <td>通知通道的名称。此值必须唯一。</td>
  </tr>
  <tr>
    <td>描述</td>
    <td>您出于文档记录目的而可能希望包含的其他信息。</td>
  </tr>
  <tr>
    <td>类型</td>
    <td>选择：**Webhook**</td>
  </tr>
  <tr>
    <td>Webhook POST URL</td>
    <td>输入应该执行 POST 操作的 URL。</td>
  </tr>
  <tr>
    <td>Webhook 头</td>
    <td>输入任何头。</td>
  </tr>
  <tr>
    <td>Webhook 查询参数</td>
    <td>输入任何查询参数。</td>
  </tr>
</table>

<table>
  <caption>PagerDuty 通知方法和必须输入以创建新通道的数据</caption>
  <tr>
     <th>字段</th>
     <th>描述</th>
  </tr>
  <tr>
    <td>名称</td>
    <td>通知通道的名称。此值必须唯一。</td>
  </tr>
  <tr>
    <td>描述</td>
    <td>您出于文档记录目的而可能希望包含的其他信息。</td>
  </tr>
  <tr>
    <td>类型</td>
    <td>选择：**PagerDuty**</td>
  </tr>
  <tr>
    <td>PagerDuty API 密钥</td>
    <td>输入 PagerDuty 密钥。</td>
  </tr>
</table>

## 步骤 3：定义度量值
{: #step3_cag}

要创建新仪表板，请完成以下步骤：

1. 选择侧菜单栏切换 ![Grafana 侧菜单栏](images/grafana_settings.gif "Grafana 侧菜单栏")。
2. 选择**仪表板**。
3. 单击**新建**。

这将打开仪表板。仪表板包含一个空行，可随时用于配置。 

接下来，添加度量值查询：

1. 添加*图形*面板。
2. 选择**图形**。
3. 单击图形标题，然后选择**编辑**。
    
    这将打开*度量值*选项卡。在此可以看到缺省数据源。
    
4. 定义用于过滤图形中所显示数据的度量值查询。 


## 步骤 4：定义警报
{: #step4_cag}

要在 Grafana UI 中定义警报，请完成以下步骤：

1. 选择**警报**选项卡。
2. 在**警报配置**部分中，定义用于定义警报通知生成条件的规则。

    配置**求值时间间隔**字段和**条件**部分。

3. 在**通知**部分中，选择一条或多条通知通道。

**注：** 

* 设置条件后，您可以在图形上看到一条红线用于定义阈值集。可以在图表上拖动该线进行更改。
* 创建警报后，如果要修改警报，必须使用警报 API 来执行此操作。
* 如果选择**删除**，将删除该警报。

## 下一步：验证是否生成了警报
{: #next_cag}

例如，如果创建了电子邮件通知通道，请检查电子邮件。

查找发件人为 **IBM Cloud Monitoring** 的电子邮件。

电子邮件中包含有关所发出警报的信息以及 Grafana 仪表板的链接，您可以在此仪表板中查看相关情况。

例如：

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


