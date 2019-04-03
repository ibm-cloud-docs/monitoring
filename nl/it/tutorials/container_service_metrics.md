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


# Analizza le metriche in Grafana per un cluster Kubernetes
{: #container_service_metrics}

Utilizza questa esercitazione per imparare ad utilizzare il servizio {{site.data.keyword.monitoringlong}} per monitorare le prestazioni del tuo contenitore. 
{:shortdesc}


## Obbiettivi
{: #ks_objectives}

Impara a cercare e analizzare le metriche del contenitore per un'applicazione distribuita in un cluster Kubernetes:

1. Identifica dove le metriche che vengono raccolte in un cluster sono inoltrate al servizio {{site.data.keyword.monitoringshort}}. 
2. Avvia Grafana e imposta il dominio {{site.data.keyword.monitoringshort}} in cui puoi visualizzare le metriche del cluster.
3. Cerca e analizza le metriche del contenitore per un'applicazione distribuita in un cluster Kubernetes in {{site.data.keyword.Bluemix_notm}}.

Questa esercitazione ti guida attraverso i passi necessari per raggiungere il seguente scenario end-to-end utilizzando {{site.data.keyword.Bluemix_notm}}: provisioning di un cluster, identificazione di dove il cluster invia le metriche al servizio {{site.data.keyword.monitoringshort}} in {{site.data.keyword.Bluemix_notm}}, distribuzione di un'applicazione nel cluster e utilizzo di Grafana per visualizzare e filtrare le metriche del contenitore per tale cluster.


**Nota:** per completare questa esercitazione, devi completare i prerequisiti e le esercitazioni che sono collegate dai diversi passi.


## Prerequisiti
{: #ks_prereqs}

1. Devi essere un membro o un proprietario di un account {{site.data.keyword.Bluemix_notm}} con le autorizzazioni per creare i cluster standard Kubernetes, distribuire le applicazioni nei cluster ed eseguire le query delle metriche in {{site.data.keyword.Bluemix_notm}} per il monitoraggio in Grafana.

    Il tuo ID utente di {{site.data.keyword.Bluemix_notm}} deve avere le seguenti politiche assegnate:
    
    * Una politica IAM di {{site.data.keyword.containershort}} con le autorizzazioni *operatore* o *amministratore*.
    
    Per ulteriori informazioni, consulta [Assegnazione di una politica IAM a un utente tramite la IU IBM Cloud](/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_ui).

2. Avere una sessione del terminale dalla quale puoi gestire il cluster Kubernetes e distribuire le applicazioni dalla riga di comando. In questa esercitazione, gli esempi vengono forniti per un sistema Ubuntu Linux.

3. Installa le CLI per utilizzare {{site.data.keyword.containershort}} nel tuo sistema Ubuntu.

    * Installa la CLI {{site.data.keyword.Bluemix_notm}}. 
    * Installa la CLI {{site.data.keyword.containershort}} per creare e gestire i tuoi cluster Kubernetes in {{site.data.keyword.containershort}} e per distribuire le applicazioni inserite nel contenitore al tuo cluster.
    
    Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).
    
    

    
 

## Passo 1: provisioning di un cluster Kubernetes
{: #ks_step1}

Completa la seguente procedura:

1. Crea un cluster Kubernetes standard. Per ulteriori informazioni, vedi [Crea un cluster standard Kubernetes](/docs/containers/cs_tutorials.html#cs_cluster_tutorial).

2. Configura il contesto del cluster in un terminale. Una volta impostato il contesto, puoi gestire il cluster Kubernetes e distribuire l'applicazione nel cluster.

    Accedi alla regione, all'organizzazione e allo spazio in {{site.data.keyword.Bluemix_notm}} associati al cluster che hai creato. Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

	Inizializza il plugin del servizio {{site.data.keyword.containershort}}.

	```
	ibmcloud cs init
	```
	{: codeblock}

    Configura il contesto del tuo terminale per il tuo cluster.
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    L'output dell'esecuzione di questo comando fornisce il comando che devi eseguire nel tuo terminale per configurare il percorso al tuo file di configurazione. Ad esempio:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Copia e incolla il comando per configurare la variabile di ambiente nel tuo terminale e poi premi **Invio**.



## Passo 2: concedi le tue autorizzazioni utente per visualizzare le metriche nel dominio dell'account
{: #ks_step2}

Per concedere a un utente le autorizzazioni per visualizzare le metriche in un dominio dell'account, devi assegnare all'utente una politica IAM per il servizio {{site.data.keyword.monitoringshort}} con il ruolo **Visualizzatore**.

Completa la seguente procedura per concedere a un utente le autorizzazioni per utilizzare il servizio {{site.data.keyword.monitoringshort}}:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.

    Apri un browser web e avvia il dashboard {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}
	
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dalla barra del menu, fai clic su **Gestisci > Account > Utenti**. 

    La finestra *Utenti* visualizza un elenco di utenti con i rispettivi indirizzi email per l'account attualmente selezionato.
	
3. Se l'utente è un membro dell'account, seleziona il nome utente dall'elenco o fai clic su **Gestisci utente** dal menu *Azioni*.

    Se l'utente non è un membro dell'account, consulta [Invito di utenti](/docs/iam/iamuserinv.html#iamuserinv).

4. Seleziona **Politiche di accesso > Assegna accesso > Assegna l'accesso alle risorse**.

5. Scegli il servizio **{{site.data.keyword.monitoringlong}}**, seleziona la regione in cui è disponibile il cluster, **Stati Uniti Sud** per questa esercitazione e seleziona un ruolo, **visualizzatore**.



## Passo 3: concedi le autorizzazioni proprietario della chiave {{site.data.keyword.containershort_notm}}
{: #ks_step3}

Quando il cluster inoltra le metriche al dominio dell'account, il proprietario della chiave {{site.data.keyword.containershort}} deve disporre delle seguenti politiche IAM:

* Politica IAM con autorizzazioni da **editor** per il servizio {{site.data.keyword.monitoringshort}}.
* Politica IAM con autorizzazioni da **amministratore** per {{site.data.keyword.containershort}}.


Completa la seguente procedura per concedere le autorizzazioni proprietario della chiave {{site.data.keyword.containershort}}:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.

    Apri un browser web e avvia il dashboard {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}
	
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dalla barra del menu, fai clic su **Gestisci > Account > Utenti**. 

    La finestra *Utenti* visualizza un elenco di utenti con i rispettivi indirizzi email per l'account attualmente selezionato.
	
3. Trova l'ID utente del proprietario della chiave {{site.data.keyword.containershort}}.

    Esegui il comando `ibmcloud cs api-key-info ClusterName` per ottenere l'ID utente del proprietario della chiave {{site.data.keyword.containershort}}.

4. Seleziona **Politiche di accesso > Assegna accesso > Assegna l'accesso alle risorse**.

5. Scegli il servizio **{{site.data.keyword.monitoringlong}}**, seleziona la regione in cui è disponibile il cluster, **Stati Uniti Sud** per questa esercitazione e seleziona un ruolo, **editor**.	

6. Ripeti i passi da 2 a 4 e scegli il servizio {{site.data.keyword.containershort}}. Seleziona **Tutte le regioni** e il ruolo **amministratore**.	




## Passo 4: distribuisci un'applicazione di esempio nel cluster Kubernetes
{: #ks_step4}

Distribuisci ed esegui un'applicazione di esempio nel cluster Kubernetes. Completa la procedura nella seguente esercitazione per distribuire un'applicazione di esempio: [Lezione 1: distribuzione di singole applicazioni dell'istanza ai cluster Kubernetes](/docs/containers/cs_tutorials_apps.html#cs_apps_tutorial_lesson1).

l'applicazione è un'applicazione Node.js Hello World:

```
var express = require('express')
    var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

In questa applicazione di esempio, quando verifichi la tua applicazione in un browser, l'applicazione scrive il seguente messaggio in stdout: `Sample app is listening on port 8080.`


## Passo 5: avvia Grafana e configura il dominio delle metriche
{: #ks_step5}

Avvia Grafana da un browser e configura il dominio {{site.data.keyword.monitoringshort}} in cui puoi visualizzare le metriche del cluster.

Per analizzare le metriche per un cluster, devi accedere a Grafana nella regione pubblica del cloud in cui viene creato il cluster. Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana da un browser web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

1. Da un browser, avvia Grafana. 

    Immetti l'URL del servizio {{site.data.keyword.monitoringshort}} della regione in cui hai creato il cluster. 
    
    Per ottenere gli URL per regione, consulta [URL per il servizio di monitoraggio](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Ad esempio, per la regione Stati Uniti Sud, avvia: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Imposta il dominio di {{site.data.keyword.monitoringshort}} su **Account**.

    In Grafana, seleziona il tuo ID. Quindi, controlla di essere nell'account corretto e scegli un dominio. Seleziona `Domain = account`.

    I cluster inoltrano le metriche al dominio delle metriche dell'account. 

## Passo 6: monitora il cluster in Grafana
{: #ks_step6}

{{site.data.keyword.containershort}} fornisce un dashboard Grafana che puoi utilizzare per monitorare le tue metriche del cluster. 

Completa la seguente procedura per aprire il dashboard di esempio:

1. Seleziona il commutatore della barra dei menu laterale ![Barra di menu laterale Grafana](images/grafana_settings.gif "Barra dei menu laterale Grafana").
2. Seleziona **Dashboard**.
3. Fai clic su **Apri**.
4. Seleziona **ClusterMonitoringDashboard_v1**.

Viene aperto il dashboard di esempio. 

![Dashboard di esempio Grafana](images/cluster_grafana_sample_dashboard.png "Dashboard di esempio Grafana")



## Passi successivi
{: #ks_next_steps}

Definisci un avviso per una metrica. Per ulteriori informazioni, vedi [Configurazione degli avvisi](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).
