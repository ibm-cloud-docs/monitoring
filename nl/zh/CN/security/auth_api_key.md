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


# 使用 API 密钥
{: #auth_api_key}

您可以使用 {{site.data.keyword.Bluemix}} CLI 或 {{site.data.keyword.Bluemix_notm}} UI 来获取 API。API 密钥不会到期。
如果 API 已遭到破坏，那么您可以将其撤销，然后生成一个新的 API。
{:shortdesc}

## 使用 IBM Cloud CLI 生成 IAM API 密钥
{: #iam_apikey_cli}

完成以下步骤，以使用 {{site.data.keyword.Bluemix_notm}} CLI 生成 API 密钥：

1. （先决条件）安装 {{site.data.keyword.Bluemix_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa)。
   
   如果 CLI 已安装，请继续执行下一步。
	
2. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。
 
3. 运行 `ibmcloud iam api-key-create` 命令来创建 API 密钥。

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	其中
	
	* NAME 是要创建的 API 密钥的名称。
	* DESCRIPTION 是用于描述 API 密钥的文本。
	* FILE 是保存密钥的文件的名称。
	
    例如，要创建 API 密钥 *MyKey*，请运行以下命令：
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## 使用 IBM Cloud UI 生成 IAM API 密钥
{: #iam_apikey_ui}

要通过 {{site.data.keyword.Bluemix_notm}} UI 生成 API 密钥，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。


    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://console.bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 在控制台菜单栏中，单击**管理 > 安全性 > IBM Cloud API 密钥**。

3. 单击**创建 API 密钥**。

4. 为 API 密钥输入名称和描述。然后，单击**创建 API 密钥**。

5. 保存 API 密钥。单击**下载 API 密钥**。

    单击**显示**以显示 API 密钥。  

**注：**API 密钥仅在创建时才可显示或下载。如果 API 密钥丢失，必须创建新的 API 密钥。


  


	
## 使用 IBM Cloud UI 撤销 API 密钥
{: #revoke_ui}
	
要通过 {{site.data.keyword.Bluemix_notm}} UI 撤销 IAM API 密钥，请完成以下步骤：



1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。


    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://console.bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 在控制台菜单栏中，单击**管理 > 安全性 > IBM Cloud API 密钥**。

3. 单击**操作**，然后单击**删除密钥**。





	

	
	
	
	
	
	
