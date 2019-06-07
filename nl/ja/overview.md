---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, overview

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


# {{site.data.keyword.mon_full_notm}}
{: #about}

{{site.data.keyword.mon_full}} は、{{site.data.keyword.cloud_notm}} アーキテクチャーの一部として組み込むことができる、サード・パーティーのクラウド・ネイティブかつコンテナー・インテリジェントな管理システムです。 このシステムを使用して、アプリケーション、サービス、およびプラットフォームのパフォーマンスと正常性について、運用の可視化が可能になります。 管理者、DevOps チーム、開発者向けのフルスタックのテレメトリーを備え、モニター、トラブルシューティング、アラートの定義、カスタム・ダッシュボードの設計を行える高度な機能も用意されています。{{site.data.keyword.mon_full_notm}} は、{{site.data.keyword.IBM_notm}} との協力関係のもと、Sysdig によって運用されます。
{:shortdesc}


{{site.data.keyword.cloud_notm}} で、モニタリング機能を {{site.data.keyword.mon_full_notm}}に追加するには、{{site.data.keyword.mon_full_notm}} サービスのインスタンスをプロビジョンする必要があります。

インスタンスをプロビジョンする前に、以下の情報を考慮してください。

* お客様のデータはサード・パーティーに送信されます。
* アカウント所有者は、{{site.data.keyword.cloud_notm}} でサービスのインスタンスを作成、表示、および削除できます。このユーザーはまた、{{site.data.keyword.mon_full_notm}} サービスを使用するための権限を他のユーザーに付与できます。
* `administrator` 権限または `editor` 権限を持つ他の {{site.data.keyword.cloud_notm}} ユーザーは、{{site.data.keyword.cloud_notm}} の {{site.data.keyword.mon_full_notm}} サービスを管理できます。 また、これらのユーザーには、インスタンスをプロビジョンする予定のリソース・グループのコンテキスト内でリソースを作成するためのプラットフォーム権限も必要です。

リソース・グループのコンテキスト内でインスタンスをプロビジョンします。 リソース・グループを使用すると、アクセス制御および請求処理のためにサービスを編成できます。{{site.data.keyword.mon_full_notm}} インスタンスは、*デフォルト*・リソース・グループまたはカスタム・リソース・グループにプロビジョンできます。

[インスタンスをプロビジョンする](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision)と、取り込みキー ([Sysdig アクセス・キー](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key)) が自動的に与えられます。

インスタンスをプロビジョンしたら、各メトリック・ソースに {{site.data.keyword.mon_full_notm}} エージェントを構成する必要があります。メトリック・ソースとは、そのパフォーマンスと正常性をモニターして制御する必要があるクラウド・リソースです。 モニターする環境ごとに、{{site.data.keyword.mon_full_notm}} エージェントを構成する必要があります。例えば、メトリック・ソースは、Kubernetes クラスターにすることができます。 アクセス・キーを使用して、メトリック・データの収集およびインスタンスへのメトリック・データの転送を行う Sysdig エージェントを構成します。

{{site.data.keyword.mon_full_notm}} エージェントがメトリック・ソースにデプロイされると、メトリックの収集およびインスタンスへのメトリックの転送は自動化されます。 {{site.data.keyword.mon_full_notm}} エージェントは、事前定義されたメトリックについて収集およびレポートを自動的に行います。 環境内でモニターするメトリックを構成できます。

{{site.data.keyword.mon_full_notm}} Web UI を使用して、データを[モニター](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring)および[管理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)できます。  

次の図は、{{site.data.keyword.cloud_notm}} で実行中の {{site.data.keyword.mon_full_notm}} サービスのコンポーネント概要を示しています。

![{{site.data.keyword.mon_full_notm}} コンポーネントの概要、{{site.data.keyword.cloud_notm}}](images/components.png "{{site.data.keyword.mon_full_notm}} コンポーネントの概要、{{site.data.keyword.cloud_notm}}")



## データ収集
{: #overview_collection}

データを収集して {{site.data.keyword.mon_full_notm}} インスタンスに転送するように Sysdig エージェントを構成すると、データは自動的に収集され、Web UI による分析に使用できるようになります。

データは 10 秒間隔で収集されます。 

## データ可用性
{: #overview_availability}

データは、最大 15 カ月間使用可能です。

Sysdig エージェントをホストまたはコンテナーから削除しても、履歴データは削除されません。 データは、エージェントがインストールされレポートしていた期間については、Web UI によって分析に使用できます。

{{site.data.keyword.mon_full_notm}} サービスのインスタンスを削除すると、データは検索および分析に使用できなくなります。



## データ保存
{: #overview_retention}

データは、*ロールアップ*・ポリシーに基づいて、インスタンスごとに保存されます。

時間の経過に伴い、3 カ月が過ぎるまで、データは細かい細分度からより荒い細分度にロールアップされます。

ロールアップ・ポリシーは、経時的なデータの細分度を記述します。

* 最初の 6 時間は、10 秒単位のデータが保持されます。
* 2 日間は、1 分単位のデータが保持されます。
* 2 週間は、10 分単位のデータが保持されます。
* 3 カ月間は、1 時間単位のデータが保持されます。
* 1 年間は、1 日単位のデータが保持されます。

## データ削除
{: #overview_data_deletion}

{{site.data.keyword.mon_full_notm}} のインスタンスを {{site.data.keyword.cloud_notm}} から削除する場合、サポートを介して Case をオープンし、データの削除を要求する必要があります。 詳しくは、[サポートへの連絡方法](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp)を参照してください。

キャプチャーを削除すると、そのキャプチャーのデータ・ファイルは自動的に削除されます。

{{site.data.keyword.mon_short}} インスタンスで単一の Sysdig エージェントから収集されたデータを削除する操作は、サポートされていません。
{: note}



## データ場所
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}} では、メトリックを収集および集約します。 

* メトリック・データは、{{site.data.keyword.cloud_notm}} 上でホストされます。
* 複数ゾーン地域 (MZR) の場所ごとに、その場所で実行される {{site.data.keyword.mon_full_notm}} の各インスタンスのメトリックが収集および集約されます。
* データは、{{site.data.keyword.mon_full_notm}} インスタンスがプロビジョンされている同じ地域に配置されます。 例えば、米国南部にプロビジョンされたインスタンスのメトリック・データは、米国南部地域でホストされます。



## {{site.data.keyword.mon_full_notm}} エージェント
{: #overview_sysdig_agent}

{{site.data.keyword.mon_full_notm}} エージェントは、事前定義されたメトリックについて収集およびレポートを自動的に行います。 

次のリストは、使用可能な {{site.data.keyword.mon_full_notm}} エージェントの概要を示しています。

* Kubernetes、GKE、および OpenShift 用の {{site.data.keyword.mon_full_notm}} エージェント
* Docker コンテナーまたはコンテナー化されていないサービス用の {{site.data.keyword.mon_full_notm}} エージェント
* Mesos、Marathon、および DCOS 用の {{site.data.keyword.mon_full_notm}} エージェント
* 手動による Linux インストール用の {{site.data.keyword.mon_full_notm}} エージェント

詳しくは、[Sysdig エージェントの構成](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent)および [Sysdig エージェントの削除](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove)を参照してください。


## 使用量の表示
{: #overview_usage}

サービスの使用量およびコストをモニターするには、[使用量の表示](/docs/billing-usage/viewing_usage.html#viewingusage)を参照してください。


## サービス・プラン
{: #overview_plans}

{{site.data.keyword.mon_full_notm}} インスタンスには、さまざまな価格プランを使用できます。 [詳細はこちら](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)。


## セキュリティーに関する考慮事項
{: #overview_security}

**キャプチャー**

キャプチャーとは、時間フレーム中のホスト内での状況を分析するために生成可能なトレース・ファイルです。 キャプチャーには、システム呼び出しおよびその他の OS イベントが含まれます。 この機能は、該当するノードからメトリックを収集する Sysdig エージェントを構成する際に、ノードごとに有効または無効にできます。 デフォルトでは、Sysdig エージェントの構成時、*キャプチャー* は有効になっています。 ノードは、Sysdig エージェントをインストールしたホスト、コンテナー、仮想マシン、ベアメタル、または任意のメトリック・ソースにすることができます。

キャプチャーを有効にすると、操作が Sysdig で詳細に認識されるようになることに注意してください。セキュリティー・インシデントおよび組織外部にデータが公開される可能性を防ぐには、ノードに対してキャプチャーを有効にする前に、組織のセキュリティー・ポリシーを確認してください。 すべての Sysdig エージェントに対して、*キャプチャー* 機能の無効化を検討してください。
{: important}

