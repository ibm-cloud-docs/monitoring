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


# 获取 IAM 令牌
{: #auth_iam}

使用 {{site.data.keyword.Bluemix}} IAM 模型来获取可用于处理 {{site.data.keyword.monitoringshort}} 服务的认证令牌。可以使用 {{site.data.keyword.Bluemix_notm}} CLI 来获取认证令牌。
{:shortdesc}

该令牌有到期时间。 

## 使用 IBM Cloud CLI 获取 IAM 令牌 
{: #iam_token_cli}

要使用 {{site.data.keyword.Bluemix_notm}} CLI 获取授权令牌，请完成以下步骤：

1. （先决条件）安装 {{site.data.keyword.Bluemix_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa)。
   
   如果 CLI 已安装，请继续执行下一步。
    
2. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。
	
3. 运行 `ibmcloud iam oauth-tokens` 命令来获取 IAM 令牌。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	输出返回 IAM 令牌。



**注：**使用令牌时，请从 API 调用中传递的令牌的值中除去 *Bearer*。
		



	

	
	
	
	
	
	
