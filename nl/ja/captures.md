---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# キャプチャーの処理
{: #captures}

キャプチャーとは、時間フレーム中のホスト内での状況を分析するために生成可能なトレース・ファイルです。 例えば、キャプチャーを使用して、ボトルネックまたはコンポーネントの対話を分析できます。 {{site.data.keyword.mon_full_notm}} サービスでは、個別のノードの*キャプチャー* を作成、探索、ダウンロード、および削除できます。 
{:shortdesc}

詳しくは、[キャプチャー](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)を参照してください。


## キャプチャーの作成
{: #captures_create}

キャプチャーは、*「探索」*ビューで作成します。

キャプチャー・ファイルを作成するには、以下のステップを実行します。

1. Web UI の*「探索」*セクションにナビゲートします。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。

2. ホストの切り替えアイコン ![ホストの切り替えアイコン](images/switch_hosts.png) をクリックします。

3. ホストまたはコンテナーを選択します。

4. アクション・アイコン ![3 つのドットのアイコン](images/actions.png) をクリックし、**「Sysdig キャプチャー (Sysdig capture)」**を選択します。

    *「Sysdig キャプチャー (Sysdig Capture)」*ウィンドウが開きます。

5. *「Sysdig キャプチャー (Sysdig Capture)」*ウィンドウで以下のパラメーターを定義します。

    1. *「キャプチャーのパスと名前 (Capture path and name)」*フィールドにキャプチャー・ファイルの名前を入力します。 デフォルト値のままにすることも、デフォルト値を変更することもできます。 デフォルト名には、キャプチャーが作成された日付とタイム・スタンプが含まれます。 

    2. *「時間フレーム」*を設定して、データを収集する秒数を指定します。 デフォルトのキャプチャー時間は 15 秒です。 最大キャプチャー時間は 86400 秒 (24 時間) です。 

    3. (オプション) フィルターを追加して、収集されるトレース情報の量を制限します。 

6. **「キャプチャーの開始 (Start capture)」**をクリックします。 Sysdig エージェントによって、キャプチャーが開始され、結果のトレース・ファイルが送り返されます。 

7. **「キャプチャー・ページに移動 (Go to captures page)」**をクリックすると、Web UI の*「キャプチャー (Captures)」*セクションにキャプチャーのリストが表示されます。 

*「キャプチャー (Captures)」*ページには、キャプチャー・ファイル名、取得元のホスト、時間フレーム、およびキャプチャーのサイズを示す表が表示されます。 

キャプチャー・ファイルの状況は、以下のいずれかの値になります。
* **要求**: ファイルが生成されています。
* **アップロードが完了しました**: ファイルをダウンロードして、分析できます。
* **エラー**: タイムアウト、受信されなかったデータ、またはエージェント・エラーにより、ファイルを使用できません。



## キャプチャーの削除
{: #captures_delete}

キャプチャー・ファイルを削除するには、以下のステップを実行します。

1. Web UI の*「キャプチャー (CAPTURES)」*セクションにナビゲートします。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。
2. 削除するキャプチャー・ファイルを識別して選択します。
3. **「削除」**をクリックします。



## キャプチャーの探索
{: #captures_explore}

キャプチャー・ファイルを探索するには、以下のステップを実行します。

1. Web UI の*「キャプチャー (CAPTURES)」*セクションにナビゲートします。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。
2. 分析するホストのデータを含むキャプチャー・ファイルを識別して選択します。
3. **「探索」**をクリックします。



## キャプチャーのダウンロード
{: #captures_download}

キャプチャー・ファイルをダウンロードするには、以下のステップを実行します。

1. Web UI の*「キャプチャー (CAPTURES)」*セクションにナビゲートします。 Web UI の起動方法について詳しくは、[Web UI へのナビゲート](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)を参照してください。
2. ダウンロードするデータを含むキャプチャー・ファイルを識別して選択します。
3. **「ダウンロード」**をクリックします。


## Chisel
{: #captures_chisels}

Sysdig の Chisel は、スクリプト言語 Lua で作成されるスクリプトです。 Chisel を使用して、キャプチャー・ファイルのデータを分析できます。 

Chisel の使用方法について詳しくは、[Chisels User Guide ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window} を参照してください。



## Csysdig
{: #captures_csysdig}

Csysdig は、モニターおよびデバッグ用に設計された Linux 向けのオープン・ソース・ツールです。 Csysdig を使用して、キャプチャー・ファイルを分析できます。 

詳しくは、以下のリソースを参照してください。
* [Csysdig ブログ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Csysdig ビデオ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


