---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# Utilizzo delle acquisizioni
{: #captures}

Un'acquisizione è un file di traccia che puoi generare per analizzare cosa succede in un host durante un intervallo di tempo. Ad esempio, puoi utilizzarla per analizzare i colli di bottiglia o le interazioni tra i componenti. Nel servizio {{site.data.keyword.mon_full_notm}}, puoi creare, esplorare, scaricare ed eliminare le *acquisizioni* per singoli nodi. 
{:shortdesc}

Per ulteriori informazioni, vedi [Acquisizioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


## Creazione di un'acquisizione
{: #captures_create}

Crea un'acquisizione nella vista *Explore*.

Completa la seguente procedura per creare un file acquisizione:

1. Passa alla sezione *EXPLORE* nell'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. Fai clic sull'icona cambia host ![icona cambia host](images/switch_hosts.png).

3. Seleziona un host o un contenitore.

4. Fai clic sull'icona azioni ![icona tre punti](images/actions.png) e seleziona **Sysdig capture**.

    Si apre la finestra *Sysdig Capture*.

5. Nella finestra *Sysdig Capture*, definisci i seguenti parametri:

    1. Nel campo *Capture path and name*, immetti il nome del file acquisizione. Puoi lasciare il valore predefinito oppure modificarlo. Il nome predefinito include la data e la data/ora di quando è stata creata l'acquisizione. 

    2. Imposta un intervallo di tempo (*Time frame*) per specificare il numero di secondi per raccogliere i dati. Il tempo di acquisizione predefinito è 15 secondi. Il tempo di acquisizione massimo è 86400 secondi (24 ore). 

    3. (Facoltativo) Aggiungi un filtro per limitare la quantità di informazioni di traccia che vengono raccolte. 

6. Fai clic su **Start capture**. All'agent Sysdig viene segnalato di avviare un'acquisizione e restituire il file di traccia risultante. 

7. Fai clic su **Go to captures page** per visualizzare l'elenco di acquisizioni nella sezione *Captures* dell'IU web. 

La pagina *Captures* mostra una tabella che elenca il nome del file acquisizione, l'host da cui è stata richiamato, l'intervallo di tempo e la dimensione dell'acquisizione. 

Lo stato di un file acquisizione può essere uno qualsiasi dei seguenti valori:
* **Requested**: un file è in fase di generazione.
* **Uploaded**:  un file è disponibile per lo scaricamento e l'analisi.
* **Error**: un file non è disponibile a causa di un timeout, i dati non sono mai stati ricevuti o si è verificato un errore con l'agent.



## Eliminazione di un'acquisizione
{: #captures_delete}

Completa la seguente procedura per eliminare un file acquisizione:

1. Passa alla sezione *CAPTURES* nell'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifica e seleziona il file acquisizione che vuoi eliminare.
3. Fai clic su **Delete**.



## Esplorazione di un'acquisizione
{: #captures_explore}

Completa la seguente procedura per esplorare un file acquisizione:

1. Passa alla sezione *CAPTURES* nell'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifica e seleziona il file acquisizione che contiene i dati per l'host che vuoi analizzare.
3. Fai clic su **EXPLORE**.



## Scaricamento di un'acquisizione
{: #captures_download}

Completa la seguente procedura per scaricare un file acquisizione:

1. Passa alla sezione *CAPTURES* nell'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifica e seleziona il file acquisizione che contiene i dati che vuoi scaricare.
3. Fai clic su **DOWNLOAD**.


## Chisel
{: #captures_chisels}

Un chisel Sysdig è uno script scritto in Lua, un linguaggio di script. Puoi utilizzarlo per analizzare i dati in un file acquisizione. 

Per ulteriori informazioni su come utilizzare un chisel, consulta questa guida utente: [Chisels User Guide ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}



## Csysdig
{: #captures_csysdig}

Csysdig è uno strumento open source per Linux progettato per il monitoraggio e il debug. Puoi utilizzarlo per analizzare i file acquisizione. 

Per ulteriori informazioni, consulta le seguenti risorse:
* [Csysdig blog ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Csysdig video ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


