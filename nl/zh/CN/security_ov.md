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


# 安全性
{: #security_ov}

要控制允许用户执行的 {{site.data.keyword.monitoringshort}} 服务操作，您可以向用户分配一个或多个角色。要认证用户以处理度量值和警报，可以使用 UAA 令牌、IAM 令牌或 API 密钥。
{:shortdesc}





## 认证模型
{: #auth}

要使用在 {{site.data.keyword.monitoringshort}} 服务中为空间存储的度量值，您需要认证令牌或 API 密钥。 

要获取安全性令牌，请参阅：

* [获取 UAA 令牌](/docs/services/cloud-monitoring/security/auth_uaa.html#auth_uaa)
* [获取 IAM 令牌](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)

要获取 API 密钥，请参阅[生成 API 密钥](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。如果 API 密钥已损坏，可以通过删除 API 密钥来将其撤销。然后，您可以重新创建一个新的 API 密钥。有关更多信息，请参阅[使用 {{site.data.keyword.Bluemix_notm}} UI 撤销 API 密钥](/docs/services/cloud-monitoring/security/auth_api_key.html#revoke_ui)。 

UAA 令牌和 IAM 令牌在一段时间后到期。API 密钥不会到期。
 

下表列出了每种类型的域支持的安全性模型：

<table>
  <caption>表 1. 每个域支持的安全性模型</caption>
  <tr>
    <th></th>
	<th align="right">帐户</th>
    <th align="right">组织</th>
    <th align="right">空间</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">否</td>
	<td align="center">是</td>
	<td align="center">是</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">是</td>
	<td align="center">是</td>
	<td align="center">是</td>
  </tr>
</table>

{{site.data.keyword.monitoringshort}} 服务使用 IAM 访问控制功能来管理用户或服务可以对域执行的操作。例如，可以定义 IAM 策略以允许用户针对域发送和创建仪表板，但不允许用户检索域中的度量值。



## Cloud Foundry 角色
{: #bmx_roles}

下表列出了使用 {{site.data.keyword.monitoringshort}} 服务的每个 Cloud Foundry 角色的特权：

<table>
  <caption>表 2. 使用 {{site.data.keyword.monitoringshort}} 服务的 Cloud Foundry 角色和特权。</caption>
  <tr>
    <th>角色</th>
	<th>域</th>
	<th>访问特权</th>
  </tr>
  <tr>
    <td>管理者</td>
	<td>组织<br>空间</td>
	<td>所有 RESTful API</td>
  </tr>
  <tr>
    <td>开发者</td>
	<td>空间</td>
	<td>所有 RESTful API</td>
  </tr>
  <tr>
    <td>审计员</td>
	<td>组织<br>空间</td>
	<td>仅限执行只读操作（如查询度量值）的 RESTful API。</td>
  </tr>
</table>

有关在 UI 中分配用户角色的信息，请参阅[管理 Cloud Foundry 访问权](/docs/iam/mngcf.html#mngcf)。



## IAM 角色
{: #iam_roles}

下表列出了在处理度量值和向用户授予许可权的 IAM 角色执行来这些任务时的 {{site.data.keyword.monitoringshort}} 服务操作：

<table>
  <caption>表 3. 处理度量值</caption>
  <tr>
	<th>操作</th>
	<th>IAM 角色</th>
  </tr>
  <tr>
    <td>向域发送度量值</td>
	<td>管理员、编辑者和操作员</td>
  </tr>
  <tr>
    <td>检索/查询度量值</td>
	<td>管理员、编辑者和查看者</td>
  </tr>
  <tr>
    <td>在域中搜索度量值</td>
	<td>管理员和编辑者</td>
  </tr>
</table>

下表列出了在使用警报和向用户授予许可权的 IAM 角色执行来这些任务时的 {{site.data.keyword.monitoringshort}} 服务操作：

<table>
  <caption>表 4. 处理警报。</caption>
  <tr>
	<th>操作</th>
	<th>IAM 角色</th>
  </tr>
  <tr>
    <td>创建、编辑和删除警报规则</td>
	<td>管理员和编辑者</td>
  </tr>
  <tr>
    <td>查看警报</td>
	<td>管理员、编辑者和查看者</td>
  </tr>
  <tr>
    <td>创建、编辑和删除警报通知</td>
	<td>管理员和编辑者</td>
  </tr>
  <tr>
    <td>查看通知</td>
	<td>管理员、编辑者和查看者</td>
  </tr>
  <tr>
    <td>查看已触发的警报历史记录</td>
	<td>管理员、编辑者和查看者</td>
  </tr>
</table>

有关在 UI 中分配用户角色的信息，请参阅[管理 IAM 访问权](/docs/iam/mngiam.html#iammanidaccser)。

