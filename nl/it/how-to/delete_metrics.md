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



# Eliminazione delle metriche
{: #delete_metrics}

Puoi eliminare le metriche dal servizio {{site.data.keyword.monitoringshort}} utilizzando [l'API Metriche](https://console.bluemix.net/apidocs/monitoring-metrics-api).
{:shortdesc}

Dopo [aver eseguito l'accesso a un regione in {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login), completa la seguente procedura per eliminare una notifica:


## Passo 1: ottieni il token di sicurezza
{: #step1_delete_metrics}

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
	
## Passo 2: verifica le autorizzazioni per utilizzare le metriche 
{: #step2_delete_metrics}

A seconda del dominio in cui sono disponibili le metriche, esamina le seguenti informazioni:

* Per utilizzare le metriche disponibili in un dominio dello spazio, l'utente ha bisogno del ruolo di *sviluppatore* nello spazio Cloud Foundry associato al dominio. 
* Per utilizzare le metriche disponibili nel dominio dell'account, l'utente ha bisogno di una politica IAM con il ruolo di *amministratore*, *operatore* o *editor*.

Per verificare le autorizzazioni dell'utente, completa la seguente procedura:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.

    Apri un browser web e avvia il dashboard {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}
	
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dalla barra del menu, fai clic su **Gestisci > Account > Utenti**. 

    La finestra *Utenti* visualizza un elenco di utenti con i rispettivi indirizzi email per l'account attualmente selezionato.
	
3. Verifica le autorizzazioni di accesso per utilizzare il servizio {{site.data.keyword.monitoringshort}}.


## Passo 3: ottieni l'ID dello spazio 
{: #step3_delete_metrics}

Questo passo viene applicato solo quando vuoi eliminare le metriche disponibili in un dominio dello spazio.

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

	

## Passo 4: elenca le metriche
{: #step4_delete_metrics}


Immetti il seguente comando cURL per elencare le metriche disponibili in un dominio dello spazio:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*

```
{: screen}

Immetti il seguente comando cURL per elencare le metriche disponibili nel dominio dell'account:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*
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

* *query* definisce il filtro che viene applicato. Ad esempio, `query=metric-service.*` elenca tutte le metriche esistenti nella gerarchia `metric-service.*` e `query=*` elenca tutte le metriche nel dominio.


## Passo 5 - Opzione 1: elimina tutte le metriche
{: #step5_delete_metrics}
  

Immetti il seguente comando cURL per eliminare tutte le metriche in un dominio dello spazio:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

Immetti il seguente comando cURL per eliminare tutte le metriche dal dominio dell'account:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

dove
	
* *X-Auth-User-Token* è un parametro che passa il token UAA {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type è il prefisso che definisce il tipo di token. I valori validi sono: *uaa* per un token UAA, *iam* per un token IAM e *api* per una chiave API.
	
* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio.
	
* *Token* rappresenta il token di sicurezza.
	
* *Space* rappresenta il GUID dello spazio. 
	
* *METRICS_ENDPOINT* rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *query* definisce il filtro che viene applicato. `query=*` indica tutte le metriche nel dominio.


## Passo 6 - Opzione 2: elimina tutte le metriche di un servizio
{: #step6_delete_metrics}
  

Immetti il seguente comando cURL per eliminare tutte le metriche di un servizio in un dominio dello spazio:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

Immetti il seguente comando cURL per eliminare tutte le metriche dal dominio dell'account:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

dove
	
* *X-Auth-User-Token* è un parametro che passa il token UAA {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type è il prefisso che definisce il tipo di token. I valori validi sono: *uaa* per un token UAA, *iam* per un token IAM e *api* per una chiave API.
	
* *X-Auth-Scope-Id* è un parametro che passa il GUID dello spazio. Il GUID deve essere come prefisso *s-* per identificare uno spazio.
	
* *Token* rappresenta il token di sicurezza.
	
* *Space* rappresenta il GUID dello spazio. 
	
* *METRICS_ENDPOINT* rappresenta il punto di ingresso del servizio. Ogni regione ha un URL differente. Per ottenere un elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *query* definisce il filtro che viene applicato. `query=*` indica tutte le metriche nel dominio.

* *metric-service.** è il nome di un servizio. Ad esempio, `containers-kubernetes`.
