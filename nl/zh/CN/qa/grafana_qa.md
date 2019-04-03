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



# 使用 Grafana 的常见问题
{: #grafana_qa}

下面是对将 Grafana 与 {{site.data.keyword.monitoringshort}} 服务一起使用时的常见问题的解答。
{:shortdesc}

* [在 Grafana 仪表板中无法查看已使用警报 API 定义的警报](/docs/services/cloud-monitoring/qa/grafana_qa.html#alerts1)
* [尝试保存对 Grafana 仪表板所做更改时收到 BXNMSAL41E](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL41E)
* [在向 Grafana 仪表板添加警报后尝试保存更改时收到 BXNMSAL36E](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL36E)
* [登录到 Monitoring 服务 Web UI 时收到 404](/docs/services/cloud-monitoring/qa/grafana_qa.html#404)
* [我刚上传了 Grafana 仪表板的 JSON 数据，为什么滚动条不见了？](/docs/services/cloud-monitoring/qa/grafana_qa.html#2)


## 在 Grafana 仪表板中无法查看已使用警报 API 定义的警报
{: #alerts1}

使用警报 API 定义的警报不会显示在 Grafana 中的“警报”选项卡中。要在 Grafana 中查看警报，您必须直接在 Grafana 仪表板中定义警报。

有关更多信息，请参阅[在 Grafana 中配置警报](/docs/services/cloud-monitoring/alerts/config_alerts_grafana.html#config_alerts_grafana)。

## 尝试保存对 Grafana 仪表板所做更改时收到 BXNMSAL41E
{: #BXNMSAL41E}

您可以在 Grafana 中定义通知通道和警报。如果在 Grafana 中删除了通知通道，但未更新规则以除去该通知通道，那么尝试保存 Grafana 仪表板时，会收到 **BXNMSAL41E** 错误。

要解决该问题，请使用警报 API 来更新规则，然后重试保存仪表板。更新规则时，请除去已删除的通知通道。

有关更多信息，请参阅[警报 API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction)。

## 在向 Grafana 仪表板添加警报后尝试保存更改时收到 BXNMSAL36E
{: #BXNMSAL36E}

如果在 {{site.data.keyword.monitoringshort}} 服务中监视度量值时达到域的配额，会收到以下错误：**BXNMSAL36E**

请升级您的套餐，然后重试。

有关如何升级套餐的更多信息，请参阅[更改套餐](/docs/services/cloud-monitoring/plan/change_plan.html#change_plan)。


## 使用 UAA 认证模型登录到 Monitoring 服务 Web UI 时收到 404
{: #404}

如果尝试登录到 {{site.data.keyword.monitoringshort}} 服务 Web UI (Grafana) 时收到 404，请检查空间是否存在，以及您是否有权访问该空间。

使用 [UAA 认证模型](/docs/services/cloud-monitoring/security/auth_uaa.html#auth_uaa)来访问 {{site.data.keyword.monitoringshort}} 服务时，必须使用登录到 {{site.data.keyword.Bluemix_notm}} 控制台时所用的相同用户标识和密码。 

要验证您是否有权访问要登录到的帐户、组织和空间，请登录到 {{site.data.keyword.Bluemix_notm}} 控制台并切换到该空间。 

还可以使用命令行来验证您是否有权访问该空间。运行以下命令来登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间：

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

遵循指示信息进行操作。输入您的 {{site.data.keyword.Bluemix_notm}} 凭证，然后选择组织和空间。


## 我刚上传了 Grafana 仪表板的 JSON 数据，为什么滚动条不见了？
{: #2}

这是 Grafana 中的一个错误，它会在导入仪表板后隐藏滚动条。 

要显示滚动条，请在导入仪表板后保存该仪表板。 








