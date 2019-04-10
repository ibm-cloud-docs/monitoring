---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, metrics

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

# Utilizzo delle metriche
{: #metrics}

Dopo aver eseguito il provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.Bluemix}} e configurato un agent Sysdig per un'origine delle metriche, puoi visualizzare, monitorare e gestire le metriche tramite l'IU web {{site.data.keyword.mon_full_notm}}. Utilizza le metriche per analizzare statisticamente i dati che hanno valori numerici. 
{:shortdesc}


**Una metrica è una misura quantitativa con una o più etichette per definire le proprie caratteristiche.**

Una metrica viene rappresentata da serie temporali. 

Una serie temporale è una serie di punti di dati numerici in un periodo di tempo. 

Le metriche sono classificate in due gruppi: 

* Metriche predefinite 
* Metriche personalizzate


## Etichette
{: #metrics_labels}

**Le etichette definiscono le caratteristiche di una metrica.**

Le etichette vengono classificate come etichette dell'infrastruttura e etichette del descrittore della metrica. Ogni metrica ha una serie di etichette predefinite. Per le metriche personalizzate, puoi configurare ulteriori etichette. 

Puoi utilizzare le etichette per identificare e differenziare le caratteristiche di una metrica, ad esempio,
* Puoi raggruppare gli oggetti dell'infrastruttura in gerarchie logiche. 
* Puoi filtrare i dati. 
* Puoi suddividere i dati aggregati in segmenti. 


## Metriche predefinite 
{: #metrics_default}

**Le metriche predefinite forniscono informazioni sul sistema, sull'orchestratore e sull'infrastruttura di rete.**

Il servizio di monitoraggio aggiunge automaticamente le etichette ad ogni metrica.


## Metriche personalizzate
{: #metrics_custom}

**Le metriche personalizzate variano in base al tipo di infrastruttura e alle applicazioni che monitori. Alcuni esempi sono JMX, Prometheus e StatsD.**

Queste metriche hanno una serie di etichette predefinite. Puoi aggiungere ulteriori etichette personalizzate.

Il servizio di monitoraggio conserva un indice di tutte le metriche e le etichette personalizzate che hanno riportato dei dati negli ultimi 14 giorni. Puoi utilizzare queste metriche per configurare dashboard, ambiti e avvisi.

Considera le seguenti informazioni su come il servizio di monitoraggio gestisce le voci di indice:
*  Una metrica viene automaticamente rimossa dall'indice del servizio di monitoraggio e contrassegnata come mancante quando si verifica una delle seguenti condizioni:
    
    * Il servizio di monitoraggio non riceve dati per una metrica o etichetta per più di 14 giorni.
    
    * Una metrica o etichetta non ha mai riportato dei dati.

* Non puoi configurare nuove risorse con una metrica o un'etichetta mancante. 
* Non puoi aggiornare le risorse esistenti finché le metriche e le etichette mancanti non vengono rimosse dalla configurazione corrente.
* Puoi utilizzare una metrica o un'etichetta mancante sui grafici e le query dei dati. 
* Le tue risorse esistenti non sono influenzate se includono una metrica o un'etichetta mancante.
* Quando vengono ricevuti dei dati per una metrica o un'etichetta mancante, la metrica o l'etichetta viene riaggiunta all'indice.



