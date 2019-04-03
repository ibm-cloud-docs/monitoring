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


# Grafana でのメトリック照会の構成
{: #define_query}

{{site.data.keyword.Bluemix}} では、選択したクラウド・サービスからのメトリックが自動的に収集されます。 {{site.data.keyword.monitoringlong}} を介してそれらをモニターするには、Grafana 照会を定義する必要があります。 
{:shortdesc}

## 手順 1: モニターする CF アプリまたはサービスのデータを集める
{: #step18}

モニターする CF アプリまたはサービスの以下の情報を取得します。

* CF アプリが実行されている**地域**。
* CF アプリが実行されている**組織**。 	
* CF アプリが実行されている**スペース**。 
* モニターするアプリの **CF アプリ名**、または**サービス名**。 


## 手順 2: Grafana の起動
{: #step27}

ブラウザーから Grafana を起動します。 詳しくは、[Web ブラウザーから Grafana ダッシュボードへのナビゲート](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser)を参照してください。

Grafana で、CF アプリまたはサービスが実行されているアカウント、組織、および地域にログインしていることを確認してください。 


## 手順 3: Grafana で照会を定義する
{: #step36}

以下のステップを実行して、Grafana ダッシュボードを作成し、照会を定義します。

1. 新規ダッシュボードを作成します。

    * サイド・メニュー・バーのトグル ![Grafana サイド・メニュー・バー](images/grafana_settings.gif "Grafana サイド・メニュー・バー") を選択します。
    * **「Dashboards」**を選択します。
    * **「New」**をクリックします

    ダッシュボードが開きます。 ダッシュボードには、すぐに構成できる空の行が含まれています。

2. *「Graph」*パネルを追加します。

    1. **「Graph」**をクリックします。

    2. グラフのタイトルをクリックし、次に**「edit」**を選択します。

        *「Metrics」*タブが開きます。 デフォルト・データ・ソースが表示されています。

3. グラフに表示されるデータをフィルターに掛ける照会を定義します。 

    *「Metrics」*タブで、**「Add query」**を選択します。 <br>照会項目が追加されます。 各照会には、1 文字のラベルが付いています。
    
    ![新規照会項目](images/grafana4_query_f1.gif "新規照会項目")
        
    1. **「Select metric」**をクリックし、ソースに `ibmcloud` を選択します。
    
    2. **「Select metric」**をクリックし、クラウド・タイプに `public` を選択します。
    
    3. **「Select metric」**をクリックし、サービス名を選択します。例えば、CF アプリのメトリックの場合は `cloud-foundry`、{{site.data.keyword.messagehub}} メトリックの場合は `message hub` とします。
    
    4. **「Select metric」**をクリックし、作業中の地域を選択します。例えば、米国南部地域の場合は `ng` です。
    
    5. モニターするサービスまたは CF アプリに適用される特定のサービス・フィールドを選択します。

        <table>
          <caption>サービスまたは CF アプリ別のメトリック照会フォーマット</caption>
          <tr>
            <th>Service name</th>
            <th>メトリック照会フォーマットへのリンク</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[コンテナーに関して収集される CPU メトリックの照会フォーマット](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers) </br>[ワーカーに関して収集されるロード・メトリックの照会フォーマット](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers) </br>[コンテナーに関して収集されるメモリー・メトリックの照会フォーマット](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)</td> 
          </tr>
          <tr>
            <td>CF アプリ</td>
            <td>[CF アプリの照会フォーマット](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format)</td> 
          </tr>
        </table>

        例えば、CF アプリの場合、以下を選択します。
    
        **「Select metric」**をクリックし、CF アプリ名 (例: `logtester`) を選択します。
    
        **「Select metric」**をクリックし、CF アプリ・インスタンス索引 (例: `0`) を選択します。

        **「Select metric」**をクリックし、`container` を選択します。
    
    9. **「Select metric」**をクリックし、メトリックのタイプを選択します。 例えば、CPU メトリックの場合は **cpu**、メモリーのメトリックの場合は **memory**、ディスクのメトリックの場合は **disk** です。 

        **注:** CF アプリの場合はこのステップをスキップしてください。 

    10. **「Select metric」**をクリックし、メトリックを選択します。 

        <table>
          <caption>サービスまたは CF アプリ別のメトリックのリスト</caption>
          <tr>
            <th>Service name</th>
            <th>メトリックへのリンク</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[CPU メトリック](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[ディスクのメトリック](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[メモリーのメトリック](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>CF アプリ</td>
            <td>[CPU メトリック](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics)  </br>[ディスクのメトリック](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[メモリーのメトリック](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Kafka トピックのメトリック](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_topic_metrics) </br>[Kafka パーティションのメトリック](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. 正符号イメージ ![追加アイコン](images/grafana_plus_image.gif "正符号イメージ") をクリックし、関数を選択します。 関数を追加すると、メトリックに使用可能なデータを変換したり、結合したり、それらのデータに対して計算を実行したりすることができます。
        
        例えば、**alias(newName)** 関数を追加して、メトリックの別名を追加することができます。 この別名は、グラフに表示される凡例にメトリック名の代わりにストリングを表示するために使用されます。
        
        メトリックの別名を追加するには、以下の手順を実行します。
        
        1. 正符号をクリックします。
        2. **「Special」**を選択します。 
        3. **「alias」**を選択します。
        4. ストリング (例えば、`My sample metric`) を入力します。


## 手順 4: 後で再使用するためにダッシュボードを保存する
{: #step44}

以下のステップを実行します。

1. ダッシュボードの保存イメージ ![ダッシュボードの保存イメージ](images/grafana_save_image.gif "ダッシュボードの保存イメージ") をクリックします。.
2. ダッシュボードの名前を入力します。
3. **「保存」**をクリックします。
