---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# 使用通知通道
{: #notifications}

配置触发警报时要通知的通知通道。您可以通过 Web UI 中的*设置*面板来管理通知通道。
{:shortdesc}
 

## 配置通知通道
{: #notifications_create}

要添加通知通道，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**设置**。

3. 选择**通知通道**。

4. 单击**我的通道** ![“添加”图标](../images/add.png)。然后，选择通道。

    **注：**第一次配置通知通道时，请单击任一通道。

5. 配置通知通道：

    * 输入通道的名称。

    * 启用*正常时通知*字段可在不再触发警报条件时接收通知。

    * 启用*解决时通知*字段可在用户手动解决警报时接收通知。

    * 对于**电子邮件**通知通道，请添加以逗号分隔的收件人列表。

    * 对于 **Slack** 通知通道，请添加 *Slack 通道*的名称。

    * 对于 **Webhook** 通知通道，请添加 *Webhook URL*。**注：**触发警报时，通知会以 JSON 格式通过 POST 操作发送到 Webhook 端点。有关更多信息，请参阅 [Configure a Webhook Channel ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}。例如，Sysdig 可以使用定制 Webhook 与 ServiceNow 集成。要了解有关配置 Sysdig 以使用 ServiceNow 的信息，请参阅 [Configure ServiceNow ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}。

    * 对于 **VictorOps** 通知通道，请添加 *API 密钥*和*路由密钥*。

    * 对于 **OpsGenie** 通知通道，请添加 *OpsGenie API 密钥*。请注意，您必须在 OpsGenie 中配置与 Sysdig 的集成。有关更多信息，请参阅 [Add Sysdig Cloud Integration in Opsgenie ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}。

    * 对于 **PagerDuty** 通知通道，首先必须授权 Sysdig 与您的帐户相集成。选择 PagerDuty 时，会打开一个向导用于配置与 Sysdig 的集成。单击**授权集成**或**使用身份提供者登录**以对 PagerDuty 授权。为 Sysdig 通知选择现有服务或设置新服务，然后单击**完成集成**。选择要用于 Sysdig 事件的升级策略。然后，在*通知*选项卡上，确认您的 PagerDuty 帐户、服务名称和服务密钥。 

    * （可选）对于允许测试的集成，请启用*测试通知*条件以接收测试通知。如果 10 分钟内未收到测试通知，请查看通道配置。 

6. 单击**创建通道**。 



## 修改通知通道
{: #notifications_update}

要修改通知通道，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**设置**。

3. 选择**通知通道**。

4. 确定要修改的目标通道，然后单击**编辑**。

5. 进行更改后，单击**保存更改**。



## 测试通知通道
{: #notifications_test}

要测试通知通道，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**设置**。

3. 选择**通知通道**。

4. 确定要测试的目标通道，然后单击**测试**。



## 禁用通知通道
{: #notifications_disable}

要临时禁用通知通道，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**设置**。

3. 选择**通知通道**。

4. 在*通知*部分中，启用*暂休*以临时禁用警报并使所有通知静音。

## 删除通知通道
{: #notifications_delete}

要删除通知通道，请完成以下步骤：

1. 启动 Web UI。有关如何启动 Web UI 的更多信息，请参阅[导航至 Web UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
    
2. 通过导航栏中的*选择器*按钮，选择**设置**。

3. 选择**通知通道**。

4. 确定要修改的目标通道，然后单击**编辑**。

5. 单击**删除通道**。

6. 确认删除通道。单击**保存更改**。




