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


# Recupero della cronologia di un avviso utilizzando l'API Avvisi
{: #retrieve_history}

Utilizza l'API Avvisi per recuperare la cronologia di un avviso. 
{:shortdesc}


Per recuperare la cronologia di un avviso utilizzando l'API Avvisi, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Ottieni il token di sicurezza. Puoi utilizzare un token UAA, IAM o una chiave API. Scegli uno dei seguenti metodi per ottenere il token di sicurezza:
	
	* Per ottenere un token UAA, vedi [Acquisizione del token UAA utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Per ottenere un token IAM, vedi [Acquisizione del token IAM utilizzando la CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Per ottenere una chiave API, vedi [ottenimento di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Dallo stesso terminale a cui hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, configura la variabile Token per il token.

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
	
	Quindi, esporta la variabile *Space*. **Nota:** il GUID deve avere come prefisso *s-* per identificare uno spazio.
	
	Ad esempio:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Recupero della cronologia di una regola

    * Per richiamare la cronologia di una regola per il suo nome, consulta [Richiamo della cronologia di una regola utilizzando il suo nome](/docs/services/cloud-monitoring/alerts/retrieve_history.html#by_name).
	* Per richiamare la cronologia di una regola per un periodo di tempo, consulta [Richiamo della cronologia di una regola per le ultime 48 ore](/docs/services/cloud-monitoring/alerts/retrieve_history.html#by_time).
	* Per richiamare un numero di voci dalla cronologia di una regola, consulta [Richiamo delle ultime 3 voci nella cronologia di una regola](/docs/services/cloud-monitoring/alerts/retrieve_history.html#number).
	
	
## Recupero della cronologia di una regola per il nome della regola
{: #by_name}
	
Immetti il seguente comando cURL per ottenere la cronologia di un avviso:

```
curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/history?rule_name=RULE_NAME
```
{: codeblock}
	
dove
	
* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

    * *apikey* identifica che il token è una chiave API.
	* *iam* identifica che il token specificato è un token generato da IAM.
	* *uaa* identifica che il token specificato è un token generato da UAA.
	
* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
* *Token* è il token di autenticazione UAA o IAM o la chiave API.
	
* *Space* è il GUID dello spazio. 
	
* *RULE_NAME* è il nome della regola utilizzata per attivare l'avviso. Il valore è quello specificato nel campo *name*.
	
* *METRICS_ENDPOINT* rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    
Ad esempio, la cronologia della regola `highNginxCPU` è la seguente:

```
curl -XGET --header "X-Auth-User-Token: iam ${Token}" --header "X-Auth-Scope-Id: ${Space}" https://metrics.ng.bluemix.net/v1/alert/history?rule_name=highNginxCPU
```
{: screen}

```
[
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T22.23.21.000",
 "value": 99.5,
 "from_level": "OK",
 "to_level": "ERROR"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.11.12.123",
 "value": 98.5,
 "from_level" : "OK",
 "to_level": "WARN"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.12.14.000",
 "value": 97.0,
 "from_level" : "WARN",
 "to_level": "OK"
 }
]
```
{: screen}


## Richiamo della cronologia di una regola per le ultime 48 ore
{: #by_time}

Immetti il seguente comando cURL per ottenere la cronologia di un avviso per le ultime 48 ore:

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?start=-48h
```
{: codeblock}

dove
	
* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

    * *apikey* identifica che il token è una chiave API.
	* *iam* identifica che il token specificato è un token generato da IAM.
	* *uaa* identifica che il token specificato è un token generato da UAA.
	
* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
* *Token* è il token di autenticazione UAA o IAM o la chiave API.
	
* *Space* è il GUID dello spazio. 
	
* *RULE_NAME* è il nome della regola utilizzata per attivare l'avviso. Il valore è quello specificato nel campo *name*.
	
* *METRICS_ENDPOINT* rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

## Richiamo delle ultime 3 voci nella cronologia di una regola
{: #number}

Immetti il seguente comando cURL per ottenere le ultime 3 voci nella cronologia di una regola:

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?max_results=3
```
{: codeblock}

dove
	
* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API.
	
* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

    * *apikey* identifica che il token è una chiave API.
	* *iam* identifica che il token specificato è un token generato da IAM.
	* *uaa* identifica che il token specificato è un token generato da UAA.
	
* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. Questa intestazione è obbligatoria se utilizzi un'autenticazione token UAA. Se utilizzi un token di autenticazione IAM, questa intestazione è facoltativa e vengono utilizzate le informazioni di dominio associate al token.
	
* *Token* è il token di autenticazione UAA o IAM o la chiave API.
	
* *Space* è il GUID dello spazio. 
	
* *RULE_NAME* è il nome della regola utilizzata per attivare l'avviso. Il valore è quello specificato nel campo *name*.
	
* *METRICS_ENDPOINT* rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
