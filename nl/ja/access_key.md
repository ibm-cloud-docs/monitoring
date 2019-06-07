---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# アクセス・キーの管理
{: #access_key}

**アクセス・キー** は、{{site.data.keyword.cloud_notm}} で {{site.data.keyword.mon_full_notm}} インスタンスにデータが正常に転送されるように Sysdig エージェントを構成するために使用する必要があるトークンです。   
{:shortdesc}


## {{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得
{: #access_key_ibm_cloud_ui}

{{site.data.keyword.cloud_notm}} UI を使用して {{site.data.keyword.mon_full_notm}} インスタンス用のアクセス・キーを取得するには、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} アカウントにログインします。

    [{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/login){:new_window} をクリックして、{{site.data.keyword.cloud_notm}} ダッシュボードを起動します。

	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.cloud_notm}} UI が開きます。

2. ナビゲーション・メニューで、**「プログラム識別情報」**を選択します。 

3. **「モニタリング」**を選択します。 {{site.data.keyword.mon_full_notm}} ダッシュボードが開きます。 {{site.data.keyword.cloud_notm}} で使用可能なモニタリング・インスタンスのリストが表示されます。

3. アクセス・キーを取得するインスタンスを特定し、**「アクセス・キーの表示 (View access key)」**をクリックします。

4. ポップ・アップ・ウィンドウが開き、**「表示」**をクリックすると、アクセス・キーが表示されます。



## CLI を使用したアクセス・キーの取得
{: #access_key_cli}

コマンド・ラインを使用して Sysdig インスタンス用のアクセス・キーを取得するには、以下のステップを実行します。

1. [前提条件] {{site.data.keyword.cloud_notm}} CLI をインストールします。

   詳しくは、[『{{site.data.keyword.cloud_notm}}CLI のインストール』](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)を参照してください。

   CLI がインストールされている場合は、次のステップに進みます。

2. Sysdig インスタンスが実行されている {{site.data.keyword.cloud_notm}} の地域にログインします。 次のコマンドを実行します。 [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Sysdig インスタンスが実行されているリソース・グループを設定します。 次のコマンドを実行します。 [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    デフォルトでは、`default` リソース・グループが設定されています。

4. インスタンス名を取得します。 次のコマンドを実行します。 [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Sysdig インスタンスに関連付けられている API キーの名前を取得します。 次の [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) コマンドを実行します。

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    ここで、INSTANCE_NAME は前のステップで取得したインスタンスの名前です。

6. アクセス・キーを取得します。 次の [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) コマンドを実行します。

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    ここで、APIKEY_NAME は、API キーの名前です。
 
    このコマンドの出力には、インスタンスのアクセス・キーを含む **Sysdig Access Key** フィールドが表示されます。


例えば、以下のコマンドは、サンプル・サービス ID の出力を示しています。

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## アクセス・キーのリセット 
{: #access_key_reset}

アクセス・キーが漏えいした場合や数日後にアクセス・キーを更新するポリシーがある場合は、新しいキーを生成して古いキーを削除できます。

{{site.data.keyword.mon_full_notm}} インスタンスのアクセス・キーを更新するには、以下のステップを実行します。

1. {{site.data.keyword.mon_full_notm}} Web UI を起動します。 詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。

2. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから、**「設定」**を選択します。

2. *「パスワード管理 (Password management)」*セクションで**「パスワードのリセット (Reset your password)」**をクリックします。

**注:** Sysdig アクセス・キーをリセットした後に、この {{site.data.keyword.mon_full_notm}} インスタンスにメトリックを転送するすべてのログ・ソースのアクセス・キーを更新する必要があります。
