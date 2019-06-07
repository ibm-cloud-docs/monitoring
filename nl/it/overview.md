---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, overview

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


# {{site.data.keyword.mon_full_notm}}
{: #about}

{{site.data.keyword.mon_full}} è un sistema di gestione di terze parti, nativo cloud e di intelligence del contenitore che puoi includere come parte della tua architettura {{site.data.keyword.cloud_notm}}. Utilizzalo per ottenere visibilità operativa sulle prestazioni e sull'integrità delle applicazioni, dei servizi e delle piattaforme. Offre agli amministratori, agli sviluppatori e ai team DevOps una telemetria di stack completa con funzioni avanzate per il monitoraggio e la risoluzione dei problemi, la definizione di avvisi e la progettazione di dashboard personalizzati. {{site.data.keyword.mon_full_notm}} è gestito da Sysdig in collaborazione con {{site.data.keyword.IBM_notm}}.
{:shortdesc}


Per aggiungere le funzioni di monitoraggio a {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}, devi eseguire il provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}}.

Prima di eseguire il provisioning di un'istanza, considera le seguenti informazioni:

* I tuoi dati vengono inviati a una terza parte.
* Il proprietario dell'account può creare, visualizzare ed eliminare un'istanza di un servizio in {{site.data.keyword.cloud_notm}}. Questo utente può inoltre concedere le autorizzazioni ad altri utenti in modo che possano utilizzare il servizio {{site.data.keyword.mon_full_notm}}. 
* Altri utenti {{site.data.keyword.cloud_notm}} con le autorizzazioni `administrator` o `editor` possono gestire il servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}. Questi utenti devo disporre anche delle autorizzazioni della piattaforma per creare le risorse all'interno del contesto del gruppo di risorse in cui pensano di eseguire il provisioning dell'istanza.

Esegui il provisioning di un'istanza all'interno del contesto di un gruppo di risorse. Utilizza un gruppo di risorse per organizzare i tuoi servizi per scopi di controllo dell'accesso e fatturazione. Puoi eseguire il provisioning di un'istanza {{site.data.keyword.mon_full_notm}} nel gruppo di risorse *predefinito* o in uno personalizzato.

Quando [esegui il provisioning di un'istanza](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision), ottieni automaticamente una chiave di inserimento, nota come la [chiave di accesso Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key).

Dopo aver eseguito il provisioning di un'istanza, devi configurare un agent {{site.data.keyword.mon_full_notm}} per ogni origine della metrica. Un'origine della metrica è una risorsa cloud che vuoi monitorare e di cui vuoi controllare le prestazioni e l'integrità. Devi configurare un agent {{site.data.keyword.mon_full_notm}} in ogni ambiente che vuoi monitorare. Ad esempio, un'origine della metrica può essere un cluster Kubernetes. Utilizza la chiave di accesso per configurare l'agent Sysdig responsabile della raccolta e dell'inoltro dei dati della metrica alla tua istanza

Dopo aver distribuito l'agent {{site.data.keyword.mon_full_notm}} in un'origine della metrica, la raccolta e l'inoltro delle metriche all'istanza sono automatici. L'agent {{site.data.keyword.mon_full_notm}} raccoglie e riporta automaticamente le metriche predefinite. Puoi configurare quali metriche monitorare in un ambiente.

Puoi [monitorare](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring) e [gestire](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage) i dati tramite l'IU web {{site.data.keyword.mon_full_notm}}.  

La seguente figura mostra la panoramica dei componenti per il servizio {{site.data.keyword.mon_full_notm}} in esecuzione su {{site.data.keyword.cloud_notm}}:

![{{site.data.keyword.mon_full_notm}} - Panoramica dei componenti su {{site.data.keyword.cloud_notm}}](images/components.png "{{site.data.keyword.mon_full_notm}} - Panoramica dei componenti su {{site.data.keyword.cloud_notm}}")



## Raccolta dei dati
{: #overview_collection}

Quando configuri un agent Sysdig per raccogliere ed inoltrare i dati a un'istanza {{site.data.keyword.mon_full_notm}}, i dati vengono automaticamente raccolti e sono disponibili per l'analisi tramite l'IU web.

I dati vengono raccolti con una frequenza di 10 secondi.  

## Disponibilità dei dati
{: #overview_availability}

I dati sono disponibili per un massimo di 15 mesi.

Dopo aver rimosso un agent Sysdig da un host o un contenitore, i dati cronologici non vengono eliminati. I dati sono disponibili per l'analisi tramite l'IU web per il periodo di tempo in cui l'agent è stato installato e ha riportato dei dati.

Dopo aver eliminato un'istanza del servizio {{site.data.keyword.mon_full_notm}}, i dati non sono disponibili per la ricerca e l'analisi.



## Conservazione dei dati
{: #overview_retention}

I dati vengono conservati per ogni istanza in base a una politica di *rollup*.

Con il passare del tempo, viene eseguito il rollup dei dati da una bassa granularità a una maggiore dopo 3 mesi.

La politica di rollup descrive la granularità dei dati nel tempo:

* I dati vengono conservati alla risoluzione di 10 secondi per le prime 6 ore.
* I dati vengono conservati alla risoluzione di 1 minuto per 2 giorni.
* I dati vengono conservati alla risoluzione di 10 minuti per 2 settimane.
* I dati vengono conservati alla risoluzione di 1 ora per 3 mesi.
* I dati vengono conservati alla risoluzione di 1 giorno per un anno.

## Eliminazione dei dati
{: #overview_data_deletion}

Quando elimini un'istanza di {{site.data.keyword.mon_full_notm}} da {{site.data.keyword.cloud_notm}}, devi aprire un caso tramite il supporto per richiedere che i dati vengano eliminati. Per ulteriori informazioni, consulta [come contattare il supporto](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp).

Quando elimini un'acquisizione, il file di dati per tale acquisizione viene eliminato automaticamente.

L'eliminazione dei dati raccolti da un solo agent Sysdig in un'istanza {{site.data.keyword.mon_short}} non è supportata.
{: note}



## Ubicazione dei dati
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}} raccoglie e aggrega le metriche. 

* I dati della metrica sono ospitati su {{site.data.keyword.cloud_notm}}.
* Ogni ubicazione regione multizona (MZR) raccoglie e aggrega le metriche per ogni istanza di {{site.data.keyword.mon_full_notm}} che vengono eseguite in tale ubicazione.
* I dati vengono posizionati nella regione in cui è stato eseguito il provisioning dell'istanza {{site.data.keyword.mon_full_notm}}. Ad esempio, i dati della metrica per un'istanza di cui è stato eseguito il provisioning in Stati Uniti Sud vengono ospitati nella regione Stati Uniti Sud.



## Agent {{site.data.keyword.mon_full_notm}}
{: #overview_sysdig_agent}

L'agent {{site.data.keyword.mon_full_notm}} raccoglie e riporta automaticamente le metriche predefinite. 

Il seguente elenco illustra gli agent {{site.data.keyword.mon_full_notm}} disponibili:

* Agent {{site.data.keyword.mon_full_notm}} per Kubernetes, GKE e OpenShift.
* Agent {{site.data.keyword.mon_full_notm}} per i contenitori Docker o i servizi non inseriti in contenitori.
* Agent {{site.data.keyword.mon_full_notm}} per Mesos, Marathon e DCOS.
* Agent {{site.data.keyword.mon_full_notm}} per le installazioni manuali di Linux.

Per ulteriori informazioni, consulta [Configurazione di un agent Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) e [Rimozione di un agent Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove).


## Visualizzazione dell'utilizzo
{: #overview_usage}

Per monitorare l'utilizzo e i costi del tuo servizio, consulta [Visualizzazione del tuo utilizzo](/docs/billing-usage/viewing_usage.html#viewingusage).


## Piani del servizio
{: #overview_plans}

Sono disponibili diversi piani del servizio per un'istanza {{site.data.keyword.mon_full_notm}}. [Ulteriori informazioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).


## Considerazioni sulla sicurezza
{: #overview_security}

**Acquisizioni**

Un'acquisizione è un file di traccia che puoi generare per analizzare cosa succede in un host durante un intervallo di tempo. Le acquisizioni contengono chiamate di sistema e altri eventi SO. Puoi abilitare o disabilitare questa funzione per il nodo quando configuri l'agent Sysdig che raccoglie le metriche per tale nodo. Per impostazione predefinita, le *acquisizioni* vengono abilitate quando configuri un agent Sysdig. Un nodo può essere un host, un contenitore, una macchina virtuale, un server bare metal o una qualsiasi origine della metrica in cui hai installato un agent Sysdig.

Quando le acquisizioni sono abilitate, tieni presente che Sysdig avrà una visibilità approfondita nelle tue operazioni. Per evitare un incidente di sicurezza e la potenziale esposizione dei dati all'esterno della tua organizzazione, controlla le politiche di sicurezza della tua organizzazione prima di abilitare le acquisizioni su un nodo. Considera di disabilitare la funzione *Capture* per tutti i tuoi agent Sysdig.
{: important}

