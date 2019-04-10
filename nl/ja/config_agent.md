---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

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

# Sysdig エージェントの構成
{: #config_agent}

{{site.data.keyword.cloud_notm}} の {{site.data.keyword.mon_full_notm}} サービスのインスタンスをプロビジョンした後に、モニターする各環境の Sysdig エージェントを構成する必要があります。 Sysdig エージェントは、事前定義メトリックを自動的に収集して報告します。 各環境でモニターするメトリックを構成できます。
{:shortdesc}

1 つ以上のタグを各 Sysdig エージェントに関連付けることができます。 タグは、**TAG_NAME:TAG_VALUE** としてフォーマットされるコンマ区切りの値です。 ご使用の環境をモニターするときには、これらのタグを使用して、エージェントから取得可能なメトリックを識別できます。 例えば、そのエージェントによって収集されるすべてのメトリックとともにサービスの名前と場所に関する情報を含めることができます。
{: tip}

## Linux での Sysdig エージェントの構成
{: #config_agent_linux}

メトリックを収集して {{site.data.keyword.mon_full_notm}} サービスのインスタンスに転送するようにするために、以下の手順を実行して Linux 上で Sysdig エージェントを構成してください。

1. Sysdig アクセス・キーを取得します。 詳しくは、[{{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)を参照してください。

2. 取り込み URL を取得します。 詳しくは、[Sysdig Collector エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)を参照してください。

3. Sysdig エージェントをデプロイします。 端末から以下のコマンドを実行します。

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    説明

    * SYSDIG_ACCESS_KEY はインスタンスの取り込みキーです。

    * COLLECTOR_ENDPOINT は、モニタリング・インスタンスが使用可能な地域の取り込み URL です。

    * TAG_DATA は、*TAG_NAME:TAG_VALUE* 形式のコンマ区切りタグです。 1 つ以上のタグを Sysdig エージェントに関連付けることができます。 例えば、*role:serviceX,location:us-south* などです。 

    * **sysdig_capture_enabled** を *false* に設定して、Sysdig キャプチャー機能を無効にします。 デフォルトでは、*true* に設定されています。 詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)を参照してください。

    * 通信に SSL を使用するには、**secure** を *true* に設定します。

Sysdig エージェントを正しくインストールできない場合には、kernel headers を手動でインストールします。 ディストリビューションを選択し、そのディストリビューションのコマンドを実行してください。 次に、Sysdig エージェントのデプロイメントを再試行します。

* **Debian および Ubuntu Linux ディストリビューションの場合**、以下のコマンドを実行します。

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **RHEL、CentOS、および Fedora Linux ディストリビューションの場合**、以下のコマンドを実行します。

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Docker コンテナーでの Sysdig エージェントの構成
{: #config_agent_docker}

メトリックを収集して {{site.data.keyword.mon_full_notm}} サービスのインスタンスに転送するようにするために、以下の手順を実行して Docker コンテナー上で Sysdig エージェントを構成してください。

1. Sysdig アクセス・キーを取得します。 詳しくは、[{{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)を参照してください。

2. 取り込み URL を取得します。 詳しくは、[Sysdig Collector エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)を参照してください。

3. Sysdig エージェントをデプロイします。 次のコマンドを実行します。

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    各部分の説明:

    * SYSDIG_ACCESS_KEY はインスタンスの取り込みキーです。

    * COLLECTOR_ENDPOINT は、モニタリング・インスタンスが使用可能な地域の取り込み URL です。

    * TAG_DATA は、*TAG_NAME:TAG_VALUE* 形式のコンマ区切りタグです。 1 つ以上のタグを Sysdig エージェントに関連付けることができます。 例えば、*role:serviceX,location:us-south* などです。 

    * **sysdig_capture_enabled** を *false* に設定して、Sysdig キャプチャー機能を無効にします。 デフォルトでは、*true* に設定されています。 詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig/captures.html#captures)を参照してください。

    * 通信に SSL を使用するには、**SECURE** を *true* に設定します。

    **注:** コンテナーは、切り離しモードで実行されます。 コンテナーの出力を確認するには、*-d* を削除してください。




## スクリプトを使用した Kubernetes クラスターでの Sysdig エージェントの構成
{: #config_agent_kube_script}

{{site.data.keyword.containerlong_notm}} で実行される Kubernetes クラスター上で Sysdig エージェントを構成するには、以下のステップを実行します。

1. Sysdig アクセス・キーを取得します。 詳しくは、[{{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)を参照してください。

2. 取り込み URL を取得します。 詳しくは、[Sysdig Collector エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)を参照してください。

3. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

4. Sysdig エージェントをデプロイします。 次のコマンドを実行します。

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    各部分の説明:

    * SYSDIG_ACCESS_KEY はインスタンスの取り込みキーです。

    * COLLECTOR_ENDPOINT は、モニタリング・インスタンスが使用可能な地域の取り込み URL です。

    * TAG_DATA は、*TAG_NAME:TAG_VALUE* 形式のコンマ区切りタグです。 1 つ以上のタグを Sysdig エージェントに関連付けることができます。 例えば、*role:serviceX,location:us-south* などです。 

    * **sysdig_capture_enabled** を *false* に設定して、Sysdig キャプチャー機能を無効にします。 デフォルトでは、*true* に設定されています。 詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig/captures.html#captures)を参照してください。



## Kubernetes クラスターでの Sysdig エージェントの手動での構成
{: #config_agent_kube_manually}

{{site.data.keyword.containerlong_notm}} で実行される Kubernetes クラスター上で Sysdig エージェントを構成するには、以下のステップを実行します。

1. Sysdig アクセス・キーを取得します。 詳しくは、[{{site.data.keyword.cloud_notm}} UI を使用したアクセス・キーの取得](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)を参照してください。

2. 取り込み URL を取得します。 詳しくは、[Sysdig Collector エンドポイント](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)を参照してください。

3. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

4. kubernetes クラスターをモニターするサービス・アカウント **sysdig-agent** を作成します。 次のコマンドを実行します。

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Kubernetes クラスターに秘密を追加します。 次のコマンドを実行します。

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY はインスタンスの取り込みキーです。

    Kubernetes Secret には、{{site.data.keyword.mon_full_notm}}サービスで Sysdig エージェントを認証するために使用される取り込みキーが含まれています。 このキーを使用して、モニタリング・バックエンド・システムの取り込みサーバーへのセキュアな Web ソケットを開きます。

6. クラスター役割およびクラスター役割バインディングを作成します。 

    [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml) をダウンロードします。
    
    クラスター役割を追加するには、次のコマンドを実行します。
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    クラスター役割バインディングを追加するには、次のコマンドを実行します。

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. **sysdig-agent-configmap.yaml** を編集し、{{site.data.keyword.cloud_notm}} で機能するようにエージェントを構成するのに必要なパラメーターを追加します。

    [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml) をダウンロードします。

    エディターを使用して、sysdig-agent-configmap.yaml ファイルを開きます。 次に、以下のパラメーターを追加します。

    * **k8s_cluster_name**: このパラメーターは、メトリック・ラベルとしてクラスター名を指定します。 ラベル *kubernetes.cluster.name* を使用して、クラスター名ごとに Kubernetes ダッシュボードをナビゲートし、そのクラスターに関連付けられているメトリックをフィルターで除外できます。

    * **collector**: このパラメーターは、モニタリング・インスタンスが使用可能な地域の取り込み URL を指定します。 

    * **collector_port**: このパラメーターは、コレクターが listen するポートを示します。 この値は、*6443* である必要があります。
    
    * **ssl**: このパラメーターは *true* に設定する必要があります。
    
    * **ssl_verfiy_certificate**: このパラメーターは *true* に設定する必要があります。
    
    * **new_k8s**: kube 状態メトリックを収集するため、このパラメーターは *true* に設定する必要があります。

    * **sysdig_capture_enabled**: このパラメーターを使用すると、Sysdig キャプチャー機能を無効にすることができます。 デフォルトでは、*true* に設定されています。 詳しくは、[キャプチャーの処理](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)を参照してください。

    以下に yaml ファイルの例を示します。

    ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: ingest.us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

8. クラスターに構成マップを適用します。 次のコマンドを実行します。

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. デーモンセットを適用して、Sysdig エージェントをクラスターにデプロイします。 次のコマンドを実行します。

    [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml) をダウンロードします。

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




