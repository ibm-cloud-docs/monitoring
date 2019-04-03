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


# Crea un dashboard Grafana per monitorare un cluster Kubernetes
{: #container_grafana_dashboard}


Utilizza questa esercitazione per imparare come creare un dashboard Grafana nel servizio {{site.data.keyword.monitoringlong}} per monitorare le prestazioni del tuo cluster. 
{:shortdesc}


## Obbiettivi
{: #cgd_objectives}

Impara a cercare e analizzare le metriche del contenitore per un'applicazione distribuita in un cluster Kubernetes:

1. Avvia Grafana e imposta il dominio {{site.data.keyword.monitoringshort}} in cui puoi visualizzare le metriche del cluster.
2. Crea un dashboard Grafana e definisci una metrica che monitora l'utilizzo della CPU di un contenitore.


## Presupposti
{: #cgd_assumptions}

L'esercitazione presuppone che:

* Sia disponibile un cluster nella regione Stati Uniti Sud. 
* Il tuo ID utente dispone di una politica IAM per il servizio {{site.data.keyword.monitoringshort}} con autorizzazioni da **visualizzatore**.

Per completare questa esercitazione devi prima completare l'esercitazione [Analizza le metriche in Grafana per un'applicazione distribuita in un cluster Kubernetes](/docs/services/cloud-monitoring/tutorials/container_service_metrics.html#container_service_metrics) o avere eseguito il provisioning del cluster con almeno 1 applicazione distribuita.



## Passo 1: avvia Grafana
{: #cgd_step1}

Avvia Grafana da un browser e configura il dominio {{site.data.keyword.monitoringshort}} in cui puoi visualizzare le metriche del cluster.

Per analizzare le metriche per un cluster, devi accedere a Grafana nella regione pubblica del cloud in cui viene creato il cluster. Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana da un browser web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

1. Da un browser, avvia Grafana. 

    Immetti l'URL del servizio {{site.data.keyword.monitoringshort}} della regione in cui hai creato il cluster. 
    
    Per ottenere gli URL per regione, consulta [URL per il servizio di monitoraggio](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Ad esempio, per la regione Stati Uniti Sud, avvia: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Imposta il dominio di {{site.data.keyword.monitoringshort}} su **account**.

    In Grafana, seleziona il tuo ID. Quindi, controlla di essere nell'account corretto e scegli `Domain = account`.


## Passo 2: crea un dashboard Grafana
{: #cgd_step2}

Completa la seguente procedura per creare un nuovo dashboard:

1. Seleziona il commutatore della barra dei menu laterale ![Barra di menu laterale Grafana](images/grafana_settings.gif "Barra dei menu laterale Grafana").
2. Seleziona **Dashboard**.
3. Fai clic su **Nuovo**

Si aprirà un dashboard. Il dashboard include una riga vuota che è pronta per la configurazione.

![Dashboard Grafana](images/grafana4_f1.gif "Dashboard Grafana")

In Grafana, aggiungi le righe per dividere il dashboard in sezioni. Una riga raggruppa 1 o più pannelli. In una riga, un pannello è l'unità di visualizzazione più piccola che puoi configurare per visualizzare i dati per una metrica, ad esempio puoi scegliere un pannello grafico o un pannello tabella. Puoi trascinare e rilasciare i pannelli per riorganizzarli in un dashboard. I dati visualizzati da un pannello vengono configurati tramite query. In un pannello, puoi definire una o più query. Ogni query rappresenta una serie di dati diversa. Puoi anche impostare l'intervallo di tempo per un pannello. Normalmente, l'intervallo di tempo è impostato dal selezionatore di tempo del *Dashboard*.

## Passo 3: aggiungi un grafico al dashboard per monitorare una metrica
{: #cgd_step3}

Completa la seguente procedura:

1. Seleziona **Grafico**.

2. Fai clic sul titolo del grafico e quindi seleziona **modifica**.

    Si apre la scheda *Metriche*. Qui puoi vedere l'origine dati predefinita.


![Pannello grafico che include le schede di configurazione](images/grafana4_f2.gif "Pannello grafico che include le schede di configurazione")


## Passo 4: definisci una query della metrica
{: #cgd_step4}

Definisci la query che filtra i dati da visualizzare nel grafico. Questa query monitora i nanosecondi del tempo cpu in tutti i core di un contenitore.

Per le informazioni sul formato della query, consulta [Formato della query per le metriche della CPU raccolte per i contenitori](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers).
 
Nella scheda *Metriche*, seleziona **Aggiungi query**. <br>Viene aggiunta una voce di query. Ogni query viene etichettata con una lettera. 

![Nuova voce di query](images/grafana4_query_f1.gif "Nuova voce di query") 
	
Completa la seguente procedura per definire la query:
        
1. Fai clic su **Seleziona metrica** per specificare l'origine e scegli `ibmcloud`.
    
2. Fai clic su **Seleziona metrica** per specificare il tipo di cloud e scegli `public`.
    
3. Fai clic su **Seleziona metrica** per specificare il nome del servizio e scegli `containers-kubernetes`.
	
4. Fai clic su **Seleziona metrica** per specificare la regione e scegli la regione in cui il tuo cluster è in esecuzione. Ad esempio, `us-south`.
    
5. Fai clic su **Seleziona metrica** per specificare il nome del cluster, e scegli quello in cui è in esecuzione il tuo contenitore.
		
6. Fai clic su **Seleziona metrica** per specificare l'origine della metrica. Seleziona **contenitore**.
		
7. Fai clic su **Seleziona metrica** per specificare lo spazio dei nomi. Quindi immetti il nome dello spazio dei nomi nel tuo cluster associato al tuo contenitore.
		
8. Fai clic su **Seleziona metrica** per specificare un nome del pod.
	
9. Fai clic su **Seleziona metrica** per specificare il nome del contenitore che desideri monitorare.
	
10. Fai clic su **Seleziona metrica** per specificare il tipo di metrica e quindi fai clic su **Seleziona metrica** per specificare il tipo secondario della metrica.
	
    Ad esempio, per monitorare i nanosecondi del tempo cpu in tutti i core per un contenitore, seleziona **cpu** per il tipo e **utilizzo** per il tipo secondario.
		
	Per un elenco di metriche della CPU, consulta [Metriche della CPU per i contenitori](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#cpu_metrics_containers).
    
11. Fai clic sull'immagine del segno più ![Icone Aggiungi](images/grafana_plus_image.gif "Immagine del segno più") e scegli una funzione. Puoi aggiungere una funzione per trasformare, combinare ed eseguire calcoli sui dati disponibili per una metrica.

    Ad esempio, puoi aggiungere la funzione **alias(newName)** per aggiungere un alias per una metrica. Questo alias viene utilizzato per stampare una stringa anziché il nome della metrica nella legenda visualizzata nel grafico.

    Per aggiungere un alias per la tua metrica, completa la seguente procedura:

    1. Fai clic sul simbolo più.
    2. Seleziona **Speciale**.
    3 Seleziona **alias**.
    4. Immetti una stringa, ad esempio `My sample metric`.

## Passo 5: salva il dashboard
{: #cgd_step5}

Salva il dashboard per un successivo riutilizzo.

1. Fai clic sull'immagine di salvataggio del dashboard ![Immagine di salvataggio del dashboard](images/grafana_save_image.gif "Immagine di salvataggio del dashboard").

    ![Salva dashboard](images/grafana_save_dashboard.gif "Salva dashboard")

2. Immetti il nome del dashboard.
3. Fai clic su **Salva**.



## Passi successivi
{: #cgd_next_steps}

Definisci un avviso per una metrica. Per ulteriori informazioni, vedi [Configurazione degli avvisi](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).
