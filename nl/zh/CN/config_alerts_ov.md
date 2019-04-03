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



# 配置警报
{: #config_alerts_ov}

{{site.data.keyword.monitoringshort}} 服务提供了基于查询的警报系统。您可以使用 {{site.data.keyword.monitoringshort}} API 或通过 Grafana 配置警报。要配置警报，必须为您要监视的每个度量值查询设置规则和通知方法。可以通过发送电子邮件、触发 Webhook 或向 PagerDuty 发出警报来进行通知。
{:shortdesc}

您可以定义警报以触发度量值的通知。警报由规则定义，该规则描述要监视的度量值查询、阈值以及超过阈值时要执行的操作和一个或多个通知方法。  

下表列出了可用于处理警报的不同方法和支持的操作：

<table>
  <caption>处理警报的方法</caption>
	<tr>
    <th>方法</th>
		<th>定义警报</th>
		<th>更新警报</th>
		<th>删除警报</th>
	</tr>
	<tr>
    <td>警报 API</td>
		<td>是</td>
		<td>是</td>
		<td>是</td>
	</tr>
	<tr>
    <td>Grafana</td>
		<td>是</td>
		<td>是</td>
		<td>是</td>
	</tr>
</table>

**注：**使用警报 API 定义的警报不会显示在 Grafana 仪表板中。


下图显示了可在 {{site.data.keyword.monitoringshort}} 服务中配置警报的不同通知类型：

![{{site.data.keyword.monitoringlong}} 服务中可用通知类型的高级别组件概览图](images/alerts_ov_f1.gif)

您可以为一个实例或多个实例定义警报。通过警报规则监视的查询包含通配符时，通配符标识多个目标（即，多个服务实例或应用程序实例）。{{site.data.keyword.monitoringshort}} 服务每 5 分钟运行一次警报规则中配置的查询，并检查针对每个实例或多个实例返回的最后一个数据点。{{site.data.keyword.monitoringshort}} 服务跟踪每个实例的最后状态，并在警报状态发生更改时生成新的警报。 



## 使用警报 API 处理警报
{: #api}

您可以使用警报 API 来定义、更新或删除警报。

要使用警报 API 针对度量值查询定义警报，必须执行以下操作：

1. 在 Grafana 仪表板上定义一个或多个度量值查询。 

    **注：**无法在使用模板变量的 Grafana 仪表板上定义警报。

2. 针对在 Grafana 仪表板上定义的度量值查询配置警报。

    * [配置用于发送电子邮件的警报](/docs/services/cloud-monitoring/alerts/configure_email_alert.html#configure_email_alert)。
    * [配置用于发送 PagerDuty 通知的警报](/docs/services/cloud-monitoring/alerts/configure_pagerduty_alert.html#configure_pagerduty_alert)。
    * [配置用于发送 Webhook 通知的警报](/docs/services/cloud-monitoring/alerts/configure_webhook_alert.html#configure_webhook_alert)。

    **注：**您只能为在帐户度量值域中定义的度量值查询定义电子邮件通知。



## 使用 Grafana 处理警报
{: #grafana}

可以直接在 Grafana 仪表板上定义和删除警报。您还可以更新规则定义。但是，任何通知通道更改都必须使用警报 API 完成。

在 Grafana 中处理警报时，请考虑以下信息：

* 要修改分配给规则的通知通道，必须使用警报 API。
* 删除空间域中的通知通道时，不会更新配置了该通道的规则。必须使用警报 API 来修改规则并从中除去该通知通道。 

要在 Grafana 仪表板上直接针对度量值查询定义警报，必须执行以下操作：

1. 在 Grafana 仪表板上定义一个或多个度量值查询。 

    **注：**无法在使用模板变量的 Grafana 仪表板上定义警报。

2. 针对在 Grafana 仪表板上定义的度量值查询配置警报。

    有关更多信息，请参阅[在 Grafana 中配置警报](/docs/services/cloud-monitoring/alerts/config_alerts_grafana.html#config_alerts_grafana)。


## 警报状态
{: #status}

启用规则后，警报可以具有以下任何状态：

* *OK*：以下情况下规则的状态设置为 *OK*：
    
	* {{site.data.keyword.monitoringshort}} 服务中提供了与该规则关联的度量值查询的数据。您已设置警告阈值和错误阈值。数据的值不会超过阈值。
	 
	* {{site.data.keyword.monitoringshort}} 服务中没有与该规则关联的度量值查询的数据，并且您将规则属性 `allow_no_data` 配置为 *true*。           
	 
* *WARNING*：当 {{site.data.keyword.monitoringshort}} 服务中提供了与该规则关联的度量值查询的数据时，该规则的状态会设置为 *WARNING*。您已设置警告阈值和错误阈值。数据的值在警告阈值和错误阈值之间。
	
* *ERROR*：当 {{site.data.keyword.monitoringshort}} 服务中提供了与该规则关联的度量值查询的数据时，该规则的状态会设置为 *ERROR*。您已设置警告阈值和错误阈值。数据的值达到错误阈值。  

* *UNKNOWN*：当 {{site.data.keyword.monitoringshort}} 服务中没有与该规则关联的度量值查询的数据时，该规则的状态会设置为 *UNKNOWN*。您可以配置是接收通知还是不基于您为规则配置的属性 `allow_no_data`。如果将此属性设置为 `false`，那么将通知您找不到该规则的任何数据。



	
## 警报历史记录
{: #history}

每次警报状态更改时，都会更新警报的历史记录。可以使用警报 API (*/v1/alert/history*) 来检索有关度量值历史记录的信息。

警报的状态用于定义以下任一场景中的状态：

* 规则触发通知之前的查询状态。
* 规则触发之后的查询状态。 

例如，如果超过了警告阈值，那么会生成一条历史记录，用于记录状态从 *OK* 转换为 *WARNING*。与此类似，当值恢复到低于阈值时，也会生成一条历史记录，用于记录状态从 *WARNING* 转换为 *OK*。

有关更多信息，请参阅[检索规则的历史记录](/docs/services/cloud-monitoring/alerts/retrieve_history.html#retrieve_history)。


## 规则
{: #rules1}

规则描述要监视的度量值查询、阈值以及超过阈值时要执行的操作。 

* 可以使用警报 API 创建、删除、更新规则，显示规则的详细信息，以及列出所有规则。有关更多信息，请参阅[使用规则](/docs/services/cloud-monitoring/alerts/rules.html#rules)。

    * 要创建规则，请参阅[创建规则](/docs/services/cloud-monitoring/alerts/rules.html#create)。
	* 要删除规则，请参阅[删除规则](/docs/services/cloud-monitoring/alerts/rules.html#delete)。
	* 要更新规则，请参阅[更新规则](/docs/services/cloud-monitoring/alerts/rules.html#update)。
	* 要列出所有规则，请参阅[列出所有规则](/docs/services/cloud-monitoring/alerts/rules.html#list)。
	* 要显示有关规则的信息，请参阅[显示规则的详细信息](/docs/services/cloud-monitoring/alerts/rules.html#showing-the-details-of-a-rule)。

* 警报系统每 5 分钟检查一次在空间中启用的规则。

* 缺省情况下，创建规则时就会启用该规则。但是，您可以定义该规则，并通过将字段 *enable* 配置为 `false` 来将其禁用。

* 当规则参数 *comparison* 设置为 below 时，error_level 值必须低于警告级别值。当规则参数 *comparison* 设置为 above 时，error_level 值应高于警告级别值。

* 缺省情况下，创建规则时字段 *allow_no_data* 会设置为 `true`。如果没有数据点可用，那么除非触发规则条件，否则不会发送通知。如果您想要接收关于找不到规则 X 的任何数据的通知，必须将字段 *allow_no_data* 设置为 `false`。 

**提示：**通过 Grafana 中的警报规则验证您监视的查询。检查该查询是否不会超时。例如，如果配置的时间段很长或者定义了包含通配符的查询，那么查询可能会超时。请注意，如果查询在 Grafana 中超时，就不会触发为该查询配置的警报。

下面是定义规则时所必需的字段：

<table>
  <caption>表 1. 用于定义规则的字段的列表。</caption>
  <tr>
    <th>字段名称</th>
	<th>描述</th>
  </tr>
  <tr>
    <td>name</td>
	<td>规则的名称。此名称必须唯一。</td>
  </tr>
  <tr>
    <td>description</td>
	<td>规则汇总。</td>
  </tr>
  <tr>
    <td>expression</td>
	<td>要监视并在超过阈值时发送警报的度量值查询。<br>有效表达式为：单个度量值名称、使用通配符标识的多个度量值或用于汇总数据的函数。<br>**提示**：可以从 Grafana 复制已验证的查询。</td>
  </tr>
  <tr>
    <td>enabled</td>
	<td>描述规则的状态：<br>设置为 `true` 可启用规则。<br>设置为 `false` 可禁用规则。<br>缺省情况下，它会设置为 `true`。</td>
  </tr>
  <tr>
    <td>from</td>
	<td>用于根据您为 expression 字段中所定义查询设置的阈值来分析数据的初始时间点。例如：`"from": "-5min"`</td>
  </tr>
  <tr>
    <td>until</td>
	<td>用于根据您为 expression 字段中所定义查询设置的阈值来分析数据的结束时间点。例如：`"until": "now"`</td>
  </tr>
  <tr>
    <td>comparison</td>
	<td>用于识别要执行哪种类型检查的比较操作。有效值为：*below* 和 *above*。</td>
  </tr>
  <tr>
    <td>comparison_scope</td>
	<td>定义要分析的数据的范围。<br>设置为 *last* 可查看序列（可用于查询的数据）中的最后一个值。</td>
  </tr>
  <tr>
    <td>error_level</td>
	<td>定义用于触发错误警报的阈值。<br>达到所设置的值时，就会生成错误警报。例如：`"error_level" : 27.94`</td>
  </tr>
  <tr>
    <td>warning_level</td>
	<td>定义用于触发警告警报的阈值。<br>达到所设置的值时，就会生成警告警报。例如：`"warning_level" : 24`</td>
  </tr>
  <tr>
    <td>frequency</td>
	<td>定义执行检查的频率。<br>它以分钟、小时或天为单位，例如，5 分钟、1 小时、7 天。<br>例如，要每分钟进行检查，可以设置 `"frequency": "1min"`。<br>**注：**目前，频率固定为 5 分钟。</td>
  </tr>
  <tr>
    <td>dashboard_url</td>
	<td>定义 Grafana 仪表板的 URL，在此仪表板中定义了受监视查询。</td>
  </tr>
    <tr>
    <td>allow_no_data</td>
	<td>定义在无数据点可用时发送通知的条件。<br>缺省情况下，它会设置为 `true`。<br>如果要在找不到规则 X 的任何数据时接收通知，请设置为 `false`。</td>
  </tr>
  <tr>
    <td>notifications</td>
	<td>通知的名称，该通知定义要针对规则触发的操作。<br>**注：**您可以通过列出以逗号分隔的通知名称，为每个规则定义一个或多个通知。</td>
  </tr>
</table>

例如，下面是规则样本：

```
{
  "name": "checkbytesin1",
  "description": "MH check Bytes In per second",
  "expression": "movingAverage(messagehub.65ad9211-1234-5678-a751-c82123411eee.1.kafka-java-console-sa
mple-topic.BytesInPerSec.15MinuteRate,\"5min\")",
  "enabled": true,
  "from": "-5min",
  "until": "now",
  "comparison": "below",
  "comparison_scope": "last",
   "error_level" : 22.94,
   "warning_level" : 25,
  "frequency": "1min",
  "dashboard_url": "https://metrics.ng.bluemix.net",
  "notifications": [
    "emailXXX"
  ]
}
```
{: screen}



## 通知
{: #alert_notifications}

通知描述在触发警报时用于进行通知的方法和详细信息。例如，要获取度量值的警告通知和错误通知，请定义一个规则用于监视警告阈值，再定义一个规则用于监视错误阈值。 

* 仅当警报的状态更改（例如，度量值警报的状态从“OK”更改为“ERROR”，或从“ERROR”更改为“WARNING”）时，才会发送通知。 

    **注：**如果警报规则保持在相同的状态（*OK*、*WARNING*、*ERROR* 或 *UNKNOWN*），那么将不会在下一次迭代时重新触发该警报规则。

* 通知被视为 24 小时事件。可以触发通知时，不能指定时间间隔。

* 您可以通过列出以逗号分隔的通知名称，为每个规则配置一个或多个通知方法。 

* 可以使用[警报 REST API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window} 来创建、删除和更新通知，显示通知的详细信息，以及列出空间中定义的通知。

    * 要创建通知，请参阅[创建通知](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create)。
	* 要删除通知，请参阅[删除通知](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_delete)。
	* 要更新通知，请参阅[更新通知](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_update)。
	* 要列出所有通知，请参阅[列出所有通知](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_list)。
	* 要显示有关通知的信息，请参阅[显示通知的详细信息](/docs/services/cloud-monitoring/alerts/notifications.html#show)。

* 您可以配置电子邮件通知、PagerDuty 配置和 Webhook 通知。 

**注**：您可独立于规则定义警报通知，这样就能将通知复用于多个规则。

	
## 通知 - JSON 模板
{: #notification_template}
	
通知是一个 JSON 文件。 

下表包含通知方法类型的通知模板：

<table>
  <caption>表 3. 通知模板</caption>
  <tr>
    <th>类型</th>
	<th>模板</th>
	<th>样本</th>
  </tr>
  <tr>
    <td>Email</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Email",
	"description" : "Description",
	"detail": "EmailAddress"
	}
	```
	{: screen}
	</td>
	<td>
	```
	{
	"name": "my-email",
	"type": "Email",
	"description" : "Send email notification when there is an infrastructure problem.",
	"detail": "xxx@yyy.com"
	}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>Webhook</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Webhook",
	"description" : "Description",
	"detail": "Endpoint"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-webhook",
	"type": "Webhook",
	"description" : "Fire a webhook when there is an infrastructure problem..",
	"detail": "https://myendpoint.bluemix.net?key=abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>Pagerduty</td>
	<td>
	```
	"name": "Template_Name",
	"type": "PagerDuty",
	"description" : "Description",
	"detail": "Pagerduty_APIkey"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-pagerduty",
	"type": "PagerDuty",
	"description" : "Fire a PagerDuty alert when there is an infrastructure problem..",
	"detail": "abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
</table>

其中

* *Template_Name* 定义通知模板的名称。
* *Description* 说明何时使用此类型的通知。
* *EmailAddress* 定义通知接收方的电子邮件地址。
* *Endpoint* 定义应该执行 POST 操作的 URL。 
* *Pagerduty_APIkey* 定义唯一 API 密钥。此 API 密钥由 PagerDuty 帐户管理员或所有者生成。



## 规则 - JSON 模板
{: #rules_template}

通过使用 JSON 文件来描述规则。 

以下代码是规则的模板：

```
{
"name": "Enter rule name",
"description": "Desccribe rule",
"expression": "Add metric query",
"enabled": true,
"from": "-5min",
"until": "now",
"comparison": "below",
"comparison_scope": "last",
"error_level" : xxxx,
"warning_level" : xxxx,
"frequency": "1min",
"dashboard_url": "https://metrics.ng.bluemix.net",
"notifications": [
 "List of Notifications by name. Include all the motification methods for this rule separated by commas."
 ]
}
```
{: screen}



