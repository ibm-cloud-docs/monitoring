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


# ユーザー権限の付与
{: #grant_permissions}

{{site.data.keyword.Bluemix}} では、ユーザーに 1 つ以上の役割を割り当てることができます。 これらの役割は、{{site.data.keyword.monitoringshort}} サービスを処理するユーザーが使用可能となるタスクを定義します。 
{:shortdesc}

メトリックを処理する権限をユーザーに付与するには、このユーザー
が {{site.data.keyword.monitoringshort}} サービスを使用して実行できるアクショ
ンを記述する、このユーザー用のポリシーをアカウントに追加する必要があります。 アカウント所有者のみが、個々のポリ
シーをユーザーに割り当てることができます。


## IBM Cloud UI を使用した IAM ポリシーのユーザーへの割り当て 
{: #assign_policy_ui}

以下の手順を実行し、{{site.data.keyword.monitoringshort}} サービスを処理する権限をユーザーに付与します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、
{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://console.bluemix.net ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    *「ユーザー」*ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. ユーザーがアカウントのメンバーの場合、リストからユーザー名を選択するか、*「アクション」*メニューから
**「ユーザーの管理 (Manage user)」**をクリックします。

    ユーザーがアカウントのメンバーではない場合、
[ユーザーの招待](/docs/iam?topic=iam-iamuserinv#iamuserinv)を参照してください。

4. **「サービス・ポリシーの割り当て (Assign service policies)」**をクリックします。

5. ポリシーに関する情報を入力します。 以下の表は、ポリシーを定義する必須またはオプションのフィールドを示します。 

    <table>
	  <caption>IAM ポリシーを構成するためのフィールドのリスト</caption>
	  <tr>
	    <th>フィールド</th>
		<th>値</th>
		<th>状況</th>
	  </tr>
	  <tr>
	    <td>サービス</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>必須</td>
	  </tr>
	  <tr>
	    <td>役割</td>
		<td>1 つ以上の IAM 役割を選択してください。 <br>有効な役割は、*アドミニストレーター*、*オペレーター*、*エディター*、*ビューアー*です。 <br>役割ごとに許可されるアクションについて詳しくは、[IAM の役割](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#iam_roles)を参照してください。</td>
		<td>必須</td>
	  </tr>
	  <tr>
	    <td>地域</td>
		<td>ユーザーがメトリックを処理する権限を付与される地域を指定することができます。 **「オプション・サービス・コンテキストを指定する (Specify optional service context)」**を選択します。 次に、1 つ以上の地域をそれぞれ追加します。または、すべての地域に権限を付与するには、**「すべての現行地域 (All current regions)」**を選択します。</td>
		<td>オプション</td>
	  </tr>
	</table>
	
6. 「**ポリシーの割り当て**」をクリックします。
	
構成したポリシーは、選択した地域で利用できます。 

## コマンド・ラインを使用した IAM ポリシーのユーザーへの割り当て
{: #assign_policy_commandline}

以下の手順を実行して、コマンド・ラインを使用してメトリックを表示する権限をユーザーに付与します。

1. (前提条件) {{site.data.keyword.Bluemix_notm}} CLI をインストールします。

   詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)を参照してください。
   
   CLI がインストールされたら、次の手順に進んでください。
	
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)を参照してください。
	
3. アカウント ID を取得します。 

    以下のコマンドを実行して、アカウント ID を取得します。

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	アカウントとその GUID のリストが表示されます。
	
	権限をユーザーに与える予定のアカウントの ID をエクスポートします。 「`$acct_id`」のようなシェル変数を構成します。以下に例を挙げます。
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. 権限を付与するユーザーの {{site.data.keyword.IBM_notm}} ID を取得します。

    1. アカウントに関連付けられたユーザーを表示します。 以下のコマンドを実行します。
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. ユーザーの GUID を取得します。 **注: この手順は、権限を付与する予定のユーザーが完了する必要があります。**
	
	    例えば、ユーザーに自分のユーザー ID を取得するために以下のコマンドを実行するよう依頼します。
		
		IAM トークンを取得します。 詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli)を参照してください。

        IAM トークンの最初の 2 つのドットの間にある IAM トークンのデータを取得します。 「`$user_data`」のようなシェル変数にデータをエクスポートします。 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		例えば、ユーザー ID を取得する以下のコマンドを実行します。 このコマンドは、このサンプルでは jq を使用して情報を JSON の定形式テキストにデコードします。
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		このコマンドの実行結果は以下のようになります。
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		ユーザー ID (*id* フィールドの値) をアカウント所有者に送信します。 
		
	3. `$user_ibm_id` のようなシェル変数にユーザー ID をエクスポートします。
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. ユーザーがアカウントのメンバーではない場合は招待します。 詳しくは、[ユーザーの招待](/docs/iam?topic=iam-iamuserinv#iamuserinv)を参照してください。

    例えば、以下のコマンドを実行してユーザー xxx@yyy.com をアカウント zzz@ggg.com に招待します。
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. ポリシー・ファイル名を作成します。 

    例えば、次のテンプレートを使用して、米国南部地域での表示権限を付与します。
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	ポリシー・ファイルに `policy.json` という名前を付けます。
	
5. ご使用のユーザー ID の IAM トークンを取得します。

    詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli)を参照してください。

    `$iam_token` のようなシェル変数に IAM トークンをエクスポートします。以下に例を挙げます。
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. {{site.data.keyword.monitoringshort}} サービスを処理する権限をユーザーに付与します。 

   次の cURL コマンドを実行して、米国南部地域での権限を付与します。
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	次の cURL コマンドを実行して、英国地域での権限を付与します。
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## IBM Cloud UI を使用したユーザーへの CF 役割の付与 
{: #grant_permissions_ui_space}


スペースのドメインまたは組織のドメインでメトリックを処理するには、ユーザーは {{site.data.keyword.Bluemix_notm}} で  Cloud Foundry (CF) 役割を割り当てられている必要があります。 CF 役割は、スペースまたは組織で、ユーザーが  {{site.data.keyword.monitoringshort}} サービスを使用して実行可能なアクションを記述します。 

以下の手順を実行し、{{site.data.keyword.monitoringshort}} サービスを処理する権限をユーザーに付与します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://bluemix.net ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    *「ユーザー」*ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. ユーザーがアカウントのメンバーの場合、リストからユーザー名を選択するか、*「アクション」*メニューから
**「ユーザーの管理 (Manage user)」**をクリックします。

    ユーザーがアカウントのメンバーではない場合、
[ユーザーの招待](/docs/iam?topic=iam-iamuserinv#iamuserinv)を参照してください。

4. **「組織の割り当て」**をクリックします。

5. ポリシーに関する情報を入力します。 以下の表は、ポリシーを定義する必須またはオプションのフィールドを示します。 

    <table>
	  <caption>CF ポリシーを構成するためのフィールドのリスト</caption>
	  <tr>
	    <th>フィールド</th>
		<th>値</th>
	  </tr>
	  <tr>
	    <td>組織</td>
		<td>リストから組織を選択してください。</td>
	  </tr>
	  <tr>
	    <td>組織の役割</td>
		<td>**「組織の役割なし」**を選択します。 ただし、ユーザーが組織の役割を割り当てられている場合、リストから組織の役割を選択します。 <br>有効な値は、**「請求管理者」**、**「監査員」**、**「管理者」** です。</td>
	  </tr>
	  <tr>
	    <td>地域</td>
		<td>リストから地域を選択します。 <br>有効な値は、**「すべての現行地域」**、**「米国南部」**、**「英国」**です。</td>
	  </tr>
	  <tr>
	    <td>スペース</td>
		<td>「*地域*」フィールドが **「すべての現行地域 (All current regions)」**に設定されている場合は、デフォルトで **「すべての現行スペース (All current spaces) 」**が事前定義されます。 個々のスペースに権限を付与するには、特定の地域を選択し、次にリストからスペースを選択します。</td>
	  </tr>
	  <tr>
	    <td>スペースの役割</td>
		<td>リストからスペースの役割を選択してください。 <br>有効な値は、**「管理者」**、**「監査員」**、**「開発者」**、および**「スペースの役割なし」**です。 詳しくは、[Cloud Foundry の役割](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#bmx_roles)を参照してください。</td>
	  </tr>
	</table>
	
6. 「**ポリシーの割り当て**」をクリックします。
	
構成したポリシーは、選択した地域で利用できます。 


