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


# CRUD ルール
{: #rules}

アラート API を使用して、ルールを作成、削除、または更新し、ルールの詳細を表示し、スペース内に定義されているルールをリストします。
{:shortdesc}


## ルールの作成
{: #create}

{{site.data.keyword.monitoringshort}} サービスでルールを構成
するには、ルールの詳細を含むルール・ファイルを作成し、{{site.data.keyword.monitoringshort}} サービス
を使用してルールを登録します。

以下のステップを実行します。

1. 有効な JSON を含むルール・ファイルを作成します。 ファイルを保存します。 

    ファイルを保存するには、例えばスペース内で実行されている照会に対して定義するルールの場合は、*s-* のような接頭部を使用します。
	
	**ヒント:** 
	
	* 照会でエラーまたは警告についてのアラートを出すためには、異なる通知方法を使用してそれぞれのルールを定義します。 
	* *~/cloud-monitoring/rules/* ディレクトリーにルール・ファイルを作成して、{{site.data.keyword.monitoringshort_notm}} サービスのリソースをグループ化します。 

    ルールのファイルに以下の情報を入力します。
	
	* *name*: 固有の名前を入力します。 このフィールドの値は、後でルールを更新および削除したり、ルールの詳細を表示したりするために使用されます。
	* *description*: 説明を入力します。
	* *expression*: モニターする照会を入力します。
	* *enabled*: ルールを有効にするには、*true* に設定します。
	* *from*: しきい値に基づいてデータを分析するために使用される初期ポイント・イン・タイム。
	* *until*: しきい値に基づいてデータを分析するために使用される最終ポイント・イン・タイム。
	* *comparison*: 実行するチェックのタイプを識別するために使用される比較演算。例えば、*below*。
	* *error_level*: エラー・アラートをトリガーするために設定するしきい値を定義します。
	* *warning_level*: 警告アラートをトリガーするために設定するしきい値を定義します。
	* *frequency*: データをチェックする頻度を定義します。
	* *dashboard_url*: 照会を含むダッシュボードを Grafana 内に表示する URL を定義します。
	* *notifications*: このルールによって記述されているアラートがトリガーされた場合の通知方法。
	
	例えば、ルール・ファイル myrulefile.json は以下のようになります。
	
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
      "emailXXX"
    ]
    }
    ```
	{: screen}
	
	次に、以下のようにして変数 *RULE_FILE* をエクスポートします。
	
	```
	export RULE_FILE="myrulefile.json"
	```
	{: screen}
	
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

3. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得] (/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli) を参照してください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの 取得](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)を参照してください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)を参照してください。
	
	例えば、IAM トークンを使用するには、以下のコマンドを実行します。
    
    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}
	
    このコマンドの結果は以下のようになります。
	
    ```
    IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
    ```
    {: screen}
	
    次に、以下のようにして変数 *Token* をエクスポートします。
	
    ```
    export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
    ```
    {: screen}
	
    **注:** このトークンは *Bearer* を除外します。
	
4. スペース GUID を取得します。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。

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
	
5. 次の cURL コマンドを実行して、{{site.data.keyword.monitoringshort}} サービスにルールを登録します。

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	ここで、
	
	* RULE_FILE は、アラート・ルールを定義する JSON ファイルです。
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* Token は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	
    以下に例を示します。 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## ルールの削除
{: #delete}

ルールを削除するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)を参照してください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの 取得](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)を参照してください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)を参照してください。
	
	例えば、IAM トークンを使用するには、以下のコマンドを実行します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	このコマンドの結果は以下のようになります。
	
	```
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	次に、以下のようにして変数 *Token* をエクスポートします。
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
		
4. 以下の cURL コマンドを実行して、ルールを削除します。

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	ここで、
	
    * *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* Token は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* Rule_Name は、*name* フィールドに指定されているルールの名前です。
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	
    
	
## すべてのルールのリスト
{: #list}

すべてのルールをリストするには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)を参照してください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの 取得](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)を参照してください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)を参照してください。
	
	例えば、IAM トークンを使用するには、以下のコマンドを実行します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	このコマンドの結果は以下のようになります。
	
	```
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	次に、以下のようにして変数 *Token* をエクスポートします。
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. 以下の cURL コマンドを実行して、スペース内のすべてのルールをリストします。

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	ここで、
	
	* *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* Token は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	

	
	

## ルールの詳細の表示
{: show}

ルールの詳細を表示するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)を参照してください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの 取得](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)を参照してください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)を参照してください。
	
	例えば、IAM トークンを使用するには、以下のコマンドを実行します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	このコマンドの結果は以下のようになります。
	
	```
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	次に、以下のようにして変数 *Token* をエクスポートします。
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. 以下の cURL コマンドを実行して、ルールの詳細を表示します。

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	ここで、
	
	* *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* Token は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* Rule_Name は、*name* フィールドに指定されているルールの名前です。
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	

## ルールの更新
{: #update}

ルールを更新するには、ルール・ファイルを更新してルールを変更してから、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

2. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
	* UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)を参照してください。
	
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの 取得](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)を参照してください。
	
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)を参照してください。
	
	例えば、IAM トークンを使用するには、以下のコマンドを実行します。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	このコマンドの結果は以下のようになります。
	
	```
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	次に、以下のようにして変数 *Token* をエクスポートします。
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. 以下の cURL コマンドを実行して、ルールを更新します。

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
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
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。

	
	
