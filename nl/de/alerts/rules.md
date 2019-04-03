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


# CRUD-Regeln
{: #rules}

Verwenden Sie die Alerts-API, um eine Regel zu erstellen, zu löschen oder zu aktualisieren, um die Details einer Regel anzuzeigen und um die Regeln aufzulisten, die in einem Bereich definiert sind.
{:shortdesc}


## Eine Regel erstellen
{: #create}

Zum Konfigurieren einer Regel im {{site.data.keyword.monitoringshort}}-Service erstellen Sie eine Regeldatei, die die Regeldetails enthält, und registrieren Sie die Regel beim {{site.data.keyword.monitoringshort}}-Service.

Führen Sie die folgenden Schritte aus:

1. Erstellen Sie eine Regeldatei mit Daten im JSON-Format. Speichern Sie die Datei. 

    Verwenden Sie zum Speichern der Datei beispielsweise ein Präfix wie *s-* für Regeln, die Sie für Abfragen definieren, die in einem Bereich ausgeführt werden.
	
	**Tipps:** 
	
	* Definieren Sie verschiedene Regeln für eine Abfrage, um auf Fehler oder Warnungen hinzuweisen, indem Sie eine andere Benachrichtigungsmethode verwenden. 
	* Erstellen Sie Ihre Regeldatei im Verzeichnis *~/cloud-monitoring/rules/*, um die Ressourcen des {{site.data.keyword.monitoringshort_notm}}-Service in einer Gruppe zusammenzufassen. 

    Geben Sie die folgenden Informationen in der Regeldatei ein:
	
	* * name *: Geben Sie einen eindeutigen Namen ein. Der Wert für dieses Feld wird später für die Aktualisierung, das Löschen und das Anzeigen von Details für die Regel verwendet.
	* *description*: Geben Sie eine Beschreibung ein.
	* *expression*: Geben Sie die Abfrage, die Sie überwachen möchten, ein.
	* *enabled*: Legen Sie für die Eigenschaft *true* fest, um die Regel zu aktivieren.
	* *from*: Anfangszeitpunkt, der für die Analyse der Daten auf Grundlage von Grenzwerten verwendet wird.
	* *until*: Exitzeitpunkt, der für die Analyse der Daten auf Grundlage von Grenzwerten verwendet wird.
	* *comparison*: Vergleichsoperation, die zur Identifizierung der durchzuführenden Art der Überprüfung verwendet wird. Beispiel: *below*.
	* *error_level*: Definiert den Schwellenwert, den Sie als Auslöser für einen Fehleralert festlegen.
	* *warning_level*: Definiert den Schwellenwert, den Sie als Auslöser für einen Warnungsalert festlegen.
	* *frequency*: Definiert wie oft Sie die Daten überprüfen.
	* *dashboard_url*: Definiert eine URL, die in Grafana ein Dashboard mit der Abfrage anzeigt.
	* *notifications*: Die Benachrichtigungsmethode für den Fall, dass der durch diese Regel beschriebene Alert ausgelöst wird.
	
	Die Regeldatei 'myrulefile.json' sieht wie im folgenden Beispiel aus:
	
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
	
	Exportieren Sie anschließend die Variable *RULE_FILE*:
	
	```
	export RULE_FILE="myrulefile.json"
	```
	{: screen}
	
2. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an.

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

3. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
	* Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
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
	
5. Führen Sie den folgenden cURL-Befehl aus, um die Regel beim {{site.data.keyword.monitoringshort}}-Service zu registrieren:

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* RULE_FILE ist die JSON-Datei, die Ihre Alertregel definiert.
	
	* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel von {{site.data.keyword.Bluemix_notm}} übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist erforderlich, wenn Sie eine UAA-Tokenauthentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
	* Space (Bereich) ist die GUID des Bereichs. 
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Beispiel: 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## Eine Regel löschen
{: #delete}

Führen Sie die folgenden Schritte aus, um eine Regel zu löschen:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
	* Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
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
		
4. Führen Sie den folgenden cURL-Befehl aus, um eine Regel zu löschen:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
    * *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist erforderlich, wenn Sie eine UAA-Tokenauthentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
	* Space (Bereich) ist die GUID des Bereichs. 
	
	* Rule_Name ist der Name der Regel, die im Feld *name* angegeben ist.
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    
	
## Alle Regeln auflisten
{: #list}

Führen Sie die folgenden Schritte aus, um alle Regeln aufzulisten:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
	* Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um alle Regeln in einem Bereich aufzulisten:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist erforderlich, wenn Sie eine UAA-Tokenauthentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
	* Space (Bereich) ist die GUID des Bereichs. 
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

	
	

## Die Details einer Regel anzeigen
{: show}

Führen Sie die folgenden Schritte aus, um die Details einer Regel anzuzeigen:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
	* Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um die Details einer Regel anzuzeigen:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token, das IAM-Token oder den API-Schlüssel übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens oder des API-Schlüssels definiert. Die folgende Liste enthält die gültigen Werte: *apikey*, *iam* oder *uaa*. Dabei gilt Folgendes:

        * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
		* *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
		* *uaa* gibt an, dass es sich bei dem Token um ein UAA-generiertes Token handelt.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist erforderlich, wenn Sie eine UAA-Tokenauthentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* Token ist das UAA- oder IAM-Authentifizierungstoken oder der API-Schlüssel.
	
	* Space (Bereich) ist die GUID des Bereichs. 
	
	* Rule_Name ist der Name der Regel, die im Feld *name* angegeben ist.
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

## Eine Regel aktualisieren
{: #update}

_Um eine Regel zu aktualisieren, müssen Sie die Regel ändern, indem Sie die Regeldatei aktualisieren, und anschließend die folgenden Schritte ausführen:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen:
	
	* Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
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
	
4. Führen Sie den folgenden cURL-Befehl aus, um eine Regel zu aktualisieren:

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
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
	
	* METRICS_ENDPOINT stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

	
	
