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

# Metriken abrufen
{: #retrieve_data_api}

Sie können Metriken vom {{site.data.keyword.monitoringshort}}-Service abrufen, indem Sie die [Metrik-API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window} verwenden.
{:shortdesc}


## Metriken aus einem Bereich abrufen
{: #uaa}

Führen Sie die folgenden Schritte aus, um Metriken von einem Bereich abzurufen:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Legen Sie das Sicherheitstoken oder den API-Schlüssel fest.
  
    Sie müssen das Feld **X-Auth-User-Token** mit einem Sicherheitstoken oder einem API-Schlüssel definieren. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden.

    Wählen Sie zunächst eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen, das Sie zum Senden von Metriken benötigen:
	
    * Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
    
	* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
    
	* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key). 

    Ein Token oder API-Schlüssel muss als Präfix einen der folgenden Werte ausweisen: `apikey`, `iam` oder `uaa`. 

    Dabei gilt Folgendes: 

    * *apikey* gibt an, dass es sich bei dem Token um einen API-Schlüssel handelt.
    * *iam* gibt an, dass es sich bei dem angegebenen Token um ein IAM-generiertes Token handelt.
    * *uaa* gibt an, dass das Token ein UAA-generiertes Token ist.

    Sie können zum Beispiel den folgenden Header für einen API-Schlüssel festlegen: `X-Auth-User-Token: apikey SomeIAMGeneratedKey`
	
	Legen Sie dann auf demselben Terminal, von dem aus Sie sich bei {{site.data.keyword.Bluemix_notm}} angemeldet haben, die Token-Variable für das Token fest.

    Legen Sie beispielsweise ein UAA-Token fest und entfernen Sie den Teil *Bearer* (Träger) aus dem Tokenwert:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. Rufen Sie die Bereichs-ID ab.

    Zum Abrufen von Metriken ist das Headerfeld **X-Auth-Scope-Id** erforderlich, das auf die Bereichs-GUID festgelegt werden muss. 

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
	
	Exportieren Sie anschließend die Variable *Space*. **Hinweis:** Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.
	
	Beispiel:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}

4. Führen Sie den folgenden cURL-Befehl aus, um Metriken zu senden:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	Dabei gilt Folgendes:
	
	* *X-Auth-User-Token* ist ein Parameter, der das UAA-Token von {{site.data.keyword.Bluemix_notm}} übergibt.
	
	* Auth_Type ist das Präfix, das den Typ des Tokens definiert. Gültige Werte sind: *uaa* für ein UAA-Token, *iam* für ein IAM-Token und *api* für einen API-Schlüssel.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen. Dieser Header ist nur erforderlich, falls Sie die UAA-Authentifizierung verwenden. Wenn Sie ein IAM-Authentifizierungstoken verwenden, dann ist dieser Header optional und die Domäneninformationen, die an das Token gebunden sind, werden verwendet.
	
	* *Token* stellt das Sicherheitstoken dar.
	
	* *Space* (Bereich) stellt die GUID des Bereichs dar. 
	
	* *Start_Time* gibt den Beginn der Anforderung an. Diese Information wird zur Berechnung des relativen oder absoluten Zeitraums verwendet. *End_Time* gibt das Ende der Anforderung an. Diese Information wird zur Berechnung des relativen oder absoluten Zeitraums verwendet. Weitere Informationen finden Sie unter [Zeitraum festlegen](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#time).
	
	* *Path* gibt eine oder mehrere Metriken an. Optional können Sie Funktionen für die jeweilige Metrik anwenden. Die Pfadangabe unterstützt auch Platzhalterzeichen, mit denen Sie mehrere Metriken in einem einzelnen Pfad angeben können. Weitere Informationen finden Sie in [Metriken definieren](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#metrics).
	
	* *METRICS_ENDPOINT* stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	

	
## Metriken definieren
{: #metrics}

Zum Abrufen von Daten für eine Metrik müssen Sie den Pfad der Metrik vom Stammverzeichnis der Metrikverzeichnisstruktur bis zur betreffenden Metrik angeben; dabei müssen die einzelnen Schritte durch einen Punkt (.) voneinander getrennt werden.

Der Pfad wird im Parameter **Target** angegeben. Pro Anforderung können maximal 5 Ziele angegeben werden.  

Optional können Sie Funktionen für die Metrik anwenden. Weitere Informationen zu unterstützten Funktionen finden Sie unter [Graphite 0.9.15-Funktionen ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://graphite.readthedocs.io/en/latest/functions.html).

Für die Definition eines Pfads können Platzhalter verwendet werden. Mithilfe von Platzhaltern können Sie mehrere Metriken in einem einzelnen Pfad angeben. 

* **Stern**: Sie können einen Stern (*) als Platzhalter für null, ein oder mehrere Zeichen angeben. 

    Innerhalb eines einzelnen Pfadelements können mehrere Sterne verwendet werden. Beispiel: `servers.sp*aeg*r.cpu.total.*`. Mit diesem Beispiel werden Daten zur gesamten CPU-Nutzung für alle Server, die dem Muster entsprechen, zurückgegeben.

* **Liste oder Bereich mit Zeichen**: Sie können Zeichen in eckigen Klammern ([...]) definieren, um eine einzelne Zeichenposition in der Pfadzeichenfolge anzugeben. 

    Sie können einen einschließenden Bereich von Zeichen festlegen, indem Sie zwei Zeichen angeben, die durch einen Bindestrich getrennt sind. Alle Zeichen zwischen diesen beiden Zeichen werden für die Pfadangabe verwendet. 
	
	Sie können innerhalb der eckigen Klammern einen oder mehrere Zeichenbereiche definieren. 
	
	Wenn die Zeichen innerhalb der eckigen Klammern nicht als Bereich gelesen werden können, werden sie als Liste mit Werten behandelt. 
	
	Sie können einen Bindestrich (-) als Zeichen in einer Werteliste angeben, indem Sie ihn an die erste oder letzte Stelle innerhalb der eckigen Klammern setzen.

* **Werteliste**: Sie können durch Kommas getrennte Werte innerhalb von geschweiften Klammern festlegen, um Wertelisten zu definieren. 

    Beispiel: Zum Herunterladen von Metriken für die Pfade `servers.myserver.cpu.total.user` und `servers.myserver.cpu.total.system` können Sie einen einzelnen Pfad für beide Typen festlegen: `servers.myserver.cpu.total.{user,system}`



## Zeitraum festlegen
{: #time}

Sie können optional einen Zeitraum angeben, indem Sie eine relative Zeit oder eine absolute Zeit verwenden. Sie müssen die Abfrageparameter **From** und **Until** definieren.  

* Wenn die Startzeit des Zeitraums nicht angegeben wird, wird als Standardwert der Zeitpunkt 24 Stunden zuvor verwendet. 

* Wenn die Endzeit des Zeitraums nicht angegeben wird, ist der Standardwert die aktuelle Uhrzeit *now*.

Der **relativen Zeit** wird stets ein Minuszeichen (-) vorangestellt und eine Zeiteinheit angefügt. 

In der folgenden Tabelle sind die verschiedenen Abkürzungen für die relative Zeit aufgeführt, die verwendet werden können:


| Abkürzung | Beschreibung |
|--------------|-------------|
| s            | Sekunden     |
| min          | Minuten     |
| h            | Stunden       |
| d            | Tage        |
| w            | Wochen       |
| mon          | Monate      |
| now          | Aktuelle Uhrzeit |


Sie können eines der folgenden Formate verwenden, um eine **absolute Zeit** zu definieren: `HH:MM_JJMMTT`, `JJJJMMTT`, `MM/TT/JJ`

| Abkürzung | Beschreibung |
|--------------|-------------|
| JJJJ         | Vierstellige Jahresangabe |
| MM           | Zweistellige Monatsangabe (01 = Jan usw.) |
| TT           | Zweistellige Angabe des Tags im Monat (01 bis 31) |
| hh           | Zweistellige Stundenangabe (00 bis 23) |
| mm           | Zweistellige Minutenangabe (00 bis 59) |
| ss           | Zweistellige Sekundenangabe (00 bis 59) |

**Beispiel**

In der folgenden Tabelle sind verschiedene Beispiele für das Festlegen unterschiedlicher Zeiträume mit den Parametern *from* und *until* aufgeführt:

<table>
  <caption>Tabelle 1. Verschiedene Beispiele für das Festlegen unterschiedlicher Zeiträume mit den Parametern *from* und *until*</caption>
  <tr>
    <th>Beispiel</th>
	<th>Beschreibung</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>Zeitraum, der Daten vom letzten Montag bis jetzt umfasst.</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>Zeitraum, für den ein Monat festgelegt wird, z. B. November. </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>Anzeigen von Daten in einem 12 Stunden umfassenden Zyklus, z. B. von 02:00 Uhr bis 14:00 Uhr am 01. Juli 2017.</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>Anzeigen von Daten für denselben Wochentag, z. B. letzte Woche.</td>
  </tr>
  
</table>


