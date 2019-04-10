---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

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


# Kubernetes クラスターにデプロイされたアプリに関するメトリックの分析
{: #kubernetes_cluster}

このチュートリアルを使用して、{{site.data.keyword.cloud_notm}} の {{site.data.keyword.mon_full_notm}} サービスにメトリックを転送するようにクラスターを構成する方法を学習します。
{:shortdesc}

{{site.data.keyword.mon_full_notm}} サービスを使用して、Kubernetes クラスターをモニターできます。

メトリックを転送するようにクラスターを構成するには、DaemonSet を使用して Kubernetes クラスターの各ワーカー・ノードにエージェントをインストールする必要があります。 Sysdig エージェントでは、{{site.data.keyword.mon_full_notm}} インスタンスでの認証のためにアクセス・キー (トークン) を使用します。 Sysdig エージェントは、データ・コレクターとして機能します。 例えば、*ワーカー CPU* や*ワーカー・メモリー*、コンテナーの入出力 HTTP トラフィック、いくつかの一般的なインフラストラクチャー・ソフトウェアなどのメトリックを自動的に収集します。 また、エージェントは、Prometheus 互換のスクレイパーまたは statsd ファサードのいずれかを使用して、カスタム・アプリケーション・メトリックを収集できます。 

Sysdig の Web ベースのユーザー・インターフェースを使用してメトリックを表示します。

![{{site.data.keyword.cloud_notm}} でのコンポーネント概要](../images/kube.png "{{site.data.keyword.cloud_notm}} でのコンポーネント概要")



## 始める前に
{: #kubernetes_cluster_prereqs}

この取得チュートリアルのステップを完了するために、米国南部地域で {{site.data.keyword.mon_full_notm}} のインスタンスをプロビジョンする説明が示されています。 既存のクラスターまたは新規**クラスター・バージョン 1.10** を使用できます。 クラスターは別の地域で使用可能です。  

{{site.data.keyword.mon_full_notm}} についてお読みください。 詳しくは、[概要](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)を参照してください。

{{site.data.keyword.cloud_notm}} アカウントのメンバーまたは所有者であるユーザー ID を使用してください。 {{site.data.keyword.cloud_notm}} ユーザー ID を取得するには、[「登録」![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} にアクセスしてください。

{{site.data.keyword.IBM_notm}}ID は、以下のリソースごとの IAM ポリシーに割り当てられている必要があります。 

| リソース                             | アクセス・ポリシー有効範囲 | 役割    | 地域    | 情報                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| リソース・グループ **デフォルト**           |  リソース・グループ            | ビューアー  | us-south  | デフォルトのリソース・グループのサービス・インスタンスをユーザーが表示するためにこのポリシーは必須です。    |
| {{site.data.keyword.mon_full_notm}} サービス |  リソース・グループ            | エディター  | us-south  | デフォルトのリソース・グループの {{site.data.keyword.mon_full_notm}} サービスをユーザーがプロビジョンおよび管理するためにこのポリシーは必須です。   |
| Kubernetes クラスター・インスタンス          |  リソース                 | エディター  | us-south  | Kubernetes クラスターで機密事項や Sysdig エージェントを構成するためにこのポリシーは必須です。 |
{: caption="表 1. チュートリアルを完了するために必要な IAM ポリシーのリスト" caption-side="top"} 

{{site.data.keyword.containerlong}} IAM 役割について詳しくは、[ユーザー・アクセス許可](/docs/containers?topic=containers-access_reference#access_reference)を参照してください。

{{site.data.keyword.cloud_notm}} CLI と Kubernetes CLI プラグインをインストールします。 詳しくは、[『{{site.data.keyword.cloud_notm}}CLI のインストール』](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)を参照してください。


## ステップ 1: {{site.data.keyword.mon_full_notm}} インスタンスのプロビジョン
{: #kubernetes_cluster_step1}

{{site.data.keyword.cloud_notm}} UI を使用して {{site.data.keyword.mon_full_notm}} のインスタンスをプロビジョンするには、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} アカウントにログインします。

    [{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} をクリックして、{{site.data.keyword.cloud_notm}} ダッシュボードを起動します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} UI が開きます。

2. **「カタログ」**をクリックします。 {{site.data.keyword.cloud_notm}} で使用可能なサービスのリストが開きます。

3. 表示されるサービスのリストをフィルタリングするには、**「開発者用ツール」**カテゴリーを選択します。

4. **「{{site.data.keyword.mon_full_notm}}」**タイルをクリックします。 *「プログラム識別情報」*ダッシュボードが開きます。

5. **「インスタンスの作成 (Create instance)」**を選択します。 

6. サービス・インスタンスの名前を入力します。

7. **「デフォルト」**リソース・グループを選択します。 

    デフォルトでは、**「デフォルト」**リソース・グループが設定されています。

8. **「トライアル」**サービス・プランを選択します。 

    デフォルトでは、**「トライアル」**プランが設定されています。

    他のサービス・プランについて詳しくは、[価格プラン](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)を参照してください。

9. ログインしている {{site.data.keyword.cloud_notm}} リソース・グループで {{site.data.keyword.mon_full_notm}} サービスをプロビジョンするには、**「作成」**をクリックします。

インスタンスがプロビジョンされると、*「プログラム識別情報」*ダッシュボードが開きます。 


**注:** CLI を使用してインスタンスをプロビジョンするには、[{{site.data.keyword.cloud_notm}} CLI を使用したインスタンスのプロビジョン](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)を参照してください。


## ステップ 2: インスタンスにメトリックを送信するように Kubernetes クラスターを構成する
{: #kubernetes_cluster_step2}

{{site.data.keyword.mon_full_notm}} インスタンスにメトリックを送信するように Kubernetes クラスターを構成するには、クラスターのノードごとに Sysdig エージェント・ポッドをインストールする必要があります。 Sysdig エージェントは DaemonSet を使用してインストールされ、それによってエージェントのインスタンスがすべてのワーカー・ノードで確実に実行されます。 Sysdig エージェントは、インストールされたポッドからメトリックを収集し、そのデータをインスタンスに転送します。

**注:** 完全なシステム・メトリックを取得するために、Sysdig エージェントには特権の状況が必要です。

{{site.data.keyword.mon_full_notm}} インスタンスにメトリックを転送するように Kubernetes クラスターを構成するには、コマンド・ラインから以下のステップを実行します。

1. 端末を開きます。 次に、{{site.data.keyword.cloud_notm}} にログインします。 以下のコマンドを実行して、プロンプトに従います。

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    {{site.data.keyword.mon_full_notm}} インスタンスをプロビジョンしたアカウントを選択します。

2. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

3. Sysdig アクセス・キーを取得します。 詳しくは、[{{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)を参照してください。

4. 取り込み URL を取得します。 詳しくは、[Sysdig Collector エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)を参照してください。

5. Sysdig エージェントをデプロイします。 次のコマンドを実行します。

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    各部分の説明:

    * SYSDIG_ACCESS_KEY はインスタンスの取り込みキーです。

    * COLLECTOR_ENDPOINT は、モニタリング・インスタンスが使用可能な地域の取り込み URL です。

    * TAG_DATA は、*TAG_NAME:TAG_VALUE* 形式のコンマ区切りタグです。 1 つ以上のタグを Sysdig エージェントに関連付けることができます。 例えば、*role:serviceX,location:us-south* などです。 後で、これらのタグを使用して、エージェントが実行されている環境のメトリックを識別できます。

    * **sysdig_capture_enabled** を *false* に設定して、Sysdig キャプチャー機能を無効にします。 デフォルトでは、*true* に設定されています。 詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)を参照してください。

6. Sysdig エージェントが正常に作成されたこと、およびその状況を確認します。 次のコマンドを実行します。

    ```
    kubectl get pods
    ```
    {: codeblock}



## ステップ 3: Sysdig Web UI の起動
{: #kubernetes_cluster_step3}

Web UI を起動するには、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} アカウントにログインします。

    [{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} をクリックして、{{site.data.keyword.cloud_notm}} ダッシュボードを起動します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} ダッシュボードが開きます。

2. ナビゲーション・メニューで、**「プログラム識別情報」**を選択します。 

3. **「モニタリング」**を選択します。 

    {{site.data.keyword.cloud_notm}} で使用可能なインスタンスのリストが表示されます。

4. インスタンスを選択します。 次に、**「Sysdig の表示 (View Sysdig)」**をクリックします。

Sysdig エージェントが正常に構成されている場合、*「探索」*ビューが開きます。

ただし、Sysdig エージェントが正常にインストールされていない場合や、誤った取り込みエンドポイントが指示されている場合、またはアクセス・キーが誤っている場合は、開いたページに対処方法が示されます。

ブラウザーごとに 1 つの Web UI セッションのみ使用できます。
{: tip}


## ステップ 4: クラスターのモニター
{: #kubernetes_cluster_step4}

Web UI で使用可能な**「探索」**ビューで、クラスターをモニターできます。 このビューは、インフラストラクチャーのトラブルシューティングやモニターの開始点となります。 ユーザーに対する Web UI のデフォルト・ホーム・ページです。

*「ホストとコンテナー (Host and containers)」*セクションで、モニタリング・インスタンスにメトリックを転送している、クラスター内のワーカーのリストを表示できます。 各ワーカーの項目は、そのワーカーの関連インフラストラクチャー・オブジェクトのグループを表します。

**「ホストとコンテナー (Host and containers)」** ![ホストとコンテナー (Host and containers)](../images/switch_hosts.png) をクリックして、データ・ソースを切り替えます。 次に、ワーカーを選択します。 表示されるデータは、選択したワーカーに対応しています。

**「探索表に戻る (Back to Explore Table)」**をクリックすると、*「探索表 (Explore table)」*が表示されます。 各列には、さまざまなメトリックが表示されます。 各メトリックを個別に構成できます。 列の順序を変更できます。 既存の列の順序を変更すると、ログインの間中、さまざまなグループ化に変更が持続して適用されることに注意してください。 列を追加または削除した場合、その変更は持続します。 また、色を構成して値を強調表示し、読みやすくすることもできます。

例えば、列の色分けを構成するには、以下のステップを実行します。

1. 列を選択します。 列タイトルの上にマウスを移動します。 次に、鉛筆アイコンを選択します。
2. 色分けを使用可能にするためにバーを切り替えます。
3. さまざまなしきい値の値を設定します。

ワーカーを選択すると、デフォルトのダッシュボードが表示されます。 ![ダッシュボードの切り替え](images/switch_dashboards_1.png) をクリックして、さまざまなデフォルトのダッシュボードとメトリックを検討します。 選択したワーカーに関連するメトリックとダッシュボードのみを選択できることに注意してください。


## 次のステップ
{: #kubernetes_cluster_next_steps}

カスタム・ダッシュボードを作成します。 詳しくは、[ダッシュボードの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)を参照してください。

アラートについても学習できます。 詳しくは、[アラートの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)を参照してください。 






