---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring

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

# 環境のモニタリング
{: #monitoring}

インフラストラクチャー、およびインフラストラクチャー上で実行されているアプリケーションを {{site.data.keyword.mon_full_notm}} サービスを使用してモニターできます。 キャプチャーを要求し、時間フレーム中のノード内での状況を分析できます。
{:shortdesc}

まずは、{{site.data.keyword.cloud_notm}} で {{site.data.keyword.mon_full_notm}} サービスのインスタンスをプロビジョンします。次に、メトリック・ソースに Sysdig エージェントを構成します。ソースの構成が完了したら、サービスの Web UI でデータを表示、モニター、および管理できます。

デフォルトのメトリックのデータは、自動的に収集されます。 カスタム・メトリックを構成し、その特性を説明するために、これらのメトリックにラベルを追加できます。 これらのカスタム・メトリックのデータも、自動的に収集されます。

Web UI の*「探索」*タブおよび*「ダッシュボード」*タブでデータを分析できます。 メトリック・ビューおよびダッシュボードを使用してデータをモニターします。 

* メトリック・ビューを使用して、個々のメトリックをモニターします。
* ダッシュボードを使用して、パネルでデータをモニターすることにより、ネットワーク・データ、アプリケーション・データ、トポロジー、サービス、ホストおよびコンテナーを専門的に洞察します。 パネルでは、メトリックまたはメトリックのグループがダッシュボードに表示されます。

メトリック・ビューおよびダッシュボードごとに、データの有効範囲、データの集約方法、およびデータに適用する時間とグループ・フィルターを定義できます。 詳しくは、[データの管理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)を参照してください。

*「探索」*タブで、デフォルトのメトリックとデフォルトのダッシュボードを使用して、データをモニターできます。 ラベルを使用すると、新しいインフラストラクチャー・グループを定義し、その後、これらのグループを使用してデータを異なる方法で集約し、環境をモニターできます。 また、*「ダッシュボード」*タブを介して定義したカスタム・ダッシュボードを使用することもできます。

*「ダッシュボード」*タブでは、デフォルトのダッシュボードのいずれかを使用するか、または新しいダッシュボードを作成して、データをモニターできます。

デフォルトのダッシュボードをチームのデフォルトのエントリー・ポイントとして構成してチームのエクスペリエンスを統一すれば、各ユーザーが自分にとって最も重要な情報にすぐに注目できるようになります。
{: tip}

アラートを使用すると、1 つ以上の通知チャネルを介して、注意が必要な問題をユーザーに通知できます。
* Web UI の*「アラート (Alerts)」*セクションには、事前定義されたアラートのリストが表示されます。 このビューで、事前定義されたアラートの有効化と無効化、既存のアラートの変更、および新しいアラートの作成を行うことができます。
* Web UI の*「設定」*セクションでは、通知チャネルを構成します。
 
ノードに対するキャプチャーを要求し、時間フレーム中のそのノード内での状況を分析できます。 例えば、キャプチャーを使用して、ボトルネックまたはコンポーネントの対話を分析できます。

## メトリック
{: #monitoring_metrics}

メトリックとは数量的な尺度であり、その特性を定義するラベルを 1 つ以上持っています。メトリックを使用して、数値を含むデータを統計的に分析します。 

メトリックは、時系列で表示されます。 時系列は、一定期間にわたる一連の数値データ・ポイントです。 

メトリックは以下の 2 つのグループに分類されます。 

* [デフォルトのメトリック](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [カスタム・メトリック](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

ラベルは、インフラストラクチャー・ラベルとメトリック記述子ラベルとして分類されます。 各メトリックには、一連の事前定義されたラベルがあります。 カスタム・メトリックの場合、追加のラベルを構成できます。 

ラベルを使用すると、例えば以下のように、メトリックの特性を識別および区別できます。
* インフラストラクチャー・オブジェクトを論理階層にグループ化できます。 
* データをフィルターで除外できます。 
* 集約データをセグメントに分割できます。 

詳しくは、[ラベル](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels)を参照してください。

## パネル
{: #monitoring_panels}

パネルでは、メトリックまたはメトリックのグループがダッシュボードに表示されます。 

以下のいずれかのパネル・タイプを使用して、メトリックを視覚化できます。

| タイプ | 説明 |
|------|-------------|
| `折れ線グラフ` | このパネルを使用して、1 つ以上のメトリックの傾向を経時的に表示します。  |
| `面グラフ` | このパネルを使用して、1 つ以上のメトリックの傾向を経時的に表示します。  |
| `上位リスト` | このパネルを使用して、エンティティーのグループ間でメトリックを比較します。 棒グラフは降順でソートされます。  |
| `ヒストグラム` | このパネルを使用して、バケットでのメトリックの頻度分布を表示します。  |
| `トポロジー` | このパネルを使用して、インフラストラクチャーをトポロジー・マップとして視覚化し、マップ内のエンティティー間の関係を視覚化します。  |
| `数値` | このパネルを使用して、1 つ以上のエンティティーについて経時的に集約されたメトリックの値を表す単一の数字を表示します。  |
| `テーブル` | このパネルを使用して、インフラストラクチャーの数値データをメトリックおよびセグメントに基づいて表示します。  |
| `テキスト` | このパネルを使用して、テキストを追加します。 マークダウンを使用して、テキストを追加します。  |
{: caption="表 1. パネル・タイプ" caption-side="top"} 

パネルに対して、コピー、有効範囲の変更、複製、削除、エクスポート、および探索を行うことができます。

パネルからデータをエクスポートできます。 データをエクスポートする場合は、以下の情報を考慮してください。

* 折れ線グラフから、**JSON ファイル**にデータをエクスポートできます。
* テーブル・チャートまたは折れ線グラフから、**CSV ファイル**にデータをエクスポートできます。


以下の表に、パネルで実行可能なタスクを示します。

| タスク | 説明 |
|------|-------------|
| [パネルのコピー](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | パネルを新しいダッシュボードにコピーします。  |
| [有効範囲の変更](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | パネルの有効範囲を変更します。 |
| [パネルの複製](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | 同じダッシュボード内にパネルをコピーします。  |
| [パネルの削除](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | ダッシュボードからパネルを削除します。  |
| [データのエクスポート ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | パネルから CSV ファイルまたは JSON ファイルにデータをエクスポートします。  |
| [アラートの作成](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | メトリックに対してアラートを定義します。 |
{: caption="表 2. パネル・タスク" caption-side="top"} 


## ダッシュボード
{: #monitoring_dashboards}

**ダッシュボード**には、単一のホストまたはホスト・グループのインフラストラクチャー、アプリケーション、サービスについて、その正常性、パフォーマンス、および状態を報告するメトリックのグループが表示されます。 ダッシュボードによって、ネットワーク・データ、アプリケーション・データ、トポロジー、サービス、ホスト、およびコンテナーに対する専門的な洞察を得ることができます。 インフラストラクチャー、アプリケーション、およびサービスをモニターするには、ダッシュボードを使用します。


Web UI の**「ダッシュボード」**セクションでは、ダッシュボードは以下の 3 つの主要なグループに編成されています。

* **マイ・ダッシュボード (My Dashboards)**: 現在ログイン中のユーザーによって作成されたダッシュボードです。
* **マイ共有ダッシュボード (My Shared Dashboards)**: 現在ログイン中のユーザーによって作成され、他のユーザーと共有されたダッシュボードです。
* **共有してもらったダッシュボード (Dashboards Shared With Me)**: 他のユーザーによって作成され、現在のユーザーと共有されたダッシュボードです。

Web UI の**「探索」**セクションでは、ダッシュボードは以下の 2 つのグループに編成されています。
* **デフォルトのダッシュボード (Default dashboards)**: 事前に定義されたダッシュボードです。
* **マイ・ダッシュボード (My Dashboards)**: 現在ログイン中のユーザーによって作成されたダッシュボードです。

事前定義されたダッシュボードを使用できます。 また、Web UI を使用するか、またはプログラムで、カスタム・ダッシュボードを作成することもできます。 Python スクリプトまたは Sysdig REST API を使用して、ダッシュボードをバックアップおよびリストアできます。

また、Web UI を使用して、ダッシュボードをコピーおよび共有することもできます。 

以下の表に、UI からダッシュボードを使用するために実行可能なタスクの概要を示します。

| タスク | 説明 |
|------|-------------|
| [ダッシュボードの作成](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | Web UI で、カスタム・ダッシュボードを作成します。 |
| [ダッシュボードのコピー](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | ダッシュボードを使用可能な現在のチームでダッシュボードのコピーを作成するか、または別のチームにダッシュボードをコピーします。 |
| [有効範囲の変更](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | ダッシュボードの有効範囲を変更します。       |
| [ダッシュボードの削除](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  ダッシュボードを削除します。 |
| [ダッシュボードの共有](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | チーム内のユーザー間でダッシュボードを共有し、ダッシュボードにパブリック URL を構成することで外部的にダッシュボードを共有します。 |
{: caption="表 3. Web UI で実行可能なダッシュボード・タスク" caption-side="top"} 

以下の表に、ダッシュボードを使用するためにプログラムで実行可能なタスクの概要を示します。

| タスク                    |	REST API の使用                |
|-------------------------|-------------------------------|
| ダッシュボードの作成      | [API を使用したダッシュボードの作成](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| ダッシュボードの削除      | [API を使用したダッシュボードの削除](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| ダッシュボードの保存       | [API を使用したチームのダッシュボードの保存](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="表 4. ダッシュボードをプログラムで管理するためのタスク" caption-side="top"} 



## イベント
{: #monitoring_events}

イベントとは、{{site.data.keyword.mon_full_notm}} インスタンスにデータを転送するノードで発生した何らかの状況について知らせる通知です。イベントを使用して、問題を確認、トラッキング、および解決します。 

さまざまなタイプのイベントの概要を以下に示します。 

* *アラート・イベント* は、ユーザーが構成したアラートによってトリガーされるイベントです。 詳しくは、[アラートの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)を参照してください。
* *インフラストラクチャー・ベース・イベント* は、Docker ノードおよび Kubernetes ノードから収集されるイベントです。 デフォルトでは、Sysdig エージェントは選択したイベントのグループから自動的にデータを検出し、収集します。 エージェント構成ファイルを編集して、さらにイベントを有効にすることができます。
* 統合 (Slackbot、事前に構築された Python スクリプト、カスタム・ユーザーによって作成された Python スクリプト、または cURL 要求) のいずれかを介して構成する*カスタム・イベント*。

デフォルトでは、イベントの状態は以下のようになります。 
* **アクティブ**: この状態は、イベントをトリガーした環境がそのまま維持される (例えば、ノードが引き続きダウンしたままになる) ことを示します。
* **OK**: この状態は、通常状態に戻る (例えば、ノードが稼働中である) ことを示します。

イベントは、Web UI の*「イベント」*セクションで管理します。 
* アラート・イベントは、*「アラート・イベント (Alert Events)」*タブで表示できます。
* インフラストラクチャー・ベース・イベントは、*「カスタム・イベント (Custom events)」*タブで表示できます。
* カスタム・イベントは、*「カスタム・イベント (Custom events)」*タブで表示できます。
* カスタム・イベントをいずれかのチームに送信するには、[該当するチーム用の API トークン](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token)を使用します。 詳しくは、[Custom events ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window} を参照してください。
* イベントを**「解決済み」**に設定すると、状況が**「OK」**に設定されるまで待たずに、問題が解決されたことを他のユーザーに通知できます。
{: #tip}



## アラート
{: #monitoring_alerts}

アラートとは、注意する必要がある状態について警告するために使用可能な通知イベントです。 各アラートには、重大度を表す状況が存在します。 この状況により、報告された情報の重要度が通知されます。 

アラートを定義する場合は、通知をトリガーする条件と、通知に使用する 1 つ以上の通知チャネルを定義する必要があります。また、アラートの重大度とアラートのタイプも定義する必要があります。 

以下のいずれかのアラート・タイプについて、アラートを定義できます。

| タイプ              | 説明 |
|-------------------|-------------|
| 異常検出 | ホストをその履歴動作に基づいてモニターし、逸脱した場合にアラートするために使用します。 |
| ダウン時間          | あらゆるタイプのエンティティー (ホスト、コンテナー、プロセス、サービスなど) をモニターし、エンティティーがダウンした場合にアラートするために使用します。 |
| イベント             | 特定のイベントの発生をモニターし、発生の合計回数がしきい値に違反した場合にアラートするために使用します。 例えば、これにより、コンテナー、オーケストレーション、およびサービス・イベントの再始動時およびデプロイメント時にアラートできます。|
| グループ外れ値     | ホストのグループをモニターし、いずれかの動作が残りのホストの動作と異なる場合に通知するために使用します。 |
| Metric (メトリック)            | 時系列メトリックをモニターし、メトリックがユーザー定義のしきい値を違反した場合にアラートするために使用します。 |
{: caption="表 5. アラート・タイプ" caption-side="top"} 

デフォルトでは、重大度は*「警告」*に設定されています。 アラートの重大度は、*「緊急 (emergency)」*、*「アラート (alert)」*、*「重大」*、*「エラー」*、*「警告」*、*「注意」*、*「通知 (informational)」*、「デバッグ* (debug*)」に設定できます。 

以下のいずれかの通知統合に対して、1 つ以上の通知チャネルを定義できます。
* E メール通知
* PagerDuty 通知
* Slack 通知
* VictorOps 通知
* OpsGenie 通知
* Webhook チャネルの構成

詳しくは、[通知チャネルの構成](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create)を参照してください。


Web UI で、および Sysdig API を使用して、事前定義されたアラートの有効化、アラートの変更、およびカスタム・アラートの作成を行うことができます。

アラートは、Web UI の*「アラート (Alerts)」*ビューで管理します。 *「アラート (Alerts)」*ビューに表示されるテーブル列を構成できます。 有効な列オプションは、*「名前」*、*「スコープ」*、*「アラート条件 (Alert When)」*、*「セグメント化の基準 (Segment By)」*、*「通知」*、*「有効」*、*「変更日時 (Modified)」*、*「キャプチャー (Captures)」 * 、*「チャネル」*、*「作成日時 (Created)」*、*「説明」*、*「E メール受信者 (Email recipients)」*、*「最小回数 (For at least)」*、*「OpsGenie」*、*「PagerDuty」*、*「重大度」*、*「Slack」*、*「Web フック」*、*「SNS トピック (SNS topics)」*、*「タイプ」*、*「VictorOps」*です。

次のリストは、アラートを使用する際のメインタスクの概要を示しています。
* [アラートの構成 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [アラートの有効化または無効化 ![ 外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [アラートの検索 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [アラートの変更 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [同じチームへのアラートのコピー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン ")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [異なるチームへのアラートのコピー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン ")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [アラートのエクスポート ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [アラートの削除 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [カスタム・ブール式としてのアラートしきい値の定義 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## キャプチャー
{: #monitoring_captures}

キャプチャーとは、時間フレーム中のノード内での状況を分析するために生成可能なトレース・ファイルです。 キャプチャー・ファイルのサイズ制限は 100 MB です。例えば、キャプチャーを使用して、ボトルネックまたはコンポーネントの対話を分析できます。 

キャプチャーには、システム呼び出しおよびその他の OS イベント (システム・レベルの待ち時間、バッチ・ジョブ所要時間、デプロイメント中断時間、自動目盛り設定待ち時間、コンテナー起動時間、アプリケーション・トランザクション時間など) が含まれます。 キャプチャーには、ノード上の各コンテナーからの詳細情報が含まれます。 

組織のガイドラインに従ってキャプチャーの無効化を検討してください。 デフォルトでは、ノード内に Sysdig エージェントを構成した場合、キャプチャーは有効になります。
{: tip}

個々のノードについて、*キャプチャー* を作成、探索、ダウンロード、および削除できます。 ノードは、Sysdig エージェントをインストールしたホスト、コンテナー、仮想マシン、ベアメタル、または任意のメトリック・ソースにすることができます。 

* Web UI の*「探索」*セクションでキャプチャーを作成し、*「キャプチャー (Captures)」*セクションでキャプチャー・ファイルを管理します。
* *Csysdig* (Sysdig 用の curses ベースのコマンド・ライン UI) またはオープン・ソースの Sysdig ユーティリティーを使用してキャプチャーのデータを視覚化し、キャプチャーのデータを分析できます。
* フィルターを使用して、キャプチャー内のデータを検索できます。
* Chisel (スクリプト) を使用して、キャプチャー内のデータを操作できます。 

チームのキャプチャー機能を有効にした場合、キャプチャー・ファイルはそのチームのメンバーにのみ表示されます。

次のリストは、キャプチャーを使用する際のメインタスクの概要を示しています。
* [キャプチャーの作成](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [キャプチャーの削除](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [キャプチャーの探索](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [キャプチャーのダウンロード](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)を参照してください。


