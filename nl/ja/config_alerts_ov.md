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



# アラートの構成
{: #config_alerts_ov}

{{site.data.keyword.monitoringshort}} サービスには、照会ベースのアラート・システムが用意されています。 アラートは、{{site.data.keyword.monitoringshort}} API を使用するか、Grafana を介して構成できます。 アラートを構成するには、モニターするメトリック照会ごとにルールと通知方法を設定する必要があります。 通知は、E メールの送信、Webhook のトリガー、または PagerDuty へのアラートの送信によって実行できます。
{:shortdesc}

メトリックの通知をトリガーするアラートを定義できます。 アラートは、モニターするメトリック照会、しきい値、およびしきい値を超えた際に実行するアクションを記述するルールと、1 つ以上の通知方法によって定義されます。  

以下の表に、アラートの処理に使用できるさまざまな方法とサポートされるアクションをリストします。

<table>
  <caption>アラートの処理方法</caption>
	<tr>
    <th>方法</th>
		<th>アラートの定義</th>
		<th>アラートの更新</th>
		<th>アラートの削除</th>
	</tr>
	<tr>
    <td>アラート API</td>
		<td>はい</td>
		<td>はい</td>
		<td>はい</td>
	</tr>
	<tr>
    <td>Grafana</td>
		<td>はい</td>
		<td>はい</td>
		<td>はい</td>
	</tr>
</table>

**注:** アラート API を使用して定義するアラートは、Grafana ダッシュボードには表示されません。


以下の図に、アラートを出すように {{site.data.keyword.monitoringshort}} サービスで構成できるさまざまな通知タイプを示します。

![{{site.data.keyword.monitoringlong}} サービス内で使用可能な通知タイプのコンポーネント概要図](images/alerts_ov_f1.gif)

単一インスタンス用または複数インスタンス用のアラートを定義できます。 アラート・ルールを通じてモニターする照会にワイルドカードが含まれる場合、そのワイルドカードは複数のターゲット (すなわち複数のサービス・インスタンスまたはアプリケーション・インスタンス) を識別します。 {{site.data.keyword.monitoringshort}} サービスは、5 分ごとに、アラート・ルールで構成されている照会を実行し、各インスタンスまたは複数インスタンスについて返された最後のデータ・ポイントをチェックします。 {{site.data.keyword.monitoringshort}} サービスは、各インスタンスの最後の状態を追跡し、アラートの状態が変わった場合に新規アラートを生成します。 



## アラート API を使用したアラートの処理
{: #api}

アラート API を使用してアラートを定義、更新、または削除できます。

アラート API を使用してメトリック照会にアラートを定義するには、以下のことを行う必要があります。

1. Grafana ダッシュボードで 1 つ以上のメトリック照会を定義します。 

    **注:** テンプレート変数を使用するアラートは、Grafana ダッシュボードでは定義できません。

2. Grafana ダッシュボードで定義されているメトリック照会にアラートを構成します。

    * [E メールを送信するアラートを構成します](/docs/services/cloud-monitoring/alerts/configure_email_alert.html#configure_email_alert)。
    * [PagerDuty 通知を送信するアラートを構成します](/docs/services/cloud-monitoring/alerts/configure_pagerduty_alert.html#configure_pagerduty_alert)。
    * [Webhook 通知を送信するアラートを構成します](/docs/services/cloud-monitoring/alerts/configure_webhook_alert.html#configure_webhook_alert)。

    **注:** E メール通知を定義できるのは、アカウント・メトリック・ドメインで定義されているメトリック照会に対してのみになります。



## Grafana を使用したアラートの処理
{: #grafana}

Grafana ダッシュボードでアラートを直接定義および削除できます。 ルール定義も更新できます。 ただし、通知チャネルの変更は、アラート API を使用して行う必要があります。

Grafana でアラートを処理する際は、以下の情報を考慮してください。

* ルールに割り当てられた通知チャネルを変更するには、アラート API を使用する必要があります。
* スペース・ドメインで通知チャネルを削除したときに、そのチャネルが構成されたルールは更新されません。 アラート API を使用してルールを変更し、そこからその通知チャネルを削除する必要があります。 

Grafana ダッシュボードで直接メトリック照会にアラートを定義するには、以下のことを行う必要があります。

1. Grafana ダッシュボードで 1 つ以上のメトリック照会を定義します。 

    **注:** テンプレート変数を使用するアラートは、Grafana ダッシュボードでは定義できません。

2. Grafana ダッシュボードで定義されているメトリック照会にアラートを構成します。

    詳しくは、[Grafana でのアラートの構成](/docs/services/cloud-monitoring/alerts/config_alerts_grafana.html#config_alerts_grafana)を参照してください。


## アラートの状態
{: #status}

ルールが有効になっている場合、アラートの状態は以下のいずれかになります。

* *OK*: 以下の場合、ルールの状態が *OK* に設定されます。
    
	* そのルールに関連付けられたメトリック照会用のデータが {{site.data.keyword.monitoringshort}} サービス内で使用可能である。 警告しきい値とエラーしきい値を設定済みである。 データの値はしきい値を超えていない。
	 
	* そのルールに関連付けられたメトリック照会用のデータが {{site.data.keyword.monitoringshort}} サービス内に存在せず、ルール・プロパティー `allow_no_data` を *true* に構成している。           
	 
* *WARNING*: そのルールに関連付けられたメトリック照会用のデータが {{site.data.keyword.monitoringshort}} サービス内で使用可能である場合、ルールの状態が *WARNING* に設定されます。 警告しきい値とエラーしきい値を設定済みです。 データの値は警告しきい値とエラーしきい値の間です。
	
* *ERROR*: そのルールに関連付けられたメトリック照会用のデータが {{site.data.keyword.monitoringshort}} サービス内で使用可能である場合、ルールの状態が *ERROR* に設定されます。 警告しきい値とエラーしきい値を設定済みです。 エラーしきい値に達しています。  

* *UNKNOWN*: そのルールに関連付けられたメトリック照会用のデータが {{site.data.keyword.monitoringshort}} サービス内に存在しない場合、ルールの状態が *UNKNOWN* に設定されます。 ルールに対して構成したプロパティー `allow_no_data` に基づいて、通知を受け取るかどうかを構成できます。 このプロパティーを `false` に設定した場合、そのルール用のデータが見つからなかったことが通知されます。



	
## アラート履歴
{: #history}

アラートの状態が変更されるたびに、アラートの履歴レコードが更新されます。 アラート API (*/v1/alert/history*) を使用して、メトリックの履歴に関する情報を取得できます。

アラートの状態は、以下のいずれかのシナリオの状況を定義するために使用されます。

* ルールが通知をトリガーする前の照会の状況。
* ルールが通知をトリガーした後の照会の状況。 

例えば、警告しきい値を超えると、*OK* から *WARNING* への遷移を記録する履歴レコードが生成されます。 同様に、値が再びしきい値を下回ると、*WARNING* から *OK* への遷移を記録する履歴レコードが生成されます。

詳しくは、
[
ルールの履歴の取得](/docs/services/cloud-monitoring/alerts/retrieve_history.html#retrieve_history)を参照してください。


## ルール
{: #rules1}

ルールは、モニターするメトリック照会、しきい値、およびしきい値を超えた際に実行するアクションを記述します。 

* アラート API を使用して、ルールの作成、削除、および更新、ルールの詳細の表示、およびすべてのルールのリストを行うことができます。 詳しくは、[ルールの処理](/docs/services/cloud-monitoring/alerts/rules.html#rules)を参照してください。

    * ルールを作成するには、
[
ルールの作成](/docs/services/cloud-monitoring/alerts/rules.html#create)を参照してください。
	* ルールを削除するには、
[ルールの削除](/docs/services/cloud-monitoring/alerts/rules.html#delete)を参照してください。
	* ルールを更新するには、
[ルールの更新](/docs/services/cloud-monitoring/alerts/rules.html#update)を参照してください。
	* すべてのルールをリストするには、
[すべてのルールのリスト表示](/docs/services/cloud-monitoring/alerts/rules.html#list)を参照してください。
	* ルールに関する情報を表示するには、
[ルールの詳細の表示](/docs/services/cloud-monitoring/alerts/rules.html#showing-the-details-of-a-rule)を参照してください。

* アラート・システムは、スペース内で有効になっているルールを 5 分ごとにチェックします。

* デフォルトでは、ルールは作成時に有効になっています。 ただし、ルールを定義し、フィールド *enable* を `false` に構成することによって、そのルールを無効にすることができます。

* ルール・パラメーター *comparison* が below に設定されている場合、error_level の値は、警告レベル値よりも低くなければなりません。 ルール・パラメーター *comparison* が above に設定されている場合、error_level の値は、警告レベル値よりも高くなければなりません。

* デフォルトでは、フィールド *allow_no_data* が `true` に設定された状態でルールが作成されます。 使用可能なデータ・ポイントがない場合、ルール条件がトリガーされない限り通知は送信されません。 ルール X のデータが見つからなかったことを伝える通知を受け取りたい場合は、フィールド *allow_no_data* を `false` に設定する必要があります。 

**ヒント:** Grafana でアラート・ルールを通じてモニターする照会を検証してください。 タイムアウトにならないことを確認してください。 例えば、長時間を構成した結果として、またはワイルドカードを含む照会を定義した場合に、照会がタイムアウトになることがあります。 Grafana で照会がタイムアウトになったときに、その照会用に構成されたアラートはトリガーされないことに注意してください。

ルールを定義するには、以下のフィールドが必要です。

<table>
  <caption>表 1. ルールを定義するために使用されるフィールドのリスト</caption>
  <tr>
    <th>フィールド名</th>
	<th>説明</th>
  </tr>
  <tr>
    <td>name</td>
	<td>ルールの名前。 この名前は固有でなければなりません。</td>
  </tr>
  <tr>
    <td>description</td>
	<td>ルールの要約。</td>
  </tr>
  <tr>
    <td>expression</td>
	<td>モニターし、しきい値を超えたらアラートを送信するメトリック照会。 <br>有効な式は、単一メトリック名、
ワイルドカードによって識別される複数のメトリック、またはデータを集約する関数です。 <br>**ヒント:** 検証済みの照会を、Grafana からコピーできます。</td>
  </tr>
  <tr>
    <td>enabled</td>
	<td>次のようにルールの状況を記述します。 <br>ルールを有効にするには、`true` に設定します。 <br>ルールを無効にするには `false` に設定します。 <br>デフォルトでは、`true` に設定されます。</td>
  </tr>
  <tr>
    <td>from</td>
	<td>expression フィールドに定義した照会に設定されているしきい値に基づいてデータを分析するために使用される初期ポイント・イン・タイム。 例: `"from": "-5min"`</td>
  </tr>
  <tr>
    <td>until</td>
	<td>expression フィールドに定義した照会に設定されているしきい値に基づいてデータを分析するために使用される終了ポイント・イン・タイム。 例: `"until": "now"`</td>
  </tr>
  <tr>
    <td>comparison</td>
	<td>実行するチェックのタイプを識別するために使用される比較演算。 有効な値は、*below* と *above* です。 </td>
  </tr>
  <tr>
    <td>comparison_scope</td>
	<td>分析するデータのスコープを定義します。 <br>シリーズ (照会に使用可能なデータ) の最後の値を表示するには、*last* に設定します。</td>
  </tr>
  <tr>
    <td>error_level</td>
	<td>エラー・アラートをトリガーするために設定するしきい値を定義します。 <br>到達したらエラー・アラートが生成される値を設定します。 例: `"error_level" : 27.94`</td>
  </tr>
  <tr>
    <td>warning_level</td>
	<td>警告アラートをトリガーするために設定するしきい値を定義します。 <br>到達したら警告アラートが生成される値を設定します。 例: `"warning_level" : 24`</td>
  </tr>
  <tr>
    <td>frequency</td>
	<td>チェックが実行される頻度を定義します。 <br>単位は分、時間、日のいずれかであり、例えば 5min、1h、7d と指定します。 <br>例えば、毎分チェックが行われるように、`"frequency": "1min"` と設定できます。 <br>**注:** 現在は、この頻度は 5 分に固定されています。</td>
  </tr>
  <tr>
    <td>dashboard_url</td>
	<td>モニターする照会が定義されている Grafana ダッシュボードの URL を定義します。</td>
  </tr>
    <tr>
    <td>allow_no_data</td>
	<td>使用可能なデータ・ポイントがない場合に通知が送信される条件を定義します。 <br>デフォルトでは、`true` に設定されます。 <br>ルール X のデータが見つからなかったという通知を受け取りたい場合は、`false` に設定します。</td>
  </tr>
  <tr>
    <td>notifications</td>
	<td>このルールでトリガーするアクションを定義する通知の名前。 <br>**注:** コンマで区切って通知名をリストすることにより、ルールごとに 1 つ以上の通知を定義できます。</td>
  </tr>
</table>

例えば、ルールのサンプルを以下に示します。

```
{
  "name": "checkbytesin1",
  "description": "MH check Bytes In per second",
  "expression": "movingAverage(messagehub.65ad9211-1234-5678-a751-c82123411eee.1.kafka-java-console-sa
mple-topic.BytesInPerSec.15MinuteRate,\"5min\")",
  "enabled": true,
  "from": "-5min",
  "until": "now",
  "comparison": "below",
  "comparison_scope": "last",
   "error_level" : 22.94,
   "warning_level" : 25,
  "frequency": "1min",
  "dashboard_url": "https://metrics.ng.bluemix.net",
  "notifications": [
    "emailXXX"
  ]
}
```
{: screen}



## 通知
{: #alert_notifications}

通知は、アラートがトリガーされた際の通知に使用される方法と詳細を記述しています。 例えば、メトリックの警告通知およびエラー通知を受け取るには、警告しきい値をモニターするルールを 1 つ定義し、それからエラーしきい値をモニターするルールを 1 つ定義します。 

* 通知が送信されるのは、アラートの状態が変わったとき (例えば、メトリックのアラートの状態が「OK」から「ERROR」、または「ERROR」から「WARNING」に変わったとき) だけです。 

    **注:** アラート・ルールが同じ状態、すなわち *OK*、*WARNING*、*ERROR*、または *UNKNOWN* のままの場合は、次の反復の際に再トリガーされません。

* 通知は、24 時間イベントと見なされます。 通知のトリガーが可能な時間間隔を指定することはできません。

* コンマで区切って通知名をリストすることにより、ルールごとに 1 つ以上の通知方法を構成できます。 

* [アラート REST API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window} を使用して、通知の作成、削除、および更新、通知の詳細表示、およびスペース内に定義されている通知のリストを行うことができます。

    * 通知を作成するには、
[通知の作成](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create)を参照してください。
	* 通知を削除するには、
[通知の削除](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_delete)を参照してください。
	* 通知を更新するには、
[通知の更新](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_update)を参照してください。
	* すべての通知をリストするには、
[すべての通知のリスト表示](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_list)を参照してください。
	* 通知に関する情報を表示するには、
[通知の詳細の表示](/docs/services/cloud-monitoring/alerts/notifications.html#show)を参照してください。

* E メール通知、PagerDuty 通知、Webhook 通知を構成することができます。 

**注:** アラート通知の定義は、ルールとは無関係に行います。それにより、それらの通知を複数のルールで再使用することができます。

	
## 通知 - JSON テンプレート
{: #notification_template}
	
通知は JSON ファイルです。 

以下の表は、通知方法のタイプごとの通知テンプレートを含んでいます。

<table>
  <caption>表 3. 通知テンプレート</caption>
  <tr>
    <th>タイプ</th>
	<th>テンプレート</th>
	<th>サンプル</th>
  </tr>
  <tr>
    <td>Email</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Email",
	"description" : "Description",
	"detail": "EmailAddress"
	}
	```
	{: screen}
	</td>
	<td>
	```
	{
	"name": "my-email",
	"type": "Email",
	"description" : "Send email notification when there is an infrastructure problem.",
	"detail": "xxx@yyy.com"
	}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>Webhook</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Webhook",
	"description" : "Description",
	"detail": "Endpoint"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-webhook",
	"type": "Webhook",
	"description" : "Fire a webhook when there is an infrastructure problem..",
	"detail": "https://myendpoint.bluemix.net?key=abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>Pagerduty</td>
	<td>
	```
	"name": "Template_Name",
	"type": "PagerDuty",
	"description" : "Description",
	"detail": "Pagerduty_APIkey"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-pagerduty",
	"type": "PagerDuty",
	"description" : "Fire a PagerDuty alert when there is an infrastructure problem..",
	"detail": "abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
</table>

各部の意味は、次のとおりです。

* *Template_Name* は、通知テンプレートの名前を定義します。
* *Description* は、このタイプの通知がどのような時に使用されるかを説明します。
* *EmailAddress* は、通知の受信者の E メール・アドレスを定義します。
* *Endpoint* は、POST を実行する URL を定義します。 
* *Pagerduty_APIkey* は、固有 API キーを定義します。 この API キーは、PagerDuty アカウントの管理者または所有者によって生成されます。



## ルール - JSON テンプレート
{: #rules_template}

ルールは JSON ファイルを使用して記述されます。 

以下のコードは、ルールのテンプレートです。

```
{
"name": "Enter rule name",
"description": "Desccribe rule",
"expression": "Add metric query",
"enabled": true,
"from": "-5min",
"until": "now",
"comparison": "below",
"comparison_scope": "last",
"error_level" : xxxx,
"warning_level" : xxxx,
"frequency": "1min",
"dashboard_url": "https://metrics.ng.bluemix.net",
"notifications": [
 "List of Notifications by name. Include all the motification methods for this rule separated by commas."
 ]
}
```
{: screen}



