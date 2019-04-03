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



# Grafana の使用に関する FAQ
{: #grafana_qa}

{{site.data.keyword.monitoringshort}} サービスでの Grafana の使用に関する一般的な質問の回答を以下に示します。 
{:shortdesc}

* [アラート API を使用して定義したアラートが Grafana ダッシュボードに表示されない](/docs/services/cloud-monitoring/qa/grafana_qa.html#alerts1)
* [Grafana ダッシュボードに加えた変更を保存しようとすると BXNMSAL41E を受け取る](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL41E)
* [Grafana ダッシュボードにアラートを追加した後で変更を保存しようとすると BXNMSAL36E を受け取る](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL36E)
* [Monitoring サービスの Web UI にログインする際に 404 を受け取る](/docs/services/cloud-monitoring/qa/grafana_qa.html#404)
* [Grafana ダッシュボード用の JSON データをアップロードしたところ、スクロール・バーが消えた](/docs/services/cloud-monitoring/qa/grafana_qa.html#2)


## アラート API を使用して定義したアラートが Grafana ダッシュボードに表示されない
{: #alerts1}

アラート API を使用して定義したアラートは、Grafana のアラート・タブに表示されません。 Grafana でアラートを表示するには、Grafana ダッシュボードで直接それらを定義する必要があります。

詳しくは、[Grafana でのアラートの構成](/docs/services/cloud-monitoring/alerts/config_alerts_grafana.html#config_alerts_grafana)を参照してください。

## Grafana ダッシュボードに加えた変更を保存しようとすると BXNMSAL41E を受け取る
{: #BXNMSAL41E}

通知チャネルおよびアラートを Grafana で定義できます。 Grafana で通知チャネルを削除したが、ルールを更新してその通知チャネルを除去していない場合、Grafana ダッシュボードを保存しようとすると **BXNMSAL41E** エラーを受け取ります。

この問題を修正するには、アラート API を使用してルールを更新し、その後でダッシュボードの保存を再試行してください。 ルールを更新する際、削除された通知チャネルを除去してください。

詳しくは、[アラート API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction) を参照してください。

## Grafana ダッシュボードにアラートを追加した後で変更を保存しようとすると BXNMSAL36E を受け取る
{: #BXNMSAL36E}

{{site.data.keyword.monitoringshort}} サービスでメトリックをモニターしているドメインの割り当て量に達した場合、**BXNMSAL36E** エラーを受け取ります。

プランをアップグレードし、再試行してください。

プランのアップグレード方法について詳しくは、[プランの変更](/docs/services/cloud-monitoring/plan/change_plan.html#change_plan)を参照してください。


## UUA 認証モデルを使用して Monitoring サービスの Web UI にログインする際に 404 を受け取る
{: #404}

{{site.data.keyword.monitoringshort}} サービスの Web UI (Grafana) にログインしようとした時に 404 を受け取る場合は、スペースが存在していること、およびそのスペースへのアクセス権を持っていることを確認してください。

[UAA 認証モデル](/docs/services/cloud-monitoring/security/auth_uaa.html#auth_uaa)を使用して {{site.data.keyword.monitoringshort}} サービスにアクセスする際は、{{site.data.keyword.Bluemix_notm}} コンソールへのログインに使用するユーザー ID およびパスワードと同じものを使用する必要があります。 

ログインしようとしているアカウント、組織、およびスペースへのアクセス権を持っているかどうか確認するには、{{site.data.keyword.Bluemix_notm}} コンソールにログインし、スペースに切り替えます。 

また、コマンド・ラインを使用して、そのスペースへのアクセス権があるかどうかを確認することもできます。 以下のコマンドを実行して、{{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

指示に従います。 {{site.data.keyword.Bluemix_notm}} の資格情報を入力し、組織とスペースを選択します。


## Grafana ダッシュボード用の JSON データをアップロードしたところ、スクロール・バーが消えた
{: #2}

Grafana には、ダッシュボードをインポートした後にスクロール・バーを非表示にするバグがあります。 

スクロール・バーを表示するには、インポートした後にダッシュボードを保存してください。 








