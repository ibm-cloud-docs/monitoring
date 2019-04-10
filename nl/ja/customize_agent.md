---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# データを制御するための Sysdig エージェントのカスタマイズ
{: #customize_agent}

デフォルトでは、Sysdig エージェントはさまざまなプラットフォームおよびアプリケーションからデータを収集します。 エージェントの構成ファイルを編集して、そのデフォルトの動作を変更し、データを含めたり、除外したりできます。 Sysdig エージェントの構成ファイルをカスタマイズして、JMX、StatsD、Prometheus などのカスタム・メトリックを含めることができます。 また、メトリック、イベント・データおよびコンテナーをフィルターで除外できます。
{:shortdesc}

## Kubernetes Sysdig エージェントのカスタマイズ
{: #kube}

Kubernetes Sysdig エージェントでは、自動的に収集されるデータを指定する 2 つの構成ファイルが使用されます。

| ファイル名                        | アクション           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | ログ・レベルの変更。 |
| `sysdig-agent-configmap.yaml`    | ポートのブロック。 </br>メトリック・データの組み込みと除外。 </br>イベントの追加または削除。 </br>コンテナーのフィルターによる除外。 |
{: caption="表 1. Kubernetes Sysdig エージェントの構成ファイル" caption-side="top"} 

Kubernetes Sysdig エージェントを編集するには、*sysdig-agent-configmap.yaml* または *sysdig-agent-daemonset-v2.yaml*、あるいはその両方を編集する必要がある場合があります。

構成ファイルを変更するには、以下の 2 つの方法を使用できます。
* 方法 1: エージェントが実行されているクラスターでファイルを直接変更します。 詳しくは、[kubectl edit を使用した Kubernetes Sysdig エージェントの構成の編集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1)を参照してください。
* 方法 2: ローカルでファイルを変更し、変更内容をクラスターに適用します。 詳しくは、[kubectl apply を使用した Kubernetes Sysdig エージェントの構成の編集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2)を参照してください。

エージェントによって収集されるデータにタグを追加できます。 
* タグを使用すると、モニターするデータの管理に役立ちます。 

    * ラベルを使用してインフラストラクチャー・リソースを論理階層にグループ化し、データをフィルターで除外して、集合データをセグメントに分割します。 
    
    * メトリックのグラフを構成したり、アラートを作成したりする場合にデータが集計される方法をカスタマイズします。 
    
    * データ・ポイントをフィルターで除外するダッシュボード、パネル、またはアラートの有効範囲を設定します。 
    
    * ユーザーのチームからのデータ・アクセスを管理して、データへのアクセスを制限します。 
    
    * データの管理方法について詳しくは、[データの管理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)を参照してください。

* タグの追加方法について詳しくは、[Kubernetes Sysdig エージェントから収集されたデータへのタグの追加](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags)を参照してください。 


**Sysdig エージェントによって収集されるデータをカスタマイズできます。** 

イベント、メトリック、およびコンテナーを除外する場合は、以下の情報を考慮してください。
* エージェントとバックエンドの負荷を削減できます。
* モニターするコンテナーからのみデータを収集します。
* 重要なコンテナーの報告、および不要または重要ではないコンテナーのフィルターによる除外によって、コストを制御できます。
* モニターする Kubernetes イベントを構成できます。 詳しくは、[一連の Kubernetes イベントの収集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events)を参照してください。

以下に、Sysdig エージェントによって収集されるデータを制御するために実行できるアクションの概要を示しています。
* [イベントの収集の無効化](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [メトリックの組み込みと除外](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [kubernetes オブジェクトおよびデータが収集されるコンテナーのフィルター処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [ポートのブロック](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [重大度別の Kubernetes イベントのフィルター処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

収集されるログおよびエントリーのタイプをカスタマイズすることもできます。 詳しくは、 [ログ・レベルの変更](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level)を参照してください。

また、エージェントがデータを報告するメトリックのリストをロギングできます。 詳しくは、[含まれるメトリックと除外されるメトリックのファイルへのロギング](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics)を参照してください。

Sysdig エージェントが */opt/draios/logs/draios.log* にログ・エントリーを生成します。 
* ログ・ファイルのサイズが 10 MB に達すると、ログ・ファイルが交替します。
* 最新の 10 個のログ・ファイルが保持されます。 ファイル名に付加される日付スタンプが、保持するファイルの判別に使用されます。
* 有効なログ・レベルは、*none*、*error*、*warning*、*info*、*debug*、および *trace* です。
* デフォルトのログ・レベルは *info* です。警告およびエラーのエントリー以外に、1 秒あたり 1 回のバックエンド・サーバーへの集計メトリック伝送ごとにエントリーが作成されます。

以下の表は、一般的なシナリオとそれぞれの場合に設定する必要がある値を示しています。

| ユース・ケース                                     | log セクションのエントリー           |
|-----------------------------------------------|-----------------------------|
| エージェントの動作のトラブルシューティング                   | `file_priority: debug`      |
| コンテナー・コンソールの出力の削減               | `console_priority: warning` |
| 重大度別のイベントのフィルター処理                  | `event_priority: warning`   |
| 含まれるメトリックと除外されるメトリックの確認  | `metrics_excess_log: true`  |

## コンテナー Sysdig エージェント
{: #container}


以下に、Sysdig エージェントによって収集されるデータを制御するために実行できるアクションの概要を示しています。
* [イベントの収集の無効化](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [メトリックの組み込みと除外](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [データが収集されるコンテナーのフィルター処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [ポートのブロック](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [重大度別のイベントのフィルター処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

収集されるログおよびエントリーのタイプをカスタマイズすることもできます。 詳しくは、 [ログ・レベルの変更](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level)を参照してください。



## Linux Sysdig エージェント
{: #linux}

Linux Sysdig エージェントでは、自動的に収集されるデータを指定する 2 つの構成ファイルが使用されます。

| ファイル                   | 説明                                                     | ロケーション                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | メイン構成ファイル </br>**注:****このファイルを編集しないでください。  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Sysdig エージェントをカスタマイズするために編集する構成ファイル。 | `/opt/draios/etc/dragent.yaml`          |
{: caption="表 1. Sysdig エージェントの構成ファイル" caption-side="top"} 

*dragent.yaml* ファイルを編集して、収集されるデータをカスタマイズできます。 ファイルを保存すると、すぐに変更内容が有効になります。 エージェントは変更を検出し、自動的に再始動されます。 Sysdig エージェントが検査する頻度やファイルは、*dragent.default.yaml* ファイルで確認できます。 詳しくは、[Editing the dragent yaml ファイルの編集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent)を参照してください。

例えば、*dragent.default.yaml* に以下の情報が含まれているとします。

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

以下に、Sysdig エージェントによって収集されるデータを制御するために実行できるアクションの概要を示しています。
* [メトリックの組み込みと除外](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [ポートのブロック](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

収集されるログおよびエントリーのタイプをカスタマイズすることもできます。 詳しくは、 [ログ・レベルの変更](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level)を参照してください。


