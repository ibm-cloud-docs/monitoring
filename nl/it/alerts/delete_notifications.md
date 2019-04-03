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



# Eliminazione delle notifiche
{: #delete_notifications}

Puoi eliminare le notifiche dal servizio {{site.data.keyword.monitoringshort}} utilizzando [l'API Avvisi](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window}.
{:shortdesc}

Dopo [aver eseguito l'accesso a un regione in {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login), completa la seguente procedura per eliminare una notifica:


## Passo 1: ottieni il token di sicurezza
{: #step1_delete_notifications}

Puoi utilizzare un token UAA, IAM o una chiave API. 

Scegli uno dei seguenti metodi per ottenere il token di sicurezza:
	
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
	

## Passo 2: ottieni l'ID dello spazio 
{: #step2_delete_notifications}

Questo passo viene applicato solo quando vuoi eliminare le notifiche disponibili in un dominio dello spazio.

Per ottenere il GUID dello spazio, immetti il seguente comando:
	
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
	
Quindi, esporta la variabile *Space*. Il GUID deve essere come prefisso *s-* per identificare uno spazio.
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## Passo 3: elenca le notifiche
{: #step3_delete_notifications}


Immetti il seguente comando cURL per elencare le notifiche in un dominio dello spazio:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/notifications

```
{: screen}

Immetti il seguente comando cURL per elencare le notifiche nel dominio dell'account:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/notifications
```
{: screen}

dove
	
* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

    * *apikey* identifica che il token è una chiave API.
	* *iam* identifica che il token specificato è un token generato da IAM.
	* *uaa* identifica che il token specificato è un token generato da UAA.
	
* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. 
	
* Token è il token di autenticazione UAA o IAM o la chiave API.
	
* Space è il GUID dello spazio. 
	
* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).


## Passo 4: elimina una notifica
{: #step4_delete_notifications}
  

Immetti il seguente comando cURL per eliminare una notifica in un dominio dello spazio:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/notification/{name} 
```
{: screen}

Immetti il seguente comando cURL per eliminare una notifica dal dominio dell'account:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/notification/{name} 
```
{: screen}

	
dove
	
* *X-Auth-User-Token* è un parametro che passa il token UAA, il token IAM o la chiave API {{site.data.keyword.Bluemix_notm}}.
	
* *Auth_Type* è il prefisso che definisce il tipo di token o chiave API. Il seguente elenco descrive i valori validi: *apikey*, *iam* o *uaa*, dove

    * *apikey* identifica che il token è una chiave API.
	* *iam* identifica che il token specificato è un token generato da IAM.
	* *uaa* identifica che il token specificato è un token generato da UAA.
	
* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio. 
	
* Token è il token di autenticazione UAA o IAM o la chiave API.
	
* Space è il GUID dello spazio. 
	
* METRICS_ENDPOINT rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *name* è il nome della notifica che vuoi eliminare.
	
