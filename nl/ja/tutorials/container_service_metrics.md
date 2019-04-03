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


# Kubernetes クラスターに関する Grafana でのメトリックの分析
{: #container_service_metrics}

このチュートリアルでは、{{site.data.keyword.monitoringlong}} サービスを使用して、コンテナーのパフォーマンスをモニターする方法を説明します。 
{:shortdesc}


## 達成目標
{: #ks_objectives}

以下のように Kubernetes クラスターにデプロイされたアプリのコンテナー・メトリックの検索および分析方法について説明します。

1. クラスターで収集されたメトリックが、{{site.data.keyword.monitoringshort}} サービスに転送される際の場所を識別します。 
2. Grafana を起動し、クラスター・メトリックを表示できる {{site.data.keyword.monitoringshort}} ドメインを設定します。
3. {{site.data.keyword.Bluemix_notm}} の Kubernetes クラスターにデプロイされたアプリに関するコンテナー・メトリックを検索および分析します。

このチュートリアルでは、{{site.data.keyword.Bluemix_notm}} で以下のエンドツーエンドのシナリオを機能させるために必要なステップを順に説明します。クラスターのプロビジョン、{{site.data.keyword.Bluemix_notm}} でクラスターがメトリックを {{site.data.keyword.monitoringshort}} サービスに送信する際の場所の識別、クラスターへのアプリのデプロイ、Grafana によるそのクラスターのコンテナー・メトリックの表示とフィルタリングの各ステップです。


**注:** このチュートリアルを完了するには、前提条件と、それぞれのステップからリンクされたチュートリアルを完了する必要があります。


## 前提条件
{: #ks_prereqs}

1. Kubernetes 標準クラスターの作成、クラスターへのアプリのデプロイ、および Grafana でモニターするための {{site.data.keyword.Bluemix_notm}} 内のメトリック照会を実行できる権限を持つ、{{site.data.keyword.Bluemix_notm}} アカウントのメンバーまたは所有者になります。

    {{site.data.keyword.Bluemix_notm}} のユーザー ID には、以下のポリシーが割り当てられている必要があります。
    
    * *オペレーター* または*管理者* 権限が設定された、{{site.data.keyword.containershort}} の IAM ポリシー。
    
    詳しくは、[IBM Cloud UI を使用してユーザーに IAM ポリシーを割り当てる](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui)を参照してください。

2. コマンド・ラインから Kubernetes クラスターの管理およびアプリのデプロイを実行できる端末セッションを用意します。 このチュートリアルの例は、Ubuntu Linux システム用です。

3. {{site.data.keyword.containershort}} の作業を行うための CLI を Ubuntu システムにインストールします。

    * {{site.data.keyword.Bluemix_notm}} CLI をインストールします。 
    * {{site.data.keyword.containershort}} での Kubernetes クラスターの作成と管理、およびクラスターへのコンテナー化アプリのデプロイを行うための {{site.data.keyword.containershort}} CLI をインストールします。
    
    詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)を参照してください。
    
    

    
 

## 手順 1 : Kubernetes クラスターのプロビジョン
{: #ks_step1}

以下のステップを実行します。

1. 標準の Kubernetes クラスターを作成します。 詳しくは、[Kubernetes 標準クラスターの作成](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial)を参照してください。

2. 端末にクラスター・コンテキストをセットアップします。 コンテキストを設定すると、Kubernetes クラスターを管理し、Kubernetes クラスターにアプリケーションをデプロイできるようになります。

    {{site.data.keyword.Bluemix_notm}} で、作成したクラスターに関連付けられた、地域、組織、およびスペースにログインします。 詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login)を参照してください。

	{{site.data.keyword.containershort}} サービス・プラグインを初期化します。

	```
	ibmcloud cs init
	```
	{: codeblock}

    端末コンテキストをクラスターに設定します。
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    このコマンド実行の出力では、構成ファイルへのパスを設定するためにご使用の端末で実行する必要のあるコマンドが示されます。 以下に例を示します。

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    ご使用の端末で環境変数を設定するコマンドをコピーして貼り付け、**Enter** を押します。



## 手順 2: アカウント・ドメイン内のメトリックを表示する権限をユーザーに付与
{: #ks_step2}

アカウント・ドメイン内のメトリックを表示する権限をユーザーに付与するには、**ビューアー**役割が設定された {{site.data.keyword.monitoringshort}} サービスの IAM ポリシーを当該ユーザーに割り当てる必要があります。

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

4. **「アクセス・ポリシー」>「アクセス権限の割り当て」>「リソースへのアクセス権限の割り当て」**と選択します。

5. サービス**「{{site.data.keyword.monitoringlong}}」**を選択し、クラスターが使用可能な地域 (このチュートリアルの場合には**「米国南部」**) を選択し、役割**「ビューアー」**を選択します。



## 手順 3: {{site.data.keyword.containershort_notm}} キー所有者に権限を付与
{: #ks_step3}

クラスターがアカウント・ドメインにメトリックを転送するためには、{{site.data.keyword.containershort}} キー所有者が次の IAM ポリシーを持っている必要があります。

* {{site.data.keyword.monitoringshort}} サービスの**エディター**権限が設定された IAM ポリシー。
* {{site.data.keyword.containershort}} の**管理者**権限が設定された IAM ポリシー。


{{site.data.keyword.containershort}} キー所有者に権限を付与するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://bluemix.net ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    *「ユーザー」*ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. {{site.data.keyword.containershort}} キー所有者のユーザー ID を調べます。

    コマンド `ibmcloud cs api-key-info ClusterName` を実行して、{{site.data.keyword.containershort}} キー所有者のユーザー ID を取得します。

4. **「アクセス・ポリシー」>「アクセス権限の割り当て」>「リソースへのアクセス権限の割り当て」**と選択します。

5. サービス**「{{site.data.keyword.monitoringlong}}」**を選択し、クラスターが使用可能な地域 (このチュートリアルの場合には**「米国南部」**) を選択し、役割**「エディター」**を選択します。	

6. 手順 2 から 4 を繰り返して、サービス「{{site.data.keyword.containershort}}」を選択します。 **「すべての地域」**を選択して、役割**「管理者」**を選択します。	




## 手順 4: Kubernetes クラスターへのサンプル・アプリのデプロイ
{: #ks_step4}

Kubernetes クラスターにサンプル・アプリをデプロイし、実行します。 チュートリアル[『演習 1: Kubernetes クラスターへの単一インスタンス・アプリのデプロイ (Lesson 1: Deploying single instance apps to Kubernetes clusters)』](/docs/containers?topic=containers-cs_apps_tutorial#cs_apps_tutorial_lesson1)の手順を実行して、サンプル・アプリをデプロイします。

このアプリは、以下のような Hello World Node.js アプリです。

```
var express = require('express')
var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

このサンプル・アプリでは、ブラウザーでアプリをテストすると、「`Sample app is listening on port 8080.`」というメッセージを標準出力に書き込みます。


## 手順 5: Grafana の起動とメトリック・ドメインの設定
{: #ks_step5}

ブラウザーから Grafana を起動し、クラスター・メトリックを表示できる {{site.data.keyword.monitoringshort}} ドメインを設定します。

クラスターのメトリックを分析するには、そのクラスターが作成されているクラウド Public 地域で Grafana にアクセスする必要があります。 詳しくは、[Web ブラウザーから Grafana ダッシュボードへのナビゲート](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)を参照してください。

1. ブラウザーから Grafana を起動します。 

    クラスターを作成した地域の {{site.data.keyword.monitoringshort}} サービス URL を入力します。 
    
    地域ごとの URL を取得するには、[Monitoring サービスの URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region) を参照してください。

    例えば、米国南部地域の場合は、[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)を起動します。

2. {{site.data.keyword.monitoringshort}} ドメインを **Account** に設定します。

    Grafana で、ID を選択します。 次に、正しいアカウントにログインしていることを確認してドメインを選択します。 `Domain = account` を選択します。

    クラスターがアカウント・メトリック・ドメインにメトリックを転送します。 

## 手順 6: Grafana でのクラスターのモニター
{: #ks_step6}

{{site.data.keyword.containershort}} では、クラスター・メトリックのモニターに使用できる Grafana ダッシュボードが提供されます。 

サンプル・ダッシュボードを開くには、以下のステップを実行します。

1. サイド・メニュー・バーのトグル を選択します。![Grafana サイド・メニュー・バー](images/grafana_settings.gif "Grafana サイド・メニュー・バー")
2. **「Dashboards」**を選択します。
3. **「Open」**をクリックします。
4. **「ClusterMonitoringDashboard_v1」**を選択します。

サンプル・ダッシュボードが開きます。 

![Grafana サンプル・ダッシュボード](images/cluster_grafana_sample_dashboard.png "Grafana サンプル・ダッシュボード")



## 次の手順
{: #ks_next_steps}

メトリックのアラートを定義します。 詳しくは、[アラートの構成](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)を参照してください。
