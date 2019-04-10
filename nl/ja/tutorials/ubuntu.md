---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# Ubuntu ホストに関するメトリックの分析
{: #ubuntu}

このチュートリアルを使用して、{{site.data.keyword.cloud_notm}} の {{site.data.keyword.mon_full_notm}} サービスにメトリックを転送するように Ubuntu ホストを構成する方法を学習します。
{:shortdesc}

メトリックを転送するように Ubuntu サーバーを構成するには、Sysdig エージェントをインストールする必要があります。 エージェントでは、{{site.data.keyword.mon_full_notm}} インスタンスでの認証のためにアクセス・キー (トークン) を使用します。 Sysdig エージェントは、データ・コレクターとして機能します。 メトリックは自動的に収集されます。

Sysdig の Web ベースのユーザー・インターフェースを使用してメトリックを表示します。

![{{site.data.keyword.cloud_notm}} でのコンポーネント概要](../images/ubuntu.png "{{site.data.keyword.cloud_notm}} でのコンポーネント概要")



## 始める前に
{: #ubuntu_prereqs}

米国南部地域で作業します。 

{{site.data.keyword.mon_full_notm}} についてお読みください。 詳しくは、[概要](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about)を参照してください。

{{site.data.keyword.cloud_notm}} アカウントのメンバーまたは所有者であるユーザー ID を使用してください。 {{site.data.keyword.cloud_notm}} ユーザー ID を取得するには、[「登録」![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} にアクセスしてください。

{{site.data.keyword.IBM_notm}}ID は、以下のリソースごとの IAM ポリシーに割り当てられている必要があります。 

| リソース                             | アクセス・ポリシー有効範囲 | 役割    | 地域    | 情報                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| リソース・グループ **デフォルト**           |  リソース・グループ            | ビューアー  | us-south  | デフォルトのリソース・グループのサービス・インスタンスをユーザーが表示するためにこのポリシーは必須です。    |
| {{site.data.keyword.mon_full_notm}} サービス |  リソース・グループ            | エディター  | us-south  | デフォルトのリソース・グループの {{site.data.keyword.mon_full_notm}} サービスをユーザーがプロビジョンおよび管理するためにこのポリシーは必須です。   |
{: caption="表 1. チュートリアルを完了するために必要な IAM ポリシーのリスト" caption-side="top"} 

{{site.data.keyword.cloud_notm}} CLI をインストールします。 詳しくは、[『{{site.data.keyword.cloud_notm}}CLI のインストール』](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)を参照してください。


## ステップ 1: {{site.data.keyword.mon_full_notm}} インスタンスのプロビジョン
{: #ubuntu_step1}

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

8. **「ライト」**サービス・プランを選択します。 

    デフォルトでは、**「ライト」**プランが設定されています。

    他のサービス・プランについて詳しくは、[価格プラン](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)を参照してください。

9. ログインしている {{site.data.keyword.cloud_notm}} リソース・グループで {{site.data.keyword.mon_full_notm}} サービスをプロビジョンするには、**「作成」**をクリックします。

インスタンスがプロビジョンされると、*「プログラム識別情報」*ダッシュボードが開きます。 


**注:** CLI を使用してインスタンスをプロビジョンするには、[{{site.data.keyword.cloud_notm}} CLI を使用したインスタンスのプロビジョン](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli)を参照してください。


## ステップ 2: インスタンスにメトリックを送信するように Ubuntu サーバーを構成する
{: #ubuntu_step2}

{{site.data.keyword.mon_full_notm}} インスタンスにメトリックを送信するように Ubuntu サーバーを構成するには、Sysdig エージェントをインストールする必要があります。 

コマンド・ラインから以下のステップを実行します。

1. 端末を開きます。 次に、{{site.data.keyword.cloud_notm}} にログインします。 以下のコマンドを実行して、プロンプトに従います。

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    {{site.data.keyword.mon_full_notm}} インスタンスをプロビジョンしたアカウントを選択します。

2. Sysdig アクセス・キーを取得します。 詳しくは、[{{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)を参照してください。

3. 取り込み URL を取得します。 詳しくは、[Sysdig Collector エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)を参照してください。

4. Sysdig エージェントをデプロイします。 次のコマンドを実行します。

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    各部分の説明:

    * SYSDIG_ACCESS_KEY はインスタンスの取り込みキーです。

    * COLLECTOR_ENDPOINT は、モニタリング・インスタンスが使用可能な地域の取り込み URL です。

    * TAG_DATA は、*TAG_NAME:TAG_VALUE* 形式のコンマ区切りタグです。 1 つ以上のタグを Sysdig エージェントに関連付けることができます。 例えば、*role:serviceX,location:us-south* などです。 後で、これらのタグを使用して、エージェントが実行されている環境のメトリックを識別できます。

    * **sysdig_capture_enabled** を *false* に設定して、Sysdig キャプチャー機能を無効にします。 デフォルトでは、*true* に設定されています。 詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)を参照してください。

Sysdig エージェントを正しくインストールできない場合には、kernel headers を手動でインストールします。 ディストリビューションを選択し、そのディストリビューションのコマンドを実行してください。 次に、Sysdig エージェントのデプロイメントを再試行します。

* **Debian および Ubuntu Linux ディストリビューションの場合**、以下のコマンドを実行します。

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **RHEL、CentOS、および Fedora Linux ディストリビューションの場合**、以下のコマンドを実行します。

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## ステップ 3: Sysdig Web UI の起動
{: #ubuntu_step3}

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


## ステップ 4: Ubuntu サーバーのモニター
{: #ubuntu_step4}

Web UI で使用可能な**「探索」**ビューで、Ubuntu サーバーをモニターできます。 このビューは、インフラストラクチャーのトラブルシューティングやモニターの開始点となります。 ユーザーに対する Web UI のデフォルト・ホーム・ページです。

*「ホストとコンテナー (Host and containers)」*セクションで、Ubuntu サーバーの項目を表示できます。 **「ホストとコンテナー (Host and containers)」** ![ホストとコンテナー (Host and containers)](../images/switch_hosts.png) をクリックして、データ・ソースを切り替えます。 次に、Ubuntu サーバーを選択します。 表示されるデータは、選択した Ubuntu サーバーに対応しています。

例えば、列の色分けを構成するには、以下のステップを実行します。

1. 列を選択します。 列タイトルの上にマウスを移動します。 次に、鉛筆アイコンを選択します。
2. 色分けを使用可能にするためにバーを切り替えます。
3. さまざまなしきい値の値を設定します。



## 次のステップ
{: #ubuntu_next_steps}

カスタム・ダッシュボードを作成します。 詳しくは、[ダッシュボードの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards)を参照してください。

アラートについても学習できます。 詳しくは、[アラートの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)を参照してください。 






