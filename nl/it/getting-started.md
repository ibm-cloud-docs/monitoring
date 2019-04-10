---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, getting started

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


# Esercitazione introduttiva
{: #getting-started}

{{site.data.keyword.mon_full_notm}} è un sistema di gestione di terze parti, nativo cloud e di intelligence del contenitore che puoi includere come parte della tua architettura {{site.data.keyword.cloud_notm}}. Utilizzalo per ottenere visibilità operativa sulle prestazioni e sull'integrità delle applicazioni, dei servizi e delle piattaforme. Offre agli amministratori, agli sviluppatori e ai team DevOps una telemetria di stack completa con funzioni avanzate per il monitoraggio e la risoluzione dei problemi, la definizione di avvisi e la progettazione di dashboard personalizzati. {{site.data.keyword.mon_full_notm}} è gestito da Sysdig in collaborazione con {{site.data.keyword.IBM_notm}}.
{:shortdesc}

La seguente figura mostra la panoramica dei componenti per il servizio {{site.data.keyword.mon_full_notm}} in esecuzione su {{site.data.keyword.cloud_notm}}:

![{{site.data.keyword.mon_full_notm}} - Panoramica dei componenti su {{site.data.keyword.cloud_notm}}](images/components.png "{{site.data.keyword.mon_full_notm}} - Panoramica dei componenti su {{site.data.keyword.cloud_notm}}")


## Funzioni
{: #features}

**Accelera la diagnosi e la risoluzione degli incidenti con le prestazioni.**

{{site.data.keyword.mon_full_notm}} offre una visibilità approfondita nell'infrastruttura e nelle applicazioni con la possibilità di risolvere i problemi dal livello del servizio fino al livello del sistema. I dashboard e gli avvisi predefiniti semplificano l'identificazione di potenziali minacce o problemi. Utilizzando {{site.data.keyword.mon_full_notm}}, gli sviluppatori e i team DevOps monitorano e risolvono i problemi con le prestazioni in tempo reale, identificano l'origine degli errori ed eliminano i problemi. 

**Controlla il costo della tua infrastruttura di monitoraggio.**

{{site.data.keyword.mon_full_notm}} include funzionalità che ti permettono di controllare il costo della tua infrastruttura di monitoraggio in {{site.data.keyword.cloud_notm}}. Puoi configurare le origini delle metriche di cui vuoi monitorare le prestazioni. Puoi abilitare un avviso predefinito per ricevere un'avvertenza relativa a modifiche di utilizzo che avranno ripercussioni sulla fatturazione. 

**Esplora e visualizza facilmente il tuo intero ambiente.**

{{site.data.keyword.mon_full_notm}} rende semplice esplorare visivamente il tuo ambiente. Le mappe dinamiche della topologia forniscono una vista delle dipendenze tra i servizi. Le query multidimensionali su metriche ad alta varianza, alta cardinalità e alta frequenza accelerano la risoluzione dei problemi. I dashboard personalizzabili ti consentono di visualizzare gli elementi più importanti. 

**Ricevi informazioni approfondite critiche sul contenitore e Kubernetes per il monitoraggio dinamico dei microservizi.**

{{site.data.keyword.mon_full_notm}} rileva automaticamente gli ambienti Kubernetes che forniscono dashboard e avvisi predefiniti per cluster, nodi, spazi dei nomi, servizi, distribuzioni, pod e altro. Un singolo agent per nodo rileva dinamicamente tutti i microservizi e raccoglie automaticamente metriche ed eventi da diverse origini, compresi Kubernetes, host, reti, contenitori, processi, applicazioni e metriche personalizzate come Prometheus, JMX e StatsD. 

**Riduce l'impatto di situazioni anomale con notifiche proattive.**

{{site.data.keyword.mon_full_notm}} include avvisi e notifiche multicanale che puoi utilizzare per ridurre l'impatto sulle tue operazioni giornaliere e accelerare la tua reazione e i tuoi tempi di risposta nel caso di anomalie, tempo di inattività e riduzione delle prestazioni. I canali di notifica che puoi configurare facilmente includono *email*, *slack*, *PagerDuty*, *Webhooks*, *OpsGenie* e *VictorOps*.


## Prima di cominciare
{: #prereqs}

Devi avere un ID utente che è un membro o un proprietario di un account {{site.data.keyword.cloud_notm}}. Per ottenere un ID utente {{site.data.keyword.cloud_notm}}, vai a: [Registrazione ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window}.

Il servizio è al momento disponibile in Stati Uniti Sud. Completa tutte le attività preliminari nella regione Stati Uniti Sud.


## Passo 1: gestisci l'accesso utente
{: #step1}

Ogni utente che accede al servizio {{site.data.keyword.mon_full_notm}} nel tuo account deve avere assegnata una politica di accesso con un ruolo utente IAM definito. La politica determina quali azioni possono essere effettuate dall'utente all'interno del contesto del servizio o dell'istanza che selezioni. Le azioni consentite vengono personalizzate e definite come operazioni che possono essere eseguite sul servizio. Le azioni vengono quindi associate ai ruoli utente IAM. Per ulteriori informazioni, consulta [Gestione dell'accesso utente in {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam#iam).

Quando a un utente vengono concesse le autorizzazioni in {{site.data.keyword.cloud_notm}} per utilizzare il servizio {{site.data.keyword.mon_full_notm}}, all'utente viene automaticamente concesso un ruolo Sysdig. Questo ruolo determina le azioni per cui un utente ha le autorizzazioni e che può eseguire. I ruoli validi sono *amministratore Sysdig* e *utente Sysdig*. Per ulteriori informazioni, vedi [Associazione dei ruoli Sysdig ai ruoli {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam#iam_sysdig).

Prima di poter eseguire il provisioning di un'istanza, prendi in considerazione le seguenti informazioni:
* Il proprietario dell'account può creare, visualizzare ed eliminare un'istanza di un servizio in {{site.data.keyword.cloud_notm}} e può concedere le autorizzazioni ad altri utenti in modo che possano utilizzare il servizio {{site.data.keyword.mon_full_notm}}.
* Devi disporre delle autorizzazioni per creare delle risorse nel gruppo di risorse predefinito (*Default*).
* Altri utenti {{site.data.keyword.cloud_notm}} con le autorizzazioni `administrator` o `editor` possono gestire il servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}. Questi utenti devo disporre anche delle autorizzazioni della piattaforma per creare le risorse all'interno del contesto del gruppo di risorse in cui pensano di eseguire il provisioning dell'istanza.

Per concedere a un utente il ruolo di amministratore per il servizio e per gestire le istanze all'interno di un gruppo di risorse nell'account, l'utente deve avere una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo della piattaforma di **amministratore** all'interno del contesto del gruppo di risorse. 

Completa la seguente procedura per assegnare a un utente il ruolo di amministratore per il servizio {{site.data.keyword.mon_full_notm}} all'interno del contesto di un gruppo di risorse. 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso in un gruppo di risorse**.
4. Seleziona un gruppo di risorse.
5. Se l'utente non ha un ruolo già concesso per il gruppo di risorse selezionato, scegli un ruolo per il campo **Assegna accesso a un gruppo di risorse**. 

    A seconda del ruolo che selezioni, l'utente può visualizzare il gruppo di risorse sul proprio dashboard, modificarne il nome o gestire l'accesso utente al gruppo. 
    
    Puoi selezionare **Nessun accesso**, se vuoi che l'utente abbia accesso solo al servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse.

6. Seleziona **{{site.data.keyword.mon_full_notm}}**.
7. Seleziona il ruolo della piattaforma **Amministratore**.
8. Fai clic su **Assegna**.

## Passo 2: provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}}
{: #step2}

Per aggiungere le funzioni di monitoraggio a {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}, devi eseguire il provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}}. 

Quando esegui il provisioning di un'istanza, i tuoi dati vengono inviati a una terza parte.
{: tip}

Esegui il provisioning di un'istanza all'interno del contesto di un gruppo di risorse. Un gruppo di risorse ti consente di organizzare i tuoi servizi per scopi di controllo dell'accesso e fatturazione. Puoi eseguire il provisioning di un'istanza {{site.data.keyword.mon_full_notm}} nel gruppo di risorse *predefinito* o in uno personalizzato.

Quando esegui il provisioning di un'istanza, ottieni automaticamente una chiave di inserimento, nota come la *chiave di accesso Sysdig*.

Per eseguire il provisioning di un'istanza tramite l'IU {{site.data.keyword.cloud_notm}}, completa la seguente procedura:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperta l'IU {{site.data.keyword.cloud_notm}}.

2. Fai clic su **Catalogo**. Viene aperto l'elenco dei servizi disponibili in {{site.data.keyword.cloud_notm}}.

3. Per filtrare l'elenco dei servizi che viene visualizzato, seleziona la categoria **Strumenti per gli sviluppatori**.

4. Fai clic sul tile **{{site.data.keyword.mon_full_notm}}**.

5. Seleziona un piano di servizio. Per impostazione predefinita, è impostato il piano **Prova**.

    Per ulteriori informazioni sui piani di servizio, vedi [Prezzi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

6. Seleziona un gruppo di risorse. Per impostazione predefinita, è impostato il gruppo **predefinito**.

7. Fai clic su **Crea** per eseguire il provisioning di un'istanza.

Viene aperta l'IU del servizio.

**Nota:** per eseguire il provisioning di un'istanza di Sysdig tramite la CLI, consulta [Provisioning di Sysdig tramite la CLI {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Passo 3: configura un agent Sysdig
{: #step3}

Dopo aver eseguito il provisioning di un'istanza, devi configurare un agent Sysdig per ogni origine della metrica che vuoi monitorare. Un'origine della metrica è una risorsa cloud che vuoi monitorare e di cui vuoi controllare le prestazioni e l'integrità. Ad esempio, un'origine della metrica può essere un cluster Kubernetes.  

L'agent Sysdig raccoglie e riporta automaticamente le metriche predefinite. Utilizza la *chiave di accesso Sysdig* per configurare l'agent Sysdig responsabile della raccolta e dell'inoltro dei dati della metrica alla tua istanza. Per ulteriori informazioni, consulta [Utilizzo delle chiavi di accesso](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key).

Puoi configurare un agent Sysdig per ognuno dei seguenti ambienti:

* Kubernetes, GKE e OpenShift.
* Contenitori Docker o servizi non inseriti in contenitori.
* Mesos, Marathon e DCOS.
* Installazioni Linux.

Ad esempio, per configurare il tuo cluster Kubernetes in modo che invii le metriche alla tua istanza Sysdig, devi installare un pod `sysdig-agent` su ogni nodo del tuo cluster. L'agent Sysdig raccoglie i dati dal pod in cui è installato e li inoltra alla tua istanza Sysdig.

Completa una delle seguenti esercitazioni per imparare come distribuire un agent Sysdig:

| Risorsa                |	Esercitazione                        | Ambiente                | Scenario   |
|-------------------------|---------------------------------|----------------------------|------------|
| Contenitori in esecuzione su {{site.data.keyword.containershort}} |[Analizza le metriche per un'applicazione distribuita in un cluster Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-kubernetes_cluster#kubernetes_cluster) | {{site.data.keyword.cloud_notm}} Pubblico | ![{{site.data.keyword.containershort}} e {{site.data.keyword.mon_full_notm}}](images/kube.png "{{site.data.keyword.containershort}} e {{site.data.keyword.mon_full_notm}}") |
|Linux Ubuntu/Debian | [Analizza le metriche per un server Ubuntu](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-ubuntu#ubuntu) | In loco | ![Ubuntu e {{site.data.keyword.mon_full_notm}}](images/kube.png "Ubuntu e {{site.data.keyword.mon_full_notm}}") |
{: caption="Tabella 1. Esercitazioni per iniziare ad utilizzare {{site.data.keyword.mon_full_notm}}" caption-side="top"} 

Per ulteriori informazioni, consulta [Configurazione di un agent Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) e [Rimozione di un agent Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove).

Dopo aver distribuito l'agent Sysdig, la raccolta e l'inoltro delle metriche all'istanza sono automatici. L'agent Sysdig raccoglie e riporta automaticamente le metriche predefinite. Puoi anche configurare quali metriche monitorare in un ambiente. Vengono raccolti automaticamente anche i dati per le metriche personalizzate.

## Passo 4: avvia l'IU web
{: #step4}

Dopo aver eseguito il provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.Bluemix}} e configurato un agent Sysdig per il tuo nodo, puoi visualizzare, monitorare e gestire i dati tramite l'IU web del servizio.

Avvia l'IU web all'interno del contesto dell'istanza Sysdig, dall'IU {{site.data.keyword.cloud_notm}}. 

Completa la seguente procedura per avviare l'IU web Sysdig:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperto il dashboard {{site.data.keyword.cloud_notm}}.

2. Nel menu di navigazione, seleziona **Osservabilità**. 

3. Seleziona **Monitoraggio**. 

    Viene visualizzato l'elenco delle istanze di monitoraggio disponibili su {{site.data.keyword.cloud_notm}} .

4. Seleziona un'istanza. Quindi, fai clic su **Visualizza Sysdig**.

Viene aperta l'IU web {{site.data.keyword.mon_full_notm}}. Per impostazione predefinita, viene visualizzata la scheda *Explore* .

Per impostazione predefinita, gli utenti vengono automaticamente aggiunti come membri del team **Monitor Operations** predefinito per ogni istanza {{site.data.keyword.mon_full_notm}}. Gli utenti dispongono di tutte le autorizzazioni per visualizzare tutti i dati nell'IU web. **Nota:** un amministratore può limitare l'accesso ai dati gestendo gli utenti in team e controllando quali dati sono visibili. Ad esempio, per limitare gli utenti che dispongono delle autorizzazioni di visualizzazione, un amministratore può creare un team predefinito con ambito e visibilità limitati. Successivamente, può assegnare manualmente gli utenti ad altri team. Per ulteriori informazioni, consulta [Utilizzo dei team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams).


## Passo 5: monitora il tuo ambiente
{: #step5}

Puoi analizzare i dati nella scheda *Explore* e nella scheda *Dashboard* dell'IU web. Monitora i dati tramite le viste e i dashboard delle metriche. 

* Utilizza una vista delle metriche per monitorare una sola metrica.
* Utilizza i dashboard per ottenere delle informazioni approfondite specializzate sui dati di rete, sui dati dell'applicazione, sulla topologia, sui servizi, sugli host e sui contenitori monitorando i dati tramite i pannelli. Un pannello visualizza una metrica o un gruppo di metriche in un dashboard.
{: tip}

Nella scheda *Explore*, puoi monitorare i dati utilizzando le metriche e i dashboard predefiniti. Puoi utilizzare delle etichette per definire i nuovi gruppi dell'infrastruttura che puoi poi utilizzare per aggregare i dati in modo diverso e monitorare il tuo ambiente. Puoi anche utilizzare i dashboard personalizzati che definisci tramite la scheda *Dashboard*.

Nella scheda *Dashboards*, puoi monitorare i dati utilizzando uno qualsiasi dei dashboard predefiniti o creandone di nuovi.

Per ulteriori informazioni, consulta [Monitoraggio dell'ambiente](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring)



## Passo 6: gestisci i dati
{: #step6}

Puoi utilizzare le etichette per raggruppare le risorse dell'infrastruttura in gerarchie logiche, filtrare i dati e suddividere i dati aggregati in segmenti. Personalizza come i dati vengono aggregati quando configuri un grafico o crei un avviso per una metrica. Configura l'ambito di un dashboard, un pannello o un avviso in modo che filtri i punti dati. Limita l'accesso ai dati gestendo l'accesso ai dati degli utenti tramite i team. 

Ad esempio, per una vista delle metriche, puoi definire l'ambito dei dati, come aggregarli e quali filtri di ora e gruppo applicare ai dati. 

Per ulteriori informazioni, consulta [Gestione dei dati](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).


## Passi successivi: configura gli avvisi ed esplora gli eventi
{: #next}

Puoi utilizzare gli eventi per controllare, tenere traccia e risolvere i problemi. Un evento è una notifica che ti informa su qualcosa che si è verificato in tutti i nodi che inoltrano i dati alla tua istanza {{site.data.keyword.mon_full_notm}}. 

Esistono diversi tipi di eventi: 

* Gli *eventi di avviso* sono eventi che vengono attivati dagli avvisi configurati dall'utente. Ad esempio, configura gli avvisi per essere avvertito dei problemi che richiedono la tua attenzione. Per ulteriori informazioni, consulta [Utilizzo degli avvisi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* Gli *eventi basati sull'infrastruttura* sono eventi raccolti dai nodi Docker e Kubernetes. Per impostazione predefinita, l'agent Sysdig rileva e raccoglie automaticamente i dati da un gruppo selezionato di eventi. Puoi modificare il file di configurazione dell'agent per abilitare ulteriori eventi.
* *Eventi personalizzati* che configuri tramite una delle seguenti integrazioni: Slackbot, script Python precostruiti, script Python creati dall'utente personalizzati o richieste cURL.

Quando definisci un avviso, devi definire la condizione che attiva la notifica, uno o più canali di notifica tramite i quali vuoi essere avvertito, la severità dell'avviso e il tipo di avviso. 

Configura uno o più canali di notifica nella sezione *Settings* nell'IU web. I canali di notifica validi sono: *email*, *slack*, *PagerDuty*, *Webhooks*, *OpsGenie* e *VictorOps*. Per ulteriori informazioni, consulta [Utilizzo dei canali di notifica](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications).

La sezione *Alerts* nell'IU web mostra l'elenco degli avvisi predefiniti. Da questa vista, puoi abilitare e disabilitare gli avvisi predefiniti, puoi modificare gli avvisi esistenti e puoi crearne di nuovi. Per ulteriori informazioni, consulta [Utilizzo degli avvisi ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts){:new_window}.

Successivamente, esplora [Utilizzo degli eventi personalizzati ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


