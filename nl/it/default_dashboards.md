---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring,  predefined dashboards

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


# Dashboard predefiniti
{: #default_dashboards}
Puoi scegliere uno qualsiasi dei seguenti dashboard predefiniti per monitorare la tua infrastruttura:
{:shortdesc}


## Applicazioni
{: #default_dashboards_applications}

La seguente tabella elenca i dashboard predefiniti che puoi selezionare per monitorare le applicazioni e i componenti dell'infrastruttura:

| Nome dashboard        | Descrizione                                                            | Utilizzo             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| HTTP Overview         | Utilizza questo dashboard per monitorare l'integrità del tuo server web. Mostra il carico sul server e la sua capacità di servire le richieste in modo tempestivo. | Utilizza i pannelli Number of Requests e Avg/Max Request Time per misurare quanto è occupato il tuo server. </br>Ricerca delle correlazioni tra gli URL per trovare delle opportunità per migliorare le prestazioni. </br>Utilizza la metrica Status Codes per monitorare i codici di errore 4xx e 5xx. |  
| HTTP Top Requests  |  Utilizza questo dashboard per monitorare i principali URL richiesti dal tuo server web, come il numero totale di richieste, i tempi massimi e medi per servire le richieste e la quantità di traffico contenuta nelle richieste e nelle risposte. |   |
| MongoDB  | Utilizza questo dashboard per monitorare quanto occupato è il tuo servizio MongoDB, quali raccolte sono le più richieste e quali raccolte hanno le prestazioni peggiori.  |  Trova quali raccolte possono trovare benefici dall'ottimizzazione delle prestazioni di query e indice. |
| MySQL/PostgreSQL  | Utilizza questo dashboard per monitorare lo stato delle prestazioni e del carico generale delle tue transazioni database SQL. Scopri il numero di richieste e quanto velocemente possono essere gestite.  | Migliora le prestazioni. Ad esempio, monitora i tempi di risposta per le query più lente ed identifica le modifiche apportate alla query o agli indici nelle tabelle.  |
| MySQL/PostgreSQL Top  | Utilizza questo dashboard per monitorare le query SQL principali. Visualizza il numero di query ricevute e la quantità di traffico inviato e ricevuto dalla query.   | Trova le query più lente, quelle eseguite più volte e quelle con traffico elevato.  |
| Nginx  | Utilizza questo dashboard per monitorare le risorse host, le connessioni http, gli URL principali e più lenti e i codici di risposta host. | Identifica le modifiche al bilanciamento del carico monitorando le seguenti metriche: Writing, Reading, Waiting connections, CPU Load by Machine, Network Bytes Activity, Requests per Second </br>Cerca le pagine che potrebbero essere ottimizzate ricercando la metrica Slowest URLs. </br>Trova i problemi ricercando Response Codes.  |
{: caption="Tabella 1. Elenco dei dashboard predefiniti dei componenti dell'applicazione e dell'infrastruttura." caption-side="top"} 


## Dashboard host e contenitore
{: #default_dashboards_host_container}

La seguente tabella elenca i dashboard predefiniti che puoi utilizzare per monitorare l'utilizzo delle risorse e l'attività di sistema sui tuoi host e nei tuoi contenitori:


| Nome dashboard        | Descrizione                                                            | Utilizzo             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| *Container Limits*    | Utilizza questo dashboard per visualizzare le metriche di CPU e memoria correlate alle risorse host raccolte per ogni contenitore. | |
| *File System*         | Utilizza questo dashboard per visualizzare i punti di montaggio della directory, i dispositivi file system e le informazioni sulla capacità e l'utilizzo per i file system montati sull'istanza.  </br>I file system che vengono montati in remoto non vengono elencati per impostazione predefinita. Per visualizzare i dati per questi file system, aggiungi la seguente voce **remotefs.enabled = true** al file */opt/draios/bin/dragent.properties* su ogni istanza. </br>Quando i gruppi vengono selezionati, le metriche sono medie di punti di montaggio del file system simili.| Trova quali file system vengono riempiti e quali sono sottoutilizzati. Ordina per *fs.bytes.used*.|
| *Overview by Container* | Utilizza questo dashboard per visualizzare le statistiche di utilizzo della risorsa come la percentuale di CPU, la percentuale di utilizzo della memoria, il numero totale di byte di rete e il totale di byte del file per i contenitori eseguiti sull'istanza o il gruppo selezionato.  </br>Utilizza la funzione *Time Travel* insieme alla funzione *Compare* in questa vista per visualizzare le informazioni cronologiche. In base ai dati, verifica se i processi vengono eseguiti come previsto, hanno un comportamento non corretto o se richiedono ulteriori risorse. | Scopri quali contenitori stanno consumando molte risorse.  </br>Utilizza queste informazioni per determinare se un'applicazione deve essere spostata su un host differente. |
| *Overview by Container Image* | Utilizza questo dashboard per ottenere una panoramica della dimensione, delle prestazioni e delle limitazioni dei servizi definiti nell'immagine contenitore. | |
| Overview by Host | Utilizza questo dashboard per visualizzare le statistiche di utilizzo della risorsa generali come la percentuale di CPU, la percentuale di utilizzo della memoria, il numero totale di byte di rete, il numero di connessioni di rete, il numero totale di byte del file, l'utilizzo del disco, per un host. </br>Puoi utilizzare questo dashboard per monitorare un gruppo di istanze. </br>Utilizza la funzione *Time Travel* insieme alla funzione *Compare* in questa vista per visualizzare le informazioni cronologiche. In base ai dati, verifica se i processi vengono eseguiti come previsto, hanno un comportamento non corretto o se richiedono ulteriori risorse. | Scopri quali host non stanno venendo utilizzati o che lo sono eccessivamente all'interno di un gruppo di host con funzioni di lavoro simili. | 
| Overview by Process | Utilizza questo dashboard per visualizzare le statistiche di utilizzo della risorsa generali come la percentuale di CPU, la percentuale di utilizzo della memoria, il numero totale di byte di rete, il numero di connessioni di rete, il numero totale di byte del file, l'utilizzo del disco, per i processi principali su un host. </br>Puoi utilizzare questo dashboard per monitorare un gruppo di istanze. </br>Utilizza la funzione *Time Travel* insieme alla funzione *Compare* in questa vista per visualizzare le informazioni cronologiche. In base ai dati, verifica se i processi vengono eseguiti come previsto, hanno un comportamento non corretto o se richiedono ulteriori risorse. | Scopri quali processi stanno consumando molte risorse.  </br>Utilizza queste informazioni per determinare se un'applicazione deve essere spostata su un host differente. |
| Sysdig Agent Summary | Utilizza questo dashboard per visualizzare il numero di agent Sysdig distribuiti nel tuo ambiente e le loro versioni. |  | 
| Top Files | Utilizza questo dashboard per visualizzare l'elenco dei file principali. Puoi visualizzare il nome del file, il numero totale di byte del file, il tempo impiegato per l'I/O del file e il numero di errori del file. | Scopri i principali utilizzatori del disco quando ordini per dimensione. </br>Trova i file più occupati quando ordini per I/O. </br>Identifica degli errori potenziali monitorando i dati nella colonna *File Error Count*. |
| Top Processes | Utilizza questo dashboard per visualizzare l'elenco dei processi principali eseguiti in un host o un gruppo di host. Puoi visualizzare il nome del processo, il suo percorso e tutti gli argomenti. </br>Utilizza la funzione di filtro per limitare i processi che vengono elencati. | Trova quali processi sono i più utilizzati in un ambiente in cui lo stesso processo viene generato più volte. |
| Top Server Processes | Utilizza questo dashboard per visualizzare il consumo della risorsa per i processi identificati che devono essere orientati solo al server (httpd, java, ntpd, ecc.). | Trova l'utilizzo di risorse per i processi del server. |
{: caption="Tabella 2. Elenco di dashboard predefiniti dell'host e del contenitore" caption-side="top"} 

## Rete
{: #default_dashboards_network}

La seguente tabella elenca i dashboard predefiniti che puoi selezionare per monitorare l'attività e le connessioni di rete:

| Nome dashboard        | Descrizione                                                            | Utilizzo             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| Connections Table     | Utilizza questo dashboard per visualizzare le connessioni tra le tue istanze e i tuoi nodi remoti. Monitora il traffico per ogni connessione. | Trova gli oratori principali che utilizzano la maggior parte del traffico di rete sulla tua rete. |
| Overview              |  Utilizza questo dashboard per visualizzare l'utilizzo di rete totale nel tempo per direzione, applicazione, processo e host.| Identifica quali risorse influiscono in modo più elevato sulle prestazioni della risposta. |
| Response Times vs Resource Usage | Utilizza questo dashboard per visualizzare le metriche della risorsa host nel tempo confrontate con il tempo di risposta dell'host nell'elaborazione delle richieste di rete. |  |
| Top Ports             |  Utilizza questo dashboard per visualizzare i byte in entrata, in uscita e totali per porta nonché il numero di connessioni a ogni numero di porta. |  |
{: caption="Tabella 3. Elenco dei dashboard predefiniti di rete" caption-side="top"} 



## Servizio
{: #default_dashboards_service}


La seguente tabella elenca i dashboard predefiniti che puoi utilizzare per monitorare le prestazioni dei tuoi servizi, anche se vengono distribuiti in contenitori orchestrati:

| Nome dashboard        | Descrizione                                                            | 
|-----------------------|------------------------------------------------------------------------|
| Overview by Service   | Utilizza questo dashboard per visualizzare la dimensione, le prestazioni e le limitazioni dei servizi in esecuzione nella stessa immagine contenitore. | 
| Service Overview      | Utilizza questo dashboard per visualizzare l'utilizzo della risorsa e i tempi di risposta di un solo servizio. | 
{: caption="Tabella 4. Elenco dei dashboard predefiniti del servizio" caption-side="top"} 



## Topologia
{: #default_dashboards_topology}

La seguente tabella elenca i dashboard predefiniti che puoi utilizzare per monitorare le dipendenze logiche dei tuoi livelli dell'applicazione:

| Nome dashboard        | Descrizione                                                            | 
|-----------------------|------------------------------------------------------------------------|
| CPU Usage             | Utilizza questo dashboard per monitorare l'interazione tra il tuo host e il resto della tua infrastruttura.  | 
| Network Traffic       | Utilizza questo dashboard per monitorare l'utilizzo della larghezza di banda dell'istanza selezionata tra i processi locali e quelli su nodi remoti. |
| Response Times        | Utilizza questo dashboard per monitorare le metriche della risposta di rete e della comunicazione tra tutti i processi sugli host selezionati. </br>I conteggi e i tempi di risposta vengono mostrati come medie con fino a 1 secondo di granularità.  |
{: caption="Tabella 5. Elenco dei dashboard predefiniti della topologia" caption-side="top"} 

**Nota:** ognuno di questi dashboard mostra linee tratteggiate e caselle grigie per le istanze che non hanno un agent Sysdig installato e per cui è stata rilevata la comunicazione.















