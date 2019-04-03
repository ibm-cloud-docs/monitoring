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


# Provisioning del servizio di monitoraggio
{: #provision}

Puoi eseguire il provisioning del servizio {{site.data.keyword.monitoringshort}} dalla IU {{site.data.keyword.Bluemix}} o dalla riga di comando.
{:shortdesc}


## Provisioning dalla IU
{: #ui}

Completa la seguente procedura per eseguire il provisioning di un'istanza del servizio {{site.data.keyword.monitoringshort}} in {{site.data.keyword.Bluemix_notm}}:

1. Accedi al tuo account {{site.data.keyword.Bluemix_notm}}.

    Il dashboard {{site.data.keyword.Bluemix_notm}} è disponibile all'indirizzo: [http://bluemix.net ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net){:new_window}.
    
	Dopo aver effettuato l'accesso con il tuo ID utente e la tua password, viene aperta la IU {{site.data.keyword.Bluemix_notm}}.

2. Fai clic su **Catalogo**. Viene aperto l'elenco dei servizi disponibili su {{site.data.keyword.Bluemix_notm}}.

3. Seleziona la categoria **DevOps** per filtrare l'elenco di servizi che viene visualizzato.

4. Fai clic sul tile **Monitoraggio**.

5. Seleziona un piano di servizio. 

    * Per raccogliere le metriche e accedere ad esse, fino a un massimo di 45 giorni, e per definire le regole di avviso, comprese le regole con caratteri jolly, seleziona il piano **Premium**. 
	
	* Per impostazione predefinita, è impostato il piano **Lite**, che dà diritto alla raccolta delle metriche di piattaforma nello spazio dove si sta eseguendo il provisioning del servizio e un periodo di conservazione di 15 giorni per tali metriche. 

    Per ulteriori informazioni sui piani di servizio, vedi [Piani di servizio](/docs/services/cloud-monitoring/monitoring_ov.html#plan).
	
6. Fai clic su **Crea** per eseguire il provisioning del servizio {{site.data.keyword.monitoringshort}} nello spazio {{site.data.keyword.Bluemix_notm}} in cui hai eseguito l'accesso.
  
 

## Provisioning dalla CLI
{: #cli}

Completa la seguente procedura per eseguire il provisioning di un'istanza del servizio {{site.data.keyword.monitoringshort}} in {{site.data.keyword.Bluemix_notm}} tramite la riga di comando:

1. [Prerequisito] Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).
   
   Se la CLI è installata, vai al passo successivo.
    
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
3. Esegui il comando `ibmcloud service create` per eseguire il provisioning di un'istanza.

    ```
	ibmcloud service create service_name service_plan service_instance_name
	```
	{: codeblock}
    
    dove
    	
    * *service_name* è **Monitoring**.
    * *service_plan* è il nome del piano di servizio. Per raccogliere le metriche e accedere ad esse, fino a un massimo di 45 giorni, e per definire le regole di avviso, comprese le regole con caratteri jolly, seleziona il piano **Premium**. Per impostazione predefinita, è impostato il piano **Lite**, che dà diritto alla raccolta delle metriche di piattaforma nello spazio dove si sta eseguendo il provisioning del servizio e un periodo di conservazione di 15 giorni per tali metriche. Per un elenco dei piani, vedi [Piani di servizio {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/monitoring_ov.html#plan).
    * *service_instance_name* è il nome che desideri utilizzare per la nuova istanza di servizio che hai creato.
    
    Ad esempio, per creare un'istanza del servizio {{site.data.keyword.monitoringshort}} con un piano premium, esegui questo comando:
    
	```
	ibmcloud service create Monitoring premium my_monitoring_svc
	```
	{: codeblock}
    
4. Verifica che il servizio venga creato correttamente. Immetti il seguente comando:

    ```	
	ibmcloud service list
	```
	{: codeblock}
	
	L'output dell'esecuzione del comando è simile al seguente:
	
	```
    Richiamo dei servizi nell'organizzazione MyOrg / space MySpace come xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_monitoring_svc              Monitoring               premium                                        create succeeded
	```
	{: screen}

	



