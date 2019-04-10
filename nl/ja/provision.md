---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# インスタンスのプロビジョニング
{: #provision}

Sysdig を使用してメトリックをモニターおよび管理するには、最初にサービスのインスタンスを {{site.data.keyword.Bluemix}} にプロビジョンする必要があります。
{:shortdesc}

Sysdig インスタンスをパブリック・クラウド地域にプロビジョンするには、そのインスタンスに関連付けられるサービス・プラン、メトリックが収集される地域、およびモニターするメトリック数とその保存期間を決定するプランを選択する必要があります。



## カタログからの Sysdig インスタンスのプロビジョニング
{: #provision_ui}

Sysdig のインスタンスを {{site.data.keyword.cloud_notm}} カタログからプロビジョンするには、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} アカウントにログインします。

    [{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} をクリックして、{{site.data.keyword.cloud_notm}} ダッシュボードを起動します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} UI が開きます。

2. **「カタログ」**をクリックします。 {{site.data.keyword.cloud_notm}} で使用可能なサービスのリストが開きます。

3. 表示されるサービスのリストをフィルタリングするには、**「開発者用ツール」**カテゴリーを選択します。

4. **「{{site.data.keyword.mon_full_notm}}」**タイルをクリックします。 *「プログラム識別情報」*ダッシュボードが開きます。

5. **「インスタンスの作成 (Create instance)」**を選択します。 

6. サービス・プランを選択します。 デフォルトでは、**「トライアル」**プランが設定されています。

    サービス・プランについて詳しくは、『[サービス・プラン](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans)』を参照してください。

7. リソース・グループを選択します。 デフォルトでは、**「デフォルト」**リソース・グループが設定されています。

8. **「作成」**をクリックします。

インスタンスをプロビジョンすると、以下のようになります。 

* *「プログラム識別情報」*ダッシュボードが開きます。 
* サービス ID が自動的に作成されます。 このサービス ID を使用して、インスタンスの Sysdig アクセス・キーを取得できます。

次に、Sysdig エージェントを追加して、メトリック・ソースを構成します。 このエージェントは、メトリックの収集および Sysdig へのメトリックの転送を行います。 



## CLI を使用した Sysdig インスタンスのプロビジョニング
{: #provision_cli}

Sysdig のインスタンスをコマンド・ラインからプロビジョンするには、以下のステップを実行します。

1. [前提条件] {{site.data.keyword.cloud_notm}} CLI をインストールします。

   詳しくは、[『{{site.data.keyword.cloud_notm}}CLI のインストール』](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)を参照してください。

   CLI がインストールされている場合は、次のステップに進みます。

2. インスタンスをプロビジョンしたい、{{site.data.keyword.cloud_notm}} の地域にログインします。 次のコマンドを実行します。 [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. インスタンスをプロビジョンするリソース・グループを設定します。 次のコマンドを実行します。 [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    デフォルトでは、`default` リソース・グループが設定されています。

4. Sysdig インスタンスを作成します。 次の [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) コマンドを実行します。

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    各部分の説明:

    * NAME は、Sysdig インスタンスの名前です。
    
    * *sysdig-monitor* は、{{site.data.keyword.cloud_notm}} 内の {{site.data.keyword.mon_full_notm}} サービス名の名前です。
    
    * SERVICE_PLAN_NAME は、プランのタイプです。 有効な値は、*「lite」*、*「graduated-tier」*です。
    
    * LOCATION は、インスタンスが作成された地域です。

    例えば、有料プランでインスタンスをプロビジョンするには、次のコマンドを実行します。

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

