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

# メトリックの取得
{: #retrieve_data_api}

[Metrics API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window} を使用して、{{site.data.keyword.monitoringshort}} サービスからメトリックを取得することができます。
{:shortdesc}


## スペースからのメトリックの取得
{: #uaa}

メトリックをスペースから取得するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)を参照してください。

2. セキュリティー・トークンまたは API キーを取得します。
  
    セキュリティー・トークンまたは API キーを指定して **X-Auth-User-Token** フィールドを設定する必要があります。 UAA トークン、IAM トークン、または API キーを使用することができます。

    最初に、以下のいずれかの方法を選択して、メトリックの送信に必要なセキュリティー・トークンを取得します。
	
    * UAA トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した UAA トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)をご覧ください。
    
	* IAM トークンを取得するには、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)をご覧ください。
    
	* API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)を参照してください。 

    トークンまたは API キーには、`apikey`、`iam`、または `uaa` のいずれかの値が接頭部として付いている必要があります。 

    ここで、 

    * *apikey* は、トークンが API キーであることを識別します。
    * *iam* は、指定されたトークンが IAM 生成トークンであることを識別します。
    * *uaa* は、指定されたトークンが UAA 生成トークンであることを識別します。

    例えば、API キーの場合、`X-Auth-User-Token: apikey SomeIAMGeneratedKey` というヘッダーを設定できます。
	
	次に、{{site.data.keyword.Bluemix_notm}} にログインした同じ端末から、トークンに Token 変数を設定します。

    例えば、UAA トークンを設定し、トークンの値から *Bearer* 部分を削除します。

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. スペース ID を取得します。

    メトリックを取得するには、ヘッダー・フィールド **X-Auth-Scope-Id** は必須で、スペース GUID に設定する必要があります。 

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

4. 以下の cURL コマンドを実行して、メトリックを送信します。

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	ここで、
	
	* *X-Auth-User-Token* は、{{site.data.keyword.Bluemix_notm}} の UAA トークンを渡すパラメーターです。
	
	* Auth_Type は、トークンのタイプを定義する接頭部です。 有効値は、UAA トークンの場合は *uaa*、IAM トークンの場合は *iam*、API キーの場合は *api* です。
	
	* *X-Auth-Scope-Id* は、スペースの GUID を渡すパラメーターです。 この GUID には、スペースを識別するための *s-* の接頭部が付いている必要があります。 UAA 認証を使用する場合、このヘッダーは必須です。 IAM 認証トークンを使用する場合、このヘッダーはオプションで、このトークンにバインドされているドメイン情報が使用されます。
	
	* *Token* はセキュリティー・トークンを示しています。
	
	* *Space* はスペースの GUID を示しています。 
	
	* *Start_Time* は、要求の開始を定義します。 この情報は、相対的または絶対的な期間を計算するために使用されます。 *End_Time* は、要求の終わりを定義します。 この情報は、相対的または絶対的な期間を計算するために使用されます。 詳しくは、[期間の設定](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#time)を参照してください。
	
	* *Path* は、1 つまたは複数のメトリックを識別します。 オプションで、関数を各メトリックに適用できます。 パスではワイルドカードもサポートします。これにより、単一のパスで複数のメトリックを識別できます。 詳しくは、[メトリックの定義](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#metrics)を参照してください。
	
	* *METRICS_ENDPOINT* はサービスへのエントリー・ポイントを示しています。 各地域の URL は異なります。 地域ごとのエンドポイントのリストを取得するには、
[エンドポイント](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)を参照してください。
	

	
## メトリックの定義
{: #metrics}

メトリックのデータを取得するには、メトリック・ツリーのルートからメトリックまでのメトリックのパスを指定する必要があり、各ステップをピリオド (.) で区切る必要があります。

パスは、**Target** パラメーターで指定されます。 要求ごとに最大 5 個のターゲットを指定できます。  

オプションで、関数をメトリックに適用できます。 サポートされる関数について詳しくは、[Graphite 0.9.15 functions ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://graphite.readthedocs.io/en/latest/functions.html) を参照してください。

ワイルドカードを使用してパスを定義できます。 ワイルドカードを使用して、単一のパスで複数のメトリックを識別できます。 

* **アスタリスク**: ゼロ個以上の文字と一致させるには、アスタリスク (*) を使用できます。 

    単一パス・エレメント内に複数のアスタリスクを含めることができます。例えば `servers.sp*aeg*r.cpu.total.*` と指定できます。この例では、パターンに一致するすべてのサーバーの合計 CPU に関するデータが返されます。

* **文字のリストまたは範囲**: 大括弧内 ([...]) で文字を定義して、パス・ストリング内の単一の文字位置を指定できます。 

    2 つの文字をハイフン (-) で区切って指定することにより、文字の範囲 (両端を含む) を設定できます。 それらの 2 つの文字の間の任意の文字が一致します。 
	
	大括弧内に 1 つ以上の文字範囲を定義できます。 
	
	1 組の大括弧内の文字を、範囲として読み取ることができない場合、それらの文字は値のリストとして扱われます。 
	
	ハイフン (-) は、それを大括弧内の先頭または末尾に置くことにより、値のリスト内の 1 文字として含めることができます。

* **値リスト**: 中括弧内にコンマで区切った値を設定して、値リストを定義できます。 

    例えば、`servers.myserver.cpu.total.user` および `servers.myserver.cpu.total.system` というパスのメトリックをダウンロードする場合、`servers.myserver.cpu.total.{user,system}` という単一パスを設定することで、両方のタイプに対応できます。



## 期間の設定
{: #time}

オプションで、相対時間または絶対時間を使用して、期間を指定できます。 照会パラメーター **From** および **Until** を定義する必要があります。  

* 期間の開始時刻が省略されている場合、デフォルト値は 24 時間前です。 

* 期間の終了時刻が省略されている場合、デフォルト値は現在時刻 *now* です。

**相対時間** の場合は常に、先頭に負符号 (-) があり、末尾に時間単位が付加されます。 

以下の表に、使用できるさまざまな相対時間の省略形を示します。


| 省略 | 説明 |
|--------------|-------------|
| s            | 秒     |
| min          | 分     |
| h            | 時       |
| d            | 日        |
| w            | 週       |
| mon          | 月      |
| now          | 現在時刻 |


**絶対時間**を定義する場合、`HH:MM_YYMMDD`、`YYYYMMDD`、`MM/DD/YY` のうちの任意の形式を使用できます。

| 省略 | 説明 |
|--------------|-------------|
| YYYY         | 4 桁の年 |
| MM           | 2 桁の月 (01 = 1 月など) |
| DD           | 2 桁の日付 (01 から 31) |
| hh           | 2 桁の時間 (00 から 23) |
| mm           | 2 桁の分 (00 から 59) |
| ss           | 2 桁の秒 (00 から 59) |

**例**

以下の表に、*from* および *until* パラメーターを設定することによってさまざまな期間を設定する方法の例を示します。

<table>
  <caption>表 1. *from* および *until* パラメーターを設定することによってさまざまな期間を設定する方法の例</caption>
  <tr>
    <th>例</th>
	<th>説明</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>最後の月曜から現在までのデータを含む期間</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>1 カ月 (例えば 11 月) に設定された期間 </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>24 時制で、例えば 2017 年 7 月 1 日の 02:00 から 14:00 までのデータを表示</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>例えば先週の同じ曜日を表示</td>
  </tr>
  
</table>


