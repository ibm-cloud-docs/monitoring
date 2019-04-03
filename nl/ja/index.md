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


# 概説のチュートリアル
{: #getting-started-with-ibm-cloud-monitoring}

このチュートリアルでは、{{site.data.keyword.Bluemix}} の {{site.data.keyword.monitoringlong}} サービスを使用した処理を始める方法について説明します。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} は、デフォルトで、選択されたサービスに対する統合モニタリング機能を提供します。 {{site.data.keyword.monitoringlong_notm}} サービスを使用すると、メトリック処理時の収集機能および保存機能を拡張でき、注意が必要な状態を通知するルールおよびアラートを定義できます。 {{site.data.keyword.monitoringshort}} サービスが提供する機能は、アプリがどのように実行されていて、どのようにリソースを消費しているのかについての洞察を得たり、傾向を迅速に把握したり、問題の検出と診断を行ったりするのに役立ち、これらのすべてを即時の価値創出までの時間 (TTV) と低い総所有コスト (TCO) で実行できます。 環境のモニターは Grafana を使用して行います。 

## 始めに
{: #cm_prereqs}

{{site.data.keyword.Bluemix_notm}} アカウントのメンバーまたは所有者であるユーザー ID が必要です。 {{site.data.keyword.Bluemix_notm}} ユーザー ID を取得するには、[登録 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/registration/){:new_window} に移動してください。

## 手順 1: モニターするクラウド・リソースを選択する
{: #cm_step1}

{{site.data.keyword.Bluemix_notm}} では、CF アプリケーション、{{site.data.keyword.containershort}} で実行中のコンテナー、および選択されたサービスは、メトリック・シリーズのデータを自動的に収集し、それを {{site.data.keyword.monitoringshort}} サービスに転送します。

以下の表は、さまざまなクラウド・リソースをリストしています。 {{site.data.keyword.monitoringshort}} サービスへの入門として、まず 1 つのリソースに関してこのチュートリアルを実行してください。

<table>
  <caption>{{site.data.keyword.monitoringshort}} サービス入門のためのチュートリアル </caption>
  <tr>
    <th>リソース</th>
    <th>チュートリアル</th>
    <th>クラウド環境</th>
    <th>シナリオ</th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containershort}} で実行中のコンテナー</td>
    <td>[Grafana での Kubernetes クラスターにデプロイされたアプリに関するメトリックの分析](/docs/services/cloud-monitoring/tutorials/container_service_metrics.html#container_service_metrics)</td>
    <td>Public </br>Dedicated</td>
    <td>![Kubernetes クラスターにデプロイされているコンテナーのコンポーネント概要図](containers/images/containers_kube_metrics_dedicated.png "Kubernetes クラスターにデプロイされているコンテナーのコンポーネント概要図")</td>
  </tr>
  <tr>
    <td>CF アプリ</td>
    <td>[Grafana での CF アプリに関するメトリックの分析](/docs/services/cloud-monitoring/tutorials/cfapps_metrics.html#cfapps_metrics)</td>
    <td>Public</td>
    <td>![{{site.data.keyword.Bluemix_notm}} における CF アプリのモニターの概要図](cf/images/cfapp_metrics_ov.png "{{site.data.keyword.Bluemix_notm}} における CF アプリのモニターの概要図")</td>
  </tr>
</table>



## 手順 2: ユーザーがメトリックを表示するための権限を設定する
{: #cm_step2}

ユーザーが実行を許可される {{site.data.keyword.monitoringshort}} アクションを制御するために、ユーザーに役割およびポリシーを割り当てることができます。 

{{site.data.keyword.Bluemix_notm}} には 2 つのタイプのセキュリティー権限があり、それによって、ユーザーが {{site.data.keyword.monitoringshort}} サービスを使用した処理を行うときに実行できるアクションが制御されます。

* Cloud Foundry (CF) 役割: ユーザーがスペース内のメトリックを表示するのに必要な権限を定義するには、ユーザーに CF 役割を付与します。
* IAM 役割: ユーザーがアカウント・ドメイン内のメトリックを表示するのに必要な権限を定義するには、ユーザーに IAM ポリシーを付与します。


スペース内のメトリックを表示する権限をユーザーに付与するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://bluemix.net ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    *「ユーザー」*ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. ユーザーがアカウントのメンバーの場合、リストからユーザー名を選択するか、*「アクション」*メニューから
**「ユーザーの管理 (Manage user)」**をクリックします。

    ユーザーがアカウントのメンバーではない場合、
[ユーザーの招待](/docs/iam/iamuserinv.html#iamuserinv)を参照してください。

4. **「Cloud Foundry アクセス権限」**を選択し、組織を選択します。

    その組織で使用可能なスペースのリストが表示されます。

5. {{site.data.keyword.monitoringshort}} サービスをプロビジョンしたスペースを選択します。 次に、メニュー・アクションから**「スペースの役割の編集」**を選択します。

6. *「監査員」*を選択します。 

    1 つ以上のスペースの役割を選択できます。 役割*「管理者」*、*「開発者」*、および*「監査員」*はすべて、ユーザーがログを表示することを許可します。
	
7. **「役割の保存」**をクリックします。


詳しくは、[権限の付与](/docs/services/cloud-monitoring/security/assign_policy.html#grant_permissions)を参照してください。

ユーザーがメトリック・データを表示できることを検証するには、チュートリアルの 1 つを実行した Cloud 地域で Grafana を起動します。 例えば、米国南部地域の場合、Web ブラウザーを開き、URL [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/) を入力します。


他の地域での Grafana の起動方法について詳しくは、[Web ブラウザーから Grafana へのナビゲート](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#navigating_grafana)を参照してください。

**注:** Grafana を起動するときに、*bearer トークンが無効*であることを示すメッセージが表示される場合は、スペースでの権限を確認してください。 このメッセージは、ご使用のユーザー ID にメトリックを表示する権限がないことを示しています。
    

## 次の手順 
{: #cm_next_steps}

メトリックのアラートを定義します。 詳しくは、[アラートの構成](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov)を参照してください。
