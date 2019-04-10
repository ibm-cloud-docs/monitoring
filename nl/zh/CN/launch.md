---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# 导航至 Web UI
{: #launch}

在 {{site.data.keyword.Bluemix}} 中供应 {{site.data.keyword.mon_full_notm}} 服务的实例，并为度量源配置了 Sysdig 代理程序后，可以通过 {{site.data.keyword.mon_full_notm}} Web UI 来查看、监视和管理度量值。
{:shortdesc}


## 向用户授予 IAM 策略以查看数据 
{: #launch_step1}

**注：**您必须是 {{site.data.keyword.mon_full_notm}} 服务的管理员、{{site.data.keyword.mon_full_notm}} 实例的管理员或具有帐户 IAM 许可权，才能向其他用户授予策略。

下表列出了用户必须拥有才能启动 {{site.data.keyword.mon_full_notm}} Web UI 和查看数据的最低策略：

|服务|角色|授予的许可权
|
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` |平台角色：查看者|允许用户在“可观察性监视”仪表板中查看服务实例的列表。|
| `{{site.data.keyword.mon_full_notm}}` |服务角色：写入者|允许用户启动 Web UI 并在 Web UI 中查看度量值。|
{: caption="表 1. IAM 策略" caption-side="top"} 

有关如何为用户配置这些策略的更多信息，请参阅[向用户授予查看度量值的许可权](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig)。


## 通过 {{site.data.keyword.cloud_notm}} UI 启动 Web UI
{: #launch_step2}

通过 {{site.data.keyword.cloud_notm}} UI，在 {{site.data.keyword.mon_full_notm}} 实例的上下文中启动 Web UI。 

要启动 Web UI，请完成以下步骤：

1. 登录到 {{site.data.keyword.cloud_notm}} 帐户。

    单击 [{{site.data.keyword.cloud_notm}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/login){:new_window} 以启动 {{site.data.keyword.cloud_notm}}“仪表板”。

	使用用户标识和密码登录后，{{site.data.keyword.cloud_notm}}“仪表板”将打开。

2. 在导航菜单中，选择**可观察性**。 

3. 选择**监视**。 

    这将显示 {{site.data.keyword.cloud_notm}} 上可用的实例的列表。

4. 选择一个实例。然后，单击**查看 Sysdig**。

这将打开 Web UI。


