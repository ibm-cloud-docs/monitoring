---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# Linux Sysdig エージェントのカスタマイズ
{: #change_linux_agent}

デフォルトでは、Sysdig エージェントはさまざまなプラットフォームおよびアプリケーションからデータを収集します。 エージェントの構成ファイルを編集して、そのデフォルトの動作を変更し、データを含めたり、除外したりできます。 Sysdig エージェントの構成ファイルをカスタマイズして、JMX、StatsD、Prometheus などのカスタム・メトリックを含めることができます。 また、メトリックやコンテナーをフィルターで除外できます。
{:shortdesc}

Sysdig エージェントでは、自動的に収集されるデータを指定する 2 つの構成ファイルが使用されます。

| ファイル                   | 説明                                                     | ロケーション                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | 主要な構成ファイル </br>**注:****このファイルを編集しないでください。| `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Sysdig エージェントをカスタマイズするために編集する構成ファイル。 | `/opt/draios/etc/dragent.yaml`          |
{: caption="表 1. Sysdig エージェントの構成ファイル" caption-side="top"} 

*dragent.yaml* ファイルを編集して、収集されるデータをカスタマイズできます。 ファイルを保存すると、すぐに変更内容が有効になります。 エージェントは変更を検出し、自動的に再始動されます。 Sysdig エージェントが検査する頻度やファイルは、*dragent.default.yaml* ファイルで確認できます。

例えば、*dragent.default.yaml* に以下の情報が含まれているとします。

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## dragent yaml ファイルの編集
{: #change_linux_agent_edit_agent}

yaml ファイルは、*/opt/draios/etc/* にあります。

ファイルを編集して変更内容を適用するには、以下のステップを実行します。

1. *dragent.yaml* に直接アクセスします。 このファイルは `/opt/draios/etc/dragent.yaml` にあります。
2. ファイルを編集します。 有効な YAML 構文を使用してください。
3. エージェントを再始動します。 次のコマンドを実行します。

    ```
    service dragent restart
    ```
    {: codeblock}


## ポートのブロック
{: #change_linux_agent_block_ports}

ネットワーク・ポートからのネットワーク・トラフィックおよびメトリックをブロックするには、*dragent.yaml* ファイルの **blacklisted_ports** セクションをカスタマイズする必要があります。 データをフィルターで除外するポートをリストする必要があります。

**注:** ポート 53 (DNS) は常にブラックリストに含まれます。 

例えば、以下のサンプルは、ポート 6666 および 6379 からのデータを除外するように Sysdig エージェントの *blacklisted_ports* セクションを設定する方法を示しています。

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## メトリックの組み込みと除外
{: #change_linux_agent_inc_exc_metrics}

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
{: #change_linux_agent_log_level}

ログ・レベルを構成するには、*dragent.yaml* ファイルの **log** セクションをカスタマイズする必要があります。 

Sysdig エージェントが */opt/draios/logs/draios.log* にログ・エントリーを生成します。 
* ログ・ファイルのサイズが 10 MB に達すると、ログ・ファイルが交替します。
* 最新の 10 個のログ・ファイルが保持されます。 ファイル名に付加される日付スタンプが、保持するファイルの判別に使用されます。
* 有効なログ・レベルは、*none*、*error*、*warning*、*info*、*debug*、および *trace* です。
* デフォルトのログ・レベルは *info* です。警告およびエラーのエントリー以外に、1 秒あたり 1 回のバックエンド・サーバーへの集計メトリック伝送ごとにエントリーが作成されます。
* Sysdig エージェントの構成ファイル **/opt/draios/etc/dragent.yaml** を構成して、収集されるログおよびエントリーのタイプをカスタマイズできます。 このファイルを編集した後に、`service dragent restart` を使用してシェルでエージェントを再始動し、変更内容をアクティブ化する必要があります。

| ユース・ケース                                     | log セクションのエントリー           |
|-----------------------------------------------|-----------------------------|
| エージェントの動作のトラブルシューティング                   | `file_priority: debug`      |
| コンテナー・コンソールの出力の削減               | `console_priority: warning` |
| 重大度別のイベントのフィルター処理                  | `event_priority: warning`   |
| 含まれるメトリックと除外されるメトリックの確認  | `metrics_excess_log: true`  |
{: caption="表 2. log セクションのエントリー" caption-side="top"} 
