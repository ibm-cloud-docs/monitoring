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



# FAQ para monitoramento de clusters do Kubernetes
{: #qa_containers}

Aqui estão as respostas para perguntas comuns sobre o serviço
do {{site.data.keyword.monitoringshort}} e o serviço do {{site.data.keyword.containershort_notm}}. 
{:shortdesc}

* [A consulta do Grafana para meus contêineres não está mostrando dados ou está com erro](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#metric_format_change)
* [Como configurar um ambiente em cluster na minha sessão de terminal?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1)
* [Onde posso obter o nome do
cluster e o ID do cluster?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa3)
* [Como obter a lista de
namespaces?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa7)
* [Como obter a lista de pods em
um namespace em um cluster do Kubernetes?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa8)
* [Como obter todos os pods em um
cluster por namespace?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa9)

## A consulta do Grafana para meus contêineres não está mostrando dados ou está com erro
{: #metric_format_change}

O formato da consulta que pode ser definido para um contêiner mudou.

O formato a seguir foi descontinuado: 

```
{Prefix}.{Version}.{Provider}.{Type}.{ServiceName}.{Region}.{Account}.{Cluster}.{Metric}.{Container in a pod}.{Functions}
```
{: screen}

Os novos formatos que são válidos são os seguintes:

* [Formato de consulta de métrica de CPU para um contêiner](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers)
* [Formato de consulta de métrica de carga para um trabalhador](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#load_workers)
* [Formato de consulta de métrica de memória para um contêiner](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#mem_containers)

Migre suas consultas antigas para o novo formato para visualizar seus dados no Grafana.

Por exemplo, se sua consulta inicia como
`crn.v1.bluemix.public.containers-kubernetes.us-south.`, deve-se migrar sua consulta para o
novo formato, ou seja, para `ibmcloud.public.containers-kubernetes.us-south`.

A tabela a seguir lista os campos no formato que foi descontinuado:

 <table>
      <caption>Tabela 1. Campos de consulta do Grafana para contêineres</caption>
      <tr>
        <th align="center">Campo</th>
        <th align="center">Descrição</th>
        <th align="center">Valores válidos</th>
      </tr>
      <tr>
        <td>Prefixo</td>
        <td>O prefixo que é usado para indicar que é um recurso do {{site.data.keyword.IBM_notm}} Cloud.</td>
        <td>`crn`</td>
      </tr>
      <tr>
        <td>Versão</td>
        <td>A versão que indica o formato e os campos dos dados de métrica coletados. </td>
        <td>`v1`</td>
      </tr>
      <tr>
        <td>Provedor</td>
        <td>Provedor em nuvem no qual os dados são coletados. Este campo é um identificador alfanumérico.</td>
        <td>Para o {{site.data.keyword.IBM_notm}} Cloud público, o valor é: `bluemix`</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>Ambiente de nuvem no qual os dados são coletados.</td>
        <td>Para o {{site.data.keyword.IBM_notm}} Cloud público, o valor é: `public`</td>
      </tr>
      <tr>
        <td>Nome do serviço</td>
        <td>Infraestrutura do Cloud onde métricas são coletadas.</td>
        <td>Para o serviço {{site.data.keyword.monitoringshort}}, o valor é: `containers-kubernetes`</td>
      </tr>
      <tr>
        <td>Região</td>
        <td>Região Cloud onde métricas são coletadas.</td>
        <td>Para a região Sul dos EUA, o valor é: `ng` <br>Para a região do Reino Unido, o valor é: `eu-gb` <br>Para Alemanha, o valor é: `eu-de` <br>Para Sydney, o valor é: `au-syd` </td>
      </tr>
      <tr>
        <td>Conta</td>
        <td>GUID da conta em que as métricas são coletadas. <br>O formato deste campo é o seguinte: `a_ID` em que ID é o GUID da conta. <br>Para obter o GUID da conta, consulte [Como obter o GUID de uma conta](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#account_guid).</td>
        <td>a_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Grupo</td>
        <td>GUID do cluster em que métricas são coletadas.</td>
        <td>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>de Métrica</td>
        <td>A métrica que é coletada automaticamente para um contêiner.</td>
        <td>Para obter uma lista de métricas da CPU, consulte
[Métricas da CPU para contêineres](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers) <br>Para obter uma lista de métricas da memória, consulte
[Métricas da memória](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#memory_metrics) </td>
      </tr>
      <tr>
        <td>Contêiner em uma vagem</td>
        <td>A combinação de nomes e GUIDs de recursos do Kubernetes que são necessários para identificar exclusivamente um contêiner que é executado em um pod. <br>**Nota:** ao observar a lista de opções disponíveis para essa entrada na
consulta, observe que há também uma entrada com o formato a seguir: {namespace}{pod_name}{deploymentname_name}_POD{container_ID}. Essas entradas correspondem aos IDs de contêineres internos que são criados pelo Kubernetes.</td>
		<td>{namespace}_{pod_name}_{deployment_name}_{container_id}</td>
      </tr>
      <tr>
        <td>Functions</td>
        <td>Funções de consulta que podem ser selecionadas para visualizar uma métrica de contêiner no painel. <br>Para obter mais informações, consulte [Functions ![(Ícone de link externo)](../../icons/launch-glyph.svg "Ícone de link externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
        <td></td>
      </tr>
    </table>


## Como configurar um ambiente em cluster na minha sessão de terminal?
{: #qa1}

Deve-se configurar o contexto de um cluster do Kubernetes para gerenciá-lo usando comandos.

**Nota:** para gerenciar um cluster, é necessária uma política do IAM para o
serviço do {{site.data.keyword.containershort_notm}} designado para o seu usuário com permissões
para concluir a tarefa.

Conclua as etapas a seguir para configurar o contexto de um cluster:

1. Efetue login na região, na organização e no espaço no {{site.data.keyword.Bluemix_notm}} que está associado ao cluster criado. Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Inicialize o plug-in do serviço {{site.data.keyword.containershort_notm}}. Execute o seguinte comando:

	```
	ibmcloud cs init
	```
	{: codeblock}

3. Configure o contexto do cluster na sessão de terminal. Execute os seguintes comandos:
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    A saída de execução desse comando fornece o comando que deve ser executado no terminal para configurar o caminho para o arquivo de configuração. Por exemplo:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Copie e cole o comando para configurar a variável de ambiente em seu terminal e, em seguida, pressione **Enter**.

 
 

## Onde posso obter o nome e o ID do cluster?
{: #qa3}

Conclua as etapas a seguir para obter o nome e o ID do cluster por meio da IU:

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}.

    O painel do {{site.data.keyword.Bluemix_notm}} pode ser localizado em: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}.
    
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. A partir do  {{site.data.keyword.Bluemix_notm}}  * Painel *, selecione  ** Menu > Contêineres **.

    The list of clusters that are available in the account are displayed.

3. Para obter o ID do cluster, selecione uma entrada de cluster. 

    The overview page opens. In this page, you can get the cluster ID.



Complete the following steps to get the cluster name and ID thorugh the command line:

1. Efetue login na região, na organização e no espaço no {{site.data.keyword.Bluemix_notm}} que está associado ao cluster criado. Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Liste os clusters que estão disponíveis na conta. Execute o seguinte comando: 

    ```
	clusters de cs ibmcloud
	``` 
	{: codeblock}
	
	The output of this command lists all the clusters in the account with their corresponding IDs.
	
3. Para obter o ID do cluster, execute o comando a seguir:

    ```
	ibmcloud cs cluster-get my_cluster
	```
    {: screen}	
 


## Como obter a lista de namespaces?
{: #qa7}

Para obter uma lista de todos os namespaces no cluster, conclua as etapas a seguir:

Conclua as etapas a seguir:

1. Configure o contexto do cluster. Para obter mais informações, veja [Como eu configuro um ambiente em cluster em minha sessão de terminal?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1).

2. Liste todos os namespaces. Run the following kubectl command:

    ```
    kubectl get namespaces
	```
	{: codeblock}

## Como obter a lista de pods por namespace em um cluster do Kubernetes?
{: #qa8}
		
To get the list of pods in a namespace, complete the following steps:

1. Configure o contexto do cluster. Para obter mais informações, veja [Como eu configuro um ambiente em cluster em minha sessão de terminal?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1).

2. Para obter a lista de pods por namespace em um cluster do Kubernetes, execute o comando a seguir:

    ```
	kubectl --namespace=NamespaceName get pods 
	```
	{: codeblock}
	
	em que Namespacename é o nome do namespace, por exemplo, *default*.

## Como obter todos os pods em um cluster por namespace?
{: #qa9}
		
Conclua as etapas a seguir:

1. Configure o contexto do cluster. Para obter mais informações, veja [Como eu configuro um ambiente em cluster em minha sessão de terminal?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1).
	
2. Para obter todos os pods em um cluster por namespace, execute o comando a seguir:

	```
	kubectl get pods --all-namespaces
	```
	{: codeblock}
		


