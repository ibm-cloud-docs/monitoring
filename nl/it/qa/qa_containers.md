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



# Domande frequenti (FAQ) per il monitoraggio dei cluster Kubernetes
{: #qa_containers}

Queste sono le risposte alle domande più frequenti sul servizio {{site.data.keyword.monitoringshort}} e il servizio {{site.data.keyword.containershort_notm}}. 
{:shortdesc}

* [La query Grafana per i miei contenitori non sta visualizzando i dati o è in errore](/docs/services/cloud-monitoring/qa/qa_containers.html#metric_format_change)
* [Come configuro un ambiente cluster nella mia sessione del terminale?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1)
* [Dove posso ottenere l'ID e il nome del cluster?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa3)
* [Come posso ottenere l'elenco degli spazi dei nomi?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa7)
* [Come posso ottenere l'elenco dei pod in uno spazio dei nomi in un cluster Kubernetes?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa8)
* [Come posso ottenere tutti i pod in un cluster per lo spazio dei nomi?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa9)

## La query Grafana per i miei contenitori non sta visualizzando i dati o è in errore
{: #metric_format_change}

Il formato della query che puoi definire per un contenitore è stato modificato.

Il seguente formato è obsoleto: 

```
{Prefix}.{Version}.{Provider}.{Type}.{ServiceName}.{Region}.{Account}.{Cluster}.{Metric}.{Container in a pod}.{Functions}
```
{: screen}

I nuovi formati validi sono i seguenti:

* [Formato della query della metrica della CPU per un contenitore](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers)
* [Formato della query della metrica di carico per un nodo di lavoro](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers)
* [Formato della query della metrica della memoria per un contenitore](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)

Migra le tue vecchie query al nuovo formato per visualizzare i tuoi dati in Grafana.

Ad esempio, se la tua query si avvia come `crn.v1.bluemix.public.containers-kubernetes.us-south.`, devi migrarla al nuovo formato, ossia `ibmcloud.public.containers-kubernetes.us-south`.

La seguente tabella elenca i campi nel formato che è diventato obsoleto:

 <table>
      <caption>Tabella 1. Campi di query Grafana per i contenitori</caption>
      <tr>
        <th align="center">Campo</th>
        <th align="center">Descrizione</th>
        <th align="center">Valori validi</th>
      </tr>
      <tr>
        <td>Prefisso</td>
        <td>Il prefisso utilizzato per indicare che è una risorsa {{site.data.keyword.IBM_notm}} Cloud.</td>
        <td>`crn`</td>
      </tr>
      <tr>
        <td>Versione</td>
        <td>La versione che indica che il formato e i campi dei dati della metrica raccolti. </td>
        <td>`v1`</td>
      </tr>
      <tr>
        <td>Provider</td>
        <td>Provider cloud in cui vengono raccolti i dati. Questo campo è un identificativo alfanumerico.</td>
        <td>Per {{site.data.keyword.IBM_notm}} Cloud pubblico, il valore è: `bluemix`</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>Ambiente cloud in cui vengono raccolti i dati.</td>
        <td>Per {{site.data.keyword.IBM_notm}} Cloud pubblico, il valore è: `public`</td>
      </tr>
      <tr>
        <td>Nome servizio</td>
        <td>Infrastruttura cloud in cui vengono raccolte le metriche.</td>
        <td>Per il servizio {{site.data.keyword.monitoringshort}}, il valore è: `containers-kubernetes`</td>
      </tr>
      <tr>
        <td>Regione</td>
        <td>Regione cloud in cui vengono raccolte le metriche.</td>
        <td>Per la regione Stati Uniti Sud, il valore è: `ng` <br>Per la regione Regno Unito, il valore è: `eu-gb` <br>Per la Germania, il valore è: `eu-de` <br>Per Sydney, il valore è: `au-syd` </td>
      </tr>
      <tr>
        <td>Account</td>
        <td>GUID dell'account in cui vengono raccolte le metriche. <br>Il formato di questo campo è il seguente: `a_ID` dove ID è il GUID dell'account. <br>Per ottenere il GUID dell'account, consulta [Come ottenere il GUID di un account](/docs/services/cloud-monitoring/qa/cli_qa.html#account_guid).</td>
        <td>a_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Cluster</td>
        <td>GUID del cluster in cui vengono raccolte le metriche.</td>
        <td>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Metrica</td>
        <td>La metrica raccolta automaticamente per un contenitore.</td>
        <td>Per un elenco di metriche della CPU, consulta [Metriche della CPU per i contenitori](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#cpu_metrics_containers) <br>Per un elenco di metriche della memoria, consulta [Metriche della memoria](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics) </td>
      </tr>
      <tr>
        <td>Contenitore in un pod</td>
        <td>Combinazione di nomi di risorse e di GUID Kubernetes richiesti per identificare in modo univoco un contenitore eseguito in un pod. <br>**Nota:** quando esamini l'elenco delle opzioni disponibili per questa voce nella query, nota che esiste anche una voce con il seguente formato: {namespace}{pod_name}{deploymentname_name}_POD{container_ID}. Queste voci corrispondono agli ID contenitore interni creati da Kubernetes.</td>
		<td>{namespace}_{pod_name}_{deployment_name}_{container_id}</td>
      </tr>
      <tr>
        <td>Funzioni</td>
        <td>Funzioni della query che puoi selezionare per visualizzare una metrica del contenitore nel pannello. <br>Per ulteriori informazioni, vedi [Funzioni![(Icona link esterno)](../../icons/launch-glyph.svg "Icona link esterno")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
        <td></td>
      </tr>
    </table>


## Come configuro un ambiente cluster nella mia sessione del terminale?
{: #qa1}

Devi configurare il contesto di un cluster Kubernetes per gestirlo utilizzando i comandi.

**Nota:** per gestire un cluster, hai bisogno di una politica IAM per il servizio {{site.data.keyword.containershort_notm}} assegnato al tuo utente con le autorizzazioni per completare l'attività.

Completa la seguente procedura per configurare il contesto di un cluster:

1. Accedi alla regione, all'organizzazione e allo spazio in {{site.data.keyword.Bluemix_notm}} associati al cluster che hai creato. Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Inizializza il plugin del servizio {{site.data.keyword.containershort_notm}}. Immetti il seguente comando:

	```
	ibmcloud cs init
	```
	{: codeblock}

3. Configura il contesto del cluster nella tua sessione del terminale. Esegui questi comandi:
    
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

 
 

## Dove posso ottenere l'ID e il nome del cluster?
{: #qa3}

Completa la seguente procedura per ottenere il nome e l'ID del cluster tramite la IU:

1. Accedi al tuo account {{site.data.keyword.Bluemix_notm}}.

    Il dashboard {{site.data.keyword.Bluemix_notm}} è disponibile all'indirizzo: [http://bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}.
    
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dal *Dashboard* {{site.data.keyword.Bluemix_notm}}, seleziona **Menu > Contenitori**.

    Viene visualizzato l'elenco dei cluster disponibili nell'account.

3. Per ottenere l'ID del cluster, seleziona una voce cluster. 

    Viene visualizzata la pagina della panoramica. In questa pagina, puoi ottenere l'ID del cluster.



Completa la seguente procedura per ottenere il nome e l'ID del cluster tramite la riga di comando:

1. Accedi alla regione, all'organizzazione e allo spazio in {{site.data.keyword.Bluemix_notm}} associati al cluster che hai creato. Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Elenca i cluster disponibili nell'account. Immetti il seguente comando: 

    ```
	ibmcloud cs clusters
	``` 
	{: codeblock}
	
	L'output di questo comando elenca tutti i cluster nell'account con gli ID corrispondenti.
	
3. Per ottenere l'ID del cluster, esegui il seguente comando:

    ```
	ibmcloud cs cluster-get my_cluster
	```
    {: screen}	
 


## Come posso ottenere l'elenco degli spazi dei nomi?
{: #qa7}

Per ottenere un elenco di tutti gli spazi dei nomi nel tuo cluster, completa la seguente procedura:

Completa la seguente procedura:

1. Configura il contesto del cluster. Per ulteriori informazioni, vedi [Come configuro un ambiente cluster nella mia sessione del terminale?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Elenca tutti gli spazi dei nomi. Immetti il seguente comando kubectl:

    ```
    kubectl get namespaces
	```
	{: codeblock}

## Come posso ottenere l'elenco dei pod per uno spazio dei nomi in un cluster Kubernetes?
{: #qa8}
		
Per ottenere l'elenco dei pod in uno spazio dei nomi, completa la seguente procedura:

1. Configura il contesto del cluster. Per ulteriori informazioni, vedi [Come configuro un ambiente cluster nella mia sessione del terminale?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Per ottenere l'elenco dei pod per uno spazio dei nomi in un cluster Kubernetes, immetti il seguente comando:

    ```
	kubectl --namespace=NamespaceName get pods 
	```
	{: codeblock}
	
	dove Namespacename è il nome dello spazio dei nomi, ad esempio, *default*.

## Come posso ottenere tutti i pod in un cluster per lo spazio dei nomi?
{: #qa9}
		
Completa la seguente procedura:

1. Configura il contesto del cluster. Per ulteriori informazioni, vedi [Come configuro un ambiente cluster nella mia sessione del terminale?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).
	
2. Per ottenere tutti i pod in un cluster per lo spazio dei nomi, immetti il seguente comando:

	```
	kubectl get pods --all-namespaces
	```
	{: codeblock}
		


