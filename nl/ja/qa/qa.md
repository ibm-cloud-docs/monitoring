---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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



# よくある質問と回答
{: #qa}

{{site.data.keyword.monitoringshort}} サービスに関する一般的な質問の回答を以下に示します。 
{:shortdesc}

* [最近メトリック値を送信していないメトリックの古いデータを表示できないのはなぜですか?](#qa31)


## 最近メトリック値を送信していないメトリックの古いデータを表示できないのはなぜですか?
{: #qa31}

{{site.data.keyword.monitoringshort}} は、過去 7 日間書き込まれていないメトリックを識別することにより、事実上一時的と思われるメトリック・パスの全データを削除します。 

以下に例を示します。

* コンテナーが削除されると、そのコンテナーに関連付けられたメトリックは 7 日間存在し、その後、それらのメトリックは削除されます。
* `<space_id>.test.statsd.gauge-hello` という名前の statsd ゲージがあり、それに 1 週間書き込まないと、メトリックは一時的と見なされ、そのメトリックはすべての履歴情報と共に削除されます。 

