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


# Navegando para o painel Grafana
{:#navigating_grafana}

No {{site.data.keyword.Bluemix}}, é possível usar o Grafana, uma plataforma de software livre para análise de dados e visualização para monitorar, procurar, analisar e visualizar suas métricas em uma variedade de gráficos, por exemplo, diagramas e tabelas. Use o Grafana para executar tarefas analíticas avançadas.
{:shortdesc}

É possível ativar o Grafana de qualquer uma das maneiras a seguir:

* No {{site.data.keyword.Bluemix_notm}}

    É possível ativar suas métricas de contêiner do Docker específicas no Grafana dentro do contexto para esse contêiner específico. Esse recurso se aplica somente aos contêineres que são implementados na infraestrutura gerenciada pelo {{site.data.keyword.Bluemix_notm}}. 
    
    Para obter mais informações, consulte [Navegando para o painel do Grafana por meio do painel do {{site.data.keyword.Bluemix_notm}}
    ](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_bluemix).

* Em um link direto do navegador

    É possível ativar o Grafana para que os dados que são exibidos agreguem logs de serviços em um espaço fornecido do {{site.data.keyword.Bluemix_notm}}.
    
    Para obter mais informações, veja [Navegando para o painel do Grafana por meio de um navegador da web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).
    
Para obter mais informações sobre Grafana, consulte o [Guia do Usuário do Grafana ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Navegando para o painel do Grafana por meio do painel do IBM Cloud
{: #launch_grafana_from_bluemix}

**Nota:** esse recurso se aplica somente aos contêineres que são implementados na infraestrutura gerenciada pelo {{site.data.keyword.Bluemix_notm}}. 

A consulta que é usada para filtrar os dados que são exibidos no Grafana recupera dados para o contêiner do {{site.data.keyword.Bluemix_notm}} no local em que o Kibana é ativado. 

Para ver as métricas de um contêiner do Docker no Grafana, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no contêiner no *Painel*. 
    
2. Na barra de navegação, clique em **Monitoramento e logs**. A guia de monitoramento é aberta. 
    
3. Clique em **Visualização avançada**. O painel do **Grafana** é aberto.


##  Navegando para o painel do Grafana por meio de um navegador da web
{: #launch_grafana_from_browser}

A consulta que é usada para filtrar os dados que são exibidos no Grafana recupera dados para um espaço na organização do {{site.data.keyword.Bluemix_notm}}. As informações de métricas que o Grafana exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado.

Conclua as etapas a seguir para ativar o Grafana em um navegador:

1. Abra um navegador da web. 
2. Insira a URL para a região em que você deseja monitorar métricas. 

    A tabela a seguir lista as URLs por região:
	<table>
      <caption>URLs para ativar o Grafana em diferentes regiões</caption>
      <tr>
        <th>Região</th>
	    <th>Nó de extremidade</th>
      </tr>
      <tr>
        <td>Alemão</td>
	    <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
      </tr>
      <tr>
        <td>Reino Unido</td>
	    <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
      </tr>
      <tr>
        <td>Sul dos Estados Unidos</td>
    	<td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
      </tr>
      <tr>
        <td>Reino Unido</td>
	    <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
      </tr>
      
    </table>
	
2. Selecione **Grafana**.
     

