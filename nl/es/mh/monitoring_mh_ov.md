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

En {{site.data.keyword.Bluemix}}, las métricas de {{site.data.keyword.messagehub}} se recopilan automáticamente. Se recopila el número de bytes dentro y fuera de un tema. Se toma un punto de comprobación cada 15 minutos. Puede utilizar Grafana para visualizar estas métricas. 
{:shortdesc}


**Nota:** Las métricas de {{site.data.keyword.messagehub}} solo están disponibles en el plan Estándar de {{site.data.keyword.messagehub}} en EE.UU. sur, Reino Unido y Sídney. 




## Ver y analizar métricas
{: #view}

Para supervisar el rendimiento de {{site.data.keyword.messagehub}} en {{site.data.keyword.Bluemix_notm}}, utilice Grafana. {{site.data.keyword.messagehub}} proporciona un panel de control que puede utilizar para ver y supervisar el rendimiento de sus temas.

El servicio {{site.data.keyword.monitoringlong}} utiliza Grafana, un análisis de código abierto y una plataforma de visualización, que puede utilizar para supervisar, buscar, analizar y visualizar las métricas en diversos gráficos, como por ejemplo diagramas y tablas. 

Puede iniciar Grafana de cualquiera de estas formas:

* Puede pulsar el botón **Grafana** en el panel de control de {{site.data.keyword.messagehub}} en la consola de {{site.data.keyword.Bluemix_notm}}.

    Grafana se abre dentro del contexto del espacio de {{site.data.keyword.Bluemix_notm}} donde {{site.data.keyword.messagehub}} se está ejecutando.
    
* Puede iniciar Grafana directamente desde un navegador web.

    Compruebe que está en la organización y en el espacio correctos donde se esté ejecutando la instancia de {{site.data.keyword.messagehub}}.
    
    Para obtener más información, consulte [Navegación al panel de control de Grafana desde un navegador web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).
    

Tenga en cuenta la información siguiente:

* Debe iniciar Grafana en la misma región de {{site.data.keyword.Bluemix_notm}} donde está en ejecución la instancia de {{site.data.keyword.messagehub}}.
* Utilice el panel de control de Grafana que se proporciona de forma predeterminada para empezar a supervisar la instancia de {{site.data.keyword.messagehub}}.
* Cree paneles de control personalizados de Grafana para crear paneles de control ad-hoc. Puede definir una o varias consultas de métrica en un panel de control de Grafana para supervisar una instancia de {{site.data.keyword.messagehub}}. Para obtener más información, consulte [Configuración de una consulta de métricas en Grafana](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query#define_query).
* También puede definir alertas en las consultas. Para obtener más información, consulte [Configuración de alertas](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).


## Métricas para un tema de Kafka
{: #kafka_topic_metrics}

Para cada tema de Kafka definido, se recopilarán las métricas siguientes:


<table>
  <caption>Métricas para un tema de Kafka</caption>
  <tr>
    <th>Métrica</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Tasa de bytes enviados al tema por las aplicaciones cliente de Kafka.</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Tasa de bytes recibidos de un tema por las aplicaciones cliente de Kafka.</td>
  </tr>
</table>



## Métricas para una partición de Kafka
{: #kafka_partition_metrics}

Para cada partición de Kafka que tenga un puente de Cloud Storage que consuma mensajes, se recopilarán las métricas siguientes:


<table>
  <caption>Métricas de partición de Kafka</caption>
  <tr>
    <th>Métrica</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>El desplazamiento para el último recurso de Kafka que procesa el puente de Cloud Storage.</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>El desplazamiento confirmado para los registros de Kafka que están procesados por el puente de Cloud Storage.</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Número de mensajes recibidos por una instancia de puente de Cloud Storage desde un tema de Kafka. Solo cuenta los mensajes que contienen JSON válido que no puede procesar el puente.</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Número de mensajes recibidos por una instancia de puente de Cloud Storage desde un tema de Kafka. Solo cuenta los mensajes que contienen datos que no se pudieron analizar porque los datos no son un documento JSON válido.</td>
  </tr>
</table>




## Referencias
{: #mhlinks}

* [Iniciación a Message Hub](/docs/services/EventStreams?topic=eventstreams-getting_started#getting_started)
* [Supervisión y registro](/docs/services/EventStreams/messagehub072.html#monitoring)

