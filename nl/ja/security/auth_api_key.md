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


# API キーの処理
{: #auth_api_key}

{{site.data.keyword.Bluemix}} CLI または
{{site.data.keyword.Bluemix_notm}} UI を使用して、API を取得
することができます。 API キーには有効期限切れはありません。 API が漏えいした場合は、取り消して新しいものを生成できます。
{:shortdesc}

## IBM Cloud CLI を使用した IAM API キーの生成
{: #iam_apikey_cli}

{{site.data.keyword.Bluemix_notm}} CLI を使用して、以下の手順を実行し API キーを生成します。

1. (前提条件) {{site.data.keyword.Bluemix_notm}} CLI をインストールします。

   詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa)を参照してください。
   
   CLI がインストールされたら、次の手順に進んでください。
	
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。
 
3. `ibmcloud iam api-key-create` コマンドを実行して、API キーを作成します。

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	ここで、
	
	* NAME は、作成する API キーの名前です。
	* DESCRIPTION は、API キーを説明するために使用するテキストです。
	* FILE は、キーを保存するファイルの名前です。
	
    例えば、API キー *MyKey* を作成するには、以下のコマンドを実行します。
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## IBM Cloud UI を使用した IAM API キーの生成
{: #iam_apikey_ui}

{{site.data.keyword.Bluemix_notm}} UI を介して API キーを生成するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、
{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://console.bluemix.net ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. コンソールのメニュー・バーから、**「管理」>「セキュリティー」>「IBM Cloud API キー」**をクリックします。

3. **「API キーの作成」**をクリックします。

4. API キーの名前と説明を入力します。 次に、**「API キーの作成」**をクリックします。

5. API キーを保存します。 **「API キーのダウンロード (Download API key)」**をクリックします。

    **「表示」**をクリックして、API キーを表示します。  

**注:** API キーは、作成時にのみ表示またはダウンロードできます。 API キーが消失した場合は、新しい API キーを作成する必要があります。  


	
## IBM Cloud UI を使用した API キーの取り消し
{: #revoke_ui}
	
{{site.data.keyword.Bluemix_notm}} UI を介して IAM API キーを取り消すには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、
{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://console.bluemix.net ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. コンソールのメニュー・バーから、**「管理」>「セキュリティー」>「IBM Cloud API キー」**をクリックします。

3. **「アクション」**をクリックしてから、**「キーの削除」**をクリックします。





	

	
	
	
	
	
	
