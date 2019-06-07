---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-10"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

subcollection: Sysdig

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


# Kubernetes クラスターにデプロイされたアプリのメトリックの分析
{: #kubernetes_cluster}

このチュートリアルでは、{{site.data.keyword.mon_full}} サービスにメトリックを転送するように {{site.data.keyword.containerlong}} クラスターを構成する方法を学習できます。
{:shortdesc}

メトリックを転送するようにクラスターを構成するには、[DaemonSet ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) を使用して Kubernetes クラスターの各ワーカー・ノードに Sysdig エージェントをインストールする必要があります。Sysdig エージェントでは、{{site.data.keyword.mon_full_notm}} インスタンスでの認証のためにアクセス・キー (トークン) を使用します。 Sysdig エージェントは、データ・コレクターとして機能します。 *ワーカー・ノード CPU* や*ワーカー・ノード・メモリー*の使用率、*コンテナーの入出力 HTTP トラフィック*、いくつかのインフラストラクチャー・コンポーネントに関するデータなどのメトリックを自動的に収集します。さらに、Prometheus 対応スクレイパーまたは StatsD ファサードを使用すれば、エージェントでカスタム・アプリケーション・メトリックを収集することもできます。 

Sysdig の Web ベースのユーザー・インターフェースを使用してメトリックを表示します。

![{{site.data.keyword.cloud_notm}} でのコンポーネント概要](../images/kube.png "{{site.data.keyword.cloud_notm}} でのコンポーネント概要")

## 達成目標
{: #kubernetes_cluster_objectives}

このチュートリアルでは、{{site.data.keyword.containerlong}} クラスターで Sysdig を使用してメトリックを構成します。具体的には、以下の操作を行います。
*  {{site.data.keyword.mon_full_notm}} インスタンスをプロビジョンします。
*  Sysdig にメトリックを送信するようにクラスターの Sysdig エージェントを構成します。
*  Sysdig Web UI を使用してクラスター・メトリックを分析します。


## 始める前に
{: #kubernetes_cluster_prereqs}

1. {{site.data.keyword.mon_full_notm}} についてお読みください。 詳しくは、[概要](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)を参照してください。

2. {{site.data.keyword.cloud_notm}} アカウントのメンバーまたは所有者であるユーザー ID を取得します。{{site.data.keyword.cloud_notm}} ユーザー ID を取得するには、[「登録」![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} にアクセスしてください。

3. {{site.data.keyword.cloud_notm}} CLI と Kubernetes CLI プラグインをインストールします。 詳しくは、[『{{site.data.keyword.cloud_notm}}CLI のインストール』](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)を参照してください。

4. [クラスターを作成する](/docs/containers?topic=containers-clusters#clusters)か、既存の {{site.data.keyword.containerlong_notm}} クラスターを使用します。
    *  クラスターで Kubernetes バージョン 1.10 以降が実行されている必要があります。
    *  クラスターは **ダラス** ロケーションに配置されている必要はありません。任意の [{{site.data.keyword.containerlong_notm}} 地域](/docs/containers/cs_regions.html#regions-and-zones)に配置できます。

5. ユーザー ID に以下の {{site.data.keyword.iamlong}} ポリシーが割り当てられていることを確認します。

| リソース                             | アクセス・ポリシー有効範囲 | 役割    | 地域    | 情報                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| リソース・グループ **デフォルト**           |  リソース・グループ            | ビューアー  | 米国南部  | デフォルトのリソース・グループのサービス・インスタンスをユーザーが表示するためにこのポリシーは必須です。    |
| {{site.data.keyword.mon_full_notm}} サービス |  リソース・グループ            | エディター  | 米国南部  | デフォルトのリソース・グループの {{site.data.keyword.mon_full_notm}} サービスをユーザーがプロビジョンおよび管理するためにこのポリシーは必須です。   |
| Kubernetes クラスター・インスタンス          |  リソース                 | エディター  | 米国南部  | Kubernetes クラスターで機密事項や Sysdig エージェントを構成するためにこのポリシーは必須です。 |
{: caption="表 1. チュートリアルを完了するために必要な IAM ポリシーのリスト" caption-side="top"}

{{site.data.keyword.containerlong}} IAM 役割について詳しくは、[ユーザー・アクセス許可](/docs/containers?topic=containers-access_reference#access_reference)を参照してください。



## ステップ 1. {{site.data.keyword.mon_full_notm}} インスタンスをプロビジョンする
{: #kubernetes_cluster_step1}

この入門チュートリアルでは、米国南部地域で {{site.data.keyword.mon_full_notm}} インスタンスをプロビジョンするための手順を説明します。サポートされている地域について詳しくは、[地域](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints)を参照してください。

{{site.data.keyword.cloud_notm}} UI を使用して {{site.data.keyword.mon_full_notm}} のインスタンスをプロビジョンするには、以下のステップを実行します。

1. [{{site.data.keyword.cloud_notm}} アカウントにログイン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} UI が開きます。

2. **「カタログ」**をクリックします。 {{site.data.keyword.cloud_notm}} で使用可能なサービスのリストが開きます。

3. 表示されるサービスのリストをフィルタリングするには、**「開発者用ツール」**カテゴリーを選択します。

4. **「{{site.data.keyword.mon_full_notm}}」**タイルをクリックします。 *「プログラム識別情報」*ダッシュボードが開きます。

5. **「インスタンスの作成 (Create instance)」**を選択します。 

6. サービス・インスタンスの名前を入力します。

7. **「デフォルト」**リソース・グループを選択します。 

    リソース作成権限を持っている任意のリソース・グループにインスタンスをプロビジョンできます。

    デフォルトでは、**default** リソース・グループが設定されています。

8. **「トライアル」**サービス・プランを選択します。 

    デフォルトでは、**「トライアル」**プランが設定されています。

    他のサービス・プランについて詳しくは、[価格プラン](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)を参照してください。

9. **「作成」**をクリックします。

    インスタンスのプロビジョンが完了すると、*「プログラム識別情報」*ダッシュボードが開き、**モニタリング**・インスタンスの詳細が表示されます。 


CLI を使用してインスタンスをプロビジョンするには、[{{site.data.keyword.cloud_notm}} CLI を使用したインスタンスのプロビジョニング](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)を参照してください。
{: note}


## ステップ 2. インスタンスにメトリックを送信するように Kubernetes クラスターを構成する
{: #kubernetes_cluster_step2}

{{site.data.keyword.mon_full_notm}} インスタンスにメトリックを送信するように Kubernetes クラスターを構成するには、クラスターのノードごとに Sysdig エージェント・ポッドをインストールする必要があります。 Sysdig エージェントは DaemonSet を使用してインストールされ、それによってエージェントのインスタンスがすべてのワーカー・ノードで確実に実行されます。 Sysdig エージェントは、インストールされたポッドからメトリックを収集し、そのデータをインスタンスに転送します。

システム・メトリックを一式すべて取得するためには、Sysdig エージェントが特権を付与された状況でなければなりません。
{: note}

{{site.data.keyword.mon_full_notm}} インスタンスにメトリックを転送するように Kubernetes クラスターを構成するには、コマンド・ラインから以下の手順を実行します。

1. 端末を開きます。 次に、{{site.data.keyword.cloud_notm}} にログインします。 以下のコマンドを実行して、プロンプトに従います。

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    クラスターを使用できるアカウントを選択します。

2. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。`KUBECONFIG` 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。{: tip}

3. Sysdig アクセス・キーを取得します。 詳しくは、[{{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)を参照してください。

4. [Sysdig コレクター・エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)の取り込み URL を取得します。

5. Sysdig エージェントをデプロイします。 次のコマンドを実行します。

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: pre}

    説明

    * **SYSDIG_ACCESS_KEY** は、先ほど取得したインスタンスの取り込みキーです。

    * **COLLECTOR_ENDPOINT** は、先ほど取得したモニタリング・インスタンスを使用できる地域の取り込み URL です。

    * **TAG_DATA** は、コンマで区切られた *TAG_NAME:TAG_VALUE* 形式のタグです。1 つ以上のタグを Sysdig エージェントに関連付けることができます。 例えば、*role:serviceX,location:us-south* などです。 後で、これらのタグを使用して、エージェントが実行されている環境のメトリックを識別できます。

    * **sysdig_capture_enabled** を *false* に設定して、Sysdig キャプチャー機能を無効にします。 デフォルトでは、*true* に設定されています。 詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)を参照してください。

6. Sysdig エージェントが正常に作成されたこと、およびその状況を確認します。 次のコマンドを実行します。

    ```
    kubectl get pods -n ibm-observe
    ```
    {: codeblock}

    1 つ以上の `sysdig-agent` ポッドが表示されたら、デプロイメントは成功です。`sysdig-agent` ポッドの数は、クラスター内のワーカー・ノードの数と等しくなります。すべてのポッドが `Running` 状態である必要があります。


## ステップ 3. Sysdig Web UI を起動する
{: #kubernetes_cluster_step3}

{{site.data.keyword.cloud_notm}} コンソールから Sysdig Web UI を起動するには、以下の手順を実行します。

ブラウザーごとに 1 つの Web UI セッションのみ使用できます。
{: imp}

1. [{{site.data.keyword.cloud_notm}} アカウントにログイン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} ダッシュボードが開きます。

2. メニュー ![外部リンク・アイコン](../../../icons/icon_hamburger.svg "メニュー・アイコン") から、**「プログラム識別情報」**を選択します。 

3. **「モニタリング」**を選択します。 {{site.data.keyword.cloud_notm}} で使用可能なインスタンスのリストが表示されます。

4. インスタンスを見つけて、**「Sysdig の表示 (View Sysdig)」**をクリックします。

    * **初回**: Sysdig エージェントは既にインストールしているのでインストール・ウィザードはスキップし、最初のオンボーディングを実行します。
    
    * **2 回目以降**: **「探索」**ビューが開きます。


Sysdig エージェントが正常にインストールされていない場合、誤った取り込みエンドポイントを指定した場合、またはアクセス・キーが誤っている場合は、開かれたページに対処方法が示されます。

例えば、Sysdig エージェントが正しくインストールされていない場合は、インストール・ウィザードをスキップできません。以下のようなメッセージが表示されるはずです。
    
```
1 番目のノードの接続を待機しています... 次に進み、以下の手順に従ってください。(Waiting for the first node to connect... Go ahead and follow the instructions below.)
```
{: screen}
    
以下の操作を試してください。
*  Sysdig エンドポイントではなく`取り込み`[エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)を使用していることを確認します。 
*  [アクセス・キー](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key) が正しいことを確認します。
*  追加の手順を実行した後に、このチュートリアルの手順を繰り返します。



## ステップ 4. クラスターをモニターする
{: #kubernetes_cluster_step4}

Sysdig Web UI で使用可能な**「探索」**ビューで、クラスターをモニターできます。 このビューがデフォルトのホーム・ページであり、クラスターのインフラストラクチャーやリソースのトラブルシューティングおよびモニターを行う開始点になります。

*「ホストとコンテナー (Host and containers)」*セクションに*「探索表 (Explore table)」*が表示されます。これは、クラスター内でモニタリング・インスタンスにメトリックを転送しているワーカーのリストです。各ワーカーの項目は、そのワーカーの関連インフラストラクチャー・オブジェクトのグループを表します。

**「ホストとコンテナー (Host and containers)」** ![ホストとコンテナー (Host and containers)](../images/switch_hosts.png) をクリックして、データ・ソースを切り替えます。 次に、ワーカーを選択します。 表示されるデータは、選択したワーカーに対応しています。**「探索表に戻る (Back to Explore Table)」**をクリックすると、*「探索表 (Explore table)」*が表示されます。  

**_「探索表 (Explore table)」_のカスタマイズ**

*「探索表 (Explore table)」*はカスタマイズできます。 

* 列ごとに別のメトリックが表示されます。  
* 各メトリックを個別に構成できます。  
* 列の順序を変更できます。  

    既存の列の順序を変更すると、ログインの間中、さまざまなグループ化に変更が持続して適用されることに注意してください。 列を追加または削除した場合、その変更は持続します。 

* また、色を構成して値を強調表示し、読みやすくすることもできます。 

例えば、列の色分けを構成するには、以下のステップを実行します。

1. 列を選択します。 列タイトルの上にマウスを移動します。 次に、鉛筆アイコンを選択します。
2. 色分けを使用可能にするためにバーを切り替えます。
3. さまざまなしきい値の値を設定します。


**ダッシュボードのカスタマイズ**

特定のワーカー・ノードの詳細情報を表示するには、インフラストラクチャー・エントリーをクリックします。表で*「ホスト別の概要 (Overview by Host)」*ダッシュボードが開きます。![ダッシュボードの切り替え](../images/switch_dashboards_1.png) アイコンをクリックして、さまざまなダッシュボードやメトリックを参照できます。選択したワーカー・ノードに関連するメトリックとダッシュボードのみを選択できることに注意してください。

_「探索表 (Explore table)」_全体に戻るには、**「X」(探索表に戻る)** ボタンをクリックします。


詳しくは、[Sysdig の資料](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822446/The+Explore+Table)を参照してください。



## 次のステップ
{: #kubernetes_cluster_next_steps}

カスタム・ダッシュボードを作成します。 詳しくは、[ダッシュボードの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)を参照してください。

アラートについても学習できます。 詳しくは、[アラートの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)を参照してください。 






