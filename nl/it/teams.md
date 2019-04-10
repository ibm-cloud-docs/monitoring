---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, teams

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

# Utilizzo dei team
{: #teams}

Un amministratore o un gestore di un'istanza {{site.data.keyword.mon_full_notm}} possono creare, eliminare, aggiungere dei membri e modificare l'ambito dei team in tale istanza. 
{:shortdesc} 

Un amministratore o un gestore di un'istanza {{site.data.keyword.mon_full_notm}} devono passare al team *Monitor Operations* prima di poter creare dei team e gestire i team esistenti.
{: tip}

## Creazione di un team
{: #teams_create}

Completa la seguente procedura per creare un team:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, seleziona **Monitor Operations**. Quindi, scegli **Settings**.

3. Seleziona **Teams**. Viene visualizzato l'elenco di team esistenti.

4. Fai clic su **Add Team**. Vene visualizzata la pagina di configurazione del team.

5. Configura i dettagli del team. 

    * Scegli un colore.

    * Immetti il nome del team.

    * [Facoltativo] Immetti una descrizione per questo team.

    * [Facoltativo] Imposta il parametro **Default team** se vuoi che questo team diventi il team predefinito per i nuovi utenti.

    * Imposta il punto di ingresso predefinito (**Default Entry Point**) per specificare la vista nell'IU web che si apre ogni volta che un utente esegue l'accesso. I punti di ingresso validi sono: le viste *Explore*, *Dashboards*, *Events*, *Alerts* e *Settings*. Per impostazione predefinita, la vista è impostata su *Explore*.

6. Configura l'ambito del team. 

    * [Facoltativo] Imposta **Scope by** per specificare il livello di dati a cui hanno accesso i membri del team. I valori validi sono *host* e *container*. Se il parametro è impostato su *Host*, i membri possono visualizzare tutte le informazioni al livello host e contenitore. Se il parametro è impostato su *Container*, i membri possono visualizzare solo le informazioni al livello contenitore.

    * Configura l'ambito (**Scope**) per limitare quali dati possono visualizzare gli utenti. Puoi impostare una o più condizioni specificando delle espressioni per le metriche. Per impostazione predefinita, l'ambito è impostato su *everywhere*.
	
    * [Facoltativo] Abilita o disabilita le acquisizioni Sysdig (**Sysdig captures**). Seleziona questa casella per consentire a questo team di prendere delle acquisizioni Sysdig. I file acquisizione saranno visibili solo ai membri di questo team. **Nota:** le acquisizioni includono informazioni dettagliate da ogni contenitore su un host, indipendentemente dall'ambito del team.

    * [Facoltativo] Abilita o disabilita gli eventi dell'infrastruttura (**Infrastructure Events**). Seleziona questa casella per consentire ai membri di visualizzare tutti gli eventi dell'infrastruttura personalizzati da ogni utente e agent Sysdig. Quando non selezionata, gli utenti possono visualizzare gli eventi dell'infrastruttura inviati specificatamente a questo team. 

6. Aggiungi i membri al team. Fai clic su **Assign user**. Cerca un utente e aggiungilo.



## Modifica dell'ambito di un team
{: #teams_scope}

Per modificare l'ambito dei dati visibili ai membri di un team, completa la seguente procedura: 

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, seleziona **Monitor Operations**. Quindi, scegli **Settings**.

3. Seleziona **Teams**. Viene visualizzato l'elenco di team esistenti.

4. Identifica il team e selezionalo. Vengono visualizzati i dettagli del team.

5. Modifica i dettagli di configurazione nella sezione *Visibility*.

6. Fai clic su **Save**. 


## Aggiunta di utenti a un team
{: #teams_users}

Per aggiungere i membri a un team, completa la seguente procedura: 

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, seleziona **Monitor Operations**. Quindi, scegli **Settings**.

3. Seleziona **Teams**. Viene visualizzato l'elenco di team esistenti.

4. Identifica il team e selezionalo. Vengono visualizzati i dettagli del team.

5. Fai clic su **Assign user** nella sezione *Team users*.

6. Fai clic su **Save**. 


## Eliminazione di un team
{: #teams_delete}

Il team predefinito, **Monitor Operations**, non può essere eliminato. 

Completa la seguente procedura per eliminare un team:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, seleziona **Monitor Operations**. Quindi, scegli **Settings**.

3. Seleziona **Teams**. Viene visualizzato l'elenco di team esistenti.

4. Identifica il team che vuoi eliminare e selezionalo. Vengono visualizzati i dettagli del team.

5. Fai clic su **Delete team**.

**Nota:** quando elimini un team, solo gli utenti che appartengono a questo team saranno spostati al team predefinito.



