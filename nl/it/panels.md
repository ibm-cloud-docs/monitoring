---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, panels

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


# Gestione dei pannelli
{: #panels}

Utilizza un pannello per visualizzare una metrica o un gruppo di metriche in un dashboard. Puoi copiare, modificare l'ambito, duplicare, eliminare, esportare ed esplorare i pannelli.
{:shortdesc}

Puoi utilizzare uno dei seguenti tipi di pannello:

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



## Copia un pannello in un dashboard.
{: #panels_copy}

Completa la seguente procedura per copiare un pannello:

1. Passa alla sezione *DASHBOARD** nell'IU web. Seleziona un dashboard. Quindi, identifica il pannello che visualizza la metrica che vuoi copiare.

2. Seleziona l'icona *More options* ![icona tre punti](images/actions.png) e seleziona **Copy panel** ![icona di copia](images/actions.png).

3. Seleziona uno dei dashboard che vengono elencati o immetti un nome per un nuovo dashboard. 

4. Fai clic su **Copy and Open**.



## Modifica l'ambito di un pannello
{: #panels_scope}

Completa la seguente procedura per modificare l'ambito di un pannello:

1. Passa alla sezione *DASHBOARD** nell'IU web. Seleziona un dashboard. Quindi, identifica il pannello che visualizza la metrica di cui vuoi modificare l'ambito.

2. Nel pannello, fai clic su **Edit Scope** per modificare l'ambito predefinito. 

    Per impostazione predefinita, è selezionato **Everywhere**.
    
3. Seleziona l'ambito. 

4. Facoltativamente, fai clic su **Override the custom panel scopes** per sovrascrivere l'ambito per tutti i pannelli con un ambito personalizzato definito. 

    **Nota: questa azione non può essere annullata.** 

    Per reimpostare l'ambito del dashboard per tutta l'infrastruttura o per aggiornare l'ambito di un dashboard esistente per tutta l'infrastruttura, seleziona **Everywhere**.
    {: tip}

5. Fai clic su **Save**.



## Duplica il pannello
{: #panels_duplicate}

Completa la seguente procedura per duplicare un pannello nel dashboard corrente:

1. Passa alla sezione *DASHBOARD** nell'IU web. Seleziona un dashboard. Quindi, identifica il pannello che visualizza la metrica che vuoi copiare.

2. Seleziona l'icona *More options* ![icona tre punti](images/actions.png) e seleziona **Duplicate panel** ![icona di copia](images/duplicate.png).


## Elimina il pannello
{: #panels_delete}

Completa la seguente procedura per eliminare un pannello nel dashboard corrente:

1. Passa alla sezione *DASHBOARD** nell'IU web. Seleziona un dashboard. Quindi, identifica il pannello che visualizza la metrica che vuoi copiare.

2. Seleziona l'icona *More options* ![icona tre punti](images/actions.png) e seleziona **Delete panel** ![icona di copia](images/delete.png).

3. Fai clic su **Yes, delete panel** per confermare l'eliminazione del pannello.



## Esporta i dati da un pannello
{: #panels_export}

Considera le seguenti informazioni quando esporti i dati:

* Puoi esportare i dati in un **file json** da un grafico a linee.
* Puoi esportare i dati in un **file csv** da un grafico a tabelle o linee.

Completa la seguente procedura per esportare i dati da un pannello:

1. Passa alla sezione *DASHBOARD** nell'IU web. Seleziona un dashboard. Quindi, identifica il pannello che visualizza la metrica che vuoi copiare.

2. Seleziona l'icona *More options* ![icona tre punti](images/actions.png).

3. Scegli una delle seguenti opzioni:

    * Seleziona **Export JSON** per esportare i dati in un file formattato JSON.

    * Seleziona **Export CSV** per esportare i dati in un file formattato csv.

4. Fai clic su **Save the file**.




## Crea avviso
{: #panels_alert}

Puoi creare gli avvisi direttamente da un pannello.

Completa la seguente procedura per creare un avviso:

1. Passa alla sezione *DASHBOARD** nell'IU web. Seleziona un dashboard. Quindi, identifica il pannello che visualizza la metrica che vuoi copiare.

2. Seleziona l'icona *More options* ![icona tre punti](images/actions.png).

3. Seleziona **Create Alert**.

4. Configura l'avviso.

5. Fai clic su **Create**.


