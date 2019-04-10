---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# 通知チャネルの処理
{: #notifications}

アラートがトリガーされた場合に通知する通知チャネルを構成します。 通知チャネルは、Web UI の*「設定」*パネルで管理します。
{:shortdesc}
 

## 通知チャネルの構成
{: #notifications_create}

通知チャネルを追加するには、以下のステップを実行します。

1. Web UI を起動します。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。 
    
2. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから、**「設定」**を選択します。

3. **「通知チャネル (Notification Channels)」**を選択します。

4. **「マイ・チャネル (MY CHANNELS)」**![「追加」アイコン](../images/add.png) をクリックします。 次に、チャネルを選択します。

    **注:** 通知チャネルを初めて構成する場合、いずれかのチャネルをクリックします。

5. 通知チャネルを構成します。

    * チャネルの名前を入力します。

    * アラート条件がトリガーされなくなった場合に通知を受信するには、*「OK の場合に通知 (Notify when OK)」*フィールドを有効にします。

    * アラートがユーザーによって手動で解決された場合に通知を受信するには、*「解決した場合に通知 (Notify when Resolved)」*条件を有効にします。

    * **E メール**通知チャネルの場合、コンマで区切られた受信者のリストを追加します。

    * **Slack** 通知チャネルの場合、*Slack チャネル* の名前を追加します。

    * **Webhook** 通知チャネルの場合、*Webhook URL* を追加します。 **注:** アラートがトリガーされると、通知は、Webhook エンドポイントに POST として JSON 形式で送信されます。 詳しくは、[Configuring a Webhook channel ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window} を参照してください。 例えば、カスタム Webhook を使用して Sysdig を ServiceNow と統合できます。 ServiceNow を使用した Sysdig の構成について詳しくは、[Configure ServiceNow ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window} を参照してください。

    * **VictorOps** 通知チャネルの場合、*API キー* および*ルーティング・キー* を追加します。

    * **OpsGenie** 通知チャネルの場合、*OpsGenie API キー* を追加します。 OpsGenie 内に Sysdig との統合を構成する必要があることに注意してください。 詳しくは、[Add Sysdig Cloud Integration in Opsgenie ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window} を参照してください。

    * **PagerDuty** 通知チャネルの場合、最初に、Sysdig に自分のアカウントとの統合を許可する必要があります。 PagerDuty を選択した場合、Sysdig との統合を構成するウィザードが開きます。 **「統合の許可 (Authorize Integration)」**または**「ID プロバイダーを使用してサインイン (Sign In Using Your Identity Provider)」**のいずれかをクリックして、PagerDuty を許可します。 既存のサービスを選択するか、または Sysdig 通知用に新しいサービスをセットアップしてから、**「統合の完了 (Finish Integration)」**をクリックします。 Sysdig インシデントに使用するエスカレーション・ポリシーを選択します。 次に、*「通知」*タブで、PagerDuty アカウント、サービス名、およびサービス・キーを確認します。 

    * オプションで、およびテストを許可する統合用に、テスト通知を受信するよう*「テスト通知 (Test notification)」*条件を有効にします。 10 分以内にテスト通知を受信しない場合は、チャネル構成を確認します。 

6. **「チャネルの作成 (CREATE CHANNEL)」**をクリックします。 



## 通知チャネルの変更
{: #notifications_update}

通知チャネルを変更するには、以下のステップを実行します。

1. Web UI を起動します。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。 
    
2. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから、**「設定」**を選択します。

3. **「通知チャネル (Notification Channels)」**を選択します。

4. 変更するターゲット・チャネルを特定し、**「編集」**をクリックします。

5. 変更後、**「変更を保存 (SAVE CHANGES)」**をクリックします。



## 通知チャネルのテスト
{: #notifications_test}

通知チャネルをテストするには、以下のステップを実行します。

1. Web UI を起動します。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。 
    
2. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから、**「設定」**を選択します。

3. **「通知チャネル (Notification Channels)」**を選択します。

4. 変更するターゲット・チャネルを特定し、**「テスト」**をクリックします。



## 通知チャネルの無効化
{: #notifications_disable}

通知チャネルを一時的に無効にするには、以下のステップを実行します。

1. Web UI を起動します。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。 
    
2. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから、**「設定」**を選択します。

3. **「通知チャネル (Notification Channels)」**を選択します。

4. *「通知」*セクションで、*「ダウン時間 (Downtime)」*を有効にしてアラートを一時的に無効にし、すべての通知をミュートします。

## 通知チャネルの削除
{: #notifications_delete}

通知チャネルを削除するには、以下のステップを実行します。

1. Web UI を起動します。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。 
    
2. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから、**「設定」**を選択します。

3. **「通知チャネル (Notification Channels)」**を選択します。

4. 変更するターゲット・チャネルを特定し、**「編集」**をクリックします。

5. **「チャネルの削除 (DELETE CHANNEL)」**をクリックします。

6. チャネルの削除を確認します。 **変更を保存 (SAVE CHANGES)」**をクリックします。




