---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, delete agent

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

# Sysdig エージェントの削除
{: #remove_agent}

{{site.data.keyword.mon_full_notm}} インスタンスを削除する場合、またはソースからメトリックの収集を停止する場合、Sysdig エージェントをアンインストールする必要があります。
{:shortdesc}


## Kubernetes クラスターからの Sysdig エージェントの削除
{: #remove_agent_kube}

Kubernetes クラスターから Sysdig エージェントを削除するには、以下のステップを実行します。

1. クラスター環境をセットアップします。 次のコマンドを実行します。

    最初に、環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    構成ファイルのダウンロードが完了すると、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

    次に、KUBECONFIG 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。

    **注:** クラスターの作業を行うために {{site.data.keyword.containerlong}} CLI にログインするたびに、これらのコマンドを実行して、クラスターの構成ファイルのパスをセッション変数として設定する必要があります。 Kubernetes CLI はこの変数を使用して、{{site.data.keyword.cloud_notm}} 内のクラスターと接続するために必要なローカル構成ファイルと証明書を検索します。

2. クラスター役割バインディングを削除します。 次のコマンドを実行します。

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. サービス・アカウントを削除します。 次のコマンドを実行します。

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. daemonset を削除します。 次のコマンドを実行します。

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. 機密事項を削除します。 次のコマンドを実行します。

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Linux での Sysdig エージェントの削除
{: #remove_agent_linux}

Linux で Sysdig エージェントを削除するには、以下のステップを実行します。

* **Debian および Ubuntu Linux ディストリビューション**からエージェントをアンインストールするには、端末から **sudo** ユーザーとして以下のコマンドを実行します。

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* **RHEL、CentOS、および Fedora Linux ディストリビューション**からエージェントをアンインストールするには、端末から **sudo** ユーザーとして以下のコマンドを実行します。

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


