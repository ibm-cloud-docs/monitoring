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



# Configurando métricas de carregamento para um trabalhador no Grafana
{: #config_load_worker}

No {{site.data.keyword.Bluemix}}, as métricas de carregamento selecionadas para um trabalhador
são coletadas automaticamente. Para monitorá-las por meio do {{site.data.keyword.monitoringlong}}, deve-se definir
uma consulta do Grafana. 
{:shortdesc}

Para obter uma lista das métricas de carregamento que são coletadas automaticamente, consulte
[Métricas
de carregamento para trabalhadores](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#load_metrics_workers).


## Etapa 1: Reunir os dados para o trabalhador que você deseja monitorar
{: #step16}

Obtenha as informações a seguir para o trabalhador que você deseja monitorar:

* **Região** na qual o cluster está em execução.
* **Nome do cluster** no qual o contêiner está em execução. 
* **Nome do trabalhador** que você deseja monitorar. 

Descubra se as métricas são encaminhadas para um domínio de espaço ou para o domínio de contas.

Para identificar o local para o qual seu cluster encaminha métricas, execute o comando a seguir:

```
$ ibmcloud cs cluster-get ClusterName --json
```
{: codeblock}

em que *ClusterName* é o nome de seu cluster.

Na saída, os campos a seguir fornecem as informações sobre o local para o qual as métricas são encaminhadas:

* **logOrg** define o ID de uma organização do CF.
* **logOrgName** define o nome de uma organização do CF.
* **logSpace** define o ID de um espaço do CF.
* **logSpaceName** define o nome de um espaço do CF.

Se os campos estiverem vazios, as métricas serão encaminhadas para o domínio de contas.
Se os campos tiverem uma organização do CF e um conjunto de espaços do CF, as métricas serão encaminhadas para
o domínio de espaço que estiver associado a esse espaço.

## Etapa 2: Ativar o Grafana
{: #step25}

Ative o Grafana por meio de um navegador. Para obter mais informações, veja [Navegando para o painel do Grafana por meio de um navegador da web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

No Grafana, assegure-se de que você está com login efetuado na conta na qual o cluster está em
execução. 

1. Em um navegador, ative o Grafana. 

    Insira a URL de serviço do {{site.data.keyword.monitoringshort}} para a região em que você criou o cluster. 
    
    Para obter as URLs por região, consulte
[URLs para o serviço de
monitoramento](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Por exemplo, para a região Sul dos EUA, ative:
[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Configure o domínio do {{site.data.keyword.monitoringshort}} no qual é possível
visualizar as métricas de cluster.

    No Grafana, selecione seu ID. Em seguida, verifique se você está na conta correta e escolha um
domínio.

    Os clusters que possuem um espaço do CF associado encaminham as métricas para o domínio de
métricas de espaço. Selecione `Domain = space` e a organização e o espaço que estão
associados ao seu cluster.

    Os clusters que são criados no nível de conta encaminham métricas para o domínio de métricas de
contas. Selecione `Domain = account`



## Etapa 3: Definir uma consulta no Grafana para uma métrica de CPU
{: #step34}

Conclua as etapas a seguir para criar um painel do Grafana e definir uma consulta para monitorar o uso
de CPU de um trabalhador:

1. Cria um novo painel.

    * Selecione a alternância de barra de menus lateral ![Barra de menus lateral do Grafana](images/grafana_settings.gif "Barra de menus lateral do Grafana").
    * Selecione **Painéis**.
    * Clique em **Novo**

    Um painel se abre. O painel inclui uma linha vazia que está pronta para configuração.

2. Inclua um painel *Gráfico* para monitorar a métrica de CPU de um pod.

    1. Selecione **Gráfico**.

    2. Clique no título do gráfico e, em seguida, selecione **Editar**.

        O *Métricas* guia é aberta. É possível ver aqui a origem de dados padrão.

3. Defina a consulta que filtra os dados que são exibidos no gráfico. 

    Para obter informações sobre o formato da consulta, veja [Formato de consulta para métricas de carga coletadas para trabalhadores](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers).

    Na guia *Métricas*, selecione **Incluir consulta**. <br>Uma entrada de consulta é incluído. Cada consulta é rotulada com uma letra.
	
	Conclua as etapas a seguir para definir a consulta:

    1. Clique em **Selecionar métrica** para especificar a origem e, em seguida,
escolha `ibmcloud`.
    
    2. Clique em **Selecionar métrica** para especificar o tipo de nuvem e, em
seguida, escolha `public`.
    
    3. Clique em **Selecionar métrica** para especificar o nome do serviço e, em seguida, escolha `containers-kubernetes`.
	
    4. Clique em **Selecionar métrica** para especificar a região e, em seguida,
escolha a região em que seu cluster está em execução. Por exemplo, `us-south`.
    
    5. Clique em **Selecionar métrica** para especificar o nome do cluster e, em
seguida, escolha o nome do cluster no qual o contêiner está em execução.
		
	6. Clique em **Selecionar métrica** para especificar o nome do trabalhador que você deseja monitorar.
	
	7. Clique em **Selecionar métrica** para especificar o tipo de métrica e, em
seguida, clique em **Selecionar métrica** para especificar o subtipo de métrica.
	
	    Para obter uma lista de métricas da CPU, consulte
[Métricas da CPU para trabalhadores](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#load_metrics_workers).
	
	10. Clique na imagem de mais ![Ícones Incluir](images/grafana_plus_image.gif "Imagem de mais") e escolha uma função. Será possível incluir uma função para transformar, combinar e executar cálculos nos dados que estiverem disponíveis para uma métrica.

        Por exemplo, é possível incluir a função **alias(newName)** para incluir um alias para uma métrica. Esse alias é usado para imprimir uma sequência em vez do nome da métrica na legenda que é exibida no gráfico.

        Para incluir um alias para sua métrica, conclua as etapas a seguir:

        1. Clique no símbolo de mais.
        2. Selecione **Especial**.
        3 Selecione **alias**.
        4. Insira uma sequência, por exemplo, `My sample metric`.

4. Salve o painel para reutilização posterior.

    1. Clique na imagem de painel salvar ![Imagem de painel salvar](images/grafana_save_dashboard.gif "Imagem de painel salvar").
    2. Insira o nome do painel.
    3. Clique em **Salvar**.

