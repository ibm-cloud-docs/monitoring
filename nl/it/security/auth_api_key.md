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


# Utilizzo delle chiavi API
{: #auth_api_key}

Puoi ottenere un'API utilizzando la CLI {{site.data.keyword.Bluemix}} o la IU {{site.data.keyword.Bluemix_notm}}. La chiave API non scade. Se un'API è compromessa, puoi revocarla e generarne una nuova.
{:shortdesc}

## Generazione di una chiave API IAM utilizzando la CLI IBM Cloud
{: #iam_apikey_cli}

Completa la seguente procedura per generare una chiave API utilizzando la CLI {{site.data.keyword.Bluemix_notm}}:

1. (Pre-req) Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa).
   
   Se la CLI è installata, vai al passo successivo.
	
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
 
3. Esegui il comando `ibmcloud iam api-key-create` per creare una chiave API.

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	dove
	
	* NAME è il nome della chiave API da creare.
	* DESCRIPTION è il testo utilizzato per descrivere la chiave API.
	* FILE è il nome del file in cui viene salvata la chiave.
	
    Ad esempio, per creare una chiave API *MyKey*, immetti il seguente comando:
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## Generazione di una chiave API IAM utilizzando la IU IBM Cloud
{: #iam_apikey_ui}

Completa la seguente procedura per generare una chiave API attraverso l'IU {{site.data.keyword.Bluemix_notm}}:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.

    Apri un browser web e avvia il dashboard {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}
	
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dalla barra dei menu della console, fai clic su **Gestisci > Sicurezza > Chiavi API IBM Cloud**.

3. Fai clic su **Crea chiave API**.

4. Immetti un nome e una descrizione per la tua chiave API. Quindi, fai clic su **Crea chiave API**.

5. Salva la chiave API. Fai clic su **Scarica chiave API**.

    Fai clic su **Mostra** per visualizzare la chiave API.  

**Nota:** la chiave API è disponibile per la visualizzazione o il download solo durante la fase di creazione. Se la chiave API viene persa, dovrai crearne una nuova.  


	
## Revoca di una chiave API utilizzando la IU IBM Cloud
{: #revoke_ui}
	
Completa la seguente procedura per revocare una chiave API IAM tramite la IU {{site.data.keyword.Bluemix_notm}}:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.

    Apri un browser web e avvia il dashboard {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}
	
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Dalla barra dei menu della console, fai clic su **Gestisci > Sicurezza > Chiavi API IBM Cloud**.

3. Fare clic su **Azioni** e su **Elimina chiave**.





	

	
	
	
	
	
	
