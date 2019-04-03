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



# Metriken löschen
{: #delete_metrics}

Sie können Metriken aus dem {{site.data.keyword.monitoringshort}}-Service löschen, indem Sie die [Metrik-API](https://console.bluemix.net/apidocs/monitoring-metrics-api) verwenden.
{:shortdesc}

Führen Sie nach der [Anmeldung bei einer Region in {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login) die folgenden Schritte aus, um eine Benachrichtigung zu löschen:


## Schritt 1: Sicherheitstoken abrufen
{: #step1_delete_metrics}

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
IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
Exportieren Sie anschließend die Variable *Token*:
	
```
export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
```
{: screen}
	
**Hinweis:** Das Token schließt *Bearer* (Träger) aus.
	
## Schritt 2: Berechtigungen zum Arbeiten mit Metriken verifizieren 
{: #step2_delete_metrics}

Abhängig von der Domäne, in der die Metriken zur Verfügung stehen, müssen die folgenden Informationen beachtet werden:

* Zum Arbeiten mit Metriken, die in einer Bereichsdomäne zur Verfügung stehen, benötigt der Benutzer die Rolle *Entwickler* in dem Cloud Foundry-Bereich, der der Domäne zugeordnet ist. 
* Zum Arbeiten mit Metriken, die in der Kontodomäne zur Verfügung stehen, benötigt der Benutzer eine IAM-Richtlinie mit der Rolle *Administrator*, *Operator* oder *Bearbeiter*.

Führen Sie die folgenden Schritte aus, um Ihre Benutzerberechtigungen zu verifizieren:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://console.bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten>Konto>Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste der Benutzer mit ihren E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Verifizieren Sie die Zugriffsberechtigungen für die Arbeit mit dem {{site.data.keyword.monitoringshort}}-Service.


## Schritt 3: Bereichs-ID abrufen 
{: #step3_delete_metrics}

Dieser Schritt trifft nur zu, wenn Sie Metriken löschen möchten, die in einer Bereichsdomäne verfügbar sind.

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

	

## Schritt 4: Metriken auflisten
{: #step4_delete_metrics}


Führen Sie den folgenden cURL-Befehl aus, um die in einer Bereichsdomäne verfügbaren Metriken aufzulisten:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*

```
{: screen}

Führen Sie den folgenden cURL-Befehl aus, um die in der Kontodomäne verfügbaren Metriken aufzulisten:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*
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

* *query* definiert den angewendeten Filter. Beispiel: Mit `query=metric-service.*` werden alle Metriken aufgelistet, die unter der Hierarchie `metric-service.*` vorhanden sind; mit `query=*` werden alle Metriken in der Domäne aufgelistet.


## Schritt 5 - Option 1: Alle Metriken löschen
{: #step5_delete_metrics}
  

Führen Sie den folgenden cURL-Befehl aus, um alle Metriken in einer Bereichsdomäne zu löschen:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

Führen Sie den folgenden cURL-Befehl aus, um alle Metriken aus der Kontodomäne zu löschen:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

Dabei gilt Folgendes:
	
* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token von {{site.data.keyword.Bluemix_notm}} übergibt.
	
* Auth_Type ist das Präfix, das den Typ des Tokens definiert. Gültige Werte sind: *uaa* für ein UAA-Token, *iam* für ein IAM-Token und *api* für einen API-Schlüssel.
	
* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.
	
* *Token* stellt das Sicherheitstoken dar.
	
* *Space* (Bereich) stellt die GUID des Bereichs dar. 
	
* *METRICS_ENDPOINT* stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

* *query* definiert den angewendeten Filter. `query=*` gibt alle Metriken in der Domäne an.


## Schritt 6 - Option 2: Alle Metriken für einen Service löschen
{: #step6_delete_metrics}
  

Führen Sie den folgenden cURL-Befehl aus, um alle Metriken für einen Service in einer Bereichsdomäne zu löschen:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

Führen Sie den folgenden cURL-Befehl aus, um alle Metriken aus der Kontodomäne zu löschen:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

Dabei gilt Folgendes:
	
* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token von {{site.data.keyword.Bluemix_notm}} übergibt.
	
* Auth_Type ist das Präfix, das den Typ des Tokens definiert. Gültige Werte sind: *uaa* für ein UAA-Token, *iam* für ein IAM-Token und *api* für einen API-Schlüssel.
	
* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.
	
* *Token* stellt das Sicherheitstoken dar.
	
* *Space* (Bereich) stellt die GUID des Bereichs dar. 
	
* *METRICS_ENDPOINT* stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

* *query* definiert den angewendeten Filter. `query=*` gibt alle Metriken in der Domäne an.

* *metric-service.** ist der Name eines Service. Beispiel: `containers-kubernetes`.
