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


# CRUD 通知
{: #notifications}

アラート API を使用して、通知の作成、削除、および更新、通知の詳細表示、およびスペース内に定義されている通知のリストを行うことができます。
{:shortdesc}

## 通知の作成
{: #notifications_create}

通知を作成するには、以下の手順を実行します。

1. 通知ファイルを作成します。

    1. 通知テンプレートを使用して通知ファイルを作成します。 詳しくは、
[通知テンプレート](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template)を参照してください。
	
	2. 以下を実行して、ファイルを更新します。
	
	    * *name* フィールドに固有の名前を入力します。 このフィールドの値は、後で通知を更新および削除したり、通知の詳細を表示したりするために使用されます。
		* 説明を入力します。
		* 有効な E メール・アドレス、URL エンドポイント、または PagerDuty キーを入力します。
		
	3. ファイルを保存します。 例えば、スペース内で実行されている照会に対して定義する通知には、*s-* のような接頭部を使用します。
	
	    **ヒント:** *~/cloud-monitoring/notifications/* ディレクトリーに通知ファイルを作成して、{{site.data.keyword.monitoringshort_notm}} サービスのリソースをグループ化します。 
	
	4. 変数 *NOTIFICATION_FILE* をエクスポートします。
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

3. セキュリティー・トークンを取得します。 UAA トークン、IAM トークン、または API キーを使用することができます。 以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
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
	
5. {{site.data.keyword.monitoringshort}} サービスを使用して通知を登録します。

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	ここで、
	
	* NOTIFICATION_FILE は、通知を定義する JSON ファイルです。
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA トークン認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* Token は、UAA トークン、IAM トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	
    以下に例を示します。 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## 通知の削除
{: #notifications_delete}

通知を削除するには、以下の手順を実行します。

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
	
	次に、以下のようにして変数 *Space* をエクスポートします。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 以下の cURL コマンドを実行して、通知を削除します。

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	ここで、
	
	* *X-Auth-User-Token* は、UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。 トークンまたは API キーには、 *apikey*、*iam* または *uaa* のいずれかの値が接頭部として付いている必要があります。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
		
	* Token は、UAA トークン、IAM トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* Notification_Name は、通知の名前です。つまり、通知のプロパティーをリストした時の *name* フィールドの値です。
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	


## すべての通知のリスト
{: #notifications_list}

すべての通知をリストするには、以下の手順を実行します。

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
	
	次に、以下のようにして変数 *Space* をエクスポートします。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 以下の cURL コマンドを実行して、すべての通知をリストします。

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	ここで、
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
		
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。 トークンまたは API キーには、 *apikey*、*iam* または *uaa* のいずれかの値が接頭部として付いている必要があります。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
		
	* Token は、UAA トークン、IAM トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。

			

## 通知の詳細の表示
{: #show}


通知に関する情報を表示するには、以下の手順を実行します。

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
	
	次に、以下のようにして変数 *Space* をエクスポートします。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 以下の cURL コマンドを実行して、通知の詳細を表示します。

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	ここで、
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
		
	* Token は、UAA トークン、IAM トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* NOTIFICATION_NAME は、通知の名前です。つまり、通知のプロパティーをリストした時の *name* フィールドの値です。
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	
     
		

			
## 通知のテスト
{: #test}	
			
通知をテストするには、以下の手順を実行します。

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
	
	次に、以下のようにして変数 *Space* をエクスポートします。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 以下の cURL コマンドを実行して、通知をテストします。

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	ここで、
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。 トークンまたは API キーには、 *apikey*、*iam* または *uaa* のいずれかの値が接頭部として付いている必要があります。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
		
	* Token は、UAA トークン、IAM トークン、または API キーです。
	
	* Space は、スペースの GUID です。 
	
	* NOTIFICATION_NAME は、通知の名前です。つまり、通知のプロパティーをリストした時の *name* フィールドの値です。
	
	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	


## 通知の更新
{: #notifications_update}

通知を更新するには、以下の手順を実行します。

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
	
	次に、以下のようにして変数 *Space* をエクスポートします。
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 以下の cURL コマンドを実行して、通知を更新します。

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	ここで、
	
	* NOTIFICATION_FILE は、通知を定義する JSON ファイルです。
	
	* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
	* *X-Auth-User-Token* は、bluemix UAA トークン、IAM トークン、または API キーを渡すパラメーターです。 トークンまたは API キーには、 *apikey*、*iam* または *uaa* のいずれかの値が接頭部として付いている必要があります。詳細は次のとおりです。

        * *apikey* は、トークンが API キーであることを識別します。
		* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
		* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
		
	* Token は、UAA トークン、IAM トークン、または API キーです。
	
	* Space は、スペースの GUID です。 

	* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。
	
        

