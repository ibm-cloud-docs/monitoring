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

# E-Mail-Alert mithilfe der {{site.data.keyword.monitoringshort}}-API konfigurieren
{: #configure_email_alert}

Wenn Sie einen E-Mail-Alert für eine Metrik konfigurieren möchten, definieren Sie eine Regel und eine E-Mail-Benachrichtigung. Anschließend registrieren Sie die Regel und die Benachrichtigungsmethode beim {{site.data.keyword.monitoringshort}}-Service.
{:shortdesc}

Führen Sie die folgenden Schritte aus:

## Schritt 1: Erstellen Sie eine Regel.
{: #cea_step1}

Erstellen Sie eine Regel für eine Metrikabfrage, die Sie in Grafana definiert haben. Weitere Informationen finden Sie unter [Eine Regel erstellen](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-rules#create).

Erstellen Sie zum Beispiel die Regeldatei `s-rule-1.json` im Verzeichnis `~/cloud-monitoring/rules/`. 

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
"NOTIFICATION_NAME"
]
}
```
{: screen}

Exportieren Sie anschließend die Variable *RULE_FILE*:
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## Schritt 2: Registrieren Sie die Regel im Überwachungsservice.
{: #cea_step2}
	
Führen Sie von einem Terminal aus die folgenden Schritte durch:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Hinweis:** Das Token schließt *Bearer* (Träger) aus.
	
3. Rufen Sie die Bereichs-GUID ab. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.

    Führen Sie folgenden Befehl aus:
	
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
	
	Exportieren Sie anschließend die Variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Führen Sie den folgenden cURL-Befehl aus, um eine Regel zu registrieren:
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	Dabei gilt Folgendes:
	
	* RULE_FILE ist die JSON-Datei, die Ihre Alertregel definiert.
	
	* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist erforderlich, wenn Sie eine UAA-Tokenauthentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
	* Space (Bereich) ist die GUID des Bereichs. 
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
	Um zu überprüfen, ob die Regel erfolgreich erstellt wurde, führen Sie den folgenden Befehl aus:
	
	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	Beispiel:

    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## Schritt 3: Erstellen Sie eine E-Mail-Benachrichtigung
{: #cea_step3}


Berücksichtigen Sie die folgenden Informationen, wenn Sie eine Benachrichtigungsdatei erstellen, die eine E-Mail sendet:

* Verwenden Sie die Benachrichtigungsvorlage zum Senden von E-Mails. Weitere Informationen finden Sie unter [Benachrichtigungsvorlagen](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template).
* Erstellen Sie die Datei in einem lokalen Verzeichnis, z. B. `~/cloud-monitoring/notifications`.

Erstellen Sie zum Beispiel die Datei **email.json** mit dem Editor vi: 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "Email",
"description" : "Send email to manager of department X when ....",
"detail": "Enter email address, for example, xxx@yyy"
}
```
{: codeblock}	
	
Weitere Informationen finden Sie unter [Eine Benachrichtigung erstellen](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-notifications#notifications_create).
	
## Schritt 4: Registrieren Sie die Benachrichtigungsmethode im Überwachungsservice.
{: #cea_step4}
	
Führen Sie von einem Terminal aus die folgenden Schritte durch:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Hinweis:** Das Token schließt *Bearer* (Träger) aus.
	
3. Rufen Sie die Bereichs-GUID ab. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.

    Führen Sie folgenden Befehl aus:
	
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
	
	Exportieren Sie anschließend die Variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Führen Sie den folgenden cURL-Befehl aus, um eine Benachrichtigung zu registrieren:

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	Dabei gilt Folgendes:
	
	* NOTIFICATION_FILE ist die JSON-Datei, die Ihre Benachrichtigung definiert.
	
	* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel von {{site.data.keyword.Bluemix_notm}} übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist erforderlich, wenn Sie eine UAA-Tokenauthentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
	* Space (Bereich) ist die GUID des Bereichs. 
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    Führen Sie folgenden Befehl aus, um zu überprüfen, ob die Benachrichtigung erfolgreich erstellt wurde:

	```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	Beispiel:
	
    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
