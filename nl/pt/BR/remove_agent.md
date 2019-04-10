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

# Removendo um agente Sysdig
{: #remove_agent}

Quando você exclui uma instância do {{site.data.keyword.mon_full_notm}} ou se deseja parar a coleta de métricas de uma origem, deve-se desinstalar o agente Sysdig.
{:shortdesc}


## Removendo um agente Sysdig de um cluster Kubernetes
{: #remove_agent_kube}

Conclua as etapas a seguir para remover um agente Sysdig de um cluster Kubernetes:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Remova a ligação de função de cluster. Execute o seguinte comando:

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. Remova a conta de serviço. Execute o seguinte comando:

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. Remova o daemonset. Execute o seguinte comando:

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Remova o segredo. Execute o seguinte comando:

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Removendo um agente Sysdig no Linux
{: #remove_agent_linux}

Conclua as etapas a seguir para remover um agente Sysdig no Linux:

* Para desinstalar o agente de **Distribuições do Debian e do Ubuntu Linux**, execute o comando a seguir como o usuário **sudo** por meio de um terminal:

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* Para desinstalar o agente de **Distribuições do RHEL, do CentOS e do Fedora Linux**, execute o comando a seguir como o usuário **sudo** por meio de um terminal:

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


