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


# Configurazione di una query della metrica in Grafana
{: #define_query}

In {{site.data.keyword.Bluemix}}, le metriche da servizi cloud selezionati vengono raccolte automaticamente. Per monitorarle tramite {{site.data.keyword.monitoringlong}}, devi definire una query Grafana. 
{:shortdesc}

## Passo 1: raccogli i dati per il servizio o l'applicazione CF che desideri monitorare
{: #step18}

Ottieni le seguenti informazioni per il servizio o l'applicazione CF che desideri monitorare:

* **Regione** in cui è in esecuzione l'applicazione CF.
* **Organizzazione** in cui è in esecuzione l'applicazione CF. 	
* **Spazio** in cui è in esecuzione l'applicazione CF. 
* **Nome dell'applicazione CF** dell'applicazione che desideri monitorare o il **Nome del servizio**. 


## Passo 2: avvia Grafana
{: #step27}

Avvia Grafana da un browser. Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana da un browser web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

Assicurati che, in Grafana, tu abbia eseguito l'accesso all'account, all'organizzazione e alla regione in cui è in esecuzione il servizio o l'applicazione CF. 


## Passo 3: definisci una query in Grafana
{: #step36}

Completa la seguente procedura per creare un dashboard Grafana e per definire una query:

1. Crea un nuovo dashboard.

    * Seleziona il commutatore della barra dei menu laterale ![Barra dei menu laterale Grafana](images/grafana_settings.gif "Barra dei menu laterale Grafana").
    * Seleziona **Dashboard**.
    * Fai clic su **Nuovo**

    Si aprirà un dashboard. Il dashboard include una riga vuota che è pronta per la configurazione.

2. Aggiungi un pannello *Grafico*.

    1. Seleziona **Grafico**.

    2. Fai clic sul titolo del grafico e quindi seleziona **modifica**.

        Si apre la scheda *Metriche*. Qui puoi vedere l'origine dati predefinita.

3. Definisci la query che filtra i dati da visualizzare nel grafico. 

    Nella scheda *Metriche*, seleziona **Aggiungi query**. <br>Viene aggiunta una voce di query. Ogni query viene etichettata con una lettera.
    
    ![Nuova voce di query](images/grafana4_query_f1.gif "Nuova voce di query")
        
    1. Fai clic su **Seleziona metrica** e scegli l'origine: `ibmcloud`.
    
    2. Fai clic su **Seleziona metrica** e scegli il tipo di cloud: `public`.
    
    3. Fai clic su **Seleziona metrica** e scegli il nome del servizio, ad esempio, `cloud-foundry` per le metriche dell'applicazione CF o `message hub` per le metriche {{site.data.keyword.messagehub}}.
    
    4. Fai clic su **Seleziona metrica** e scegli la regione da cui stai lavorando, ad esempio, `ng` per la regione Stati Uniti Sud.
    
    5. Seleziona i campi del servizio specifici che si applicano al servizio o all'applicazione CF che desideri monitorare.

        <table>
          <caption>Formati della query della metrica per il servizio o l'applicazione CF</caption>
          <tr>
            <th>Nome servizio</th>
            <th>Link al formato della query della metrica</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Formato della query per le metriche della CPU raccolte per i contenitori](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers) </br>[Formato della query delle metriche del carico per i nodi di lavoro](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers) </br>[Formato della query per le metriche della memoria raccolte per i contenitori](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)</td> 
          </tr>
          <tr>
            <td>Applicazioni CF</td>
            <td>[Formato della query per le applicazioni CF](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format)</td> 
          </tr>
        </table>

        Ad esempio, per un'applicazione CF, scegli:
    
        Fai clic su **Seleziona metrica** e scegli il nome dell'applicazione CF, ad esempio, `logtester`.
    
        Fai clic su **Seleziona metrica** e scegli l'indice dell'istanza dell'applicazione CF, ad esempio, `0`.

        Fai clic su **Seleziona metrica** e scegli `container`.
    
    9. Fai clic su **Seleziona metrica** e scegli un tipo di metrica. Ad esempio, **cpu** per le metriche della CPU, **memoria** per le metriche della memoria e **disco** per le metriche del disco. 

        **Nota:** salta questo passo per le applicazioni CF. 

    10. Fai clic su **Seleziona metrica** e scegli una metrica. 

        <table>
          <caption>Elenco delle metriche per servizio o applicazione CF</caption>
          <tr>
            <th>Nome servizio</th>
            <th>Link alle metriche</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Metriche CPU](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Metriche del disco](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[Metriche della memoria](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>Applicazioni CF</td>
            <td>[Metriche CPU](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Metriche del disco](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[Metriche della memoria](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Metriche per un argomento Kafka](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_topic_metrics) </br>[Metriche per una partizione Kafka](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. Fai clic sull'immagine del segno più ![Icone Aggiungi](images/grafana_plus_image.gif "Immagine del segno più") e scegli una funzione. Puoi aggiungere una funzione per trasformare, combinare ed eseguire calcoli sui dati disponibili per una metrica.
        
        Ad esempio, puoi aggiungere la funzione **alias(newName)** per aggiungere un alias per una metrica. Questo alias viene utilizzato per stampare una stringa anziché il nome della metrica nella legenda visualizzata nel grafico.
        
        Per aggiungere un alias per la tua metrica, completa la seguente procedura:
        
        1. Fai clic sul simbolo più.
        2. Seleziona **Speciale**. 
        3 Seleziona **alias**.
        4. Immetti una stringa, ad esempio `My sample metric`.


## Passo 4: salva il dashboard per un successivo riutilizzo
{: #step44}

Completa la seguente procedura:

1. Fai clic sull'immagine di salvataggio del dashboard ![Immagine di salvataggio del dashboard](images/grafana_save_image.gif "Immagine di salvataggio del dashboard").
2. Immetti il nome del dashboard.
3. Fai clic su **Salva**.
