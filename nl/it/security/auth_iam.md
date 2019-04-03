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


# Acquisizione di un token IAM
{: #auth_iam}

Utilizza il modello IAM {{site.data.keyword.Bluemix}} per ottenere un token di autenticazione che puoi utilizzare con il servizio {{site.data.keyword.monitoringshort}}. Puoi ottenere il token di autenticazione utilizzando la CLI {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Il token ha un tempo di scadenza, 

## Acquisizione del token IAM utilizzando la CLI IBM Cloud 
{: #iam_token_cli}

Per ottenere il token di autorizzazione utilizzando la CLI {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

1. (Pre-req) Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa).
   
   Se la CLI è installata, vai al passo successivo.
    
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
3. Esegui il comando `ibmcloud iam oauth-tokens` per ottenere il token IAM.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	L'output restituisce il token IAM.

**Nota:** quando utilizzi il token, rimuovi *Bearer* dal valore del token che passi nelle chiamate API.
		



	

	
	
	
	
	
	
