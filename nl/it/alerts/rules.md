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


# Regole CRUD
{: #rules}

Utilizza l'API Avvisi per creare, eliminare o aggiornare una regola, per visualizzare i dettagli di una regola e per elencare le regole definite in uno spazio.
{:shortdesc}


## Creazione di una regola
{: #create}

Per configurare una regola nel servizio {{site.data.keyword.monitoringshort}}, crea un file delle regole che ne include i dettagli e la registra con il servizio {{site.data.keyword.monitoringshort}}.

Completa la seguente procedura:

1. Crea un file di regole che contiene un JSON valido. Salva il file. 

    Ad esempio, per salvare il file, utilizza un prefisso come *s-* per le regole che definisci per le query in esecuzione in uno spazio.
	
	**Suggerimenti:** 
	
	* Definisci diverse regole per una query per la segnalazione di errori o avvertenze utilizzando un metodo di notifica differente. 
	* Crea il tuo file di regole nella seguente directory: *~/cloud-monitoring/rules/* per raggruppare le risorse del servizio {{site.data.keyword.monitoringshort_notm}}. 

    Nel file delle regole, immetti le seguenti informazioni:
	
	* *name*: immetti un nome univoco. Il valore di questo campo viene utilizzato in seguito per aggiornare, eliminare e mostrare i dettagli della regola.
	* *description*: immetti una descrizione.
	* *expression*: immetti la query che desideri monitorare.
	* *enabled*: imposta su *true* per abilitare la regola.
	* *from*: punto temporale iniziale utilizzato per analizzare i dati in base ai valori di soglia.
	* *until*: punto temporale finale utilizzato per analizzare i dati in base ai valori di soglia.
	* *comparison*: operazione di confronto utilizzata per identificare il tipo di controllo da effettuare, ad esempio *below*.
	* *error_level*: definisce la soglia che imposti per attivare un avviso di errore.
	* *warning_level*: definisce la soglia che imposti per attivare un avviso di avvertenza.
	* *frequency*: definisce la frequenza di controllo dei dati.
	* *dashboard_url*: definisce un URL che mostra in Grafana un dashboard con la query.
	* *notifications*: il metodo di notifica nel caso in cui venga attivato l'avviso descritto con questa regola.
	
	Ad esempio, il file delle regole myrulefile.json è simile al seguente:
	
	```
	{
    "name": "checkbytesin",
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
      "emailXXX"
    ]
    }
    ```
	{: screen}
	
	Quindi, esporta la variabile *RULE_FILE*:
	
	```
	export RULE_FILE="myrulefile.json"
	```
	{: screen}
	
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}.

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

3. Ottieni il token di sicurezza. Puoi utilizzare un token UAA, IAM o una chiave API. Scegli uno dei seguenti metodi per ottenere il token di sicurezza:
	
	* Per ottenere un token UAA, vedi [Acquisizione del token UAA utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli.
	
	* Per ottenere un token IAM, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Per ottenere una chiave API, vedi [ottenimento di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Ad esempio, per utilizzare il token IAM, esegui questo comando:
    
    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}
	
    Il risultato di questo comando è il seguente:
	
    ```
    IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
    ```
    {: screen}
	
    Quindi, esporta la variabile *Token*:
	
    ```
    export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
5. Immetti il seguente comando cURL per registrare la regola nel servizio {{site.data.keyword.monitoringshort}}:

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
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
	
    Ad esempio, 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## Eliminazione di una regola
{: #delete}

Per eliminare una regola, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
		
4. Immetti il seguente comando cURL per eliminare una regola:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	dove
	
    * *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* Token è il token di autenticazione UAA o IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* Rule_Name è il nome della regola come specificato nel campo *name*.
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    
	
## Elenco di tutte le regole
{: #list}

Per elencare tutte le regole, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per elencare tutte le regole in uno spazio:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	dove
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* Token è il token di autenticazione UAA o IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

	
	

## Visualizzazione dei dettagli di una regola
{: show}

Per visualizzare una regola, completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per visualizzare i dettagli di una regola:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	dove
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* Token è il token di autenticazione UAA o IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* Rule_Name è il nome della regola come specificato nel campo *name*.
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

## Aggiornamento di una regola
{: #update}

Per aggiornare una regola, modificala aggiornando il file delle regole e quindi completa la seguente procedura:

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Quindi, esporta la variabile *Token*:
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. Immetti il seguente comando cURL per aggiornare una regola:

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	dove
	
	* RULE_FILE è il file JSON che definisce la tua regola di avviso.
	
	* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
	* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

        * *apikey* identifica che il token è una chiave API.
		* *iam* identifica che il token specificato è un token generato da IAM.
		* *uaa* identifica che il token specificato è un token generato da UAA.
	
	* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
	* Token è il token di autenticazione UAA o IAM o la chiave API.
	
	* Space è il GUID dello spazio. 
	
	* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

	
	
