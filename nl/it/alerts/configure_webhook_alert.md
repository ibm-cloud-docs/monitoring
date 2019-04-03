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


# Configurazione di un avviso Webhook utilizzando l'API {{site.data.keyword.monitoringshort}}
{: #configure_webhook_alert}

Per configurare un avviso webhook per una metrica, definisci una regola e una notifica webhook. Quindi, registra il metodo di notifica e la regola con il servizio {{site.data.keyword.monitoringshort}}.
{:shortdesc}

Completa la seguente procedura:

## Passo 1: Crea una regola
{: #step14}

Crea una regola per una query della metrica che hai definito in Grafana. Per ulteriori informazioni, vedi [Creazione di una regola](/docs/services/cloud-monitoring/alerts/rules.html#create).

Ad esempio, crea il file di regole `s-rule-1.json` nella directory `~/cloud-monitoring/rules/`. 

```
{
    "name": "RULE_NAME",
    "description": "MH check Bytes In per second",
    "expression": "movingAverage(messagehub.65qser11-8034-1234-5678-c82fb42wdfgh.1.kafka-java-console-sample-topic.BytesInPerSec.15MinuteRate,\"5min\")",
    "enabled": true,
    "from": "-5min",
    "until": "now",
    "comparison": "above",
    "comparison_scope": "last",
    "error_level" : 27,
    "warning_level" : 25,
    "frequency": "1min",
    "dashboard_url": "https://metrics.ng.bluemix.net",
    "notifications": [
      "NOTIFICATION_NAME"
    ]
}
```
{: screen}

Quindi, esporta la variabile *RULE_FILE*:
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## Passo 2: Registra la regola nel servizio Monitoraggio
{: #step23}
	
Da un terminale, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Ottieni il token di sicurezza. Puoi utilizzare un token UAA, IAM o una chiave API. Scegli uno dei seguenti metodi per ottenere il token di sicurezza:
	
	* Per ottenere un token UAA, vedi [Acquisizione del token UAA utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Per ottenere un token IAM, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Per ottenere una chiave API, vedi [ottenimento di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Ad esempio, per utilizzare il token IAM, esegui questo comando:

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	Il risultato di questo comando è il seguente:
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Nota:** il token esclude *Bearer*.
	
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
	
	Quindi, esporta la variabile *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Immetti il seguente comando cURL per registrare una regola:
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	dove
	
	* RULE_FILE è il file JSON che definisce la tua regola di avviso.
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* Token è il token di autenticazione UAA o IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
	Per verificare che la regola sia stata creata correttamente, esegui questo comando:
	
	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	Ad esempio:

    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## Passo 3: crea una notifica webhook
{: #step32}


Per creare un file di notifica, considera le seguenti informazioni:

* Utilizza un template di notifica per gli avvisi webhook. Per ulteriori informazioni, vedi [Template di notifica](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template).
* Crea il file in una directory locale, ad esempio, `~/cloud-monitoring/notifications`.

Ad esempio, crea il file **webhook.json** utilizzando l'editor vi: 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "Webhook",
"description" : "Fire this webhook when ....",
	"detail": "https://myendpoint.bluemix.net?key=abcd1234"
	}
```
{: codeblock}	

Per richiamare un webhook, il campo *detail* deve essere impostato sull'URL in cui effettuare il POST. Configura un webhook per gli endpoint https e aggiungi un parametro.
	
Per ulteriori informazioni, vedi [Creazione di una notifica](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create).
	
## Passo 4: Registra il metodo di notifica nel servizio Monitoraggio
{: #step42}
	
Da un terminale, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Ottieni il token di sicurezza. Puoi utilizzare un token UAA, IAM o una chiave API. Scegli uno dei seguenti metodi per ottenere il token di sicurezza:
	
	* Per ottenere un token UAA, vedi [Acquisizione del token UAA utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Per ottenere un token IAM, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Per ottenere una chiave API, vedi [ottenimento di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Ad esempio, per utilizzare il token IAM, esegui questo comando:

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	Il risultato di questo comando è il seguente:
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Nota:** il token esclude *Bearer*.
	
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
	
	Quindi, esporta la variabile *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Immetti il seguente comando cURL per registrare una notifica:

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	dove
	
	* NOTIFICATION_FILE è il file JSON che definisce la tua notifica.
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* Token è il token di autenticazione UAA o IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Per verificare che la notifica sia stata creata correttamente, esegui questo comando:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
