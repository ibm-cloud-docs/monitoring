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


# CRUD-Benachrichtigungen
{: #notifications}

Verwenden Sie die Alerts-API zum Erstellen, Löschen oder Aktualisieren einer Benachrichtigung, um die Details einer Benachrichtigung anzuzeigen und um die Benachrichtigungen aufzulisten, die in einem Bereich definiert sind.
{:shortdesc}

## Eine Benachrichtigung erstellen
{: #notifications_create}

Führen Sie die folgenden Schritte aus, um eine Benachrichtigung zu erstellen:

1. Erstellen Sie eine Benachrichtigungsdatei.

    1. Verwenden Sie eine Benachrichtigungsvorlage zum Erstellen einer Benachrichtigungsdatei. Weitere Informationen finden Sie unter [Benachrichtigungsvorlagen](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template).
	
	2. Aktualisieren Sie die Datei:
	
	    * Geben Sie einen eindeutigen Namen in das Feld *Name* ein. Der Wert für dieses Feld wird später für die Aktualisierung, das Löschen und das Anzeigen von Details für die Benachrichtigung verwendet.
		* Geben Sie eine Beschreibung ein.
		* Geben Sie eine gültige E-Mail-Adresse, einen URL-Endpunkt oder einen PagerDuty-Schlüssel ein.
		
	3. Speichern Sie die Datei. Verwenden Sie beispielsweise ein Präfix wie *s-* für Benachrichtigungen, die Sie für Abfragen definieren, die in einem Bereich ausgeführt werden.
	
	    **Tipp:** Erstellen Sie Ihre Benachrichtigungsdatei im Verzeichnis *~/cloud-monitoring/notifications/*, um die Ressourcen des {{site.data.keyword.monitoringshort_notm}}-Service in einer Gruppe zusammenzufassen. 
	
	4. Exportieren Sie die Variable *NOTIFICATION_FILE*:
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

3. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Hinweis:** Das Token schließt *Bearer* (Träger) aus.
	
4. Rufen Sie die Bereichs-GUID ab. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.

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
	
5. Registrieren Sie eine Benachrichtigung beim {{site.data.keyword.monitoringshort}}-Service.

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* NOTIFICATION_FILE ist die JSON-Datei, die Ihre Benachrichtigung definiert.
	
	* *X-Auth-User-Token* ist ein Parameter, der das {{site.data.keyword.Bluemix_notm}} UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist erforderlich, wenn Sie eine UAA-Tokenauthentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* 'Token' ist das UAA-Token, das IAM-Token oder der API-Schlüssel.
	
	* 'Space' (Bereich) ist die GUID des Bereichs. 
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    Beispiel: 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## Eine Benachrichtigung löschen
{: #notifications_delete}

Führen Sie die folgenden Schritte aus, um eine Benachrichtigung zu löschen:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um eine Benachrichtigung zu löschen:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-User-Token* ist ein Parameter, der das {{site.data.keyword.Bluemix_notm}} UAA-Token, das IAM-Token oder den API-Schlüssel übergibt. Das Token oder der API-Schlüssel muss als Präfix einen der folgenden Werte ausweisen: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
		
	* 'Token' ist das UAA-Token, das IAM-Token oder der API-Schlüssel.
	
	* 'Space' (Bereich) ist die GUID des Bereichs. 
	
	* 'Notification_Name' ist der Name der Benachrichtigung, d. h., der Wert für das Feld *name*, wenn Sie die Eigenschaften einer Benachrichtigung auflisten.
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	


## Alle Benachrichtigungen auflisten
{: #notifications_list}

Führen Sie die folgenden Schritte aus, um alle Benachrichtigungen aufzulisten:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um alle Benachrichtigungen aufzulisten:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* *X-Auth-User-Token* ist ein Parameter, der das {{site.data.keyword.Bluemix_notm}} UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
		
	* *X-Auth-User-Token* ist ein Parameter, der das {{site.data.keyword.Bluemix_notm}} UAA-Token, das IAM-Token oder den API-Schlüssel übergibt. Das Token oder der API-Schlüssel muss als Präfix einen der folgenden Werte ausweisen: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
		
	* 'Token' ist das UAA-Token, das IAM-Token oder der API-Schlüssel.
	
	* 'Space' (Bereich) ist die GUID des Bereichs. 
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

			

## Die Details einer Benachrichtigung anzeigen
{: #show}


Führen Sie die folgenden Schritte aus, um die Informationen zu einer Benachrichtigung anzuzeigen:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um die Details einer Benachrichtigung anzuzeigen:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* *X-Auth-User-Token* ist ein Parameter, der das {{site.data.keyword.Bluemix_notm}} UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
		
	* 'Token' ist das UAA-Token, das IAM-Token oder der API-Schlüssel.
	
	* 'Space' (Bereich) ist die GUID des Bereichs. 
	
	* NOTIFICATION_NAME ist der Name der Benachrichtigung, d. h., der Wert für das Feld *name*, wenn Sie die Eigenschaften einer Benachrichtigung auflisten.
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
     
		

			
## Eine Benachrichtigung testen
{: #test}	
			
Führen Sie die folgenden Schritte aus, um eine Benachrichtigung zu testen:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um eine Benachrichtigung zu testen:

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* *X-Auth-User-Token* ist ein Parameter, der das {{site.data.keyword.Bluemix_notm}} UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-User-Token* ist ein Parameter, der das {{site.data.keyword.Bluemix_notm}} UAA-Token, das IAM-Token oder den API-Schlüssel übergibt. Das Token oder der API-Schlüssel muss als Präfix einen der folgenden Werte ausweisen: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
		
	* 'Token' ist das UAA-Token, das IAM-Token oder der API-Schlüssel.
	
	* 'Space' (Bereich) ist die GUID des Bereichs. 
	
	* NOTIFICATION_NAME ist der Name der Benachrichtigung, d. h., der Wert für das Feld *name*, wenn Sie die Eigenschaften einer Benachrichtigung auflisten.
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	


## Eine Benachrichtigung aktualisieren
{: #notifications_update}

Führen Sie die folgenden Schritte aus, um eine Benachrichtigung zu aktualisieren:

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
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportieren Sie anschließend die Variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um eine Benachrichtigung zu aktualisieren:

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* NOTIFICATION_FILE ist die JSON-Datei, die Ihre Benachrichtigung definiert.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-User-Token* ist ein Parameter, der das Bluemix UAA-Token, das IAM-Token oder den API-Schlüssel übergibt. Das Token oder der API-Schlüssel muss als Präfix einen der folgenden Werte ausweisen: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
		
	* 'Token' ist das UAA-Token, das IAM-Token oder der API-Schlüssel.
	
	* 'Space' (Bereich) ist die GUID des Bereichs. 

	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
        

