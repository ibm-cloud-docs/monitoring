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



# IBM Cloud CLI の使用に関する FAQ
{: #cli_qa}

{{site.data.keyword.monitoringshort}} サービスでの {{site.data.keyword.Bluemix}} CLI の使用に関する一般的な質問の回答を以下に示します。 
{:shortdesc}

* [{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)
* [{{site.data.keyword.Bluemix_notm}} CLI のインストール方法を教えてください](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#install_bmx_cli)
* [アカウントの GUID の取得方法を教えてください](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#account_guid)
* [組織の GUID の取得方法を教えてください](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#org_guid)
* [スペースの GUID の取得方法を教えてください](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid)

## IBM Cloud にログインするにはどうすればよいですか
{: #login}

以下のコマンドを実行して、{{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。

```
ibmcloud login -a Endpoint
```
{: codeblock}
	
ここで、*Endpoint* は、{{site.data.keyword.Bluemix_notm}} にログインするための URL です。 この URL は地域ごとに異なります。
	
<table>
    <caption>{{site.data.keyword.Bluemix_notm}} にアクセスするためのエンドポイントのリスト</caption>
	<tr>
	  <th>地域</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>ドイツ</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>シドニー</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>英国</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
	<tr>
	  <td>米国南部</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
</table>

例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

指示に従います。 

次に、組織およびスペースを設定します。 以下のコマンドを実行します。

```
ibmcloud target -o OrgName -s SpaceName
```
{: codeblock}

ここで、

* OrgName は、組織の名前です。
* SpaceName は、スペースの名前です。

	
## IBM Cloud CLI のインストール方法を教えてください
{: #install_bmx_cli}

[{{site.data.keyword.Bluemix_notm}} CLI のダウンロードとインストール](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)を参照してください。

## アカウントの GUID の取得方法を教えてください
{: #account_guid}
	
アカウントの GUID を取得するには、以下の手順を実行します。
	
1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 以下のコマンドを実行します。

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	ここで、*Endpoint* は、{{site.data.keyword.Bluemix_notm}} にログインするための URL です。 この URL は地域ごとに異なります。
	
	<table>
	    <caption>{{site.data.keyword.Bluemix_notm}} にアクセスするためのエンドポイントのリスト</caption>
		<tr>
		  <th>地域</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>米国南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英国</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    指示に従います。 {{site.data.keyword.Bluemix_notm}} の資格情報を入力し、組織とスペースを選択します。
	
	**統合ユーザー ID** の場合は、次のコマンドを実行し、指示に従います。
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. `ibmcloud iam accounts` コマンドを実行して、アカウントの GUID を取得します。

    ```
	ibmcloud iam accounts
	```
	{: codeblock} 
	
	例えば、ユーザー xxx@yyy.com のすべてのアカウントを、対応する GUID と共に取得するには、以下のコマンドを実行します。
	
	```
	ibmcloud iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## 組織の GUID の取得方法を教えてください
{: #org_guid}

組織の GUID を取得するには、以下の手順を実行します。
	
1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 以下のコマンドを実行します。

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	ここで、*Endpoint* は、{{site.data.keyword.Bluemix_notm}} にログインするための URL です。 この URL は地域ごとに異なります。
	
	<table>
	    <caption>{{site.data.keyword.Bluemix_notm}} にアクセスするためのエンドポイントのリスト</caption>
		<tr>
		  <th>地域</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>米国南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英国</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    指示に従います。 {{site.data.keyword.Bluemix_notm}} の資格情報を入力し、組織とスペースを選択します。
	
	統合ユーザー ID の場合は、次のコマンドを実行し、指示に従います。
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}

2. `ibmcloud iam org` コマンドを実行して、組織の GUID を取得します。 

    ```
    ibmcloud iam org NAME --guid
    ```
    {: codeblock}
	
    ここで、NAME は {{site.data.keyword.Bluemix_notm}} 組織の名前です。        
		
## スペースの GUID の取得方法を教えてください
{: #space_guid}
	
スペースの GUID を取得するには、以下の手順を実行します。
	
1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 以下のコマンドを実行します。

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	ここで、*Endpoint* は、{{site.data.keyword.Bluemix_notm}} にログインするための URL です。 この URL は地域ごとに異なります。
	
	<table>
	    <caption>{{site.data.keyword.Bluemix_notm}} にアクセスするためのエンドポイントのリスト</caption>
		<tr>
		  <th>地域</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>米国南部</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>英国</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    指示に従います。 {{site.data.keyword.Bluemix_notm}} の資格情報を入力し、組織とスペースを選択します。
	
	統合ユーザー ID の場合は、次のコマンドを実行し、指示に従います。
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. `ibmcloud iam space` コマンドを実行して、スペースの GUID を取得します。 

    ```
    ibmcloud iam space NAME --guid
    ```
    {: codeblock}
	
    ここで、NAME は、{{site.data.keyword.Bluemix_notm}} スペースの名前です。 
	
    例えば、スペース *dev* の GUID を取得するには、以下のコマンドを実行します。
	
    ```
    ibmcloud iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		
