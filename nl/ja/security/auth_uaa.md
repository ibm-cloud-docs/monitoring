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


# UAA トークンの取得
{: #auth_uaa}

{{site.data.keyword.Bluemix}} UAA モデルを使用して、
{{site.data.keyword.monitoringshort}} サービスを処理するために使用することができる認証トークンを取得します。 この認証トークンは、{{site.data.keyword.Bluemix_notm}} CLI を使用して取得できます。
{:shortdesc}

トークンには有効期限があります。 
		
## IBM Cloud CLI を使用した UAA トークンの取得
{: #uaa_cli}


UAA トークンを取得するには、以下の手順を実行します。

1. (前提条件) {{site.data.keyword.Bluemix_notm}} CLI をインストールします。

   詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa)を参照してください。
   
   CLI がインストールされたら、次の手順に進んでください。
    
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。
	
3. `ibmcloud iam oauth-tokens` コマンドを実行して、UAA トークンを取得します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	出力は UAA トークンを返します。

**注:** トークンを使用する場合、API 呼び出しで渡すトークンの値から *Bearer* を削除してください。
	


	
