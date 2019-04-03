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


# Configurando uma consulta de métrica no Grafana
{: #define_query}

No {{site.data.keyword.Bluemix}}, as métricas de serviços do Cloud selecionadas são coletadas automaticamente. Para monitorá-las por meio do {{site.data.keyword.monitoringlong}}, deve-se definir
uma consulta do Grafana. 
{:shortdesc}

## Etapa 1: Reunir os dados para o app ou serviço do CF que você deseja monitorar
{: #step18}

Obtenha as informações a seguir para o app ou serviço do CF que você deseja monitorar:

* **Região** na qual o app CF está em execução.
* **Organização** na qual o app CF está em execução. 	
* **Espaço** no qual o app CF está em execução. 
* **Nome do app CF** do app que você deseja monitorar ou o **Nome do serviço**. 


## Etapa 2: Ativar o Grafana
{: #step27}

Ative o Grafana por meio de um navegador. Para obter mais informações, veja [Navegando para o painel do Grafana por meio de um navegador da web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

No Grafana, assegure-se de que você está com login efetuado na conta, na organização e na região nas quais o app CF está em execução. 


## Etapa 3: Definir uma consulta no Grafana
{: #step36}

Conclua as etapas a seguir para criar um painel do Grafana e definir uma consulta:

1. Cria um novo painel.

    * Selecione a alternância de barra de menus lateral
![Barra de menus lateraldo Grafana](images/grafana_settings.gif "Barra de menus lateral do Grafana").

    * Selecione **Painéis**.
    * Clique em **Novo**

    Um painel se abre. O painel inclui uma linha vazia que está pronta para configuração.

2. Inclua um painel *Gráfico*.

    1. Selecione **Gráfico**.

    2. Clique no título do gráfico e, em seguida, selecione **Editar**.

        O *Métricas* guia é aberta. É possível ver aqui a origem de dados padrão.

3. Defina a consulta que filtra os dados que são exibidos no gráfico. 

    Na guia *Métricas*, selecione **Incluir consulta**. <br>Uma entrada de consulta é incluído. Cada consulta é rotulada com uma letra.
    
    ![New query entry](images/grafana4_query_f1.gif "New query entry")
        
    1. Clique em **Selecionar métrica** e, em seguida, escolha a origem:
`ibmcloud`.
    
    2. Clique em **Selecionar métrica** e, em seguida, escolha o tipo de nuvem:
`public`.
    
    3. Clique em **Selecionar métrica** e, em seguida, escolha o nome do serviço, por exemplo, `cloud-foundry` para as métricas de app CF ou `message hub` para métricas do {{site.data.keyword.messagehub}}.
    
    4. Clique em **Selecionar métrica** e, em seguida, escolha a região em que você está trabalhando, por exemplo, `ng` para a região Sul dos EUA.
    
    5. Selecione os campos de serviços específicos que se aplicam ao serviço ou ao app CF que você deseja monitorar.

        <table>
          <caption>Formatos de consulta de métrica por serviço ou app CF</caption>
          <tr>
            <th>Nome do serviço</th>
            <th>Link para o formato de consulta de métrica</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Formato de consulta para as métricas da CPU coletadas para os contêineres](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers) </br>[Formato de consulta para as métricas de carregamento coletadas para os trabalhadores](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers) </br>[Formato de consulta para as métricas da memória coletadas para contêineres](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)</td> 
          </tr>
          <tr>
            <td>Apps CF</td>
            <td>[Formato da consulta para apps CF](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format)</td> 
          </tr>
        </table>

        Por exemplo, para um app CF, escolha:
    
        Clique em **Selecionar métrica** e, em seguida, escolha o nome do app CF, por
exemplo, `logtester`.
    
        Clique em **Selecionar métrica** e, em seguida, escolha o índice da instância
do app CF, por exemplo, `0`.

        Clique em **Selecionar métrica** e, em seguida, escolha
`container`.
    
    9. Clique em **Selecionar métrica** e, em seguida, escolha um tipo de métrica. Por exemplo, **cpu** para as métricas da CPU, **memory** para as métricas da memória e **disk** para as métricas de disco. 

        **Nota:** ignore esta etapa para apps CF. 

    10. Clique em **Selecionar métrica** e, em seguida, escolha uma métrica. 

        <table>
          <caption>Lista de métricas por serviço ou app CF</caption>
          <tr>
            <th>Nome do serviço</th>
            <th>Link para métricas</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Métricas da CPU](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Métricas de disco](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[Métricas da memória](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>Apps CF</td>
            <td>[Métricas da CPU](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics)  </br>[Métricas de disco](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[Métricas da memória](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Métricas para um tópico do Kafka](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_topic_metrics) </br>[Métricas para uma partição do Kafka](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. Clique na imagem de mais ![Ícones Incluir](images/grafana_plus_image.gif "Imagem de mais") e escolha uma função. Será possível incluir uma função para transformar, combinar e executar cálculos nos dados que estiverem disponíveis para uma métrica.
        
        Por exemplo, é possível incluir a função **alias(newName)** para incluir um alias para uma métrica. Esse alias é usado para imprimir uma sequência em vez do nome da métrica na legenda que é exibida no gráfico.
        
        Para incluir um alias para sua métrica, conclua as etapas a seguir:
        
        1. Clique no símbolo de mais.
        2. Selecione **Especial**. 
        3 Selecione **alias**.
        4. Insira uma sequência, por exemplo, `My sample metric`.


## Etapa 4: Salvar o painel para reutilização posterior
{: #step44}

Conclua as etapas a seguir:

1. Clique na imagem de painel salvar ![Imagem de painel salvar](images/grafana_save_image.gif "Imagem de painel salvar").
2. Insira o nome do painel.
3. Clique em **Salvar**.
