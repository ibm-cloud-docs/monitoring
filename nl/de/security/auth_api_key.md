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


# Mit API-Schlüsseln arbeiten
{: #auth_api_key}

Sie können eine API über die {{site.data.keyword.Bluemix}}-CLI oder die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle abrufen. Der API-Schlüssel läuft nicht ab. Wenn eine API beschädigt ist, können Sie sie neu aufrufen und eine neue API generieren.
{:shortdesc}

## IAM-API-Schlüssel über die IBM Cloud-CLI generieren
{: #iam_apikey_cli}

Führen Sie die folgenden Schritte aus, um einen API-Schlüssel unter Verwendung der {{site.data.keyword.Bluemix_notm}}-CLI zu generieren:

1. (Voraussetzung) Installieren Sie die {{site.data.keyword.Bluemix_notm}}-CLI.

   Weitere Informationen dazu finden Sie unter [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa).
   
   Wenn die CLI installiert ist, fahren Sie mit dem nächsten Schritt fort.
	
2. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
 
3. Führen Sie den Befehl `ibmcloud iam api-key-create` aus, um einen API-Schlüssel zu erstellen.

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	Dabei gilt Folgendes:
	
	* NAME ist der Name des zu erstellenden API-Schlüssels.
	* DESCRIPTION ist der Text, den Sie für die Beschreibung des API-Schlüssels verwenden.
	* FILE ist der Name der Datei, in der der Schlüssel gespeichert wird.
	
    Führen Sie zum Beispiel folgenden Befehl aus, um den API-Schlüssel *MyKey*zu erstellen:
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## IAM-API-Schlüssel über die IBM Cloud-Benutzerschnittstelle generieren
{: #iam_apikey_ui}

Führen Sie die folgenden Schritte aus, um einen API-Schlüssel über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle zu generieren:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://console.bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste der Konsole auf **Verwalten > Sicherheit > IBM Cloud API-Schlüssel**.

3. Klicken Sie auf **API-Schlüssel erstellen**.

4. Geben Sie einen Namen und eine Beschreibung für Ihren API-Schlüssel ein. Klicken Sie anschließend auf **API-Schlüssel erstellen**.

5. Speichern Sie den API-Schlüssel. Klicken Sie auf **API-Schlüssel herunterladen**.

    Klicken Sie auf **Anzeigen**, um den API-Schlüssel anzuzeigen.  

**Hinweis:** Der API-Schlüssel ist während der Erstellung nur zum Anzeigen oder zum Herunterladen verfügbar. Wenn der API-Schlüssel nicht mehr vorhanden ist, müssen Sie einen neuen API-Schlüssel erstellen.  


	
## API-Schlüssel über die IBM Cloud-Benutzerschnittstelle widerrufen
{: #revoke_ui}
	
Führen Sie folgende Schritte aus, um einen IAM-API-Schlüssel über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle zu widerrufen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://console.bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste der Konsole auf **Verwalten > Sicherheit > IBM Cloud API-Schlüssel**.

3. Klicken Sie auf **Aktionen** und dann auf **Schlüssel löschen**.





	

	
	
	
	
	
	
