---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring

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

# Monitoraggio del tuo ambiente
{: #monitoring}

Puoi monitorare la tua infrastruttura e le applicazioni in esecuzione su essa con il servizio {{site.data.keyword.mon_full_notm}}. Puoi richiedere un'acquisizione per analizzare cosa succede in un nodo durante un intervallo di tempo.
{:shortdesc}

Per prima cosa, esegui il provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}. Successivamente, configura gli agent Sysdig per le tue origini delle metriche. Dopo aver configurato le origini, puoi visualizzare, monitorare e gestire i dati tramite l'IU web del servizio.

I dati per le metriche predefinite vengono raccolti automaticamente. Puoi configurare delle metriche personalizzate e aggiungere delle etichette a quelle metriche per descriverne le caratteristiche. Anche i dati per queste metriche personalizzate vengono raccolti automaticamente.

Puoi analizzare i dati nella scheda *Explore* e nella scheda *Dashboard* dell'IU web. Monitora i dati tramite le viste e i dashboard delle metriche. 

* Utilizza una vista delle metriche per monitorare una sola metrica.
* Utilizza i dashboard per ottenere delle informazioni approfondite specializzate sui dati di rete, sui dati dell'applicazione, sulla topologia, sui servizi, sugli host e sui contenitori monitorando i dati tramite i pannelli. Un pannello visualizza una metrica o un gruppo di metriche in un dashboard.

Per ogni vista e dashboard della metrica, puoi definire l'ambito dei dati, come aggregarli e quali filtri di ora e gruppo applicare ai dati. Per ulteriori informazioni, consulta [Gestione dei dati](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

Nella scheda *Explore*, puoi monitorare i dati utilizzando le metriche e i dashboard predefiniti. Puoi utilizzare delle etichette per definire i nuovi gruppi dell'infrastruttura che puoi poi utilizzare per aggregare i dati in modo diverso e monitorare il tuo ambiente. Puoi anche utilizzare i dashboard personalizzati che definisci tramite la scheda *Dashboard*.

Nella scheda *Dashboards*, puoi monitorare i dati utilizzando uno qualsiasi dei dashboard predefiniti o creandone di nuovi.

Puoi configurare un dashboard predefinito come punto di ingresso predefinito per un team, unificando l'esperienza di un team e consentendo agli utenti di focalizzare la propria attenzione immediata sulle informazioni più importanti per loro.
{: tip}

Puoi utilizzare gli avvisi per avvertire gli utenti di problemi che richiedono attenzione tramite uno o più canali di notifica.
* La sezione *Alerts* nell'IU web mostra l'elenco degli avvisi predefiniti. Da questa vista, puoi abilitare e disabilitare gli avvisi predefiniti, puoi modificare gli avvisi esistenti e puoi crearne di nuovi.
* La sezione *Settings* nell'IU web è dove puoi configurare i canali di notifica.
 
Puoi richiede un'acquisizione di un nodo per analizzare cosa succede in tale nodo durante un intervallo di tempo. Ad esempio, puoi utilizzarla per analizzare i colli di bottiglia o le interazioni tra i componenti.

## Metriche
{: #monitoring_metrics}

Una metrica è una misura quantitativa con una o più etichette per definire le proprie caratteristiche. Utilizza le metriche per analizzare statisticamente i dati che hanno valori numerici. 

Una metrica viene rappresentata da serie temporali. Una serie temporale è una serie di punti di dati numerici in un periodo. 

Le metriche sono classificate in due gruppi: 

* [Metriche predefinite](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [Metriche personalizzate](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

Le etichette vengono classificate come etichette dell'infrastruttura e etichette del descrittore della metrica. Ogni metrica ha una serie di etichette predefinite. Per le metriche personalizzate, puoi configurare ulteriori etichette. 

Puoi utilizzare le etichette per identificare e differenziare le caratteristiche di una metrica, ad esempio,
* Puoi raggruppare gli oggetti dell'infrastruttura in gerarchie logiche. 
* Puoi filtrare i dati. 
* Puoi suddividere i dati aggregati in segmenti. 

Per ulteriori informazioni, vedi [Etichette](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels).

## Pannelli
{: #monitoring_panels}

Un pannello visualizza una metrica o un gruppo di metriche in un dashboard. 

Puoi utilizzare uno dei seguenti tipi di pannello per visualizzare le metriche:

| Tipo | Descrizione |
|------|-------------|
| `Line` | Utilizza questo pannello per visualizzare gli andamenti nel tempo di una o più metriche.  |
| `Area` | Utilizza questo pannello per visualizzare gli andamenti nel tempo di una o più metriche.  |
| `Top list` | Utilizza questo pannello per confrontare una metrica tra i gruppi di entità. Il grafico a barre viene ordinato in ordine decrescente.  |
| `Histogram` | Utilizza questo pannello per visualizzare la frequenza di distribuzione di una metrica nei bucket.  |
| `Topology` | Utilizza questo pannello per visualizzare l'infrastruttura come una mappa della topologia e le relazioni tra le entità nella mappa.  |
| `Number` | Utilizza questo pannello per visualizzare un solo numero che rappresenta il valore di una metrica aggregata nel tempo per una o più entità.  |
| `Table` | Utilizza questo pannello per visualizzare i dati numerici per la tua infrastruttura basati sulle metriche e i segmenti.  |
| `Text` | Utilizza questo pannello per aggiungere del testo. Utilizza la markdown per aggiungere il tuo testo.  |
{: caption="Tabella 1. Tipi di pannello" caption-side="top"} 

Puoi copiare, modificare l'ambito, duplicare, eliminare, esportare ed esplorare i pannelli.

Puoi esportare i dati da un pannello. Considera le seguenti informazioni quando esporti i dati:

* Puoi esportare i dati in un **file json** da un grafico a linee.
* Puoi esportare i dati in un **file csv** da un grafico a tabelle o linee.


La seguente tabella elenca le attività che puoi eseguire con i pannelli:

| Attività | Descrizione |
|------|-------------|
| [Copia il pannello](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | Copia un pannello in un nuovo dashboard.  |
| [Modifica l'ambito](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Modifica l'ambito di un pannello. |
| [Duplica il pannello](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | Copia un pannello nello stesso dashboard.  |
| [Elimina il pannello](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | Elimina un pannello dal dashboard.  |
| [Esporta i dati](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | Esporta i dati da un pannello in un file csv o json.  |
| [Crea un avviso](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | Definisci un avviso su una metrica. |
{: caption="Tabella 2. Attività del pannello" caption-side="top"} 


## Dashboard
{: #monitoring_dashboards}

Un **dashboard** mostra i gruppi di metriche che forniscono informazioni sull'integrità, le prestazioni e lo stato dell'infrastruttura, delle applicazioni e dei servizi per un solo host o un gruppo di host. I dashboard offrono delle informazioni approfondite specializzate sui dati di rete, sui dati dell'applicazione, sulla topologia, sui servizi, sugli host e sui contenitori. Utilizza i dashboard per monitorare l'infrastruttura, le applicazioni e i servizi.


Nella sezione **DASHBOARDS** dell'IU web, i dashboard sono organizzati in tre gruppi principali:

* **My Dashboards**: questi sono i dashboard creati dall'utente che al momento ha eseguito l'accesso.
* **My Shared Dashboards**: questi sono i dashboard creati dall'utente che al momento ha eseguito l'accesso e che sono condivisi con altri utenti.
* **Dashboards Shared With Me**: questi sono i dashboard creati da altri utenti e condivisi con l'utente corrente.

Nella sezione **EXPLORE** dell'IU web, i dashboard sono organizzati in due gruppi:
* **Default dashboards**: questi sono i dashboard predefiniti.
* **My Dashboards**: questi sono i dashboard creati dall'utente che al momento ha eseguito l'accesso.

Puoi utilizzare dei dashboard predefiniti. Puoi anche creare dei dashboard personalizzati tramite l'IU web o in modo programmatico. Puoi eseguire il backup e il ripristino dei dashboard utilizzando gli script Python o l'API REST Sysdig. 

Puoi anche copiare e condividere i dashboard tramite l'IU web. 

La seguente tabella illustra le attività che puoi eseguire per utilizzare i dashboard dall'IU:

| Attività | Descrizione |
|------|-------------|
| [Crea un dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | Crea un dashboard personalizzato nell'IU web. |
| [Copia un dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | Fai una copia di un dashboard nel team corrente in cui è disponibile o copialo in un altro team. |
| [Modifica dell'ambito](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Modifica l'ambito di un dashboard.       |
| [Elimina un dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  Elimina un dashboard. |
| [Condividi un dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | Condividi i dashboard tra gli utenti in un team ed esternamente configurando un URL pubblico per il dashboard. |
{: caption="Tabella 3. Attività del dashboard che puoi eseguire nell'IU web" caption-side="top"} 

La seguente tabella illustra le attività che puoi eseguire in modo programmatico per utilizzare i dashboard:

| Attività                    |	Utilizzo dell'API REST                |
|-------------------------|-------------------------------|
| Crea un dashboard      | [Creazione di un dashboard utilizzando l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Elimina un dashboard      | [Eliminazione di un dashboard utilizzando l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Salvataggio dei dashboard       | [Salvataggio dei dashboard di un team utilizzando l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabella 4. Attività per gestire i dashboard in modo programmatico" caption-side="top"} 



## Eventi
{: #monitoring_events}

Un evento è una notifica che ti informa su qualcosa che si verifica in tutti i nodi che inoltrano i dati alla tua istanza {{site.data.keyword.mon_full_notm}}.Utilizza gli eventi per controllare, tenere traccia e risolvere i problemi. 

Il seguente elenco mostra i diversi tipi di eventi: 

* Gli *eventi di avviso* sono eventi che vengono attivati dagli avvisi configurati dall'utente. Per ulteriori informazioni, consulta [Utilizzo degli avvisi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* Gli *eventi basati sull'infrastruttura* sono eventi raccolti dai nodi Docker e Kubernetes. Per impostazione predefinita, l'agent Sysdig rileva e raccoglie automaticamente i dati da un gruppo selezionato di eventi. Puoi modificare il file di configurazione dell'agent per abilitare ulteriori eventi.
* *Eventi personalizzati* che configuri tramite una delle seguenti integrazioni: Slackbot, script Python precostruiti, script Python creati dall'utente personalizzati o richieste cURL.

Per impostazione predefinita, un evento ha uno stato: 
* **Active**: questo stato indica che le circostanze che hanno attivato l'evento rimangono invariate, ad esempio, un nodo continua ad essere inattivo.
* **OK**: questo stato indica che la situazione è tornata normale, ad esempio, un nodo è operativo.

Gestisci gli eventi nella sezione *Events* dell'IU web. 
* Puoi visualizzare gli eventi di avviso tramite la scheda *Alert Events*.
* Puoi visualizzare gli eventi basati sull'infrastruttura tramite la scheda *Custom events*.
* Puoi visualizzare gli eventi personalizzati tramite la scheda *Custom events*.
* Puoi inviare gli eventi personalizzati a uno qualsiasi dei tuoi team utilizzando il [token API per tale team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token). Per ulteriori informazioni, consulta [Custom events ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.
* Puoi impostare un evento come risolto (**Resolved**) per avvisare altri utenti che il problema è stato risolto invece di attendere che lo stato venga impostato su **OK**.
{: #tip}



## Avvisi
{: #monitoring_alerts}

Un avviso è un evento di notifica che puoi utilizzare per avvertire di situazioni che richiedono attenzione. Ogni avviso ha uno stato di severità. Questo stato ti informa sulla criticità delle informazioni che riporta. 

Quando definisci un avviso, devi definire la condizione che attiva la notifica e uno o più canali di notifica tramite i quali vuoi essere avvertito. Devi inoltre definire la severità dell'avviso e il tipo di avviso. 

Puoi definire gli avvisi per tutti i seguenti tipi di avviso:

| Tipo              | Descrizione |
|-------------------|-------------|
| Rilevamento anomalie | Utilizza per monitorare gli host in base ai loro comportamenti cronologici e avvertire quando vengono modificati. |
| Tempo di inattività          | Utilizza per monitorare tutti i tipi di entità, ad esempio, host, contenitore, processo o servizio, e avvertire quando l'entità si arresta. |
| Evento             | Utilizza per monitorare le ricorrenze di eventi specifici e avvertire se il numero totale di ricorrenze viola una soglia. Ad esempio, puoi utilizzarlo per avvertire di riavvii e distribuzioni di contenitori, orchestrazioni e eventi del servizio.|
| Outlier gruppo     | Utilizza per monitorare un gruppo di host ed essere avvertito quando uno agisce in modo diverso dagli altri. |
| Metrica            | Utilizza per monitorare le metriche di serie temporali e avvertire se violano le soglie definite dall'utente. |
{: caption="Tabella 5. Tipi di avviso" caption-side="top"} 

Per impostazione predefinita, la severità è impostata su *warning*. Puoi impostare la severità di un avviso su uno dei seguenti valori: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *informational*, debug* 

Puoi definire uno o più canali di notifica per ognuna delle seguenti integrazioni di notifica:
* Notifiche email
* Notifiche PagerDuty
* Notifiche Slack
* Notifiche VictorOps
* Notifiche OpsGenie
* Configura un canale webhook

Per ulteriori informazioni, consulta [Configurazione di un canale di notifica](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create).


Puoi abilitare avvisi predefiniti, modificarli e crearne di personalizzati nell'IU web e utilizzando l'API Sysdig.

Gestisci gli avvisi nella vista *Alerts* dell'IU web. Puoi configurare le colonne della tabella che vengono visualizzate nella vista *Alerts*. Le opzioni di colonna valide sono *Name*, *Scope*, *Alert When*, *Segment By*, *Notifications*, *Enabled*, *Modified*, *Captures*, *Channels*, *Created*, *Description*, *Email recipients*, *For at least*, *OpsGenie*, *PagerDuty*, *Severity*, *Slack*, *WebHook*, *SNS topics*, *Type* e *VictorOps*.

Il seguente elenco illustra le attività principali quando utilizzi gli avvisi:
* [Configure an alert ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [Enable or disable an alert ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [Search for an alert ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [Modify an alert ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [Copy an Alert to the same team ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [Copy an Alert to a Different Team ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [Export an alert ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [Delete an alert ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [Define alert thresholds as custom boolean expressions ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## Acquisizioni
{: #monitoring_captures}

Un'acquisizione è un file di traccia che puoi generare per analizzare cosa succede in un nodo durante un intervallo di tempo. Il limite della dimensione del file acquisizione è 100 MB. Ad esempio, puoi utilizzarla per analizzare i colli di bottiglia o le interazioni tra i componenti. 

Le acquisizioni contengono chiamate di sistema e altri eventi SO come le latenze al livello del sistema, la durata dei lavori batch, i tempi di interruzione delle distribuzioni, le latenze del ridimensionamento automatico, i tempi di avvio del contenitore o il tempo di transazione dell'applicazione. Le acquisizioni includono informazioni dettagliate da ogni contenitore su un nodo. 

A seconda delle linee guida della tua organizzazione, considera di disabilitare le acquisizioni. Per impostazione predefinita, le acquisizioni vengono abilitate quando configuri un agent Sysdig in un nodo.
{: tip}

Puoi creare, esplorare, scaricare ed eliminare le *acquisizioni* per singoli nodi. Un nodo può essere un host, un contenitore, una macchina virtuale, un server bare metal o una qualsiasi origine della metrica in cui hai installato un agent Sysdig. 

* Nell'IU web, crea le acquisizioni nella sezione *Explore* e gestisci i file acquisizione tramite la sezione *Captures*.
* Puoi visualizzare i dati da un'acquisizione utilizzando *Csysdig* (l'IU della riga di comando basata su curses per sysdig) o le funzionalità Sysdig open source per analizzare i dati in un'acquisizione.
* Puoi ricercare i dati in un'acquisizione utilizzando i filtri.
* Puoi manipolare i dati in un'acquisizione utilizzando i chisel (script). 

Quando abiliti la funzione di acquisizione per un team, i file acquisizione sono visibili solo ai membri di tale team.

Il seguente elenco illustra le attività principali quando utilizzi le acquisizioni:
* [Creazione di un'acquisizione](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [Eliminazione di un'acquisizione](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [Esplorazione di un'acquisizione](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [Scaricamento di un'acquisizione](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

Per ulteriori informazioni, consulta [Utilizzo delle acquisizioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


