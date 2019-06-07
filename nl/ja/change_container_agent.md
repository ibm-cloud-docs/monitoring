---

copyright:
  years: 2018, 2019
lastupdated: "2018-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# コンテナー Sysdig エージェントのカスタマイズ
{: #change_agent}

{{site.data.keyword.mon_full_notm}} では、Sysdig エージェントの構成をカスタマイズして、ログ・レベルの設定、ポートのブロック、メトリック・データの組み込みまたは除外、イベントの追加または削除、およびコンテナーのフィルターによる除外を行うことができます。 
{:shortdesc}




## dragent yaml ファイルの編集
{: #edit_agent}

yaml ファイルは、*/opt/draios/etc/* にあります。

ファイルを編集して変更内容を適用するには、以下のステップを実行します。

1. `/opt/draios/etc/dragent.yaml` の *dragent.yaml* に直接アクセスします。
2. ファイルを編集します。 有効な YAML 構文を使用してください。
3. エージェントを再始動します。 次のコマンドを実行します。

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## ポートのブロック
{: #ports}

ネットワーク・ポートからのネットワーク・トラフィックおよびメトリックをブロックするには、*dragent.yaml* ファイルの **blacklisted_ports** セクションをカスタマイズする必要があります。 データをフィルターで除外するポートをリストする必要があります。

**注:** ポート 53 (DNS) は常にブラックリストに含まれます。 

例えば、以下のサンプルは、ポート 6666 および 6379 からのデータを除外するように Sysdig エージェントの *blacklisted_ports* セクションを設定する方法を示しています。

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## 一連の Docker イベントの収集
{: #docker}

{{site.data.keyword.mon_full_notm}} では、Docker とのイベント統合がサポートされています。 Sysdig エージェントでは、Docker ソースの検出とそこからのイベント・データの収集が自動的に行われます。 エージェントの構成ファイルを編集して、そのデフォルトの動作を変更し、イベント・データを含めたり、除外したりできます。 

デフォルトでは、限定されたイベント・セットのみが収集されます。 デフォルトの設定構成ファイル */opt/draios/etc/dragent.default.yaml* には、収集されたイベントが含まれます。 デフォルトで収集されるイベントについて詳しくは、[Docker events ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window} を参照してください。

イベントを追加または削除するには、*dragent.yaml* ファイルをカスタマイズして、含めるイベントおよびフィルターで除外するイベントを指定する必要があります。 **注:** *dragent.yaml* のセクションのエントリーは、デフォルトの構成のセクション全体をオーバーライドします。
{: tip}

例えば、Docker イメージ・イベントをフィルターで除外し、アクションを添付、コミット、およびコピーするイベントのみを収集するには、以下のように *docker* セクションを設定する必要があります。

* オプション 1: エントリーのシーケンスを箇条書きで定義します。

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* オプション 2: エントリーのシーケンスを大括弧で囲まれた 1 つの行で定義します。

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## イベントの収集の無効化
{: #disable}

Sysdig エージェントのイベントの収集を無効にするには、*dragent.default.yaml* ファイルを変更します。 *dragent.yaml* ファイルの **events** セクションを *none* に設定します。

例えば、Docker イベントをフィルターで除外するには、*dragent.yaml* ファイルの *events* セクションを以下のように設定する必要があります。

```
events:
  docker: none
```
{: codeblock}



## 重大度別のイベントのフィルター処理
{: #severity}

重大度別にイベントをフィルタリングするには、*dragent.yaml* ファイルでイベントのログ・エントリー・タイプを変更することもできます。 

デフォルトのログ・レベルは **information** です。 この場合、警告以上の重大度のイベントのみが伝送されます。

有効なレベルは、*emergency*、*alert*、*critical*、*error*、*warning*、*notice*、*information*、*debug*、および *none* です。 **注**: 値は優先度の高いものから低いものの順にリストされます。

例えば、重大度の低いイベント (*notice*、*information*、*debug*) をフィルターで除外するには、log セクションの **event_priority** を *warning* に設定する必要があります。

```
log:
  event_priority: warning
```
{: codeblock}


イベントの収集をブロックするには、log セクションの **event_priority** を *none* に設定する必要があります。

```
log:
  event_priority: none
```
{: codeblock}




## メトリックの組み込みと除外
{: #params}

カスタム・メトリックをフィルタリングするには、*dragent.yaml* ファイルの **metrics_filter** セクションをカスタマイズする必要があります。 **include** と **exclude** のフィルタリング・パラメーターを構成して、含めるメトリックおよびフィルターで除外するメトリックを指定できます。

**注:** フィルタリング規則の順序は、メトリックに一致する最初のルールが適用されるように設定されています。

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


## ログ・レベルの変更
{: #log_level}

ログ・レベルを構成するには、*dragent.yaml* ファイルの **log** セクションをカスタマイズする必要があります。 

Sysdig エージェントが */opt/draios/logs/draios.log* にログ・エントリーを生成します。 
* ログ・ファイルのサイズが 10 MB に達すると、ログ・ファイルが交替します。
* 最新の 10 個のログ・ファイルが保持されます。 ファイル名に付加される日付スタンプが、保持するファイルの判別に使用されます。
* 有効なログ・レベルは、*none*、*error*、*warning*、*info*、*debug*、および *trace* です。
* デフォルトのログ・レベルは *info* です。警告およびエラーのエントリー以外に、1 秒あたり 1 回のバックエンド・サーバーへの集計メトリック伝送ごとにエントリーが作成されます。
* Sysdig エージェントの構成ファイル **/opt/draios/etc/dragent.yaml** を構成して、収集されるログおよびエントリーのタイプをカスタマイズできます。 このファイルを編集した後に、`docker restart sysdig-agent` を使用してシェルでエージェントを再始動し、変更内容をアクティブ化する必要があります。

| ユース・ケース                                     | log セクションのエントリー           |
|-----------------------------------------------|-----------------------------|
| エージェントの動作のトラブルシューティング                   | `file_priority: debug`      |
| コンテナー・コンソールの出力の削減               | `console_priority: warning` |
| 重大度別のイベントのフィルター処理                  | `event_priority: warning`   |
| 含まれるメトリックと除外されるメトリックの確認  | `metrics_excess_log: true`  |
{: caption="表 2. log セクションのエントリー" caption-side="top"} 


