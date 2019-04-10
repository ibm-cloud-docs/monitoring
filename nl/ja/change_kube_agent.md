---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# Kubernetes Sysdig エージェントのカスタマイズ
{: #change_kube_agent}

{{site.data.keyword.mon_full_notm}} では、Sysdig エージェントの構成をカスタマイズして、ログ・レベルの設定、ポートのブロック、メトリック・データの組み込みまたは除外、イベントの追加または削除、およびコンテナーのフィルターによる除外を行うことができます。 
{:shortdesc}

Kubernetes Sysdig エージェントをカスタマイズするには、以下のファイルのセクションを構成する必要がある場合があります。

| ファイル名                        | アクション       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | ログ・レベルの変更。 |
| `sysdig-agent-configmap.yaml`    | ポートのブロック。 </br>メトリック・データの組み込みと除外。 </br>イベントの追加または削除。 </br>コンテナーのフィルターによる除外。 |
{: caption="表 1. Kubernetes Sysdig エージェントの構成ファイル" caption-side="top"} 

Kubernetes Sysdig エージェントを編集するには、*sysdig-agent-configmap.yaml* または *sysdig-agent-daemonset-v2.yaml*、あるいはその両方を編集する必要がある場合があります。
{: tip}

構成ファイルを変更するには、以下の 2 つの方法を使用できます。
* 方法 1: エージェントが実行されているクラスターでファイルを直接変更します。
* 方法 2: ローカルでファイルを変更し、変更内容をクラスターに適用します。

## kubectl edit を使用した Kubernetes Sysdig エージェントの構成の編集
{: #change_kube_agent_edit_kube_agent_method1}

Kubernetes Sysdig エージェントの構成を編集するには、以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-configmap.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    変更を加えます。 **注:** 変更方法の詳細は、`vi` エディターの手順を参照してください。

    変更を保存します。 変更内容は自動的に適用されます。 

3. *sysdig-agent-daemonset-v2.yaml* ファイルを編集します。 

    次のコマンドを実行します。 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    変更を加えます。 **注:** 変更方法の詳細は、`vi` エディターの手順を参照してください。

    変更を保存します。 変更内容は自動的に適用されます。

## kubectl apply を使用した Kubernetes Sysdig エージェントの構成の編集
{: #change_kube_agent_edit_kube_agent_method2}

ソース制御システムに保管および管理された yaml 構成ファイルがある場合は、この方法を使用します。

Kubernetes Sysdig エージェントの構成を編集するには、以下のステップを実行します。

1. ソース・コントローラーから各ファイルの最新コピーを取得します。 

    クラスターにデプロイされた構成でローカル・ファイルを作成する場合、以下のコマンドを実行することもできます。
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    または 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. 構成を編集します。

3. 以下のコマンドを使用して、変更内容を適用します。

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    または
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

エージェントを実行すると、Kubernetes がクラスター内のすべてのノードに変更内容をプッシュした後に、新しい構成が自動的にピックされます。


## Kubernetes Sysdig エージェントから収集されたデータへのタグの追加
{: #change_kube_agent_add_tags}

既にデプロイした Kubernetes Sysdig エージェントの構成にタグを追加するには、以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-configmap.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 **注:** 変更方法の詳細は、`vi` エディターの手順を参照してください。

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. 変更を保存します。 

変更内容は自動的に適用されます。 

提供されているサンプルでは、タグ **agent.tag.cluster_version** および **agent.tag.region** を取得します。 これらのタグを使用して、アラートの定義や有効範囲のカスタマイズなどを行うことができます。



## 一連の Kubernetes イベントの収集
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} では、Kubernetes とのイベント統合がサポートされています。 Sysdig エージェントでは、サービスの検出とそこからのイベント・データの収集が自動的に行われます。 エージェントの構成ファイルを編集して、そのデフォルトの動作を変更し、イベント・データを含めたり、除外したりできます。 

デフォルトでは、限定されたイベント・セットのみが収集されます。 デフォルトで収集されるイベントについて詳しくは、[Kubernetes events ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window} を参照してください。

イベントを追加または削除するには、*sysdig-agent-configmap.yaml* ファイルをカスタマイズして、含めるイベントおよびフィルターで除外するイベントを指定する必要があります。 **注:** *sysdig-agent-configmap.yaml* のセクションのエントリーは、デフォルトの構成のセクション全体をオーバーライドします。
{: tip}

Kubernetes ポッドからイベントをフィルタリングするには、以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-configmap.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *events* セクションを追加するか、セクションを更新します。

    **注:** 変更方法の詳細は、`vi` エディターの手順を参照してください。

    例えば、Kubernetes ポッドのプリング・イベントを収集し、デフォルトで収集されるその他のポッド・イベントをフィルターで除外するとします。 ただし、ノードおよび replicationControllers のデフォルトの Kubernetes イベントは収集するものとします。

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. 変更を保存します。 

変更内容は自動的に適用されます。 


Kubernetes イベントのサブセットの収集方法を確認できる別の例として、ポッドのプリング・イベント、プルされたイベント、および失敗したイベントのみをモニターするとします。

* オプション 1: エントリーのシーケンスを箇条書きで定義します。

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - 失敗
    ```
    {: codeblock}

* オプション 2: エントリーのシーケンスを大括弧で囲まれた 1 つの行で定義します。

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

カスタム・イベントの使用方法について詳しくは、[Working with custom events ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window} を参照してください。


## イベントの収集の無効化
{: #change_kube_agent_disable_events}

Sysdig エージェントの Kubernetes イベントの収集を無効にするには、*sysdig-agent-configmap.yaml* ファイルを変更する必要があります。 **events** セクションの **Kubernetes** エントリーを *none* に設定します。 

以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-configmap.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *events* セクションを追加するか、セクションを更新します。

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. 変更を保存します。 

変更内容は自動的に適用されます。 






## メトリックの組み込みと除外
{: #change_kube_agent_inc_exc_metrics}

カスタム・メトリックをフィルタリングするには、*sysdig-agent-configmap.yaml* ファイルの **metrics_filter** セクションをカスタマイズする必要があります。 **include** と **exclude** のフィルタリング・パラメーターを構成して、含めるメトリックおよびフィルターで除外するメトリックを指定できます。

<p class="important">フィルタリング規則の順序は、メトリックに一致する最初のルールが適用されるように設定されています。 そのメトリックの後続規則は無視されます。</p>

以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-configmap.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *metrics_filter* セクションを追加するか、セクションを更新します。

    例えば、Sysdig エージェントの *metrics_filter* セクションが以下のようであるとします。

    ```
    metrics_filter:
      - include: metricA.*
      - exclude: metricA.*
      - include: metricB.*
      - include: haproxy.backend.*
      - exclude: haproxy.*
      - exclude: metricC.*
    ```
    {: screen}

    * *metricA*、*metricB*、および *haproxy.backend* で始まるメトリックからのすべてのデータを収集する Sysdig エージェントを構成しています。 

    * *metricC* で始まるメトリックおよび *haproxy* で始まるその他のメトリックをフィルターで除外します。 

    * エントリー `exclude: metricA.*` は無視されます。

4. 変更を保存します。 

変更内容は自動的に適用されます。 




## kubernetes オブジェクトおよびデータが収集されるコンテナーのフィルター処理
{: #change_kube_agent_filter_data}

Kubernetes Sysdig エージェントでは、Prometheus メトリック、StatsD メトリック、JMX メトリック、app-checks メトリック、built-in メトリックなど、クラスターで検出された*すべてのコンテナー*から自動的にメトリックが収集されます。
 
メトリックの収集からコンテナーを除外するように Sysdig エージェントをカスタマイズできます。 

コンテナーを除外する場合は、以下の情報を考慮してください。
* エージェントとバックエンドの負荷を削減します。
* モニターするコンテナーからのみデータを収集します。
* 重要なコンテナーの報告、および不要または重要ではないコンテナーのフィルターによる除外によって、コストを制御できます。

Sysdig エージェントがコンテナーをフィルタリングする機能を有効にするには、*sysdig-agent-configmap.yaml* ファイルをカスタマイズする必要があります。 **containers** セクションの **use_container_filter** エントリーを *true* に設定します。 **注:** デフォルトでは、この機能はオフになっています。 次に、適用する 1 つ以上の条件を含む規則を定義します。

以下の表は、クラスター内のフィルタリング規則を設定するために定義できるパラメーターの概要を示しています。

| パラメーター                          | 条件                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | コンテナーのイメージ名                           |
| `container.name`                   | コンテナー名                                 |
| `container.label.*`                | コンテナーのラベル                                |
| `kubernetes.object.*`             | Kubernetes オブジェクト。 オブジェクトはポッド、名前空間などにすることができます。   |
| `kubernetes.object.annotation.*`  | Kubernetes オブジェクトのアノテーション                   |
| `kubernetes.object.label.*`       | Kubernetes オブジェクトのラベル                        |
| `all`                              | すべてのオブジェクトを指定するデフォルトの規則            |
{: caption="表 2. コンテナーの条件を定義するパラメーター" caption-side="top"} 

**container_filter** セクションで定義した規則の Sysdig エージェントへの適用方法に関する以下の情報を考慮してください。
* 条件を定義するには、**include** および **exclude** フィルタリング・パラメーターを使用して条件を構成します。 
* リストの最初のマッチング規則では、コンテナーを含めるか、または除外するかが決定されます。
* 条件はキー名と値で構成されます。 コンテナーの指定されたキーが値と一致する場合は、規則が適用されます。
* 規則に複数の条件が含まれる場合、規則が適用されるには、`all the conditions` が一致する必要があります。

クラスターで Sysdig エージェントがモニターするコンテナーをフィルターで除外するには、以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-configmap.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *metrics_filter* セクションを追加するか、セクションを更新します。

    例えば、以下の構成マップの抽出を確認してください。

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. 変更を保存します。 

変更内容は自動的に適用されます。 


## ポートのブロック
{: #change_kube_agent_block_ports}

ネットワーク・ポートからのネットワーク・トラフィックおよびメトリックをブロックするには、*sysdig-agent-configmap.yaml* ファイルの **blacklisted_ports** セクションをカスタマイズする必要があります。 データをフィルターで除外するポートをリストする必要があります。

**注:** ポート 53 (DNS) は常にブラックリストに含まれます。 

以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-configmap.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *metrics_filter* セクションを追加するか、セクションを更新します。

    例えば、以下のサンプルは、ポート 6666 および 6379 からのデータを除外するように Sysdig エージェントの *blacklisted_ports* セクションを設定する方法を示しています。

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. 変更を保存します。 

変更内容は自動的に適用されます。 



## ログ・レベルの変更
{: #change_kube_agent_log_level}

ログ・レベルを構成するには、*sysdig-agent-daemonset-v2.yaml* ファイルの **log** セクションをカスタマイズする必要があります。 

Sysdig エージェントが */opt/draios/logs/draios.log* にログ・エントリーを生成します。 
* ログ・ファイルのサイズが 10 MB に達すると、ログ・ファイルが交替します。
* 最新の 10 個のログ・ファイルが保持されます。 ファイル名に付加される日付スタンプが、保持するファイルの判別に使用されます。
* 有効なログ・レベルは、*none*、*error*、*warning*、*info*、*debug*、および *trace* です。
* デフォルトのログ・レベルは *info* です。警告およびエラーのエントリー以外に、1 秒あたり 1 回のバックエンド・サーバーへの集計メトリック伝送ごとにエントリーが作成されます。
* Sysdig エージェントの構成ファイル **/opt/draios/etc/dragent.yaml** を構成して、収集されるログおよびエントリーのタイプをカスタマイズできます。 このファイルを編集した後に、`service dragent restart` を使用してシェルでエージェントを再始動し、変更内容をアクティブ化する必要があります。

以下の表は、一般的なシナリオとそれぞれの場合に設定する必要がある値を示しています。

| ユース・ケース                                     | log セクションのエントリー           |
|-----------------------------------------------|-----------------------------|
| エージェントの動作のトラブルシューティング                   | `file_priority: debug`      |
| コンテナー・コンソールの出力の削減               | `console_priority: warning` |
| 重大度別のイベントのフィルター処理                  | `event_priority: warning`   |
| 含まれるメトリックと除外されるメトリックの確認  | `metrics_excess_log: true`  |
{: caption="表 2. log セクションのエントリー" caption-side="top"} 

ログ・レベルを構成するには、以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-daemonset-v2.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *log* セクションを追加するか、セクションを更新します。

    例えば、重大度の低いイベント (*notice*、*information*、*debug*) をフィルターで除外するには、**log** セクションの **metrics_excess_log** エントリーを *true* に設定する必要があります。

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. 変更を保存します。 

変更内容は自動的に適用されます。 


## 重大度別の Kubernetes イベントのフィルター処理
{: #change_kube_agent_filterby_severity}

重大度別にイベントをフィルタリングするには、*sysdig-agent-daemonset-v2.yaml* ファイルを変更する必要があります。 **log** セクションの **event_priority** エントリーを *none* に設定します。 

デフォルトのログ・レベルは **information** です。 この場合、警告以上の重大度のイベントのみが伝送されます。

有効なレベルは、*emergency*、*alert*、*critical*、*error*、*warning*、*notice*、*information*、*debug*、および *none* です。 **注**: 値は優先度の高いものから低いものの順にリストされます。

以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-daemonset-v2.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *log* セクションを追加するか、セクションを更新します。

    例えば、重大度の低いイベント (*notice*、*information*、*debug*) をフィルターで除外するには、log セクションの **event_priority** を *warning* に設定する必要があります。

    ```
    log:
  event_priority: warning
    ```
    {: codeblock}

6. 変更を保存します。 

変更内容は自動的に適用されます。 

## 含まれるメトリックと除外されるメトリックのファイルへのロギング
{: #change_kube_agent_log_metrics}

含まれるカスタム・メトリックと除外されるカスタム・メトリックに関する情報をファイルにロギングするには、*sysdig-agent-daemonset-v2.yaml* ファイルをカスタマイズする必要があります。 **log** セクションの **metrics_excess_log** エントリーを **true** に設定します。

* デフォルトでは、ロギングは無効になっています。 
* ロギングは INFO レベルで 30 秒ごとに発生し、10 秒間続きます。 
* ログ・ファイルは、*/opt/draios/logs/draios.log* にあります。
* データのロギングは以下のようにフォーマットされます。

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* は、メトリックが含まれるか除外されるかを示す記号です。 プラス (*+*) は、メトリックが含まれることを示します。 マイナス (*-*) は、メトリックが除外されることを示します。 

    * *[type]* は、*statsd* などのメトリック・タイプを指定します。
    
    * *[metric included/excluded]* は、メトリックが含まれるか除外されるかを人間が読むことができる方法で示します。

    *  *metric.name* は、メトリック名を示します。

    * *(filter: +/-[metric.filter])* は、*sysdig-agent-daemonset-v2.yaml* ファイルの **metrics_filter** セクションで定義されているフィルターに関する情報を提供します。

サンプル・エントリーは、以下のようになります。

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. *sysdig-agent-daemonset-v2.yaml* ファイルを編集します。 

    次のコマンドを実行します。

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 変更を加えます。 *log* セクションを追加するか、セクションを更新します。

    例えば、重大度の低いイベント (*notice*、*information*、*debug*) をフィルターで除外するには、**log** セクションの **metrics_excess_log** エントリーを *true* に設定する必要があります。

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. 変更を保存します。 

変更内容は自動的に適用されます。 


## サンプルの configmap yaml ファイル
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:    
      kubernetes:
        node: 
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter: 
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## サンプルの daemonset yaml ファイル
{: #change_kube_agent_sample_daemonset}

```
 Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

