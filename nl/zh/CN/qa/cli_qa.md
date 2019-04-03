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



# 使用 IBM Cloud CLI 的常见问题
{: #cli_qa}

下面是对将 {{site.data.keyword.Bluemix}} CLI 与 {{site.data.keyword.monitoringshort}} 服务一起使用时的常见问题的解答。
{:shortdesc}

* [如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)
* [如何安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa/cli_qa.html#install_bmx_cli)
* [如何获取帐户的 GUID](/docs/services/cloud-monitoring/qa/cli_qa.html#account_guid)
* [如何获取组织的 GUID](/docs/services/cloud-monitoring/qa/cli_qa.html#org_guid)
* [如何获取空间的 GUID](/docs/services/cloud-monitoring/qa/cli_qa.html#space_guid)

## 如何登录到 IBM Cloud？
{: #login}

运行以下命令来登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间：

```
ibmcloud login -a Endpoint
```
{: codeblock}
	
其中，*Endpoint* 是用于登录到 {{site.data.keyword.Bluemix_notm}} 的 URL。 此 URL 对于每个区域是不同的。
	
<table>
    <caption>用于访问 {{site.data.keyword.Bluemix_notm}} 的端点列表</caption>
	<tr>
	  <th>区域</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>德国</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>悉尼</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>英国</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
	<tr>
	  <td>美国南部</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
</table>

例如，要登录到美国南部区域，请运行以下命令：
	
```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

遵循指示信息进行操作。 

然后，设置组织和空间。运行以下命令：

```
ibmcloud target -o OrgName -s SpaceName
```
{: codeblock}

其中

* OrgName 是组织的名称。
* SpaceName 是组织的名称。

	
## 如何安装 IBM Cloud CLI？
{: #install_bmx_cli}

请参阅[下载并安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview)。

## 如何获取帐户的 GUID
{: #account_guid}
	
要获取帐户的 GUID，请完成以下步骤：
	
1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。运行以下命令：

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	其中，*Endpoint* 是用于登录到 {{site.data.keyword.Bluemix_notm}} 的 URL。 此 URL 对于每个区域是不同的。
	
	<table>
	    <caption>用于访问 {{site.data.keyword.Bluemix_notm}} 的端点列表</caption>
		<tr>
		  <th>区域</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>美国南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英国</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例如，要登录到美国南部区域，请运行以下命令：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    遵循指示信息进行操作。输入您的 {{site.data.keyword.Bluemix_notm}} 凭证，然后选择组织和空间。
	
	对于**联合用户标识**，请运行以下命令并遵循指示信息：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. 运行 `ibmcloud iam accounts` 命令来获取帐户的 GUID。

    ```
	ibmcloud iam accounts
	```
	{: codeblock} 
	
	例如，要检索用户 xxx@yyy.com 的所有帐户及其对应的 GUID，请运行以下命令：
	
	
	```
	ibmcloud iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## 如何获取组织的 GUID
{: #org_guid}

要获取组织的 GUID，请完成以下步骤：
	
1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。运行以下命令：

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	其中，*Endpoint* 是用于登录到 {{site.data.keyword.Bluemix_notm}} 的 URL。 此 URL 对于每个区域是不同的。
	
	<table>
	    <caption>用于访问 {{site.data.keyword.Bluemix_notm}} 的端点列表</caption>
		<tr>
		  <th>区域</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>美国南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英国</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例如，要登录到美国南部区域，请运行以下命令：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    遵循指示信息进行操作。输入您的 {{site.data.keyword.Bluemix_notm}} 凭证，然后选择组织和空间。
	
	对于联合用户标识，请运行以下命令并遵循指示信息：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}

2. 运行 `ibmcloud iam org` 命令来获取组织 GUID。 

    ```
    ibmcloud iam org NAME --guid
    ```
    {: codeblock}
	
    其中，NAME 是 {{site.data.keyword.Bluemix_notm}} 组织的名称。        
		
## 如何获取空间的 GUID
{: #space_guid}
	
要获取空间的 GUID，请完成以下步骤：
	
1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。运行以下命令：

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	其中，*Endpoint* 是用于登录到 {{site.data.keyword.Bluemix_notm}} 的 URL。 此 URL 对于每个区域是不同的。
	
	<table>
	    <caption>用于访问 {{site.data.keyword.Bluemix_notm}} 的端点列表</caption>
		<tr>
		  <th>区域</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>美国南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英国</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例如，要登录到美国南部区域，请运行以下命令：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    遵循指示信息进行操作。输入您的 {{site.data.keyword.Bluemix_notm}} 凭证，然后选择组织和空间。
	
	对于联合用户标识，请运行以下命令并遵循指示信息：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. 运行 `ibmcloud iam space` 命令来获取空间 GUID。 

    ```
    ibmcloud iam space NAME --guid
    ```
    {: codeblock}
	
    其中，NAME 是 {{site.data.keyword.Bluemix_notm}} 空间的名称。
	
     
	
    例如，要获取空间 *dev* 的 GUID，请运行以下命令：

	
    ```
    ibmcloud iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		
