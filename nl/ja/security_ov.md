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


# セキュリティー
{: #security_ov}

ユーザーが実行可能な
{{site.data.keyword.monitoringshort}} サービス・アクションを
制御するために、1 人のユーザーに 1 つ以上の役割を割り当てることができます。 メトリックおよびアラートを処
理するユーザーを認証するには、UAA トークン、IAM トークン、または API キーを使用することができます。 
{:shortdesc}





## 認証モデル
{: #auth}

スペースの {{site.data.keyword.monitoringshort}} サービスに保管されているメトリックを処理するには、認証トークンまたは API キーが必要です。 

セキュリティー・トークンを取得する場合は、以下を参照してください。

* [UAA トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa)
* [IAM トークンの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)

API キーを取得する場合は、
[API キーの取得](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)を参照してください。 API キーが漏えいした場合は、それを削除することによって取り消すことができます。 その後、新しい API キーを再作成できます。 詳しくは、[{{site.data.keyword.Bluemix_notm}} UI を使用した API キーの取り消し](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#revoke_ui)を参照してください。 

UAA トークンおよび IAM トークンは、一定期間後に期限切れになります。 API キーには有効期限切れはありません。 

以下の表に、各ドメイン・タイプでサポートされているセキュリティー・モデルをリストします。

<table>
  <caption>表 1. 各ドメインでサポートされるセキュリティー・モデル</caption>
  <tr>
    <th></th>
	<th align="right">アカウント</th>
    <th align="right">組織</th>
    <th align="right">スペース</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">いいえ</td>
	<td align="center">はい</td>
	<td align="center">はい</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">はい</td>
	<td align="center">はい</td>
	<td align="center">はい</td>
  </tr>
</table>

{{site.data.keyword.monitoringshort}} サービスは、IAM アクセス制御機能を使用して、ユーザーまたはサービスがドメインに対して実行できるアクションまたは操作を管理します。 例えば、ユーザーがドメインに対してダッシュボードを送信および作成することは許可するが、ドメインからメトリックを取り出すことは許可しないように IAM ポリシーを定義することができます。



## Cloud Foundry の役割
{: #bmx_roles}

以下の表に、{{site.data.keyword.monitoringshort}} サービスを処理するための Cloud Foundry の各役割をリストします。

<table>
  <caption>表 2. {{site.data.keyword.monitoringshort}} サービスを処理するための Cloud Foundry の役割および特権</caption>
  <tr>
    <th>役割</th>
	<th>ドメイン</th>
	<th>アクセス権</th>
  </tr>
  <tr>
    <td>管理者</td>
	<td>組織の <br>スペース</td>
	<td>すべての RESTful API</td>
  </tr>
  <tr>
    <td>開発者</td>
	<td>スペース</td>
	<td>すべての RESTful API</td>
  </tr>
  <tr>
    <td>監査員</td>
	<td>組織の <br>スペース</td>
	<td>メトリックの照会などの読み取り専用操作を実行する RESTful API のみ。</td>
  </tr>
</table>

UI でのユーザー役割の割り当てについては、[Cloud Foundry アクセス権限の管理](/docs/iam?topic=iam-mngcf#mngcf)を参照してください。



## IAM の役割
{: #iam_roles}

以下の表は、メトリックを処理する際の
{{site.data.keyword.monitoringshort}} サービス・アクション、およびこれらのタスクを実行する権限をユーザーに付与する IAM 役割を示します。

<table>
  <caption>表 3. メトリックの処理 </caption>
  <tr>
	<th>アクション</th>
	<th>IAM 役割</th>
  </tr>
  <tr>
    <td>ドメインにメトリックを送信する</td>
	<td>管理者、エディター、オペレーター</td>
  </tr>
  <tr>
    <td>メトリックを取得/照会する</td>
	<td>管理者、エディター、ビューアー</td>
  </tr>
  <tr>
    <td>ドメイン内でメトリックを検索する</td>
	<td>管理者、エディター</td>
  </tr>
</table>

以下の表は、アラートを処理する際の
{{site.data.keyword.monitoringshort}} サービス・アクション、およびこれらのタスクを実行する権限をユーザーに付与する IAM 役割を示します。

<table>
  <caption>表 4. アラートの処理 </caption>
  <tr>
	<th>アクション</th>
	<th>IAM 役割</th>
  </tr>
  <tr>
    <td>アラート・ルールの作成、編集、および削除</td>
	<td>管理者、エディター</td>
  </tr>
  <tr>
    <td>アラートの表示</td>
	<td>管理者、エディター、ビューアー</td>
  </tr>
  <tr>
    <td>アラート通知の作成、編集、および削除</td>
	<td>管理者、エディター</td>
  </tr>
  <tr>
    <td>通知の表示</td>
	<td>管理者、エディター、ビューアー</td>
  </tr>
  <tr>
    <td>トリガーされたアラートの履歴レコードの表示</td>
	<td>管理者、エディター、ビューアー</td>
  </tr>
</table>

UI でのユーザー役割の割り当てについては、[IAM アクセス権限の管理](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)を参照してください。

