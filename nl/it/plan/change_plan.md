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


# Modifica del piano
{: #change_plan}

Puoi modificare il tuo piano di servizio {{site.data.keyword.monitoringshort}} tramite il dashboard {{site.data.keyword.monitoringlong_notm}} o eseguendo il comando `cf update-service`. Puoi aggiornare o ridurre il tuo piano in qualsiasi momento.
{:shortdesc}

## Modifica del piano di servizio attraverso la IU
{: #change_plan_ui}

Per modificare il tuo piano di servizio nel dashboard {{site.data.keyword.monitoringlong_notm}}, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul servizio {{site.data.keyword.monitoringshort}} dal dashboard. 

    Si apre il dashboard del servizio {{site.data.keyword.monitoringshort}}.
    
2. Seleziona la scheda **Piano**.

    Vengono visualizzate le informazioni sul tuo piano corrente.
	
3. Seleziona un nuovo piano per aggiornare o ridurre il tuo piano. 

4. Fai clic su **Salva**.



## Modifica del piano di servizio attraverso la CLI
{: #change_plan_cli}

Per modificare il tuo piano di servizio in {{site.data.keyword.Bluemix_notm}} tramite la CLI, completa la seguente procedura:

1. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
2. Esegui il comando `ibmcloud service list` per controllare il tuo piano corrente e per ottenere il nome del servizio {{site.data.keyword.loganalysisshort}} dall'elenco di servizi disponibili nello spazio. 

    Il valore del campo **name** è quello che devi utilizzare per modificare il piano. 

    Ad esempio,
	
	```
	$ ibmcloud service list
	Getting services in org MyOrg / space dev as xxx@yyy.com...
	OK
	name            service      plan   bound apps   last operation
	Monitoring-0c   Monitoring   premium             create succeeded
    ```
	{: screen}
    
3. Aggiorna o riduci il tuo piano. Esegui il comando `ibmcloud service update`.
    
	```
	ibmcloud service update service_name [-p new_plan]
	```
	{: codeblock}
	
	dove 
	
	* *service_name* è il nome del tuo servizio. 
	* *new_plan* è il nome del piano.
	
	La seguente tabella elenca i diversi piani e i relativi valori supportati:
	
	<table>
	  <caption>Tabella 1. Elenco dei piani.</caption>
	  <tr>
	    <th>Piano</th>
		<th>Funzioni</th>
	    <th>Nome</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>Monitoraggio gratuito.</td>
		<td>lite</td>
	  </tr>
	  <tr>
	    <td>Premium</td>
	    <td>Monitoraggio aggiuntivo.</td>
		<td>premium</td>
	  </tr>
	</table>
	
	Ad esempio, per ridurre il tuo piano al piano *Lite*, immetti il seguente comando:
	
	```
	ibmcloud service update "Monitoring-0c" -p lite
    Updating service instance Monitoring-0c as xxx@yyy.com...
    OK
	```
	{: screen}

4. Verifica che il nuovo piano sia stato modificato. Esegui il comando `ibmcloud service list`.

    ```
	ibmcloud service list
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service       plan   bound apps   last operation
    Monitoring-0c     Monitoring    lite                create succeeded
	```
	{: screen}






