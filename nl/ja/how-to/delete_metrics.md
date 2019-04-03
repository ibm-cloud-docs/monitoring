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



# メトリックの削除
{: #delete_metrics}

[メトリック API](https://console.bluemix.net/apidocs/monitoring-metrics-api) を使用して、{{site.data.keyword.monitoringshort}} サービスからメトリックを削除することができます。
{:shortdesc}

[{{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login) の地域にログインした後で、以下の手順を実行して通知を削除します。


## 手順 1: セキュリティー・トークンの取得
{: #step1_delete_metrics}

UAA トークン、IAM トークン、または API キーを使用することができます。 

以下のいずれかの方法を選択して、セキュリティー・トークンを取得します。
	
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
	
## 手順 2: メトリックを処理するための権限の確認 
{: #step2_delete_metrics}

メトリックが使用可能なドメインによっては、以下の情報を考慮してください。

* スペース・ドメインで使用可能なメトリックを処理するには、ユーザーは、このドメインに関連付けられた Cloud Foundry スペースでの*開発者* 役割が必要です。 
* アカウント・ドメインで使用可能なメトリックを処理するには、ユーザーは、*管理者* 役割、*オペレーター* 役割、または*エディター* 役割を持つ IAM ポリシーが必要です。

ユーザー権限を確認するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、
{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://console.bluemix.net ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    *「ユーザー」*ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. {{site.data.keyword.monitoringshort}} サービスを処理するためのアクセス権限を確認します。


## 手順 3: スペース ID の取得 
{: #step3_delete_metrics}

この手順は、スペース・ドメインで使用可能なメトリックを削除する場合にのみ適用されます。

スペース GUID を取得するには、以下のコマンドを実行します。
	
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
	
次に、変数 *Space* をエクスポートします。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## 手順 4: メトリックのリスト
{: #step4_delete_metrics}


以下の cURL コマンドを実行して、スペース・ドメインで使用可能なメトリックをリストします。

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*

```
{: screen}

以下の cURL コマンドを実行して、アカウント・ドメインで使用可能なメトリックをリストします。

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

ここで、
	
* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} UAA トークン、IAM トークン、または API キーを渡すパラメーターです。
	
* *Auth_Type* は、トークンまたは API キーのタイプを定義する接頭部です。 以下のリストに、有効値 *apikey*、*iam*、または *uaa* の概要を示します。詳細は次のとおりです。

  * *apikey* は、トークンが API キーであることを識別します。
	* *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
	* *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。
	
* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 
	
* Token は、UAA 認証トークン、IAM 認証トークン、または API キーです。
	
* Space は、スペースの GUID です。 
	
* METRICS_ENDPOINT はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。

* *query* は、適用されるフィルターを定義します。 例えば、`query=metric-service.*` は階層 `metric-service.*` の下に存在するメトリックをすべてリストし、`query=*` はドメイン内のメトリックをすべてリストします。


## 手順 5 - オプション 1: すべてのメトリックの削除
{: #step5_delete_metrics}
  

以下の cURL コマンドを実行して、スペース・ドメイン内のメトリックをすべて削除します。

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

以下の cURL コマンドを実行して、アカウント・ドメインからメトリックをすべて削除します。

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

ここで、
	
* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} の UAA トークンを渡すパラメーターです。
	
* Auth_Type は、トークンのタイプを定義する接頭部です。 有効値は、UAA トークンの場合は *uaa*、IAM トークンの場合は *iam*、API キーの場合は *api* です。
	
* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。
	
* *Token* はセキュリティー・トークンを示しています。
	
* *Space* はスペースの GUID を示しています。 
	
* *METRICS_ENDPOINT* はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。

* *query* は、適用されるフィルターを定義します。 `query=*` は、ドメイン内のすべてのメトリックを示しています。


## 手順 6 - オプション 2: サービスのすべてのメトリックを削除
{: #step6_delete_metrics}
  

以下の cURL コマンドを実行して、スペース・ドメイン内のサービスのメトリックをすべて削除します。

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

以下の cURL コマンドを実行して、アカウント・ドメインからメトリックをすべて削除します。

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

ここで、
	
* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} の UAA トークンを渡すパラメーターです。
	
* Auth_Type は、トークンのタイプを定義する接頭部です。 有効値は、UAA トークンの場合は *uaa*、IAM トークンの場合は *iam*、API キーの場合は *api* です。
	
* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。
	
* *Token* はセキュリティー・トークンを示しています。
	
* *Space* はスペースの GUID を示しています。 
	
* *METRICS_ENDPOINT* はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照してください。

* *query* は、適用されるフィルターを定義します。 `query=*` は、ドメイン内のすべてのメトリックを示しています。

* *metric-service.** はサービスの名前です。 例えば、`containers-kubernetes` です。
