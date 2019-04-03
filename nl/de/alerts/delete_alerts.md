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



# Alerts löschen
{: #delete_alerts}

Sie können Alerts aus dem {{site.data.keyword.monitoringshort}}-Service löschen, indem Sie [Alert-API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window} verwenden.
{:shortdesc}


Führen Sie nach der [Anmeldung bei einer Region in {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login) die folgenden Schritte aus, um eine Benachrichtigung zu löschen:


## Schritt 1: Sicherheitstoken abrufen
{: #step1_delete_alerts}

Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. 

Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
* Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
Führen Sie zum Beispiel den folgenden Befehl aus, um das IAM-Token zu verwenden:

```
ibmcloud iam oauth-tokens
```
{: codeblock}
	
Das Ergebnis dieses Befehls lautet wie folgt:
	
```
IAM token:  Bearer djn.._l_HWtlNTibmcloudsl0qjBI9GqCnuQ
UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
Exportieren Sie anschließend die Variable *Token*:
	
```
export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
```
{: screen}
	
**Hinweis:** Das Token schließt *Bearer* (Träger) aus.
	

## Schritt 2: Bereichs-ID abrufen 
{: #step2_delete_alerts}

Dieser Schritt trifft nur zu, wenn Sie Alerts löschen möchten, die in einer Bereichsdomäne verfügbar sind.

Führen Sie den folgenden Befehl aus, um die Bereichs-GUID abzurufen:
	
```
ibmcloud iam space SpaceName --guid
```
{: codeblock}
	
Dabei ist *SpaceName* der Name des Bereichs, in dem Sie eine Benachrichtigung definieren werden. 
	
Um beispielsweise die GUID eines Bereichs mit dem Namen *dev* abzurufen, führen Sie den folgenden Befehl aus:
	
```
ibmcloud iam space dev --guid
```
{: screen}
	
Das Ergebnis dieses Befehls lautet wie folgt:
	
```
667fadfc-jhtg-1234-9f0e-cf4123451095
```
{: screen}
	
Exportieren Sie anschließend die Variable *Space*. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## Schritt 3: Regeln auflisten
{: #step3_delete_alerts}


Führen Sie den folgenden cURL-Befehl aus, um die in einer Bereichsdomäne definierten Regeln aufzulisten:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules

```
{: screen}

Führen Sie den folgenden cURL-Befehl aus, um die Benachrichtigungen in der Kontodomäne aufzulisten:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules
```
{: screen}

Dabei gilt Folgendes:
	
* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel von {{site.data.keyword.Bluemix_notm}} übergibt.
	
* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

    * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
	* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
	* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. 
	
* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
* Space (Bereich) ist die GUID des Bereichs. 
	
* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).


## Schritt 4: Alertregel löschen
{: #step4_delete_alerts}
  

Führen Sie den folgenden cURL-Befehl aus, um eine Regel in einer Bereichsdomäne zu löschen:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

Führen Sie den folgenden cURL-Befehl aus, um eine Regel aus der Kontodomäne zu löschen:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

	
Dabei gilt Folgendes:
	
* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel von {{site.data.keyword.Bluemix_notm}} übergibt.
	
* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

    * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
	* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
	* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. 
	
* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
* Space (Bereich) ist die GUID des Bereichs. 
	
* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

* *Name* ist der Name der Regel, die gelöscht werden soll.
	
