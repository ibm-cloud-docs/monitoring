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



# {{site.data.keyword.messagehub}}
{: #monitoring_mh_ov}

No {{site.data.keyword.Bluemix}}, as métricas do {{site.data.keyword.messagehub}} são coletadas automaticamente. O número de bytes de entrada e saída de um tópico são coletados. Um ponto de verificação é obtido a cada 15 minutos. É possível usar o Grafana para visualizar essas métricas. 
{:shortdesc}


**Nota:** as métricas do {{site.data.keyword.messagehub}} estão disponíveis no Plano Standard do {{site.data.keyword.messagehub}} apenas no Sul dos EUA, no Reino Unido e em Sydney. 




## Visualizando e analisando métricas
{: #view}

Para monitorar o desempenho do {{site.data.keyword.messagehub}} no {{site.data.keyword.Bluemix_notm}}, use o Grafana. O {{site.data.keyword.messagehub}} fornece um painel que pode ser usado para visualizar e monitorar o desempenho de seus tópicos.

O serviço do {{site.data.keyword.monitoringlong}} usa o Grafana, uma plataforma de software livre para análise de dados e visualização, que pode ser usada para monitorar, procurar, analisar e visualizar suas métricas em uma variedade de gráficos, por exemplo, diagramas e tabelas. 

É possível ativar o Grafana de qualquer uma das maneiras a seguir:

* É possível clicar no botão do **Grafana** no painel do {{site.data.keyword.messagehub}} no console do {{site.data.keyword.Bluemix_notm}}.

    O Grafana é aberto dentro do contexto do espaço no {{site.data.keyword.Bluemix_notm}} onde o {{site.data.keyword.messagehub}} está em execução.
    
* É possível ativar o Grafana diretamente de um navegador da web.

    Verifique se você está na organização e no espaço corretos onde a instância do {{site.data.keyword.messagehub}} está em execução.
    
    Para obter mais informações, veja [Navegando para o painel do Grafana por meio de um navegador da web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).
    

Considere as seguintes informações:

* Deve-se ativar o Grafana na mesma região do {{site.data.keyword.Bluemix_notm}} em que a instância do {{site.data.keyword.messagehub}} está em execução.
* Use o painel do Grafana fornecido por padrão para iniciar o monitoramento de sua instância do {{site.data.keyword.messagehub}}.
* Crie painéis customizados do Grafana para construir painéis ad hoc. É possível definir uma ou mais consultas de métricas em um painel do Grafana para monitorar uma instância do {{site.data.keyword.messagehub}}. Para obter mais informações, consulte [Configurando uma consulta de métrica no Grafana](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query#define_query).
* Também é possível definir alertas em consultas. Para obter mais informações, consulte [Configurando alertas](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).


## Métricas para um tópico do Kafka
{: #kafka_topic_metrics}

Para cada tópico do Kafka que é definido, as métricas a seguir são coletadas:


<table>
  <caption>Métricas para tópico do Kafka</caption>
  <tr>
    <th>de Métrica</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Taxa de bytes enviados para o tópico por aplicativos cliente do Kafka.</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Taxa de bytes recebidos de um tópico por aplicativos cliente do Kafka.</td>
  </tr>
</table>



## Métricas para uma partição do Kafka
{: #kafka_partition_metrics}

Para cada partição do Kafka com uma ponte do Cloud Storage que consome mensagens, as métricas a seguir são coletadas:


<table>
  <caption>Métricas de partição do Kafka</caption>
  <tr>
    <th>de Métrica</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>A compensação para o último registro do Kafka que é processada pela ponte do Cloud Storage.</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>A compensação confirmada para registros do Kafka que são processados pela ponte do Cloud Storage.</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Número de mensagens que são recebidas por uma instância da ponte do Cloud Storage de um tópico do Kafka. Conta somente as mensagens que contêm o JSON válido que não pode ser processado pela ponte.</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Número de mensagens que são recebidas por uma instância da ponte do Cloud Storage de um tópico do Kafka. Conta somente mensagens que contêm dados que não puderam ser analisados porque os dados não são um documento JSON válido.</td>
  </tr>
</table>




## References
{: #mhlinks}

* [Introdução ao Message Hub](/docs/services/EventStreams?topic=eventstreams-getting_started#getting_started)
* [Monitoramento e criação de log](/docs/services/EventStreams/messagehub072.html#monitoring)

