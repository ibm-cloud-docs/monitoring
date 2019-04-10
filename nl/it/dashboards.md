---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, dashboards

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


# Utilizzo dei dashboard
{: #dashboards}

Utilizza i dashboard per monitorare l'infrastruttura, le applicazioni e i servizi. Puoi utilizzare dei dashboard predefiniti. Puoi anche creare dei dashboard personalizzati tramite l'IU web o in modo programmatico. Puoi eseguire il backup e ripristinare i dashboard utilizzando gli script Python.
{:shortdesc}

Un **dashboard** mostra i gruppi di metriche che forniscono informazioni sull'integrità, le prestazioni e lo stato dell'infrastruttura, delle applicazioni e dei servizi per un solo host o un gruppo di host. I dashboard offrono delle informazioni approfondite specializzate sui dati di rete, sui dati dell'applicazione, sulla topologia, sui servizi, sugli host e sui contenitori.

Nella sezione **DASHBOARDS** dell'IU web, i dashboard sono organizzati in tre gruppi principali:

* *My Dashboards*: questi sono i dashboard creati dall'utente che al momento ha eseguito l'accesso.
* *My Shared Dashboards*: questi sono i dashboard creati dall'utente che al momento ha eseguito l'accesso e che sono condivisi con altri utenti.
* *Dashboards Shared With Me*: questi sono i dashboard creati da altri utenti e condivisi con l'utente corrente.

Nella sezione **EXPLORE** dell'IU web, i dashboard sono organizzati in due gruppi:
* *Default dashboards*: questi sono i dashboard predefiniti.
* *My Dashboards*: questi sono i dashboard creati dall'utente che al momento ha eseguito l'accesso.

Puoi copiare e condividere i dashboard tramite l'IU web. 

Puoi eseguire degli script per completare tutte le seguenti azioni in modo programmatico:
* Salva i dashboard esistenti in un file locale.
* Crea dei nuovi dashboard che sono identici a quelli che hai salvato.
* Ripristina i dashboard.



## Dashboard predefiniti
{: #dashboards_predefined}

I dashboard predefiniti sono progettati per applicazioni, topologie di rete, layout dell'infrastruttura e servizi supportati di vario genere. 

I dashboard predefiniti includono una serie di pannelli già configurati.

La seguente tabella elenca i diversi tipi di dashboard predefiniti:

| Tipo | Descrizione | Ulteriori informazioni | 
|------|-------------|------------------|
| Applicazioni | Dashboard che puoi utilizzare per monitorare le applicazioni e i componenti dell'infrastruttura.  | [Dashboard dell'applicazione](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_applications) |
| Host e contenitori | Dashboard che puoi utilizzare per monitorare l'utilizzo delle risorse e l'attività di sistema sui tuoi host e nei tuoi contenitori. | [Dashboard host e contenitore](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_host_container) |
| Rete | Dashboard che puoi utilizzare per monitorare l'attività e le connessioni di rete. | [Dashboard di rete](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_network) |
| Servizio | Dashboard che puoi utilizzare per monitorare le prestazioni dei tuoi servizi, anche se vengono distribuiti in contenitori orchestrati. | [Dashboard del servizio](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_service) |
| Topologia | Dashboard che puoi utilizzare per monitorare le dipendenze logiche dei livelli dell'applicazione e delle metriche di sovrapposizione. | [Dashboard della topologia](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_topology) |
{: caption="Tabella 1. Elenco dei dashboard predefiniti" caption-side="top"} 



## Creazione di dashboard personalizzati nell'IU web
{: #dashboards_create}

Quando crei un dashboard personalizzato, puoi iniziare da un template come ad esempio un dashboard predefinito o sceglierne uno vuoto. Un dashboard include dei pannelli configurati per visualizzare dati specifici in vari formati differenti. Puoi anche configurare come vengono aggregati i dati. L'**ambito** definisce quali dati vengono utilizzati per l'aggregazione e visualizzati. Puoi configurare l'ambito al livello del dashboard o sovrascrivere dei singoli pannelli. 

Completa la seguente procedura per creare un dashboard personalizzato:

1. Passa alla sezione *DASHBOARD** nell'IU web e seleziona **Add Dashboard**. Viene aperta la pagina *Create a New Dashboard*.

    1. Seleziona un dashboard predefinito o scegli *Blank Dashboard*. 

    2. Immetti un nome per il tuo dashboard.

    3. Fai clic su **Create Dashboard**.

2. Configura l'ambito del dashboard. Fai clic su **Edit Scope** per modificare l'ambito predefinito. Per impostazione predefinita, è selezionato **Everywhere**.
    
    1. Seleziona l'ambito. 

    2. Facoltativamente, fai clic su **Override the custom panel scopes** per sovrascrivere l'ambito per tutti i pannelli che al momento hanno un ambito personalizzato definito. **Nota: questa azione non può essere annullata.** 

    **Nota:** per reimpostare l'ambito del dashboard per tutta l'infrastruttura o per aggiornare l'ambito di un dashboard esistente per tutta l'infrastruttura, seleziona **Everywhere**.

    3. Fai clic su **Save**.

3. Configura i pannelli. Ripeti questo passo per tutti i pannelli nel dashboard che vuoi modificare.

    1. Identifica il pannello che vuoi modificare.

    2. Seleziona **Edit Panel**. Questa è l'icona matita.
    
    3. Modifica il tipo di grafico.

    4. Modifica la metrica e la frequenza. La frequenza definisce il tipo di aggregazione effettuata sui dati.

    5. Modifica l'ambito del pannello. Fai clic su **Override Dashboard Scope**. Quindi, modifica l'ambito. Se devi ripristinare l'ambito del dashboard del pannello, seleziona **Default to Dashboard Scope**.

    6. Nel campo *Compare to*, fai clic su **Configure**. Imposta l'intervallo di tempo per il confronto.

    7. Imposta il colore di background del pannello in base alle soglie della metrica. Fai clic su **Override Color Coding**, poi su **Enable**. Imposta i valori per diverse soglie.

    8. Fai clic su **Save**.


## Modifica dell'ambito
{: #dashboards_scope}

Invece di modificare l'ambito di un dashboard predefinito, copia il dashboard e modifica l'ambito nel dashboard copiato.
{: tip}

Completa la seguente procedura per modificare l'ambito di un dashboard:

1. Passa alla sezione **DASHBOARD** nell'IU web e seleziona un dashboard.

2. Fai clic su **Edit Scope** per modificare l'ambito predefinito. 

    Per impostazione predefinita, è selezionato **Everywhere**.
    
3. Seleziona l'ambito. 

4. Facoltativamente, fai clic su **Override the custom panel scopes** per sovrascrivere l'ambito per tutti i pannelli che al momento hanno un ambito personalizzato definito. 

    **Nota: questa azione non può essere annullata.** 

    Per reimpostare l'ambito del dashboard per tutta l'infrastruttura o per aggiornare l'ambito di un dashboard esistente per tutta l'infrastruttura, seleziona **Everywhere**.
    {: tip}

5. Fai clic su **Save**.



## Copia di un dashboard
{: #dashboards_copy}

Quando copi un dashboard, crei un duplicato.

La seguente tabella illustra le diverse azioni e autorizzazioni utente necessarie agli utenti per copiare un dashboard:

| Azione     |	Chi può copiare     |	Istanza del dashboard	   | Chi può visualizzare il dashboard     | Chi può modificare il dashboard  |
|------------|-------------------|-------------------------|--------------------------------|-----------------------------|
| Copia per il team corrente    |	Utenti nel team con autorizzazioni da editor | Nuova istanza del dashboard  | Membri del team con autorizzazioni di visualizzazione	 | Utenti nel team con autorizzazioni da editor |
| Copia per un altro team    | Utenti nel team con autorizzazioni da editor in entrambi i team | Nuova istanza del dashboard  | Se il dashboard originale non è condiviso, ha accesso solo l'utente che copia il dashboard. </br>Se il dashboard originale è condiviso, hanno accesso tutti i membri del team. | Se il dashboard originale non è condiviso, solo l'utente che copia il dashboard. </br>Se il dashboard originale è condiviso, tutti i membri del team con autorizzazioni da editor. |
{: caption="Tabella 2. Informazioni sugli utenti e i dashboard correlati alla copia dei dashboard" caption-side="top"} 

Completa la seguente procedura per copiare un dashboard nell'IU web:

1. Passa alla sezione *DASHBOARDS* nell'IU web.
2. Seleziona il dashboard dal pannello di sinistra.
3. Fai clic su **Settings** (icona tre punti) e seleziona **Copy dashboard**. 
4. Seleziona dove copiare il dashboard.

    1. Scegli **Current Team** per copiare il dashboard per il team corrente.
    
    2. Scegli **Other Teams** per copiare il dashboard per altri team. Seleziona i team in cui vuoi copiare il dashboard.

    3. Immetti un nome per il dashboard.

    4. Fai clic su **Send copy**.
    
    5. Controlla che l'ambito del dashboard nel nuovo team sia aggiornato in base alle autorizzazioni del team di destinazione.

## Eliminazione di un dashboard
{: #dashboards_delete}

Completa la seguente procedura per eliminare un dashboard nell'IU web:

1. Passa alla sezione *DASHBOARDS* nell'IU web.
2. Seleziona il dashboard dal pannello di sinistra.
3. Fai clic su **Settings** ![icona tre punti](images/actions.png) e seleziona **Delete dashboard**. 
4. Conferma l'eliminazione facendo clic su **Yes, delete dashboard**.


## Condivisione di un dashboard
{: #dashboards_share}

Puoi condividere i dashboard tra gli utenti in un team ed esternamente configurando un URL pubblico per il dashboard.  

La seguente tabella illustra le diverse azioni e autorizzazioni utente necessarie agli utenti per condividere o utilizzare un dashboard condiviso:

| Azione      |	Chi può condividere        |	Istanza del dashboard	       | Chi può visualizzare il dashboard        | Chi può modificare il dashboard  |
|-------------|-------------------|-----------------------------|------------------------------------|-----------------------------|
| Condividi con il team corrente |	Creatore del dashboard         |	Condividi la stessa istanza del dashboard   | Membri del team con autorizzazioni di visualizzazione  | Membri del team con autorizzazioni di modifica   |
| Condividi pubblicamente come URL	  | Tutti gli utenti con autorizzazione di modifica del team |	Condividi la stessa istanza del dashboard   | Chiunque     | Nessuno                      |
{: caption="Tabella 3. Informazioni sugli utenti e i dashboard correlati alla condivisione dei dashboard" caption-side="top"} 


Completa la seguente procedura per condividere un dashboard nell'IU web:

1. Passa alla sezione *DASHBOARDS* nell'IU web.
2. Seleziona il dashboard dal pannello di sinistra.
3. Fai clic su **Settings** ![icona tre punti](images/actions.png) e seleziona **Share**.
4. Scegli con chi vuoi condividere il dashboard:

    * Attiva lo slider **Share with Team** per condividere il dashboard con il team corrente. Il team in cui è condiviso il dashboard viene visualizzato.

    * Attiva lo slider **Share Public URL** per mostrare l'URL pubblico personalizzato.

5. Fai clic su **Close**.

Condividi un dashboard esternamente per consentire ad utenti esterni di visualizzare le metriche del dashboard, mentre limiti l'accesso per la modifica di pannelli e configurazioni.
{: tip}


## Gestione dei dashboard programmatica
{: #dashboards_programmatically}

Utilizza l'API REST Sysdig per automatizzare le attività di routine e monitorare le notifiche. Puoi anche utilizzare la libreria Python Sysdig. 

**Nota:** la libreria Python espone parte delle funzionalità API REST Sysdig. 


Quando utilizzi l'API dai tuoi script o programmi personalizzati, devi utilizzare un token Sysdig per l'autenticazione con l'istanza {{site.data.keyword.mon_full_notm}}. Per ulteriori informazioni, consulta [Utilizzo dei token API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token).


| Attività                    | Utilizzo dell'API REST                |
|-------------------------|-------------------------------|
| Crea un dashboard      | [Creazione di un dashboard utilizzando l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Elimina un dashboard      | [Eliminazione di un dashboard utilizzando l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Salvataggio dei dashboard       | [Salvataggio dei dashboard di un team utilizzando l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabella 4. Attività per gestire i dashboard in modo programmatico" caption-side="top"} 


