---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, api token

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


# API トークンの処理
{: #api_token}

Python スクリプトまたは Sysdig REST API を使用してルーチン・タスクを自動化し、通知をモニターする場合に、API トークンを使用して {{site.data.keyword.mon_full_notm}} サービスで認証します。 
{:shortdesc}

{{site.data.keyword.mon_full_notm}} サービスの各インスタンスに関する以下の情報を考慮してください。

* チームごとに API トークンがあります。
* トークンが漏えいした場合や組織のセキュリティー・ポリシーによって特定の条件後にトークンをリセットする必要がある場合、管理権限を持つユーザーは API トークンをリセットできます。


## Sysdig API トークンの取得
{: #api_token_get}


トークンを取得するには、以下のステップを実行します。

1. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから**「設定」**を選択します。
2. *「Sysdig Monitor API (Sysdig Monitor API)」*セクションから**「Sysdig Monitor API トークン (Sysdig Monitor API Token)」**をコピーします。

## Sysdig API トークンのリセット
{: #api_token_reset}

トークンをリセットするには、以下のステップを実行します。

1. ナビゲーション・バーの*「セレクター (Selector)」*ボタンから、**「設定」**を選択します。
2. *「Sysdig Monitor API (Sysdig Monitor API)」*セクションで**「トークンのリセット (Reset Token)」**をクリックすると、API トークンがリセットされます。
