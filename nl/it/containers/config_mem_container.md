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



# Configurazione delle metriche della memoria per un contenitore in Grafana
{: #config_mem_container}

In {{site.data.keyword.Bluemix}}, le metriche della memoria selezionate per un contenitore vengono raccolte automaticamente. Per monitorarle tramite {{site.data.keyword.monitoringlong}}, devi definire una query Grafana. 
{:shortdesc}

Per un elenco di metriche della memoria, consulta [Metriche della memoria](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics)


## Passo 1: raccogli i dati per il contenitore che desideri monitorare
{: #step17}

Ottieni le seguenti informazioni per il contenitore che desideri monitorare:

* **Regione** in cui è in esecuzione il cluster.
* **Nome del cluster** in cui è in esecuzione il contenitore. 
* **Spazio dei nomi** in cui viene distribuito il contenitore. 

    Uno spazio dei nomi viene utilizzato per raggruppare le risorse del cluster.
	
* **Nome del pod** che viene associato al contenitore che desideri monitorare. 

    Un pod definisce un gruppo di 1 o più contenitori, con rete e memoria condivise e i dettagli su come eseguire i contenitori nel cluster.
	
* **Nome del contenitore** del contenitore che desideri monitorare.

Scopri se le metriche vengono inoltrate a un dominio dello spazio o dell'account.

Per identificare dove il tuo cluster inoltra le metriche, immetti il seguente comando:

```
$ ibmcloud cs cluster-get ClusterName --json
```
{: codeblock}

dove *ClusterName* è il nome del tuo cluster.

Nell'output, i seguenti campi forniscono le informazioni su dove le metriche vengono inoltrate:

* **logOrg** definisce l'ID di un'organizzazione CF.
* **logOrgName** definisce il nome di un'organizzazione CF.
* **logSpace** definisce l'ID di uno spazio CF.
* **logSpaceName** definisce il nome di uno spazio CF.

Se i campi sono vuoti, le metriche vengono inoltrate al dominio dell'account.
Se i campi hanno uno spazio o un'organizzazione CF impostati, le metriche vengono inoltrate al dominio dello spazio associato a questo spazio.

## Passo 2: avvia Grafana
{: #step26}

Avvia Grafana da un browser. Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana da un browser web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

Assicurati che, in Grafana, tu abbia eseguito l'accesso all'account in cui è in esecuzione il cluster. 

1. Da un browser, avvia Grafana. 

    Immetti l'URL del servizio {{site.data.keyword.monitoringshort}} della regione in cui hai creato il cluster. 
    
    Per ottenere gli URL per regione, consulta [URL per il servizio di monitoraggio](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Ad esempio, per la regione Stati Uniti Sud, avvia: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Imposta il dominio {{site.data.keyword.monitoringshort} in cui puoi visualizzare le metriche del cluster.

    In Grafana, seleziona il tuo ID. Quindi, controlla di essere nell'account corretto e scegli un dominio.

    I cluster con uno spazio CF associato inoltrano le metriche al dominio delle metriche dello spazio. Seleziona `Domain = space` e lo spazio e l'organizzazione associati al tuo cluster.

    I cluster creati al livello dell'account inoltrano le metriche al dominio delle metriche dell'account. Seleziona `Domain = account`




## Passo 3: definisci una query in Grafana per una metrica della CPU
{: #step35}

Completa la seguente procedura per creare un dashboard Grafana e definisci una query per monitorare l'utilizzo della CPU di un nodo di lavoro:

1. Crea un nuovo dashboard.

    * Seleziona il commutatore della barra dei menu laterale ![Barra di menu laterale Grafana](images/grafana_settings.gif "Barra dei menu laterale Grafana").
    * Seleziona **Dashboard**.
    * Fai clic su **Nuovo**

    Si aprirà un dashboard. Il dashboard include una riga vuota che è pronta per la configurazione.

2. Aggiungi un pannello *Grafico* per monitorare una metrica della CPU per un pod.

    1. Seleziona **Grafico**.

    2. Fai clic sul titolo del grafico e quindi seleziona **modifica**.

        Si apre la scheda *Metriche*. Qui puoi vedere l'origine dati predefinita.

3. Definisci la query che filtra i dati da visualizzare nel grafico. 

    Per le informazioni sul formato della query, consulta [Formato della query per le metriche della memoria raccolte per i contenitori](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers).

    Nella scheda *Metriche*, seleziona **Aggiungi query**. <br>Viene aggiunta una voce di query. Ogni query viene etichettata con una lettera.
	
	Completa la seguente procedura per definire la query:

    1. Fai clic su **Seleziona metrica** per specificare l'origine e scegli `ibmcloud`.
    
    2. Fai clic su **Seleziona metrica** per specificare il tipo di cloud e scegli `public`.
    
    3. Fai clic su **Seleziona metrica** per specificare il nome del servizio e scegli `containers-kubernetes`.
	
    4. Fai clic su **Seleziona metrica** per specificare la regione e scegli la regione in cui il tuo cluster è in esecuzione. Ad esempio, seleziona `us-south` per un cluster disponibile nella regione Stati Uniti Sud.
    
    5. Fai clic su **Seleziona metrica** per specificare il nome del cluster, e scegli quello in cui è in esecuzione il tuo contenitore.
		
	6. Fai clic su **Seleziona metrica** per specificare l'origine della metrica. Seleziona **contenitore**.
		
	7. Fai clic su **Seleziona metrica** per specificare lo spazio dei nomi. Quindi immetti il nome dello spazio dei nomi nel tuo cluster associato al tuo contenitore.
		
	8. Fai clic su **Seleziona metrica** per specificare un nome del pod.
	
	9. Fai clic su **Seleziona metrica** per specificare il nome del contenitore che desideri monitorare.
	
	10. Fai clic su **Seleziona metrica** per specificare il tipo di metrica e quindi fai clic su **Seleziona metrica** per specificare il tipo secondario della metrica.
	
	    Ad esempio, per monitorare i byte di memoria che un contenitore sta al momento utilizzando, seleziona **memoria** per il tipo e **corrente** per il tipo secondario.
	
	    Per un elenco di metriche della memoria, consulta [Metriche della memoria per i contenitori](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics) 
	
	11. Fai clic sull'immagine del segno più ![Icone Aggiungi](images/grafana_plus_image.gif "Immagine del segno più") e scegli una funzione. Puoi aggiungere una funzione per trasformare, combinare ed eseguire calcoli sui dati disponibili per una metrica.

        Ad esempio, puoi aggiungere la funzione **alias(newName)** per aggiungere un alias per una metrica. Questo alias viene utilizzato per stampare una stringa anziché il nome della metrica nella legenda visualizzata nel grafico.

        Per aggiungere un alias per la tua metrica, completa la seguente procedura:

        1. Fai clic sul simbolo più.
        2. Seleziona **Speciale**.
        3 Seleziona **alias**.
        4. Immetti una stringa, ad esempio `My sample metric`.

4. Salva il dashboard per un successivo riutilizzo.

    1. Fai clic sull'immagine di salvataggio del dashboard ![Immagine di salvataggio del dashboard](images/grafana_save_image.gif "Immagine di salvataggio del dashboard").
    2. Immetti il nome del dashboard.
    3. Fai clic su **Salva**.

	
