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

# Grafana でのアラートの構成
{: #config_alerts_grafana}

{{site.data.keyword.monitoringshort}} サービスには、照会ベースのアラート・システムが用意されています。 テンプレート変数を持たないアラートは、ダッシュボードで Grafana に構成できます。 
{:shortdesc}

Grafana UI を使用してメトリック照会にアラートを構成するには、以下の手順を実行します。

1. Grafana を起動します。
2. 1 つ以上の通知チャネルを定義します。
3. グラフと、少なくとも 1 つの照会メトリックを含む Grafana ダッシュボードを作成します。 
4. Grafana グラフの**「Alerts」**タブでアラートを構成します。

## 手順 1: Grafana の起動
{: #step1_cag1}

ブラウザーから Grafana を起動します。 例えば、米国南部の地域で Grafana を開くには、次の URL を入力します。[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)

地域ごとの Grafana URL のリストについては、[{{site.data.keyword.monitoringshort}} サービスの URL](/docs/services/cloud-monitoring/monitoring_ov.html#region) を参照してください。

## 手順 2: 1 つ以上の通知チャネルの定義
{: #step2_cag2}

以下のステップを実行します。

1. Grafana でサイド・メニュー・バーを選択します。

2. **「Alerting」>「Notification channels」>「New channel」**を選択します。

3. 新規チャネルのデータを入力します。 例えば、E メール通知チャネルを追加します。

<table>
  <caption>新規チャネルを作成するために入力する必要がある E メール通知方法とデータ</caption>
  <tr>
     <th>フィールド</th>
     <th>説明</th>
  </tr>
  <tr>
    <td>名前</td>
    <td>通知チャネルの名前。 この値は固有でなければなりません。</td>
  </tr>
  <tr>
    <td>説明</td>
    <td>文書化の目的のために含めることのできる追加情報。</td>
  </tr>
  <tr>
    <td>タイプ</td>
    <td>**「E メール」**を選択します。</td>
  </tr>
  <tr>
    <td>E メール ID</td>
    <td>受信者の E メール・アドレスを入力します。 </br>複数の E メール・アドレスをコンマで区切って入力できます。</td>
  </tr>
</table>

<table>
  <caption>新規チャネルを作成するために入力する必要がある Webhook 通知方法とデータ</caption>
  <tr>
     <th>フィールド</th>
     <th>説明</th>
  </tr>
  <tr>
    <td>名前</td>
    <td>通知チャネルの名前。 この値は固有でなければなりません。</td>
  </tr>
  <tr>
    <td>説明</td>
    <td>文書化の目的のために含めることのできる追加情報。</td>
  </tr>
  <tr>
    <td>タイプ</td>
    <td>**「Webhook 」**を選択します。</td>
  </tr>
  <tr>
    <td>Webhook POST URL</td>
    <td>POST を実行する URL を入力します。</td>
  </tr>
  <tr>
    <td>Webhook ヘッダー (Webhook headers)</td>
    <td>任意のヘッダーを入力します。</td>
  </tr>
  <tr>
    <td>Webhook 照会パラメーター (Webhook query parameters)</td>
    <td>任意の照会パラメーターを入力します。</td>
  </tr>
</table>

<table>
  <caption>新規チャネルを作成するために入力する必要がある PagerDuty 通知方法とデータ</caption>
  <tr>
     <th>フィールド</th>
     <th>説明</th>
  </tr>
  <tr>
    <td>名前</td>
    <td>通知チャネルの名前。 この値は固有でなければなりません。</td>
  </tr>
  <tr>
    <td>説明</td>
    <td>文書化の目的のために含めることのできる追加情報。</td>
  </tr>
  <tr>
    <td>タイプ</td>
    <td>**「PagerDuty」**を選択します。</td>
  </tr>
  <tr>
    <td>PagerDuty API キー (PagerDuty API key)</td>
    <td>PagerDuty キーを入力します。</td>
  </tr>
</table>

## 手順 3: メトリックの定義
{: #step3_cag3}

以下の手順を実行して、新規ダッシュボードを作成します。

1. サイド・メニュー・バーのトグル を選択します。![Grafana サイド・メニュー・バー](images/grafana_settings.gif "Grafana サイド・メニュー・バー")
2. **「Dashboards」**を選択します。
3. **「New」**をクリックします

ダッシュボードが開きます。 ダッシュボードには、すぐに構成できる空の行が含まれています。 

次に、以下のようにしてメトリック照会を追加します。

1. *「Graph」*パネルを追加します。
2. **「Graph」**をクリックします。
3. グラフのタイトルをクリックし、次に**「edit」**を選択します。
    
    *「Metrics」*タブが開きます。 デフォルト・データ・ソースが表示されています。
    
4. グラフに表示されるデータをフィルターに掛けるメトリック照会を定義します。 


## 手順 4: アラートの定義
{: #step4_cag4}

Grafana UI でアラートを定義するには、以下の手順を実行します。

1. **「Alert」**タブを選択します。
2. **「Alert Config」**セクションで、アラート通知の生成条件を定義するルールを定義します。

    **「Evaluate every」**フィールドと、**「Conditions」**セクションを構成します。

3. **「Notifications」**セクションで、1 つ以上の通知チャネルを選択します。

**注:** 

* 条件が設定されると、しきい値セットを定義するための赤い線がグラフに表示されます。 それをグラフ上にドラッグしてグラフを変更することができます。
* アラートが作成されたら、アラートを変更する場合は、アラート API を使用して行う必要があります。
* **「Delete」**を選択すると、アラートが削除されます。

## 次: アラートが生成されることの確認
{: #next_cag5}

例えば、E メール通知チャネルを作成した場合、E メールを確認します。

**「IBM Cloud Monitoriing」**が送信者になっている E メールを探します。

E メールには、出されたアラートに関する情報と、状態を表示できる Grafana ダッシュボードへのリンクが含まれています。

以下に例を示します。

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


