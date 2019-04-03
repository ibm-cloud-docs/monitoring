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


# UAA-Token abrufen
{: #auth_uaa}

Verwenden Sie das {{site.data.keyword.Bluemix}} UAA-Modell, um ein Authentifizierungstoken abzurufen, das Sie verwenden können, um mit dem {{site.data.keyword.monitoringshort}}-Service zu arbeiten. Sie können das Authentifizierungstoken abrufen, indem Sie die {{site.data.keyword.Bluemix_notm}}-CLI verwenden.
{:shortdesc}

Das Token hat eine Ablaufzeit. 
		
## UAA-Token über die IBM Cloud-CLI abrufen
{: #uaa_cli}


Führen Sie die folgenden Schritte aus, um das UAA-Token abzurufen:

1. (Voraussetzung) Installieren Sie die {{site.data.keyword.Bluemix_notm}}-CLI.

   Weitere Informationen dazu finden Sie unter [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa).
   
   Wenn die CLI installiert ist, fahren Sie mit dem nächsten Schritt fort.
    
2. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
	
3. Führen Sie den Befehl `ibmcloud iam oauth-tokens` aus, um das UAA-Token abzurufen.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	Die Ausgabe gibt das UAA-Token zurück.

**Hinweis:** Wenn Sie das Token verwenden, müssen Sie *Bearer* (Träger) aus dem Wert des Tokens entfernen, das Sie in API-Aufrufen übergeben.
	


	
