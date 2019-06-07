---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.mon_full_notm}} のトラブルシューティング
{: #troubleshoot}

{{site.data.keyword.mon_full_notm}} サービスの使用時に発生する一般的な問題のいくつかについて説明します。多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}

## キャプチャーの作成中にエラーが発生します
{: #troubleshoot-entry-1}

インフラストラクチャー内のホストの[キャプチャー・ファイル](/docs/services/Monitoring-with-Sysdig/captures.html#captures)の作成に失敗します。 

ホストのキャプチャー・ファイルの作成を試行したときに、Web UI の*「キャプチャー (Captures)」*セクションでエラーを受け取ります。
{: tsSymptoms}

ホストで実行されている Sysdig エージェントで、機能 **sysdig_capture_enabled** が *false* に設定されています。
{: tsCauses}

ホストで実行されている Sysdig エージェントの **sysdig_capture_enabled** 機能を有効にします。
{: tsResolve}


## キャプチャー・ファイルの状況が *requested* に設定され、状況 *uploaded* に変更されません
{: #troubleshoot-entry-2}

[キャプチャー・ファイル](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)の状況が *requested* に設定され、状況 *uploaded* に変更されません。 分析のためにキャプチャー・ファイルが使用可能になるまで待機しています。

Web UI の*「キャプチャー (Captures)」*セクションで、ホストのキャプチャー・ファイルの状況が *uploaded* に変わりません。
{: tsSymptoms}

ホストの TCP ポート 6443 が無効になっています。
{: tsCauses}


ポート 6443 がオープンであることを確認します。 詳しくは、[ネットワーク・トラフィックの管理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send)を参照してください。
{: tsResolve}


