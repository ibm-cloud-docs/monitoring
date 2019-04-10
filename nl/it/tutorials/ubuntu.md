---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# Analizza le metriche su un host Ubuntu
{: #ubuntu}

Utilizza questa esercitazione per imparare come configurare un host Ubuntu in modo che inoltri le metriche al servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Per configurare un server Ubuntu in modo che inoltri le metriche devi installare un agent Sysdig. L'agent utilizza una chiave di accesso (token) per l'autenticazione con l'istanza {{site.data.keyword.mon_full_notm}}. L'agent Sysdig agisce come un raccoglitore di dati. Raccoglie automaticamente le metriche.

Visualizzi le metriche tramite l'interfaccia utente basata sul web di Sysdig.

![Panoramica dei componenti su {{site.data.keyword.cloud_notm}}](../images/ubuntu.png "Panoramica dei componenti su {{site.data.keyword.cloud_notm}}")



## Prima di cominciare
{: #ubuntu_prereqs}

Utilizza la regione Stai Uniti Sud. 

Informazioni su {{site.data.keyword.mon_full_notm}}. Per ulteriori informazioni, vedi [Informazioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Utilizza un ID utente che è un membro o un proprietario di un account {{site.data.keyword.cloud_notm}}. Per ottenere un ID utente {{site.data.keyword.cloud_notm}}, vai a: [Registrazione ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window}.

Il tuo ID {{site.data.keyword.IBM_notm}} deve avere delle politiche IAM assegnate per ognuna delle seguenti risorse: 

| Risorsa                             | Ambito della politica di accesso | Ruolo    | Regione    | Informazioni                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Gruppo di risorse **Default**           |  Gruppo di risorse            | Visualizzatore  | us-south  | Questa politica è obbligatoria per consentire all'utente di visualizzare le istanze del servizio nel gruppo di risorse Default.    |
| Servizio {{site.data.keyword.mon_full_notm}} |  Gruppo di risorse            | Editor  | us-south  | Questa politica è obbligatoria per consentire agli utenti di eseguire il provisioning e di gestire il servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse Default.   |
{: caption="Tabella 1. Elenco delle politiche IAM necessarie per completare l'esercitazione" caption-side="top"} 

Installa la CLI {{site.data.keyword.cloud_notm}}. Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Passo 1: esegui il provisioning di un'istanza {{site.data.keyword.mon_full_notm}}
{: #ubuntu_step1}

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

8. Seleziona il piano del servizio **Lite**. 

    Per impostazione predefinita, è impostato il piano **Lite**.

    Per ulteriori informazioni sugli altri piani del servizio, vedi [Piani dei prezzi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Per eseguire il provisioning del servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse {{site.data.keyword.cloud_notm}} in cui hai eseguito l'accesso, fai clic su **Crea**.

Dopo aver eseguito il provisioning di un'istanza, si apre il dashboard *Osservabilità*. 


**Nota:** per eseguire il provisioning di un'istanza tramite la CLI, consulta [Provisioning di un'istanza tramite la CLI {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Passo 2: configura il tuo server Ubuntu e invia le metriche alla tua istanza
{: #ubuntu_step2}

Per configurare il tuo server Ubuntu in modo che invii le metriche alla tua istanza {{site.data.keyword.mon_full_notm}}, devi installare un agent Sysdig. 

Completa la seguente procedura dalla riga di comando:

1. Apri un terminale. Quindi, accedi a {{site.data.keyword.cloud_notm}}. Immetti il seguente comando e segui le istruzioni:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    Seleziona l'account in cui hai eseguito il provisioning dell'istanza {{site.data.keyword.mon_full_notm}}.

2. Ottieni la chiave di accesso Sysdig. Per ulteriori informazioni, consulta [Ottenimento della chiave di accesso tramite l'IU {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

3. Ottieni l'URL di inserimento. Per ulteriori informazioni, consulta [Endpoint raccoglitore Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

4. Distribuisci l'agent Sysdig. Immetti il seguente comando:

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    dove

    * SYSDIG_ACCESS_KEY è la chiave di inserimento per l'istanza.

    * COLLECTOR_ENDPOINT è l'URL di inserimento per la regione in cui è disponibile l'istanza di monitoraggio.

    * TAG_DATA sono tag separate da virgole formattate come *TAG_NAME:TAG_VALUE*. Puoi associare una o più tag al tuo agent Sysdig. Ad esempio: *role:serviceX,location:us-south*. In seguito, puoi utilizzare queste tag per identificare le metriche dall'ambiente in cui è in esecuzione l'agent.

    * Imposta **sysdig_capture_enabled** su *false* per disabilitare la funzione di acquisizione Sysdig. Per impostazione predefinita è impostato su *true*. Per ulteriori informazioni, consulta [Utilizzo delle acquisizioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

Se l'installazione dell'agent Sysdig non viene eseguita correttamente, installa manualmente le intestazioni kernel. Scegli una distribuzione ed esegui il comando per tale distribuzione. Quindi, ritenta la distribuzione dell'agent Sysdig.

* **Per le distribuzioni Debian e Ubuntu Linux**, immetti il seguente comando:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **Per le distribuzioni RHEL, CentOS e Fedora Linux**, immetti il seguente comando:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## Passo 3: avvia l'IU web Sysdig
{: #ubuntu_step3}

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


## Passo 4: monitora il tuo server Ubuntu
{: #ubuntu_step4}

Puoi monitorare il tuo server Ubuntu nella vista **EXPLORE** disponibile tramite l'IU web. Questa vista è il punto di partenza per risolvere i problemi e monitorare la tua infrastruttura. È la homepage predefinita dell'IU web per gli utenti.

Nella sezione *Host and containers*, puoi trovare la voce del tuo server Ubuntu. Fai clic su **Host and containers** ![Host and containers](../images/switch_hosts.png) per passare alle origini dati. Quindi, seleziona il tuo server Ubuntu. I dati visualizzati corrispondono al server Ubuntu che hai selezionato.

Ad esempio, per configurare una codifica colori per una colonna, completa la seguente procedura:

1. Seleziona una colonna. Passa con il mouse sul titolo della colonna. Quindi, seleziona l'icona matita.
2. Attiva la barra per abilitare la codifica colori.
3. Imposta i valori per le diverse soglie.



## Passi successivi
{: #ubuntu_next_steps}

Crea un dashboard personalizzato. Per ulteriori informazioni, consulta [Utilizzo dei dashboard](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Puoi anche avere ulteriori informazioni sugli avvisi. Per ulteriori informazioni, consulta [Utilizzo degli avvisi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






