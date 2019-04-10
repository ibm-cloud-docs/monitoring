---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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


# Analizza le metriche per un'applicazione distribuita in un cluster Kubernetes
{: #kubernetes_cluster}

Utilizza questa esercitazione per imparare come configurare un cluster per inoltrare le metriche al servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Puoi utilizzare il servizio {{site.data.keyword.mon_full_notm}} per monitorare i cluster Kubernetes.

Per configurare un cluster che inoltri le metriche, devi installare un agent su ogni nodo di lavoro nel tuo cluster Kubernetes utilizzando una serie di daemon. L'agent Sysdig utilizza una chiave di accesso (token) per l'autenticazione con l'istanza {{site.data.keyword.mon_full_notm}}. L'agent Sysdig agisce come un raccoglitore di dati. Raccoglie automaticamente le metriche come *CPU di lavoro* e memoria di lavoro*, *il traffico HTTP in entrata e in uscita dai tuoi contenitori* e diverse parti di software dell'infrastruttura comuni. Inoltre, l'agent può raccogliere le metriche dell'applicazione personalizzate utilizzando uno scraper compatibile con Prometheus o uno statsd facade. 

Visualizzi le metriche tramite l'interfaccia utente basata sul web di Sysdig.

![Panoramica dei componenti su {{site.data.keyword.cloud_notm}}](../images/kube.png "Panoramica dei componenti su {{site.data.keyword.cloud_notm}}")



## Prima di cominciare
{: #kubernetes_cluster_prereqs}

Per completare la procedura in questa esercitazione introduttiva, vengono fornite le istruzioni per eseguire il provisioning di un'istanza di {{site.data.keyword.mon_full_notm}} nella regione Stati Uniti Sud. Puoi utilizzare un cluster esistente o un nuovo **cluster versione 1.10**. Il cluster può essere disponibile in una regione diversa.  

Informazioni su {{site.data.keyword.mon_full_notm}}. Per ulteriori informazioni, vedi [Informazioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Utilizza un ID utente che è un membro o un proprietario di un account {{site.data.keyword.cloud_notm}}. Per ottenere un ID utente {{site.data.keyword.cloud_notm}}, vai a: [Registrazione ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window}.

Il tuo ID {{site.data.keyword.IBM_notm}} deve avere delle politiche IAM assegnate per ognuna delle seguenti risorse: 

| Risorsa                             | Ambito della politica di accesso | Ruolo    | Regione    | Informazioni                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Gruppo di risorse **Default**           |  Gruppo di risorse            | Visualizzatore  | us-south  | Questa politica è obbligatoria per consentire all'utente di visualizzare le istanze del servizio nel gruppo di risorse Default.    |
| Servizio {{site.data.keyword.mon_full_notm}} |  Gruppo di risorse            | Editor  | us-south  | Questa politica è obbligatoria per consentire agli utenti di eseguire il provisioning e di gestire il servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse Default.   |
| Istanza cluster Kubernetes          |  Risorsa                 | Editor  | us-south  | Questa politica è obbligatoria per configurare il segreto e l'agent Sysdig nel cluster Kubernetes. |
{: caption="Tabella 1. Elenco delle politiche IAM necessarie per completare l'esercitazione" caption-side="top"} 

Per ulteriori informazioni sui ruoli IAM {{site.data.keyword.containerlong}}, consulta [Autorizzazioni di accesso utente](/docs/containers?topic=containers-access_reference#access_reference).

Installa la CLI {{site.data.keyword.cloud_notm}} e il plugin CLI Kubernetes. Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Passo 1: esegui il provisioning di un'istanza {{site.data.keyword.mon_full_notm}}
{: #kubernetes_cluster_step1}

Per eseguire il provisioning di un'istanza {{site.data.keyword.mon_full_notm}} tramite l'IU {{site.data.keyword.cloud_notm}}, completa la seguente procedura:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperta l'IU {{site.data.keyword.cloud_notm}}.

2. Fai clic su **Catalogo**. Viene aperto l'elenco dei servizi disponibili in {{site.data.keyword.cloud_notm}}.

3. Per filtrare l'elenco dei servizi che viene visualizzato, seleziona la categoria **Strumenti per gli sviluppatori**.

4. Fai clic sul tile **{{site.data.keyword.mon_full_notm}}**. Si apre il dashboard *Osservabilità*.

5. Seleziona **Crea istanza**. 

6. Immettere un nome per l'istanza del servizio.

7. Seleziona il gruppo di risorse **Default**. 

    Per impostazione predefinita, è impostato il gruppo di risorse **Default**.

8. Seleziona il piano del servizio **Trial**. 

    Per impostazione predefinita, è impostato il piano **Trial**.

    Per ulteriori informazioni sugli altri piani del servizio, vedi [Piani dei prezzi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Per eseguire il provisioning del servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse {{site.data.keyword.cloud_notm}} in cui hai eseguito l'accesso, fai clic su **Crea**.

Dopo aver eseguito il provisioning di un'istanza, si apre il dashboard *Osservabilità*. 


**Nota:** per eseguire il provisioning di un'istanza tramite la CLI, consulta [Provisioning di un'istanza tramite la CLI {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Passo 2: configura il tuo cluster Kubernetes e invia le metriche alla tua istanza
{: #kubernetes_cluster_step2}

Per configurare il tuo cluster Kubernetes e inviare le metriche alla tua istanza {{site.data.keyword.mon_full_notm}}, devi installare un pod dell'agent Sysdig su ogni nodo del tuo cluster. L'agent Sysdig viene installato tramite una serie di daemon che garantiscono che un'istanza dell'agent sia in esecuzione su ogni nodo di lavoro. L'agent Sysdig raccoglie le metriche dal pod su cui è installato e inoltra i dati alla tua istanza.

**Nota:** per fornire una suite completa di metriche del sistema, l'agent Sysdig deve avere uno stato privilegiato.

Per configurare il tuo cluster Kubernetes in modo che inoltri le metriche alla tua istanza {{site.data.keyword.mon_full_notm}}, completa la seguente procedura dalla riga di comando:

1. Apri un terminale. Quindi, accedi a {{site.data.keyword.cloud_notm}}. Immetti il seguente comando e segui le istruzioni:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    Seleziona l'account in cui hai eseguito il provisioning dell'istanza {{site.data.keyword.mon_full_notm}}.

2. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scarica i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

3. Ottieni la chiave di accesso Sysdig. Per ulteriori informazioni, consulta [Ottenimento della chiave di accesso tramite l'IU {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

4. Ottieni l'URL di inserimento. Per ulteriori informazioni, consulta [Endpoint raccoglitore Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

5. Distribuisci l'agent Sysdig. Immetti il seguente comando:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    dove

    * SYSDIG_ACCESS_KEY è la chiave di inserimento per l'istanza.

    * COLLECTOR_ENDPOINT è l'URL di inserimento per la regione in cui è disponibile l'istanza di monitoraggio.

    * TAG_DATA sono tag separate da virgole formattate come *TAG_NAME:TAG_VALUE*. Puoi associare una o più tag al tuo agent Sysdig. Ad esempio: *role:serviceX,location:us-south*. In seguito, puoi utilizzare queste tag per identificare le metriche dall'ambiente in cui è in esecuzione l'agent.

    * Imposta **sysdig_capture_enabled** su *false* per disabilitare la funzione di acquisizione Sysdig. Per impostazione predefinita è impostato su *true*. Per ulteriori informazioni, consulta [Utilizzo delle acquisizioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

6. Verifica che l'agent Sysdig sia stato creato correttamente e controllane lo stato. Immetti il seguente comando:

    ```
    kubectl get pods
    ```
    {: codeblock}



## Passo 3: avvia l'IU web Sysdig
{: #kubernetes_cluster_step3}

Completa la seguente procedura per avviare l'IU web:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperto il dashboard {{site.data.keyword.cloud_notm}}.

2. Nel menu di navigazione, seleziona **Osservabilità**. 

3. Seleziona **Monitoraggio**. 

    Viene visualizzato l'elenco di istanze disponibili su {{site.data.keyword.cloud_notm}}.

4. Seleziona la tua istanza. Quindi, fai clic su **Visualizza Sysdig**.

Se l'agent Sysdig è configurato correttamente, si apre la vista *EXPLORE*.

Tuttavia, se l'agent Sysdig non è installato correttamente, punta all'endpoint di inserimento non corretto o la chiave di accesso non è corretta, la pagina che si apre ti avverte su cosa fare successivamente.

Puoi avere solo una sessione IU web aperta per browser.
{: tip}


## Passo 4: monitora il tuo cluster
{: #kubernetes_cluster_step4}

Puoi monitorare il tuo cluster nella vista **EXPLORE** disponibile tramite l'IU web. Questa vista è il punto di partenza per risolvere i problemi e monitorare la tua infrastruttura. È la homepage predefinita dell'IU web per gli utenti.

Nella sezione *Host and containers*, puoi vedere l'elenco dei nodi di lavoro nel tuo cluster che stanno inoltrando le metriche all'istanza di monitoraggio. Ogni voce di lavoro rappresenta un gruppo di oggetti dell'infrastruttura correlati per tale nodo di lavoro.

Fai clic su **Host and containers** ![Host and containers](../images/switch_hosts.png) per passare alle origini dati. Quindi, seleziona un nodo di lavoro. I dati visualizzati corrispondono al nodo di lavoro che hai selezionato.

Se fai clic su ** Back to Explore Table**, viene visualizzata la tabella di esplorazione (*Explore table*). Ogni colonna mostra una metrica diversa. Puoi configurare ogni metrica individualmente. Puoi modificare l'ordine delle colonne. Tieni presente che quando apporti delle modifiche all'ordine delle colonne esistenti, la modifica è persistente tra i raggruppamenti diversi mentre sei collegato. Se aggiungi o rimuovi una colonna la modifica è persistente. Puoi anche configurare dei colori per evidenziare dei valori e migliorare la leggibilità.

Ad esempio, per configurare una codifica colori per una colonna, completa la seguente procedura:

1. Seleziona una colonna. Passa con il mouse sul titolo della colonna. Quindi, seleziona l'icona matita.
2. Attiva la barra per abilitare la codifica colori.
3. Imposta i valori per le diverse soglie.

Se selezioni un nodo di lavoro, viene visualizzato un dashboard predefinito. Fai clic su ![cambia dashboard](images/switch_dashboards_1.png) ed esplora i diversi dashboard e metriche predefiniti. Tieni presente che puoi solo selezionare le metriche e i dashboard pertinenti per il nodo di lavoro selezionato.


## Passi successivi
{: #kubernetes_cluster_next_steps}

Crea un dashboard personalizzato. Per ulteriori informazioni, consulta [Utilizzo dei dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Puoi anche avere ulteriori informazioni sugli avvisi. Per ulteriori informazioni, consulta [Utilizzo degli avvisi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






