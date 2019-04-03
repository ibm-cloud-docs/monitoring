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

In {{site.data.keyword.Bluemix}}, le metriche {{site.data.keyword.messagehub}} vengono raccolte automaticamente. Viene raccolto il numero di byte in e out di un argomento. Viene preso un checkpoint ogni 15 minuti. Puoi utilizzare Grafana per visualizzare queste metriche. 
{:shortdesc}


**Nota:** le metriche di {{site.data.keyword.messagehub}} sono disponibili nel piano {{site.data.keyword.messagehub}} Standard solo in Stati Uniti Sud, Regno Unito e Sydney. 




## Visualizzazione e analisi delle metriche
{: #view}

Per monitorare le prestazioni di {{site.data.keyword.messagehub}} in {{site.data.keyword.Bluemix_notm}}, utilizza Grafana. {{site.data.keyword.messagehub}} fornisce un dashboard che puoi utilizzare per visualizzare e monitorare le prestazioni dei tuoi argomenti.

Il servizio {{site.data.keyword.monitoringlong}} utilizza Grafana, una piattaforma di analisi e visualizzazione open source, che puoi utilizzare per monitorare, ricercare, analizzare e visualizzare le tue metriche in vari tipi di grafici, ad esempio, diagrammi e tabelle. 

Puoi avviare Grafana in uno dei seguenti modi:

* Puoi fare clic sul pulsante **Grafana** nel dashboard {{site.data.keyword.messagehub}} nella console {{site.data.keyword.Bluemix_notm}}.

    Grafana si apre all'interno del contesto dello spazio in {{site.data.keyword.Bluemix_notm}} dove è in esecuzione {{site.data.keyword.messagehub}}.
    
* Puoi avviare Grafana direttamente da un browser web.

    Controlla di essere nell'organizzazione e nello spazio corretti dove è in esecuzione l'istanza {{site.data.keyword.messagehub}}.
    
    Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana da un browser web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).
    

Considera le seguenti informazioni:

* Devi avviare Grafana nella stessa regione {{site.data.keyword.Bluemix_notm}} in cui è in esecuzione l'istanza {{site.data.keyword.messagehub}}.
* Utilizza il dashboard Grafana fornito per impostazione predefinita per avviare il monitoraggio della tua istanza {{site.data.keyword.messagehub}}.
* Crea dashboard Grafana personalizzati per creare dashboard ad hoc. Puoi definire una o più query della metrica in un dashboard Grafana per monitorare un'istanza {{site.data.keyword.messagehub}}. Per ulteriori informazioni, vedi [Configurazione di una query della metrica in Grafana](/docs/services/cloud-monitoring/grafana/define_query.html#define_query).
* Puoi anche definire gli avvisi per le query. Per ulteriori informazioni, vedi [Configurazione degli avvisi](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).


## Metriche per un argomento Kafka
{: #kafka_topic_metrics}

Per ogni argomento Kafka che viene definito, vengono raccolte le seguenti metriche:


<table>
  <caption>Metriche per un argomento Kafka</caption>
  <tr>
    <th>Metrica</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Frequenza di byte inviati all'argomento dalle applicazioni client Kafka.</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Frequenza di byte ricevuta da un argomento dalle applicazioni client Kafka.</td>
  </tr>
</table>



## Metriche per una partizione Kafka
{: #kafka_partition_metrics}

Per ogni partizione Kafka con un bridge dell'archivio cloud che utilizza i messaggi, vengono raccolte le seguenti metriche:


<table>
  <caption>Metriche della partizione Kafka</caption>
  <tr>
    <th>Metrica</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>L'offset dell'ultimo record Kafka elaborato dal bridge dell'archivio cloud.</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>L'offset di cui è stato eseguito il commit per i record Kafka elaborati dal bridge dell'archivio cloud.</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Numero di messaggi ricevuti da un'istanza bridge dell'archivio cloud da un argomento Kafka. Vengono contati solo i messaggi che contengono un JSON valido che non può essere elaborato dal bridge.</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Numero di messaggi ricevuti da un'istanza bridge dell'archivio cloud da un argomento Kafka. Vengono contati solo i messaggi che contengono i dati che non possono essere analizzati perché non sono un documento JSON valido.</td>
  </tr>
</table>




## Riferimenti
{: #mhlinks}

* [Introduzione a Message Hub](/docs/services/EventStreams/index.html#getting_started)
* [Monitoraggio e registrazione](/docs/services/EventStreams/messagehub072.html#monitoring)

