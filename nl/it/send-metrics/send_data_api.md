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

# Invio dei dati utilizzando l'API Metriche
{: #send_data_api}

Puoi inviare metriche al servizio {{site.data.keyword.monitoringshort}} utilizzando l'API Metriche. 
{:shortdesc}


Per i contenitori Docker {{site.data.keyword.Bluemix_notm}}, le metriche del sistema di base vengono raccolte automaticamente. Per le applicazioni Cloud Foundry e per le applicazioni in esecuzione in una macchina virtuale (VM), le metriche devono essere inviate direttamente dall'applicazione utilizzando [l'API Metriche](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}. 



## Invio delle metriche a un dominio dello spazio
{: #space_uaa}

Per inviare le metriche a uno spazio utilizzando cURL, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Ottieni il token di sicurezza. Puoi utilizzare un token UAA, IAM o una chiave API.

    Scegli uno dei seguenti metodi per ottenere il token di sicurezza di cui hai bisogno per inviare le metriche:
	
	* Per ottenere un token UAA, vedi [Acquisizione del token UAA utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli);
	
	* Per ottenere un token IAM, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Per ottenere una chiave API, vedi [Ottenimento di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Dallo stesso terminale a cui hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, configura la variabile *Token* per il token.

    Ad esempio, configura un token UAA e rimuovi la parte *Bearer* dal valore del token:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. Ottieni il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio.

    Immetti il seguente comando:
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	Dove *SpaceName* è il nome dello spazio in cui intendi definire una notifica.
	
	Ad esempio, per ottenere il GUID di uno spazio con nome *dev*, immetti il seguente comando:
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	Il risultato di questo comando è il seguente:
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	Quindi, esporta la variabile *Space*. **Nota:** il GUID deve avere come prefisso *s-* per identificare uno spazio.
	
	Ad esempio:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
5. Immetti il seguente comando cURL per inviare le metriche:

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	dove
	
	* Metrics_File rappresenta il file JSON che include la definizione delle metriche inviate al servizio {{site.data.keyword.monitoringshort}}.
	
	* *X-Auth-User-Token* è un parametro che passa il token di sicurezza.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token. I valori validi sono: *uaa* per un token UAA, *iam* per un token IAM e *api* per una chiave API.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio.
	
	* Token rappresenta il token di sicurezza o la chiave API.
	
	* Space rappresenta il GUID dello spazio. 
	
	* Endpoint rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
	Ad esempio, puoi immettere il seguente comando per inviare 2 metriche, `myhost.cpu.idle` e `myapp.login.attempts`, al servizio {{site.data.keyword.monitoringshort}}:
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	Il file di esempio *metric.json* è definito come segue:

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
