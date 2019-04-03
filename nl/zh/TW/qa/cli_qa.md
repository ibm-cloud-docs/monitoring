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



# 使用 IBM Cloud CLI 的常見問題
{: #cli_qa}

以下是關於搭配使用 {{site.data.keyword.Bluemix}} CLI 與 {{site.data.keyword.monitoringshort}} 服務的常見問題與解答。
{:shortdesc}

* [如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)
* [如何安裝 {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#install_bmx_cli)
* [如何取得帳戶的 GUID](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#account_guid)
* [如何取得組織的 GUID](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#org_guid)
* [如何取得空間的 GUID](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid)

## 如何登入 IBM Cloud？
{: #login}

請執行下列指令，以登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間：

```
ibmcloud login -a Endpoint
```
{: codeblock}
	
其中 *Endpoint* 是用來登入 {{site.data.keyword.Bluemix_notm}} 的 URL。每個地區的這個 URL 都不同。
	
<table>
    <caption>存取 {{site.data.keyword.Bluemix_notm}} 的端點清單</caption>
	<tr>
	  <th>地區</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>德國</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>雪梨</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>英國</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
	<tr>
	  <td>美國南部</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
</table>

例如，若要登入「美國南部」地區，請執行下列指令：
	
```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

遵循指示。 

然後，設定組織及空間。執行下列指令：

```
ibmcloud target -o OrgName -s SpaceName
```
{: codeblock}

其中

* OrgName 是組織的名稱。
* SpaceName 是空間的名稱。

	
## 如何安裝 IBM Cloud CLI？
{: #install_bmx_cli}

請參閱[下載並安裝 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)。

## 如何取得帳戶的 GUID
{: #account_guid}
	
請完成下列步驟，以取得帳戶的 GUID：
	
1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。執行下列指令：

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	其中 *Endpoint* 是用來登入 {{site.data.keyword.Bluemix_notm}} 的 URL。每個地區的這個 URL 都不同。
	
	<table>
	    <caption>存取 {{site.data.keyword.Bluemix_notm}} 的端點清單</caption>
		<tr>
		  <th>地區</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>美國南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英國</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例如，若要登入「美國南部」地區，請執行下列指令：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    請遵循指示。輸入您的 {{site.data.keyword.Bluemix_notm}} 認證，選取組織及空間。
	
	若為**聯合使用者 ID**，請執行下列指令並遵循指示：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. 執行 `ibmcloud iam accounts` 指令，以取得帳戶的 GUID。

    ```
	ibmcloud iam accounts
	```
	{: codeblock} 
	
	例如，若要擷取使用者 xxx@yyy.com 的所有帳戶及其對應 GUID，請執行下列指令：
	
	```
	ibmcloud iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## 如何取得組織的 GUID
{: #org_guid}

請完成下列步驟，以取得組織的 GUID：
	
1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。執行下列指令：

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	其中 *Endpoint* 是用來登入 {{site.data.keyword.Bluemix_notm}} 的 URL。每個地區的這個 URL 都不同。
	
	<table>
	    <caption>存取 {{site.data.keyword.Bluemix_notm}} 的端點清單</caption>
		<tr>
		  <th>地區</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>美國南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英國</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例如，若要登入「美國南部」地區，請執行下列指令：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    請遵循指示。輸入您的 {{site.data.keyword.Bluemix_notm}} 認證，選取組織及空間。
	
	若為聯合使用者 ID，請執行下列指令並遵循指示：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}

2. 執行 `ibmcloud iam org` 指令，以取得組織 GUID。 

    ```
    ibmcloud iam org NAME --guid
    ```
    {: codeblock}
	
    其中，NAME 是 {{site.data.keyword.Bluemix_notm}} 組織的名稱。        
		
## 如何取得空間的 GUID
{: #space_guid}
	
請完成下列步驟，以取得空間的 GUID：
	
1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。執行下列指令：

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	其中 *Endpoint* 是用來登入 {{site.data.keyword.Bluemix_notm}} 的 URL。每個地區的這個 URL 都不同。
	
	<table>
	    <caption>存取 {{site.data.keyword.Bluemix_notm}} 的端點清單</caption>
		<tr>
		  <th>地區</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>美國南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英國</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例如，若要登入「美國南部」地區，請執行下列指令：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    請遵循指示。輸入您的 {{site.data.keyword.Bluemix_notm}} 認證，選取組織及空間。
	
	若為聯合使用者 ID，請執行下列指令並遵循指示：
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. 執行 `ibmcloud iam space` 指令，以取得空間 GUID。 

    ```
    ibmcloud iam space NAME --guid
    ```
    {: codeblock}
	
    其中，NAME 是 {{site.data.keyword.Bluemix_notm}} 空間的名稱。 
	
    例如，若要取得空間 *dev* 的 GUID，請執行下列指令：
	
    ```
    ibmcloud iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		
