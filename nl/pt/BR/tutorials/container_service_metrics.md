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


# Analise as métricas no Grafana para um cluster Kubernetes
{: #container_service_metrics}

Use este tutorial para aprender como usar o serviço do {{site.data.keyword.monitoringlong}} para monitorar o desempenho de seu contêiner. 
{:shortdesc}


## Objetivos
{: #ks_objectives}

Aprenda como procurar e analisar métricas do contêiner para um app que é implementado em um cluster
do Kubernetes:

1. Identifique o local em que as métricas que são coletadas em um cluster são encaminhadas para o serviço do {{site.data.keyword.monitoringshort}}. 
2. Ative o Grafana e configure o domínio do {{site.data.keyword.monitoringshort}} em que é possível visualizar as métricas do cluster.
3. Procure e analise as métricas de contêiner para um app que é implementado em um cluster do Kubernetes no {{site.data.keyword.Bluemix_notm}}.

Este tutorial percorre as etapas necessárias para o funcionamento do cenário de ponta a ponta a seguir no {{site.data.keyword.Bluemix_notm}}: provisionar um cluster, identificar onde o cluster envia métricas para o serviço {{site.data.keyword.monitoringshort}} no {{site.data.keyword.Bluemix_notm}}, implementar um app no cluster e usar o Grafana para visualizar e filtrar métricas de contêiner para esse cluster.


**Nota:** para concluir este tutorial, deve-se concluir os pré-requisitos e os tutoriais que são vinculados nas diferentes etapas.


## Pré-requisitos
{: #ks_prereqs}

1. Seja um membro ou um proprietário de uma conta do {{site.data.keyword.Bluemix_notm}} com permissões para criar clusters padrão do Kubernetes, implementar apps em clusters e consultar as métricas no {{site.data.keyword.Bluemix_notm}} para o monitoramento no Grafana.

    Seu ID do usuário para o {{site.data.keyword.Bluemix_notm}} deve ter as políticas a seguir designadas:
    
    * Uma política do IAM para o {{site.data.keyword.containershort}} com permissões de *operador* ou *administrador*.
    
    Para obter mais informações, consulte [Designar uma política do IAM a um usuário por meio da IU do IBM Cloud](/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_ui).

2. Tenha uma sessão de terminal da qual seja possível gerenciar o cluster do Kubernetes e implementar apps por meio da linha de comandos. Os exemplos neste tutorial são fornecidos para um sistema Ubuntu Linux.

3. Instale as CLIs para trabalhar com o {{site.data.keyword.containershort}} no seu sistema Ubuntu.

    * Instale a CLI do {{site.data.keyword.Bluemix_notm}}. 
    * Instale a CLI do {{site.data.keyword.containershort}} para criar e gerenciar seus clusters do Kubernetes no {{site.data.keyword.containershort}} e para implementar apps conteinerizados em seu cluster.
    
    Para obter mais informações, veja [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).
    
    

    
 

## Etapa 1: provisionar um cluster do Kubernetes
{: #ks_step1}

Conclua as etapas a seguir:

1. Crie um cluster padrão do Kubernetes. Para obter mais informações, consulte [Criar um cluster padrão do Kubernetes](/docs/containers/cs_tutorials.html#cs_cluster_tutorial).

2. Configure o contexto do cluster em um terminal. Após o contexto ser configurado, é possível gerenciar o cluster do Kubernetes e implementar o aplicativo no cluster do Kubernetes.

    Efetue login na região, na organização e no espaço no {{site.data.keyword.Bluemix_notm}} que está associado ao cluster criado. Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

	Inicialize o plug-in do serviço {{site.data.keyword.containershort}}.

	```
	ibmcloud cs init
	```
	{: codeblock}

    Configure o seu contexto de terminal para o seu cluster.
    
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



## Etapa 2: conceder ao usuário permissões para ver métricas no domínio de contas
{: #ks_step2}

Para conceder a um usuário permissões para visualizar métricas em um domínio de contas, deve-se designar ao usuário uma política do IAM para o serviço {{site.data.keyword.monitoringshort}} com a função **Visualizador**.

Conclua as etapas a seguir para conceder permissões a um usuário para trabalhar com o serviço {{site.data.keyword.monitoringshort}}:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Se o usuário é um membro da conta, selecione o nome do usuário na lista ou clique em **Gerenciar usuário** no menu *Ações*.

    Se o usuário não é um membro da conta, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

4. Selecione **Políticas de acesso > Designar acesso > Designar acesso a recursos**.

5. Escolha o serviço **{{site.data.keyword.monitoringlong}}**, selecione a região em que o cluster está disponível, **Sul dos EUA** para esse tutorial, e selecione uma função, **visualizador**.



## Etapa 3: conceder permissões de proprietário de chave do {{site.data.keyword.containershort_notm}}
{: #ks_step3}

Para que o cluster encaminhe métricas ao domínio de contas, o proprietário de chave do {{site.data.keyword.containershort}} deve ter as políticas do IAM a seguir:

* Política do IAM com permissões de **editor** para o serviço {{site.data.keyword.monitoringshort}}.
* Política do IAM com permissões de **administrador** para o {{site.data.keyword.containershort}}.


Conclua as etapas a seguir para conceder as permissões de proprietário de chave do {{site.data.keyword.containershort}}:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Localize o ID do proprietário da chave do {{site.data.keyword.containershort}}.

    Execute o comando `ibmcloud cs api-key-info ClusterName` para obter o ID do usuário do proprietário da chave do {{site.data.keyword.containershort}}.

4. Selecione **Políticas de acesso > Designar acesso > Designar acesso a recursos**.

5. Escolha o serviço **{{site.data.keyword.monitoringlong}}**, selecione a região em o cluster está disponível, **Sul dos EUA** para esse tutorial, e selecione uma função, **editor**.	

6. Repita as etapas de 2 a 4 e escolha o serviço {{site.data.keyword.containershort}}. Selecione **Todas as regiões** e a função **administrador**.	




## Etapa 4: implementar um app de amostra no cluster do Kubernetes
{: #ks_step4}

Implemente e execute um aplicativo de amostra no cluster do Kubernetes. Conclua as etapas no tutorial a seguir para implementar o app de amostra: [Lição 1: Implementando apps de instância única em clusters do Kubernetes](/docs/containers/cs_tutorials_apps.html#cs_apps_tutorial_lesson1).

O app é um app Hello World Node.js:

```
var express = require('express')
    var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

Nesse aplicativo de amostra, quando você testa seu app em um navegador, o app grava no stdout a mensagem a seguir: `Sample app is listening on port 8080.`


## Etapa 5: ativar o Grafana e configurar o domínio de métricas
{: #ks_step5}

Ative o Grafana em um navegador e configure o domínio do {{site.data.keyword.monitoringshort}}
no qual é possível visualizar as métricas do cluster.

Para analisar métricas para um cluster, deve-se acessar o Grafana na região Pública de nuvem na qual o cluster estiver criado. Para obter mais informações, veja [Navegando para o painel do Grafana por meio de um navegador da web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

1. Em um navegador, ative o Grafana. 

    Insira a URL de serviço do {{site.data.keyword.monitoringshort}} para a região em que você criou o cluster. 
    
    Para obter as URLs por região, consulte
[URLs para o serviço de
monitoramento](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Por exemplo, para a região Sul dos EUA, ative:
[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Configure o domínio do {{site.data.keyword.monitoringshort}} como **Conta**.

    No Grafana, selecione seu ID. Em seguida, verifique se você está na conta correta e escolha um domínio. Selecione `Domain = account`.

    Os clusters encaminham métricas ao domínio de métricas da conta. 

## Etapa 6: monitorar o cluster no Grafana
{: #ks_step6}

O {{site.data.keyword.containershort}} fornece um painel do Grafana que pode ser usado para monitorar suas métricas do cluster. 

Conclua as etapas a seguir para abrir o painel de amostra:

1. Selecione a alternância de barra de menus lateral ![Barra de menus lateral do Grafana](images/grafana_settings.gif "Barra de menus lateral do Grafana").
2. Selecione **Painéis**.
3. Clique em **Abrir**.
4. Selecione **ClusterMonitoringDashboard_v1**.

O painel de amostra é aberto. 

![Painel de amostra do Grafana](images/cluster_grafana_sample_dashboard.png "Painel de amostra do Grafana")



## Etapas Seguintes
{: #ks_next_steps}

Defina um alerta para uma métrica. Para obter mais informações, consulte [Configurando alertas](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).
