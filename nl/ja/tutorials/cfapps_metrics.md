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


# CF アプリに関する Grafana でのメトリックの分析
{: #cfapps_metrics}

このチュートリアルでは、{{site.data.keyword.monitoringlong}} サービスを使用して、{{site.data.keyword.Bluemix_notm}} Public で実行される Cloud Foundry (CF) アプリのパフォーマンスをモニターする方法を説明します。 
{:shortdesc}


## 達成目標
{: #objectives}

CF アプリのメトリックを以下のように検索および分析する方法を学習します。

1. CF アプリをデプロイします。
2. Grafana を起動し、CF アプリのメトリックを表示できる {{site.data.keyword.monitoringshort}} ドメインを設定します。
3. {{site.data.keyword.Bluemix_notm}} のスペースで実行される CF アプリのメトリックを検索および分析します。

このチュートリアルでは、米国南部地域で作業していることを想定しています。


## 前提条件
{: #cfapps_prereqs}

1. スペース内のサービスのプロビジョン、CF アプリのデプロイ、{{site.data.keyword.monitoringshort}} サービスによる {{site.data.keyword.Bluemix_notm}} 内のメトリック照会を実行できる権限を持つ {{site.data.keyword.Bluemix_notm}} アカウントのメンバーまたは所有者になります。

    {{site.data.keyword.Bluemix_notm}} のユーザー ID には、{{site.data.keyword.monitoringshort}} サービスと CF アプリがプロビジョンされているスペースに対する CF 役割が必要です。 必要な役割は  *開発者* です。
    
    詳しくは、[IBM Cloud UI の使用によるユーザーへの CF 役割の付与 (Granting a user a CF role by using the IBM Cloud UI)](/docs/services/cloud-monitoring/security/assign_policy.html#grant_permissions_ui_space) を参照してください。

2. 米国南部地域内で、サービスをプロビジョンする権限があるスペースで、{{site.data.keyword.monitoringshort}} サービスをプロビジョンします。

    詳しくは、[{{site.data.keyword.monitoringshort}} サービスのプロビジョニング](/docs/services/cloud-monitoring/how-to/provision.html#provision)を参照してください。

## 手順 1: CF アプリおよび {{site.data.keyword.monitoringshort}} サービスの作業を行うための権限をユーザーに付与
{: #cfapps_step1}

スペースに CF アプリをデプロイする権限またはスペース・ドメイン内のメトリックを表示する権限をユーザーに付与するには、スペース内および {{site.data.keyword.Bluemix_notm}} 内でユーザーが {{site.data.keyword.monitoringshort}} サービスを使用して実行できるアクションを記述した CF 役割を、当該ユーザーに割り当てる必要があります。 

**注:** このチュートリアルは、作業者がアカウント所有者であるか、ユーザー ID に役割を追加する権限があることを想定しています。 権限がない場合は、このステップを実行するよう所有者に依頼してください。

チュートリアルを完了するための権限をユーザーに付与するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動
します。[http://bluemix.net ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://bluemix.net){:new_window}
	
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    *「ユーザー」*ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. リストからユーザー名を探し、*「アクション」*メニューから**「ユーザーの管理」**をクリックします。

4. **「Cloud Foundry アクセス権限」**を選択し、次に**「組織の割り当て」** を選択します。

5. 以下の値を入力します。 

    <table>
      <caption>選択する値のリスト</caption>
      <tr>
        <th>フィールド</th>
        <th>値</th>
      </tr>
      <tr>
        <td>組織</td>
        <td>MyOrg</td>
      </tr>
      <tr>
        <td>組織の役割</td>
        <td>組織の役割なし</td>
      </tr>
      <tr>
        <td>地域</td>
        <td>米国南部</td>
      </tr>
      <tr>
        <td>スペース</td>
        <td>dev</td>
      </tr>
      <tr>
        <td>スペースの役割</td>
        <td>開発者</td>
      </tr>
    </table>
	
6. **「役割の保存」**をクリックします。
 

## 手順 2: CF アプリのデプロイ
{: #cfapps_step2}

{{site.data.keyword.Bluemix_notm}} コンソールから以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} ツールバーで**「カタログ」**をクリックします。

2. **「Cloud Foundry アプリ」>「Liberty for Java」**をクリックします。 

3. 以下の情報を入力します。

    * **アプリ名**: アプリケーションの名前。 固有でなければなりません。
    * **地域**: 「米国南部」を選択します。
    * **組織**: {{site.data.keyword.monitoringshort}} サービスをプロビジョンした組織を選択します。
    * **スペース**: {{site.data.keyword.monitoringshort}} サービスをプロビジョンしたスペースを選択します。

3. **「作成」**をクリックします。

CF アプリが実行中になるとすぐに、メトリックが収集され、{{site.data.keyword.monitoringshort}} サービスに転送されます。

## 手順 3: Grafana の起動とメトリック・ドメインの設定
{: #cfapps_step3}

ブラウザーから Grafana を起動し、CF アプリのメトリックを表示できる {{site.data.keyword.monitoringshort}} ドメインを設定します。

1. ブラウザーから Grafana を起動します。 

    {{site.data.keyword.monitoringshort}} サービスがプロビジョンされている地域の {{site.data.keyword.monitoringshort}} サービス URL を入力します。
    
    地域ごとの URL を取得するには、[Monitoring サービスの URL](/docs/services/cloud-monitoring/monitoring_ov.html#region) を参照してください。

    例えば、米国南部地域の場合は、[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)を起動します。

2. クラスター・メトリックを表示できる {{site.data.keyword.monitoringshort}} ドメインを設定します。

    Grafana で、ID を選択します。 次に、正しいアカウントにログインしていることを確認して、`Domain = space` を選択します。

    組織名とスペース名が、CF アプリをデプロイし、{{site.data.keyword.monitoringshort}} サービスをプロビジョンした組織名とスペース名に一致することを確認します。


## 手順 4: メトリックをモニターするための Grafana ダッシュボードの作成
{: #cfapps_step4}


Grafana で新規ダッシュボードを作成するには、以下の手順を実行します。

1. サイド・メニュー・バーのトグル を選択します。![Grafana サイド・メニュー・バー](images/grafana_settings.gif "Grafana サイド・メニュー・バー")
2. **「Dashboards」**を選択します。
3. **「New」**をクリックします

ダッシュボードが開きます。 ダッシュボードには、すぐに構成できる空の行が含まれています。

![Grafana ダッシュボード](images/grafana4_f1.gif "Grafana ダッシュボード")

Grafana で、ダッシュボードを複数のセクションに分割するための行を追加します。 行は、1 つ以上のパネルをグループ化します。 1 行の中では、パネルが最小の視覚化単位であり、メトリックのデータを表示するために構成 (例えば、グラフ・パネルや表パネルを選択できる) できます。 パネルをドラッグ・アンド・ドロップして、ダッシュボード内でパネルを再配置することができます。 パネルが表示するデータは、照会を介して構成されます。 1 つのパネルに 1 つ以上の照会を定義できます。 各照会は、異なるデータ・セットを表しています。 その他に、パネルの時刻範囲を設定することもできます。 通常、この時刻範囲は、*ダッシュボード*のタイム・ピッカーによって設定されます。

グラフに表示されるデータをフィルターに掛ける照会を定義します。 この照会は、コンテナーの限度に対する CPU 使用率のパーセンテージをモニターします。

照会のフォーマットについては、[CF アプリに関する Grafana の照会フォーマット](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format)を参照してください。
    
1. コンテナーの全コアにわたって CPU 時間のナノ秒をモニターするために、*「Graph」*パネルを追加します。
    
    1. **「Graph」**をクリックします。
    
    2. グラフのタイトルをクリックし、次に**「edit」**を選択します。
    
        *「Metrics」*タブが開きます。 デフォルト・データ・ソースが表示されています。
    
        ![構成タブを含む「Graph」パネル](images/grafana4_f2.gif "構成タブを含む「Graph」パネル")
    
2. グラフに表示されるデータをフィルターに掛ける照会を定義します。 
    
    *「Metrics」*タブで、**「Add query」**を選択します。 <br>照会項目が追加されます。 各照会には、1 文字のラベルが付いています。
    
    ![新規照会項目](images/grafana4_query_f1.gif "新規照会項目")
        
    1. **「Select metric」**をクリックし、ソースに `ibmcloud` を選択します。
    
    2. **「Select metric」**をクリックし、クラウド・タイプに `public` を選択します。
    
    3. **「Select metric」**をクリックし、`cloud-foundry` を選択します。
    
    4. **「Select metric」**をクリックし、作業している地域 (例えば、米国南部地域の場合には `us-south`) を選択します。
    
    5. **「Select metric」**をクリックし、CF アプリ名 (例: `logtester`) を選択します。
    
    6. **「Select metric」**をクリックし、CF アプリ・インスタンス索引 (例: `0`) を選択します。

    7. **「Select metric」**をクリックし、`container` を選択します。
    
    9. **「Select metric」**をクリックし、メトリックを選択します。 コンテナーの *CPU 使用率* をモニターするには、`cpu-utilization` を選択します。

    10. 正符号イメージ ![追加アイコン](images/grafana_plus_image.gif "正符号イメージ") をクリックし、関数を選択します。 関数を追加すると、メトリックに使用可能なデータを変換したり、結合したり、それらのデータに対して計算を実行したりすることができます。
        
        例えば、**alias(newName)** 関数を追加して、メトリックの別名を追加することができます。 この別名は、グラフに表示される凡例にメトリック名の代わりにストリングを表示するために使用されます。
        
        メトリックの別名を追加するには、以下の手順を実行します。
        
        1. 正符号をクリックします。
        2. **「Special」**を選択します。 
        3. **「alias」**を選択します。
        4. ストリング (例えば、`My sample metric`) を入力します。
        

## 手順 5: ダッシュボードの保存
{: #cfapps_step5}

後で再利用するためにダッシュボードを保存します。

1. ダッシュボードの保存イメージ ![ダッシュボードの保存イメージ](images/grafana_save_image.gif "ダッシュボードの保存イメージ") をクリックします。.

    ![ダッシュボードの保存](images/grafana_save_dashboard.gif "ダッシュボードの保存")

2. ダッシュボードの名前を入力します。
3. **「保存」**をクリックします。


## 次の手順
{: #cfapps_next_steps}

メトリックのアラートを定義します。 詳しくは、[アラートの構成](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov)を参照してください。
