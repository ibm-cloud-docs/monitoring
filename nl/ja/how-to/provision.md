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


# Monitoring サービスのプロビジョニング
{: #provision}

{{site.data.keyword.Bluemix}} UI またはコマンド・ラインから {{site.data.keyword.monitoringshort}} サービスをプロビジョンできます。
{:shortdesc}


## UI からのプロビジョニング
{: #ui}

{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.monitoringshort}} サービスのインスタンスをプロビジョンするには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} アカウントにログインします。

    {{site.data.keyword.Bluemix_notm}} ダッシュボードは、[http://bluemix.net ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window} にあります。
    
	ユーザー ID およびパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. **「カタログ」**をクリックします。 {{site.data.keyword.Bluemix_notm}} で使用可能なサービスのリストが開きます。

3. **「DevOps」**カテゴリーを選択して、表示されるサービスのリストをフィルターに掛けます。

4. **「モニタリング」**タイルをクリックします。

5. サービス・プランを選択します。 

    * 最大 45 日間のメトリックの収集およびアクセス、およびワイルドカードを使用するルールを含むアラート・ルールの定義を行うには、**「プレミアム」**プランを選択します。 
	
	* デフォルトでは、**「ライト」**プランが設定されます。このプランでは、サービスをプロビジョンしているスペース内のプラットフォーム・メトリックを収集し、それらのメトリックを 15 日間保持することが可能です。 

    サービス・プランについて詳しくは、[サービス・プラン](/docs/services/cloud-monitoring/monitoring_ov.html#plan)を参照してください。
	
6. **「作成」**をクリックして、ログインした {{site.data.keyword.Bluemix_notm}} スペースで {{site.data.keyword.monitoringshort}} サービスをプロビジョンします。
  
 

## CLI からのプロビジョニング
{: #cli}

コマンド・ラインを通じて {{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.monitoringshort}} サービスのインスタンスをプロビジョンするには、以下の手順を実行します。

1. [前提条件] {{site.data.keyword.Bluemix_notm}} CLI をインストールします。

   詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/cli/index.html#overview)を参照してください。
   
   CLI がインストールされたら、次の手順に進んでください。
    
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。
	
3. `ibmcloud service create` コマンドを実行して、インスタンスをプロビジョンします。

    ```
	ibmcloud service create service_name service_plan service_instance_name
	```
	{: codeblock}
    
    ここで、
    	
    * *service_name* は**「モニタリング」**です。
    * *service_plan* は、サービス・プラン名です。 最大 45 日間のメトリックの収集およびアクセス、およびワイルドカードを使用するルールを含むアラート・ルールの定義を行うには、**「プレミアム」**プランを選択します。 デフォルトでは、**「ライト」**プランが設定されます。このプランでは、サービスをプロビジョンしているスペース内のプラットフォーム・メトリックを収集し、それらのメトリックを 15 日間保持することが可能です。 プランのリストについては、[{{site.data.keyword.monitoringshort}} サービス・プラン](/docs/services/cloud-monitoring/monitoring_ov.html#plan)を参照してください。
    * *service_instance_name* は、作成する新規サービス・インスタンスに使用する名前です。
    
    例えば、プレミアム・プランで {{site.data.keyword.monitoringshort}} サービスのインスタンスを作成するには、以下のコマンドを実行します。
    
	```
	ibmcloud service create Monitoring premium my_monitoring_svc
	```
	{: codeblock}
    
4. サービスが正常に作成されたことを確認します。 以下のコマンドを実行します。

    ```	
	ibmcloud service list
	```
	{: codeblock}
	
	コマンド実行の出力は、以下のようになります。
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_monitoring_svc              Monitoring               premium                                        create succeeded
	```
	{: screen}

	



