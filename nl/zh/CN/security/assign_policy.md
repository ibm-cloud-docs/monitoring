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


# 授予用户许可权
{: #grant_permissions}

在 {{site.data.keyword.Bluemix}} 中，您可以向用户分配一个或多个角色。这些角色会定义为该用户启用哪些任务，以使用 {{site.data.keyword.monitoringshort}} 服务。
{:shortdesc}

要为用户授予使用度量值的许可权，您必须为该用户添加一个策略，该策略描述此用户可在帐户中对 {{site.data.keyword.monitoringshort}} 服务执行的操作。只有帐户所有者可以向用户分配个别策略。


## 通过 IBM Cloud UI 向用户分配 IAM 策略 
{: #assign_policy_ui}

完成以下步骤以授予用户使用 {{site.data.keyword.monitoringshort}} 服务的许可权：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。


    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://console.bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 从菜单栏中，单击**管理 > 帐户 > 用户**。 

    *用户*窗口将显示一个用户列表，其中包含当前选定帐户的电子邮件地址。
	
3. 如果用户是帐户的成员，请从列表中选择用户名，或从*操作*菜单中单击**管理用户**。

    如果用户不是帐户的成员，请参阅[邀请用户](/docs/iam?topic=iam-iamuserinv#iamuserinv)。

4. 单击**分配服务策略**。

5. 输入有关策略的信息。下表列出了定义策略所需的字段或可选字段： 

    <table>
	  <caption>用于配置 IAM 策略的字段列表。</caption>
	  <tr>
	    <th>字段</th>
		<th>值</th>
		<th>状态</th>
	  </tr>
	  <tr>
	    <td>服务</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>必需</td>
	  </tr>
	  <tr>
	    <td>角色</td>
		<td>选择一个或多个 IAM 角色。<br>有效角色为：*管理员*、*操作员*、*编辑者*和*查看者*。<br>有关每个角色允许的操作的更多信息，请参阅 [IAM 角色](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#iam_roles)。</td>
		<td>必需</td>
	  </tr>
	  <tr>
	    <td>区域</td>
		<td>您可以指定将授予用户对使用度量值的访问权的区域。选择**指定可选服务上下文**。然后，单独添加一个或多个区域，或选择**所有当前区域**以授予对所有区域的访问权。</td>
		<td>可选</td>
	  </tr>
	</table>
	
6. 单击**分配策略**。
	
您配置的策略适用于所选区域。
 

## 使用命令行向用户分配 IAM 策略
{: #assign_policy_commandline}

完成以下步骤以通过使用命令行授予用户查看度量值的访问权：

1. （先决条件）安装 {{site.data.keyword.Bluemix_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)。
   
   如果 CLI 已安装，请继续执行下一步。
	
2. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。
	
3. 获取帐户标识。 

    运行以下命令，以获取帐户标识：

    

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	这将显示帐户及其 GUID 的列表。
	
	导出计划向用户授予许可权的帐户的标识。配置 shell 变量（如 `$acct_id`），例如：

	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. 获取要向其授予许可权的用户的 {{site.data.keyword.IBM_notm}} 标识。

    1. 显示与帐户关联的用户。运行以下命令：
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. 获取用户的 GUID。**注：此步骤必须由您计划向其授予许可权的用户完成。**
	
	    例如，请求用户运行以下命令以获取其用户标识：


		
		获取 IAM 令牌。有关更多信息，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli)。

        从 IAM 令牌的前两个点之间的 IAM 令牌获取数据。将数据导出到 shell 变量，例如，`$user_data`。 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		例如，运行以下命令，以获取用户标识。此命令在此样本中使用 jq，将信息编码到 JSON 格式的文本中：
		
		
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		运行此命令的输出如下：
		
		
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		将用户标识（即 *id* 字段的值）发送给帐户所有者。 
		
	3. 将用户标识导出到 shell 变量，例如 `$user_ibm_id`。
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. 如果用户尚未成为成员，请邀请用户加入帐户。有关更多信息，请参阅[邀请用户](/docs/iam?topic=iam-iamuserinv#iamuserinv)。

    例如，运行以下命令以邀请用户 xxx@yyy.com 加入帐户 zzz@ggg.com：
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. 创建策略文件名。 

    例如，使用以下模板在美国南部区域授予查看许可权：
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	将策略文件命名为：`policy.json`
	
5. 获取您用户标识的 IAM 令牌。

    有关更多信息，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli)。

    将 IAM 令牌导出到 shell 变量（如 `$iam_token`），例如：
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. 授予用户使用 {{site.data.keyword.monitoringshort}} 服务的许可权。 

   运行以下 cURL 命令以在美国南部区域授予许可权：
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	运行以下 cURL 命令以在英国区域授予许可权：


	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## 通过 IBM Cloud UI 向用户授予 CF 角色 
{: #grant_permissions_ui_space}


要使用空间域或组织域中的度量值，用户必须具有在 {{site.data.keyword.Bluemix_notm}} 中分配的 Cloud Foundry (CF) 角色。CF 角色描述用户可以对空间或组织中的 {{site.data.keyword.monitoringshort}} 服务执行的操作。
 

完成以下步骤以授予用户使用 {{site.data.keyword.monitoringshort}} 服务的许可权：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。


    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}}“仪表板”：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 从菜单栏中，单击**管理 > 帐户 > 用户**。 

    *用户*窗口将显示一个用户列表，其中包含当前选定帐户的电子邮件地址。
	
3. 如果用户是帐户的成员，请从列表中选择用户名，或从*操作*菜单中单击**管理用户**。

    如果用户不是帐户的成员，请参阅[邀请用户](/docs/iam?topic=iam-iamuserinv#iamuserinv)。

4. 单击**分配组织**。

5. 输入有关策略的信息。下表列出了定义策略所需的字段或可选字段： 

    <table>
	  <caption>用于配置 CF 策略的字段列表。</caption>
	  <tr>
	    <th>字段</th>
		<th>值</th>
	  </tr>
	  <tr>
	    <td>组织</td>
		<td>从列表中选择一个组织。</td>
	  </tr>
	  <tr>
	    <td>组织角色</td>
		<td>选择**无组织角色**。但是，如果用户具有组织角色，请从列表中选择组织角色。<br>有效值为：**记帐管理者**、**审计员**、**管理者**</td>
	  </tr>
	  <tr>
	    <td>区域</td>
		<td>从列表中选择一个区域。<br>有效值为：**所有当前区域**、**美国南部**、**英国**</td>
	  </tr>
	  <tr>
	    <td>空间</td>
		<td>缺省情况下，当*区域*字段设置为**所有当前区域**时，会预定义**所有当前空间**。要授予个别空间的许可权，请选择特定区域，然后从列表中选择一个空间。</td>
	  </tr>
	  <tr>
	    <td>空间角色</td>
		<td>从列表中选择一个空间角色。<br>有效值为：**管理者**、**审计员**、**开发者**和**无空间角色**。有关更多信息，请参阅 [Cloud Foundry 角色](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#bmx_roles)。</td>
	  </tr>
	</table>
	
6. 单击**分配策略**。
	
您配置的策略适用于所选区域。
 


