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


# Notifiche CRUD
{: #notifications}

Utilizza l'API Avvisi per creare, eliminare e aggiornare una notifica, per visualizzare i dettagli di una notifica e per elencare le notifiche definite in uno spazio.
{:shortdesc}

## Creazione di una notifica
{: #notifications_create}

Per creare una notifica, completa la seguente procedura:

1. Crea un file di notifica.

    1. Utilizza un template di notifica per creare un file di notifica. Per ulteriori informazioni, vedi [Template di notifica](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template).
	
	2. Aggiorna il file:
	
	    * Immetti un nome univoco nel campo *name*. Il valore di questo campo viene utilizzato in seguito per aggiornare, eliminare e mostrare i dettagli della notifica.
		* Immetti una descrizione.
		* Immetti un indirizzo e-mail, un endpoint URL o una chiave PagerDuty validi.
		
	3. Salva il file. Ad esempio, utilizza un prefisso come *s-* per le notifiche che definisci per le query in esecuzione in uno spazio.
	
	    **Suggerimento:** crea il tuo file di notifica nella seguente directory: *~/cloud-monitoring/notifications/* per raggruppare le risorse del servizio {{site.data.keyword.monitoringshort_notm}}. 
	
	4. Esporta la variabile *NOTIFICATION_FILE*:
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

3. Ottieni il token di sicurezza. Puoi utilizzare un token UAA, IAM o una chiave API. Scegli uno dei seguenti metodi per ottenere il token di sicurezza:
	
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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Nota:** il token esclude *Bearer*.
	
4. Ottieni il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio.

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
	
5. Registra una notifica con il servizio {{site.data.keyword.monitoringshort}}.

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	dove
	
	* NOTIFICATION_FILE è il file JSON che definisce la tua notifica.
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* Token è il token UAA, il token IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Ad esempio, 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## Eliminazione di una notifica
{: #notifications_delete}

Per eliminare una notifica, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per eliminare una notifica:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	dove
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}. Il token o la chiave API devono avere come prefisso uno dei seguenti valori: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
		
	* Token è il token UAA, il token IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* Notification_Name è il nome della notifica, ossia, il valore del campo *name* quando elenchi le proprietà di una notifica.
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	


## Elenco di tutte le notifiche
{: #notifications_list}

Per elencare tutte le notifiche, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per elencare tutte le notifiche:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	dove
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
		
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}. Il token o la chiave API devono avere come prefisso uno dei seguenti valori: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
		
	* Token è il token UAA, il token IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

			

## Visualizzazione dei dettagli di una notifica
{: #show}


Per visualizzare le informazioni su una notifica, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per visualizzare i dettagli di una notifica:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	dove
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
		
	* Token è il token UAA, il token IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* NOTIFICATION_NAME è il nome della notifica, ossia, il valore del campo *name* quando elenchi le proprietà di una notifica.
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
     
		

			
## Verifica di una notifica
{: #test}	
			
Per verificare una notifica, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per verificare una notifica:

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	dove
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}. Il token o la chiave API devono avere come prefisso uno dei seguenti valori: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
		
	* Token è il token UAA, il token IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* NOTIFICATION_NAME è il nome della notifica, ossia, il valore del campo *name* quando elenchi le proprietà di una notifica.
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	


## Aggiornamento di una notifica
{: #notifications_update}

Per aggiornare una notifica, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per aggiornare una notifica:

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	dove
	
	* NOTIFICATION_FILE è il file JSON che definisce la tua notifica.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API Bluemix. Il token o la chiave API devono avere come prefisso uno dei seguenti valori: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
		
	* Token è il token UAA, il token IAM o la chiave API.
	
	* Space è il GUID dello spazio. 

	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
        

