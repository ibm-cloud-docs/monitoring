---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, manage

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

# Gestione dei dati
{: #manage}

Utilizza le etichette per raggruppare le risorse dell'infrastruttura in gerarchie logiche, filtrare i dati e suddividere i dati aggregati in segmenti. Personalizza come i dati vengono aggregati quando configuri un grafico o crei un avviso per una metrica. Configura l'ambito di un dashboard, un pannello o un avviso in modo che filtri i punti dati. Limita l'accesso ai dati gestendo l'accesso ai dati degli utenti tramite i team. 
{:shortdesc}



## Etichette
{: #manage_labels}

Le **etichette** definiscono le caratteristiche di una metrica. Puoi utilizzare le etichette per identificare e differenziare le caratteristiche di una metrica. 

Le etichette vengono classificate come etichette dell'infrastruttura e etichette del descrittore della metrica. Ogni metrica ha una serie di etichette predefinite. Per le metriche personalizzate, puoi configurare ulteriori etichette. 

* Puoi utilizzare le **etichette dell'infrastruttura** per identificare gli oggetti all'interno dell'infrastruttura. Queste etichette si ottengono dall'infrastruttura. Ad esempio, un'etichetta può essere *kubernetes.pod.name*.
* Puoi utilizzare le **etichette del descrittore della metrica** per definire le etichette personalizzate. Queste etichette sono coppie di chiave-valore che si applicano direttamente alle metriche e si ottengono da integrazioni come StatsD, Prometheus, e JMX. 

## Gruppi
{: #manage_groups}

I **gruppi** organizzano gli oggetti dell'infrastruttura in gerarchie logiche. Utilizza i gruppi per strutturare la tua infrastruttura e facilitare come monitori il tuo ambiente.

Nella vista *Explore* dell'IU web, puoi eseguire una qualsiasi delle seguenti azioni:

| Attività                                                                                        | Descrizione     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Copia di un gruppo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#copy_group)                | Copia un gruppo in altri team. |
| [Crea un gruppo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#create_group)            | Crea un gruppo. |
| [Elimina un gruppo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#delete_group)            | Elimina un gruppo. |
| [Ridenomina un gruppo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#rename_group)            | Ridenomina un gruppo. |
| [Condividi un gruppo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#share_group)              | Condividi un gruppo con altri membri nel team. |
{: caption="Tabella 1. Etichette di raggruppamento delle attività" caption-side="top"} 



## Aggregazione
{: #manage_aggregation}

L'**aggregazione** dei dati si verifica automaticamente quando configuri un grafico o crei un avviso per una metrica. 

Esistono diversi tipi di aggregazione che vengono utilizzati per le metriche:  
* L'aggregazione temporale viene sempre eseguita prima dell'aggregazione gruppo.
* Per creare dei confronti tra più serie e più avvisi, puoi anche suddividere i dati aggregati in sezioni più piccole denominate **segmenti** utilizzando le etichette. 

L'aggregazione temporale viene sempre eseguita prima dell'aggregazione gruppo.

Sysdig aggrega i dati nel tempo. Successivamente, prende questi punti di dati e li raggruppa per visualizzare i dati nelle metriche, nei dashboard o calcolare le soglie dell'avviso.
{: tip}

Puoi personalizzare come i dati vengono aggregati quando configuri un grafico o crei un avviso per una metrica.





### Aggregazione temporale
{: #manage_time_aggregation}

**Per impostazione predefinita, un agent Sysdig raccoglie e riporta le metriche a una risoluzione di 10 secondi.**

Nei grafici delle serie temporali che includono i dati per 5 minuti o meno, 
* I punti di dati vengono tracciati alla risoluzione di 10 secondi
* Non si verifica l'aggregazione temporale.

L'aggregazione temporale si verifica automaticamente in una delle seguenti situazioni:

* Nei grafici delle serie temporali che includono i dati per una quantità di tempo superiore a 5 minuti, i punti di dati vengono tracciati come un aggregato per un intervallo di tempo appropriato. Ad esempio, per un grafico che mostra i dati per 1 ora, ogni punto di dati rappresenta un intervallo di 1 minuto.
* Quando visualizzi i dati cronologici, i dati eseguono il rollup nel tempo. Puoi scegliere quali punti di dati utilizzare quando visualizzi dei dati obsoleti.

La seguente tabella elenca i diversi tipi di aggregazione per i grafici delle serie temporali:

| Tipo di aggregazione | Descrizione                                                              |
|------------------|--------------------------------------------------------------------------|
| `average`          | Media dei valori della metrica richiamata nel periodo di tempo valutato. |
| `rate (timeAvg)`   | Valore medio della metrica nel periodo di tempo valutato.            |
| `maximum`	         | Il valore più elevato durante il periodo di tempo valutato.                          |
| `minimum`         | Il valore più basso durante il periodo di tempo valutato.                           |
| `sum`              | La somma combinata della metrica nel periodo di tempo valutato.             |
{: caption="Tabella 2. Tipi di aggregazione per i grafici delle serie temporali" caption-side="top"} 

**Nota:** per impostazione predefinita, viene utilizzata la media per visualizzare i punti di dati per un intervallo temporale.

La frequenza e la media sono tipi di aggregazione simili. Forniscono spesso lo stesso risultato. Tuttavia, il loro calcolo è diverso. Se l'aggregazione temporale è impostata su 1 minuto, l'agent Sysdig viene impostato per richiamare sei esempi, uno ogni 10 secondi. Tieni presente che in alcuni casi, gli esempi potrebbero non essere presenti a causa di disconnessioni o altre circostanze.


### Aggregazione gruppo
{: #manage_group_aggregation}

**Per impostazione predefinita, le metriche applicate a un gruppo di risorse, come ad esempio diversi contenitori, host o nodi, sono calcolate come una media tra i membri del gruppo.**

Ad esempio, se tre host riportano diversi utilizzi di CPU per uno stesso intervallo, viene calcolata la media dei tre valori e riportata sul grafico come un singolo punto di dati per tale metrica.

La seguente tabella elenca i diversi tipi di aggregazione gruppo:

| Tipo di aggregazione | Descrizione                                        |
|------------------|----------------------------------------------------|
| `average`          | Il valore medio degli esempi dell'intervallo.           |
| `maximum`	         | Il valore più elevato degli esempi dell'intervallo.           |
| `minimum`	         | Il valore più basso degli esempi dell'intervallo.            |
| `sum`              | Il valore combinato degli esempi dell'intervallo.          |
{: caption="Tabella 3. Tipi di aggregazione per l'aggregazione gruppo" caption-side="top"} 


**L'aggregazione gruppo dipende dalla segmentazione.** Per una vista che mostra le metriche per un gruppo di elementi, se viene modificata la selezione *Segment By* per suddividere i singoli elementi, non si verifica l'aggregazione gruppo.



## Ambito
{: #manage_scope}

L'**ambito** è una raccolta di etichette che definisce le condizioni di filtro dei punti di dati quando crei i dashboard e i pannelli, configuri gli avvisi e personalizzi i team. 

La seguente tabella elenca le attività che puoi eseguire per modificare l'ambito nel servizio di monitoraggio:

| Attività                                                                                        | Descrizione     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Modifica dell'ambito di un dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Modifica l'ambito di un dashboard per filtrare i punti di dati per tutte le metriche visualizzate tramite i pannelli sul dashboard. |
| [Modifica dell'ambito di un pannello](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Modifica l'ambito di un pannello per filtrare i dati di una metrica specifica visualizzata tramite il pannello. |
| [Modifica dell'ambito di un team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope) | Modifica l'ambito dei dati visibili agli utenti che appartengono a un team. |
{: caption="Tabella 4. Attività per modificare l'ambito" caption-side="top"} 


## Team
{: #manage_teams}

I **team** raggruppano gli utenti e controllano i dati e le autorizzazioni per utilizzare gli eventi dell'infrastruttura e le acquisizioni Sysdig per tali utenti. 

Un amministratore Sysdig può definire un qualsiasi numero di team. Per ogni team, un amministratore può configurare le seguenti informazioni:
* `The default team`: puoi impostare questo team come quello a cui viene assegnato qualsiasi utente che accede all'IU web per la prima volta. 
* `The default entrypoint`: puoi specificare la vista nell'IU web che si apre ogni volta che accede un utente. I punti di ingresso validi sono le viste *Explore*, *Dashboards*, *Events*, *Alerts* e *Settings*. 
* `The scope`: puoi limitare quali dati possono visualizzare gli utenti. Puoi scegliere *Host* o *Container* per definire il livello di dati visibile. Successivamente, puoi aggiungere una o più condizioni. Se l'ambito è impostato su *Host*, gli utenti possono visualizzare tutte le informazioni al livello host e contenitore. Se l'ambito è impostato su *Container*, gli utenti possono visualizzare solo le informazioni al livello contenitore.
* `Permissions`: puoi abilitare o disabilitare le seguenti funzioni: *acquisizioni Sysdig* e *eventi infrastruttura*. I file acquisizione sono visibili ai membri del team. **Nota:** le acquisizioni includono informazioni dettagliate da ogni contenitore su un host, indipendentemente dall'ambito del team. Quando vengono abilitati gli eventi dell'infrastruttura, gli utenti possono visualizzare tutti gli eventi dell'infrastruttura personalizzati da ogni utente e agent Sysdig nell'istanza.

Per impostazione predefinita, un team **Monitor Operations** è predefinito per ogni istanza {{site.data.keyword.mon_full_notm}}.
* Questo team non può essere eliminato.
* Gli utenti vengono automaticamente aggiunti come membri di questo team e gli viene concessa la visibilità completa su tutte le risorse disponibili nell'istanza. 

**Nota:** 
* Un amministratore deve passare al team *Monitor Operations* per creare dei team o modificare le impostazioni di altri team.
* Dopo che un utente accede a {{site.data.keyword.cloud_notm}} e avvia l'IU web Sysdig, un amministratore può gestire tale utente nell'IU web Sysdig. L'utente viene creato nel database Sysdig quando accede all'IU web Sysdig per la prima volta. 

Un amministratore può eseguire tutte le seguenti azioni per limitare la visualizzazione delle autorizzazioni di un utente: 
* Modificare il ruolo dell'utente nel team *Monitor Operations* predefinito con utente in *lettura*. 
* Creare un team predefinito con ambito e visibilità limitati. Quindi, assegnare gli utenti manualmente ad altri team. 

La seguente tabella elenca le attività che puoi eseguire quando utilizzi i team:

| Attività                                                                            | Descrizione                 |
|---------------------------------------------------------------------------------|-----------------------------|
| [Creazione di un team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_create)      | Crea un team per controllare la visibilità dei dati.  |
| [Eliminazione di un team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_delete)      | Elimina un team. </br>**Nota:** quando elimini un team, solo gli utenti che appartengono a questo team sono spostati al team predefinito.|
| [Aggiunta di membri del team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_users)   | Aggiungi ulteriori utenti a un team. |
| [Modifica di un team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope)          | Modifica l'ambito dei dati visibili agli utenti che appartengono a un team.  |
{: caption="Tabella 5. Attività per utilizzare i team" caption-side="top"} 





    


