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


# {{site.data.keyword.monitoringshort}} API を使用した PagerDuty アラートの構成
{: #configure_pagerduty_alert}

メトリックに PagerDuty のアラートを構成するには、ルールと PagerDuty による通知を定義します。 次に、
{{site.data.keyword.monitoringshort}} サービスを使用してルールと通知方法を登録します。
{:shortdesc}

以下のステップを実行します。

## 手順 1: ルールの作成
{: #cpa_step1}

Grafana に定義したメトリック照会のルールを作成します。 詳しくは、
[
ルールの作成](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#create)を参照してください。

例えば、ルール・ファイル `s-rule-1.json` を `~/cloud-monitoring/rules/` ディレクトリーに作成します。 

```
{
    "name": "checkbytesin",
    "description": "MH check Bytes In per second",
    "expression": "movingAverage(messagehub.65qser11-8034-1234-5678-c82fb42wdfgh.1.kafka-java-console-sample-topic.BytesInPerSec.15MinuteRate,\"5min\")",
    "enabled": true,
    "from": "-5min",
    "until": "now",
    "comparison": "above",
    "comparison_scope": "last",
    "error_level" : 27,
    "warning_level" : 25,
    "frequency": "1min",
    "dashboard_url": "https://metrics.ng.bluemix.net",
    "notifications": [
      "NOTIFICATION_NAME"
    ]
}
```
{: screen}

次に、以下のようにして変数 *RULE_FILE* をエクスポートします。
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## 手順 2: Monitoring サービスでのルールの登録
{: #cpa_step2}
	
端末から、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)をご覧ください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)をご覧ください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)を参照してください。
	
	例えば、IAM トークンを使用するには、以下のコマンドを実行します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	このコマンドの結果は以下のようになります。
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	次に、以下のようにして変数 *Token* をエクスポートします。
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**注:** このトークンは *Bearer* を除外します。
	
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
	
	次に、以下のようにして変数 *Space* をエクスポートします。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 次の cURL コマンドを実行して、ルールを登録します。
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	ここで、
	
	* RULE_FILE は、アラート・ルールを定義する JSON ファイルです。
	
	* *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* Token は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)を参照してください。
	
	ルールが正常に作成されていることを検証するには、以下のコマンドを実行します。

	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	以下に例を示します。
	
    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## 手順 3: PagerDuty 通知の作成
{: #cpa_step3}


通知ファイルを作成するには、次の情報を考慮します。

* PagerDuty アラートのための通知テンプレートを使用します。 詳しくは、
[通知テンプレート](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template)を参照してください。
* ローカル・ディレクトリー (例: 「`~/cloud-monitoring/notifications`」) にファイルを作成します。

例えば、以下のように、vi エディターを使用してファイル **pagerduty.json** を作成します。 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "PagerDuty",
"description" : "Send notification to PagerDuty when ....",
"detail": "Enter a PagerDuty Key"
}
```
{: codeblock}	
	
詳細情報については、[通知の作成](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#create)を参照してください。
	
## 手順 4: Monitoring サービスへの通知方法の登録
{: #cpa_step4}
	
端末から、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)をご覧ください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)をご覧ください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)を参照してください。
	
	例えば、IAM トークンを使用するには、以下のコマンドを実行します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	このコマンドの結果は以下のようになります。
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	次に、以下のようにして変数 *Token* をエクスポートします。
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**注:** このトークンは *Bearer* を除外します。
	
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
	
	次に、以下のようにして変数 *Space* をエクスポートします。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 次の cURL コマンドを実行して、通知を登録します。

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	ここで、
	
	* NOTIFICATION_FILE は、通知を定義する JSON ファイルです。
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* Token は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)を参照してください。
	
    通知が正常に作成されていることを検証するには、以下のコマンドを実行します。

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
