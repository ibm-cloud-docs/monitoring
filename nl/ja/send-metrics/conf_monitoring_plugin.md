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

# Monitoring プラグインを使用したデータの送信 (collectd)
{: #conf_monitoring_plugin}

collectd を構成して、環境内でメトリックを収集することができます。 {{site.data.keyword.monitoringshort}} プラグインを使用して、
これらのメトリックをご使用の環境からスペース・ドメインに送信することができます。 
{: shortdesc}

以下の図は、{{site.data.keyword.monitoringshort}} プラグインを使用して {{site.data.keyword.monitoringshort}}
サービスにメトリックを送信する方法の概要図を示しています。

![{{site.data.keyword.monitoringshort}} プラグインの使用方法を示す概要図](images/monitoring_plugin_ov.png "{{site.data.keyword.monitoringshort}} プラグインの使用方法を示す概要図")



## Monitoring プラグインのインストール
{: #install}

端末から、以下の手順を実行します。 

1. (前提条件) {{site.data.keyword.Bluemix_notm}} CLI をインストールします。

   詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa)を参照してください。
   
   CLI がインストールされたら、次の手順に進んでください。
	
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/cloud-monitoring/qa/cli_qa.html#login)を参照してください。

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
	ibmcloud target -o MyOrg -s MySpace
    ```
    {: codeblock}

    指示に従います。 {{site.data.keyword.Bluemix_notm}} の資格情報を入力し、組織とスペースを選択します。

### 手順 1: collectd のインストール
{: #collectd}

管理者として以下の手順を実行し、collectd をインストールします。

1.	root ユーザーとしてログインします。 

    ```
    sudo -s
    ```
    {: codeblock}

2.	ログの時刻を同期するために、Network Time Protocol (NTP) パッケージをインストールします。 

    例えば、Ubunutu システムの場合、`timedatectl status` に *Network time on: yes* と表示されるかどうか確認します。 表示される場合、ご使用の Ubuntu システムは ntp を使用するように既に構成済みのため、このステップはスキップできます。
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    以下のステップを実行して、Ubuntu システムに ntp をインストールします。

    1.	以下のコマンドを実行して、パッケージを更新します。 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	以下のコマンドを実行して、ntp パッケージをインストールします。 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	以下のコマンドを実行して、ntpdate パッケージをインストールします。 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	以下のコマンドを実行して、サービスを停止します。 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	以下のコマンドを実行して、システム・クロックを同期化します。 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        以下の例のように、時刻が調整されていることが結果で確認できます。
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	以下のコマンドを実行して、ntpd を再度開始します。 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        サービスが開始されていることが結果で確認できます。

3. collectd をインストールします。 以下のコマンドを実行します。

    ```
	apt-get install collectd 
	```
	{: codeblock}


### 手順 2: Monitoring プラグインのインストール
{: #plugin}

{{site.data.keyword.monitoringshort}} プラグインをインストールするには、以下の手順を実行します。

1. 	root ユーザーとしてログインします。 

    ```
    sudo -s
    ```
    {: codeblock}
	
2. {{site.data.keyword.monitoringshort}} サービス・リポジトリーを追加します。 以下のコマンドを実行します。

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
   {: codeblock}
   
3. プラグインをインストールします。 以下のコマンドを実行します。

    ```
	apt-get install ibmcloud-monitoring
	```
	{: codeblock}


## Monitoring プラグインの構成
{: #configure}

{{site.data.keyword.monitoringshort}} プラグインを構成するには、以下の手順を実行します。
	
### 手順 1: IAM ポリシーのユーザーへの割り当て
{: #iam_policy}

メトリックをいずれかのドメインに送信するには、ご使用のユーザー ID に Monitoring サービスにメトリックを送信する権限を持つ IAM 役割が付与されている必要があります。
 
* IBM Cloud でそのユーザーに IAM ポリシーを割り当てることにより、権限が設定されます。 
* 次の IAM 役割により、ユーザーはメトリックを送信することができます。 *管理者*、*編集者*、*オペレーター*。 

IAM ポリシーをユーザーに割り当てるには、以下のいずれかの方法を選択します。

* {{site.data.keyword.Bluemix_notm}} UI を使用する: 詳しくは、[{{site.data.keyword.Bluemix_notm}} UI を使用した IAM ポリシーのユーザーへの割り当て](/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_ui)を参照してください。
* コマンド・ラインを使用する: 詳しくは、[コマンド・ラインを使用した IAM ポリシーのユーザーへの割り当て](/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline)を参照してください。
 
### 手順 2: API キーの取得
{: #api_key}
 
スペースにメトリックを送信するには、{{site.data.keyword.monitoringshort}} サービスを使用して認証する API キーを取得する必要があります。

API キーの取得方法について詳しくは、[API キーの取得](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)を参照してください。
	
{{site.data.keyword.Bluemix_notm}} にログインした同じ端末から、トークンに APIKEY 変数を設定します。

以下に例を示します。

```
export APIKEY="kjshdgf.....ldkdjdj"
```
{: screen}
	
### 手順 3: エンドポイントに関する情報の取得
{: #endpoint}

{{site.data.keyword.monitoringshort}}  エンドポイントを決定するには、地域ごとのエンドポイントのリストおよび[エンドポイント](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)を参照し、メトリックを送信する地域のエンドポイントを識別します。

{{site.data.keyword.Bluemix_notm}} にログインした同じ端末から、**METRIC_ENDPOINT** 変数を設定します。 以下に例を示します。

```
export METRIC_ENDPOINT="metrics.ng.bluemix.net"
```
{: screen}



### 手順 4: スペース・ドメイン ID に関する情報の取得 
{: #domain}

スペースのドメイン ID を取得するには、[スペース GUID を取得](/docs/services/cloud-monitoring/qa/cli_qa.html#space_guid)します。 次に、「`s-SpaceID`」としてドメイン ID を設定します。ここで「SpaceID」は、スペースの GUID です。

{{site.data.keyword.Bluemix_notm}} にログインした同じ端末から、SpaceID 変数を設定します。

```
export SpaceID="kjshdgf.....ldkdjdj"
```
{: screen}



### 手順 5: 構成スクリプトの実行
{: #script}

以下のスクリプトを実行して、スペースにメトリックが送信されるように {{site.data.keyword.monitoringshort}} プラグインを構成します。

```
/opt/ibmcloud_monitoring/configure -e $METRIC_ENDPOINT -a $APIKEY -s s-$SpaceID
```
{: codeblock}


スクリプトは、**Include** スタンザをメインの collectd.conf ファイルに自動的に追加します。

```
<LoadPlugin IBMCloudMonitoring>
   FlushInterval 60
</LoadPlugin>
<Plugin IBMCloudMonitoring>
  <Endpoint "ng">
     Host "metrics.ng.bluemix.net"
     Port 9095
     ApiKey "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
     SkipInternalPrefixForStatsd false
     RateCounter false
     ScopeId "s-cedc73c5-6d55-4193-a9de-378620d6fab5"
  </Endpoint>
</Plugin>
```
{: screen}


### 手順 6: collectd デーモンの再始動
{: #restart}

以下のステップを実行します。

1. 	root ユーザーとしてログインします。 

    ```
    sudo -s
    ```
    {: codeblock}
	
2.  collectd を再始動します。

   collectd デーモンがサービスとして追加された場合は、以下のコマンドを実行します。
	
	```
	service collectd restart
	```
	{: codeblock}

collectd で使用可能なメトリックが、Grafana での分析に使用可能なメトリックです。


