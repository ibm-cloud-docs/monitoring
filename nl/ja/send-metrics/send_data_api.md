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

# Metrics API を使用したデータの送信
{: #send_data_api}

Metrics API を使用して、{{site.data.keyword.monitoringshort}} サービスにメトリックを送信することができます。 
{:shortdesc}


{{site.data.keyword.Bluemix_notm}} Docker コンテナーの場合、基本のシステム・メトリックは自動的に収集されます。 Cloud Foundry アプリケーション、および仮想計算機 (VM) で実行されているアプリの場合、メトリックは、[Metrics API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window} を使用してアプリから直接送信する必要があります。 



## スペース・ドメインへのメトリックの送信
{: #space_uaa}

cURL を使用してメトリックをスペースに送信するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。

    以下のいずれかの方法を選択して、メトリックの送信に必要なセキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)を参照してください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの 取得](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)を参照してください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)を参照してください。
	
	{{site.data.keyword.Bluemix_notm}} にログインした同じ端末から、トークンに *Token* 変数を設定します。

    例えば、UAA トークンを設定し、トークンの値から *Bearer* 部分を削除します。

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. スペース GUID を取得します。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。

    以下のコマンドを実行します。
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	ここで、*SpaceName* は、通知を定義するスペースの名前です。
	
	例えば、*dev* という名前のスペースの GUID を取得するには、以下のコマンドを実行します。
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	このコマンドの結果は以下のようになります。
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	次に、変数 *Space* をエクスポートします。 **注:** この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。
	
	以下に例を示します。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
5. 以下の cURL コマンドを実行して、メトリックを送信します。

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	ここで、
	
	* Metrics_File は、{{site.data.keyword.monitoringshort}} サービスに送信されるメトリックの定義を含む JSON ファイルを表しています。
	
	* *X-Auth-User-Token* は、セキュリティー・トークンを渡すパラメーターです。
	
	* *Auth_Type* は、トークンのタイプを定義する接頭部です。 有効値は、UAA トークンの場合は *uaa*、IAM トークンの場合は *iam*、API キーの場合は *api* です。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。
	
	* Token は、セキュリティー・トークン、または API キーを表します。
	
	* Space は、スペースの GUID を表します。 
	
	* Endpoint はサービスへのエントリー ・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	
	例えば、以下のコマンドを実行して、2 つのメトリック `myhost.cpu.idle` と `myapp.login.attempts` を {{site.data.keyword.monitoringshort}} サービスに送信することができます。
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	サンプル・ファイル *metric.json* は以下のように定義されています。

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
