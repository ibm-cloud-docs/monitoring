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


# アラート API を使用したアラートの履歴の取得
{: #retrieve_history}

アラート API を使用してアラートの履歴を取得します。 
{:shortdesc}


アラート API を使用してアラートの履歴を取得するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)をご覧ください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)をご覧ください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)を参照してください。
	
	{{site.data.keyword.Bluemix_notm}} にログインした同じ端末から、トークンに Token 変数を設定します。

    例えば、IAM トークンを使用するには、以下のコマンドを実行します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	このコマンドの結果は以下のようになります。
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	次に、以下のようにして変数 *Token* をエクスポートします。
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
	次に、変数 *Space* をエクスポートします。 **注:** この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。
	
	以下に例を示します。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. ルールの履歴の取得

    * 名前によりルールの履歴を取得するには、[名前を使用したルールの履歴の取得](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_name)を参照してください。
	* 一定期間のルールの履歴を取得するには、[過去 48 時間のルールの履歴の取得](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_time)を参照してください。
	* 一定期間のルールの履歴を取得するには、[ルールの履歴の過去 3 エントリーの取得](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#number)を参照してください。
	
	
## ルール名によるルールの履歴の取得
{: #by_name}
	
以下の cURL コマンドを実行して、アラートの履歴を取得します。

```
curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/history?rule_name=RULE_NAME
```
{: codeblock}
	
ここで、
	
* *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

    * *apikey* は、トークンが API キーであることを識別します。
	* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
	* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
* *Token* は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
* *Space* は、スペースの GUID です。 
	
* *RULE_NAME* は、アラートをトリガーするために使用されるルールの名前です。 この値は、*name* フィールドに指定されている値です。
	
* *METRICS_ENDPOINT* はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)を参照してください。
	
    
例えば、ルール `highNginxCPU` の履歴は以下のようになります。

```
curl -XGET --header "X-Auth-User-Token: iam ${Token}" --header "X-Auth-Scope-Id: ${Space}" https://metrics.ng.bluemix.net/v1/alert/history?rule_name=highNginxCPU
```
{: screen}

```
[
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T22.23.21.000",
 "value": 99.5,
 "from_level": "OK",
 "to_level": "ERROR"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.11.12.123",
 "value": 98.5,
 "from_level" : "OK",
 "to_level": "WARN"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.12.14.000",
 "value": 97.0,
 "from_level" : "WARN",
 "to_level": "OK"
 }
]
```
{: screen}


## 過去 48 時間のルールの履歴の取得
{: #by_time}

以下の cURL コマンドを実行して、過去 48 時間のアラートの履歴を取得します。

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?start=-48h
```
{: codeblock}

ここで、
	
* *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

    * *apikey* は、トークンが API キーであることを識別します。
	* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
	* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
* *Token* は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
* *Space* は、スペースの GUID です。 
	
* *RULE_NAME* は、アラートをトリガーするために使用されるルールの名前です。 この値は、*name* フィールドに指定されている値です。
	
* *METRICS_ENDPOINT* はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)を参照してください。
	

## ルールの履歴の過去 3 エントリーの取得
{: #number}

以下の cURL コマンドを実行して、アラートの履歴の過去 3 エントリーを取得します。

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?max_results=3
```
{: codeblock}

ここで、
	
* *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

    * *apikey* は、トークンが API キーであることを識別します。
	* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
	* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
* *Token* は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
* *Space* は、スペースの GUID です。 
	
* *RULE_NAME* は、アラートをトリガーするために使用されるルールの名前です。 この値は、*name* フィールドに指定されている値です。
	
* *METRICS_ENDPOINT* はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)を参照してください。
	
