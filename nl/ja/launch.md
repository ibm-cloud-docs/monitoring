---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# Web UI へのナビゲート
{: #launch}

{{site.data.keyword.Bluemix}} に {{site.data.keyword.mon_full_notm}} サービスのインスタンスをプロビジョンして、メトリック・ソースに対して Sysdig エージェントを構成すると、{{site.data.keyword.mon_full_notm}} Web UI を介してメトリックを表示、モニター、および管理できます。
{:shortdesc}


## データを表示する IAM ポリシーのユーザーへの付与 
{: #launch_step1}

**注:** {{site.data.keyword.mon_full_notm}} サービスの管理者または {{site.data.keyword.mon_full_notm}} インスタンスの管理者であるか、他のユーザーにポリシーを付与するアカウントの IAM 権限を持っている必要があります。

以下の表は、ユーザーが {{site.data.keyword.mon_full_notm}} Web UI を起動してデータを表示するために最低限必要なポリシーを示しています。

| サービス                        | 役割                      | 付与された権限     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | プラットフォーム役割: ビューアー     | ユーザーは「プログラム識別情報モニタリング (Observability Monitoring)」ダッシュボードでサービス・インスタンスのリストを表示できます。 |
| `{{site.data.keyword.mon_full_notm}}` | サービス役割: ライター      | ユーザーは Web UI を起動して、Web UI でメトリックを表示できます。  |
{: caption="表 1. IAM ポリシー" caption-side="top"} 

ユーザーのこれらのポリシーを構成する方法について詳しくは、[メトリックを表示するための権限のユーザーへの付与](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig)を参照してください。


## {{site.data.keyword.cloud_notm}} UI を使用した Web UI の起動
{: #launch_step2}

{{site.data.keyword.cloud_notm}} UI から {{site.data.keyword.mon_full_notm}} インスタンスのコンテキスト内で Web UI を起動します。 

Web UI を起動するには、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} アカウントにログインします。

    [{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} をクリックして、{{site.data.keyword.cloud_notm}} ダッシュボードを起動します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} ダッシュボードが開きます。

2. ナビゲーション・メニューで、**「プログラム識別情報」**を選択します。 

3. **「モニタリング」**を選択します。 

    {{site.data.keyword.cloud_notm}} で使用可能なインスタンスのリストが表示されます。

4. インスタンスを 1 つ選択します。 次に、**「Sysdig の表示 (View Sysdig)」**をクリックします。

Web UI が開きます。


