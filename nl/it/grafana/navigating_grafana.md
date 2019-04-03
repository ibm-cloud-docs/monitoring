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


# Passaggio al dashboard Grafana
{:#navigating_grafana}

In {{site.data.keyword.Bluemix}}, puoi utilizzare Grafana, una piattaforma di analisi e visualizzazione open source, per monitorare, ricercare, analizzare e visualizzare le tue metriche in vari tipi di grafici, ad esempio, diagrammi e tabelle. Utilizza Grafana per eseguire attività di analisi avanzate.
{:shortdesc}

Puoi avviare Grafana in uno dei seguenti modi:

* Da {{site.data.keyword.Bluemix_notm}}

    Puoi avviare le metriche del tuo specifico contenitore Docker in Grafana, nel contesto di quello specifico contenitore. Questa funzione si applica solo ai contenitori distribuiti nell'infrastruttura gestita da {{site.data.keyword.Bluemix_notm}}. 
    
    Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana dal dashboard {{site.data.keyword.Bluemix_notm}}
    ](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_bluemix).

* Da un link diretto del browser

    Puoi avviare Grafana in modo che i dati che visualizzi aggreghino i log dai servizi all'interno di uno spazio {{site.data.keyword.Bluemix_notm}} fornito.
    
    Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana da un browser web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).
    
Per ulteriori informazioni su Grafana, vedi la [Guida per l'utente Grafana ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Passaggio al dashboard Grafana dal dashboard IBM Cloud
{: #launch_grafana_from_bluemix}

**Nota:** questa funzione si applica solo ai contenitori distribuiti nell'infrastruttura gestita da {{site.data.keyword.Bluemix_notm}}. 

La query che viene utilizzata per filtrare i dati visualizzati in Grafana richiama i dati per il contenitore {{site.data.keyword.Bluemix_notm}} da cui è stato avviato Kibana. 

Per visualizzare le metriche di un contenitore Docker in Grafana, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul contenitore dal *Dashboard*. 
    
2. Nella barra di navigazione, fai clic su **Monitoraggio e log**. Viene visualizzata la scheda Monitoraggio. 
    
3. Fai clic su **Vista avanzata**. Si aprirà il dashboard **Grafana**.


##  Passaggio al dashboard Grafana da un browser web
{: #launch_grafana_from_browser}

La query utilizzata per filtrare i dati visualizzati in Grafana richiama i dati per uno spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. Le informazioni sulle metriche visualizzate da Grafana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso.

Completa la seguente procedura per avviare Grafana da un browser:

1. Apri un browser web 
2. Immetti l'URL della regione in cui desideri monitorare le metriche. 

    La seguente tabella elenca gli URL per regione:
	<table>
      <caption>URL per avviare Grafana in regioni differenti</caption>
      <tr>
        <th>Regione</th>
	    <th>Endpoint</th>
      </tr>
      <tr>
        <td>Germania</td>
	    <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
      </tr>
      <tr>
        <td>Regno Unito</td>
	    <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
      </tr>
      <tr>
        <td>Stati Uniti Sud</td>
    	<td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
      </tr>
      <tr>
        <td>Regno Unito</td>
	    <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
      </tr>
      
    </table>
	
2. Seleziona **Grafana**.
     

