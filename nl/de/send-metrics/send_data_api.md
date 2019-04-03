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

# Daten mithilfe der Metrik-API senden
{: #send_data_api}

Sie können Metriken an den {{site.data.keyword.monitoringshort}}-Service senden, indem Sie die Metrik-API verwenden. 
{:shortdesc}


Bei den {{site.data.keyword.Bluemix_notm}} Docker-Containern werden die Systemmetriken automatisch erfasst. Bei Cloud Foundry-Anwendungen und Apps, die auf einer virtuellen Maschine ausgeführt werden, müssen Metriken direkt von der App über die [Metrik-API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window} gesendet werden. 



## Metriken an eine Bereichsdomäne senden
{: #space_uaa}

Führen Sie die folgenden Schritte aus, um Metriken mithilfe von cURL an einen Bereich zu senden:

1. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Rufen Sie das Sicherheitstoken ab. Sie können ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden.

    Wählen Sie eine der folgenden Methoden aus, um das Sicherheitstoken abzurufen, das Sie zum Senden von Metriken benötigen:
	
	* Informationen zum Abrufen eines UAA-Tokens finden Sie unter [UAA-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Informationen zum Abrufen eines IAM-Tokens finden Sie unter [IAM-Token über die {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
	Legen Sie auf demselben Terminal, von dem aus Sie sich bei {{site.data.keyword.Bluemix_notm}} angemeldet haben, die *Token*-Variable für das Token fest.

    Legen Sie beispielsweise ein UAA-Token fest und entfernen Sie den Teil *Bearer* (Träger) aus dem Tokenwert:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
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
	
	Exportieren Sie anschließend die Variable *Space*. **Hinweis:** Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.
	
	Beispiel:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
5. Führen Sie den folgenden cURL-Befehl aus, um Metriken zu senden:

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	Dabei gilt Folgendes:
	
	* 'Metrics_File' stellt die JSON-Datei dar, die die Definition der Metriken enthält, die an den {{site.data.keyword.monitoringshort}}-Service gesendet wurden.
	
	* *X-Auth-User-Token* ist ein Parameter, der das Sicherheitstoken übergibt.
	
	* *Auth_Type* ist das Präfix, das den Typ des Tokens definiert. Gültige Werte sind: *uaa* für ein UAA-Token, *iam* für ein IAM-Token und *api* für einen API-Schlüssel.
	
	* *X-Auth-Scope-Id* ist ein Parameter, der die Bereichs-GUID übergibt. Die GUID muss das Präfix *s-* aufweisen, um einen Bereich zu kennzeichnen.
	
	* 'Token' stellt das Sicherheitstoken oder den API-Schlüssel dar.
	
	* 'Space' (Bereich) stellt die GUID des Bereichs dar. 
	
	* 'Endpoint' stellt den Eingangspunkt zum Service dar. Jede Region verfügt über eine andere URL. Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
	Sie können zum Beispiel den folgenden Befehl verwenden, um die beiden Metriken `myhost.cpu.idle` und `myapp.login.attempts` an den {{site.data.keyword.monitoringshort}}-Service zu senden:
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	Die Beispieldatei *metric.json* ist wie folgt definiert:

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
