---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# インスタンスの削除
{: #remove}

{{site.data.keyword.mon_full_notm}} サービスのインスタンスは、{{site.data.keyword.Bluemix}} UI またはコマンド・ラインを使用して削除できます。
{:shortdesc}

{{site.data.keyword.cloud_notm}} からインスタンスを削除する場合、タイディアップ (整理) のために、以下の情報を検討してください。

1. 削除する {{site.data.keyword.mon_full_notm}} インスタンスにメトリックを転送しているソースのリストを作成します。 ソースごとに Sysdig エージェントを削除する必要があります。
2. インスタンスを使用するためにユーザーに付与されている権限を削除します。 

    アクセス・グループを使用してインスタンスへのアクセス権限を管理している場合は、アクセス・グループを削除する必要があります。

    アクセス・グループを使用してさまざまなサービス・インスタンスへのアクセス権限を管理している場合は、削除するインスタンスへの権限を付与しているポリシーを削除する必要があります。
    
    ユーザーに個別にポリシーを付与している場合は、インスタンスへのアクセス権限を持っている各ユーザーの情報を集める必要があります。次に、削除するインスタンスに関連するポリシーを 1 つずつ削除する必要があります。


その後、{{site.data.keyword.cloud_notm}} ダッシュボードからインスタンスを削除します。


## {{site.data.keyword.cloud_notm}} UI を使用したインスタンスの削除
{: #remove_ui}

{{site.data.keyword.cloud_notm}} UI を使用して {{site.data.keyword.mon_full_notm}} のインスタンスを削除するには、以下のステップを実行します。

1. [{{site.data.keyword.cloud_notm}} アカウントにログイン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} UI が開きます。

2. **「プログラム識別情報」**を選択します。 

3. **「モニタリング」**を選択します。 インスタンスのリストが表示されます。

4. 削除するインスタンスを選択します。

5. *「アクション」*メニューから**「削除」**を選択します。


## CLI を使用したインスタンスの削除
{: #remove_cli}

コマンド・ラインを使用して {{site.data.keyword.mon_full_notm}} のインスタンスを削除するには、以下のステップを実行します。

1. [前提条件] {{site.data.keyword.cloud_notm}} CLI をインストールします。CLI がインストールされている場合は、次のステップに進みます。

   詳しくは、[『{{site.data.keyword.cloud_notm}}CLI のインストール』](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)を参照してください。

2. インスタンスをプロビジョンしたい、{{site.data.keyword.cloud_notm}} の地域にログインします。 次のコマンドを実行します。 [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. インスタンスがプロビジョンされているリソース・グループを設定します。 次のコマンドを実行します。 [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    デフォルトでは、`default` リソース・グループが設定されています。

4. インスタンスを削除します。 次の [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete) コマンドを実行します。

    ```
    ibmcloud resource service-instance-delete NAME 
    ```
    {: codeblock}

    ここで、NAME は、インスタンスの名前です

    例えば、インスタンスを削除するために以下のコマンドを実行します。

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
