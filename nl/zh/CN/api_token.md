---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, api token

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


# 使用 API 令牌
{: #api_token}

通过 Python 脚本或 Sysdig REST API 来自动执行例程任务和监视通知时，请使用 API 令牌向 {{site.data.keyword.mon_full_notm}} 服务进行认证。
{:shortdesc}

请考虑 {{site.data.keyword.mon_full_notm}} 服务的每个实例的以下信息：

* 每个团队都有一个 API 令牌。
* 如果令牌泄漏或组织的安全策略需要在特定条件后重置令牌，那么具有管理许可权的用户可以重置 API 令牌。


## 获取 Sysdig API 令牌
{: #api_token_get}


要获取令牌，请完成以下步骤：

1. 通过导航栏中的*选择器*按钮，选择**设置**。
2. 在 *Sysdig 监视 API* 部分中，复制 **Sysdig 监视 API 令牌**。

## 重置 Sysdig API 令牌
{: #api_token_reset}

要获取令牌，请完成以下步骤：

1. 通过导航栏中的*选择器*按钮，选择**设置**。
2. 在 *Sysdig 监视 API* 部分中，单击**重置令牌**以重置 API 令牌。
