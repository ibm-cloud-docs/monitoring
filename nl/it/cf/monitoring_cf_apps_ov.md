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


# Applicazioni Cloud Foundry
 {:#monitoring_bluemix_apps}

In {{site.data.keyword.Bluemix}}, le metriche sono raccolte automaticamente per le applicazioni CF (Cloud Foundry) in esecuzione nella regione pubblica e inoltrate al servizio {{site.data.keyword.monitoringlong}}. Puoi utilizzare Grafana per le analisi e per monitorare le prestazioni della tua applicazione CF. Puoi anche utilizzare l'API Metriche per eseguire la query delle metriche dell'applicazione CF ed eseguire azioni in base ai dati.
{:shortdesc}


## Monitoraggio delle applicazioni CF in esecuzione su Pubblico
{: #public}


Tieni conto delle seguenti informazioni quando utilizzi il servizio {{site.data.keyword.monitoringshort}} per monitorare un'applicazione CF:

* Devi eseguire il provisioning del servizio {{site.data.keyword.monitoringshort}} nello stesso spazio in cui l'applicazione CF è in esecuzione.
* Le metriche che vengono raccolte per un'applicazione CF vengono automaticamente inoltrate al dominio dello spazio nel servizio {{site.data.keyword.monitoringshort}}. 
* Le metriche vengono inoltrate a un dominio dello spazio. Il dominio dello spazio corrisponde a quello in cui l'applicazione CF è in esecuzione. 
* Puoi anche utilizzare l'API Metriche per eseguire la query delle metriche CF ed eseguire azioni in base ai dati. Ad esempio, puoi creare un'automazione che esegue le query dell'utilizzo della CPU della tua applicazione CF e lo ridimensiona se la CPU sta diventando troppo elevata.

La seguente figura mostra una visualizzazione di alto livello del monitoraggio delle applicazioni CF in {{site.data.keyword.Bluemix_notm}}:

![Visualizzazione di alto livello del monitoraggio delle applicazioni CF in {{site.data.keyword.Bluemix_notm}}](images/cfapp_metrics_ov.png "Visualizzazione di alto livello del monitoraggio delle applicazioni CF in {{site.data.keyword.Bluemix_notm}}")

## Monitoraggio delle applicazioni CF in esecuzione all'esterno di {{site.data.keyword.Bluemix_notm}}
{: #outside}

Per monitorare le applicazioni CF in esecuzione all'esterno di {{site.data.keyword.Bluemix_notm}}, puoi utilizzare l'API Metriche per inoltrare le metriche della tua applicazione CF al servizio {{site.data.keyword.monitoringshort}}.

* Per ulteriori informazioni sull'API, consulta [API Metriche](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-metrics-api?&language=node#introduction).
* Per ulteriori informazioni sull'utilizzo dell'API, consulta [Invio dei dati utilizzando l'API Metriche](/docs/services/cloud-monitoring/send-metrics/send_data_api.html#send_data_api).




## Visualizzazione e analisi delle metriche delle applicazioni CF
{: #monitoring_cfapps}

Per monitorare le prestazioni delle applicazioni CF in {{site.data.keyword.Bluemix_notm}}, utilizza Grafana. 

Il servizio {{site.data.keyword.monitoringlong}} utilizza Grafana, una piattaforma di analisi e visualizzazione open source, che puoi utilizzare per monitorare, ricercare, analizzare e visualizzare le tue metriche in vari tipi di grafici, ad esempio, diagrammi e tabelle.

Puoi avviare Grafana da un browser. Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana da un browser web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

**Nota:** devi avviare Grafana nella stessa regione {{site.data.keyword.Bluemix_notm}} in cui è in esecuzione l'istanza dell'applicazione CF.


Per monitorare le applicazioni CF, devi definire una o più query in Grafana. Per ulteriori informazioni, vedi [Configurazione di una query della metrica in Grafana](/docs/services/cloud-monitoring/grafana/define_query.html#define_query). 

Puoi anche definire gli avvisi per le query. Per ulteriori informazioni, vedi [Configurazione degli avvisi](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).



## Metriche CPU
{: #cpu_metrics}

Le serie di metriche che vengono raccolte automaticamente per ogni applicazione CF includono i dati sull'utilizzo della CPU.


<table>
  <caption>Metriche della CPU raccolte per un'applicazione CF</caption>
  <tr>
    <th>Metrica</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>cpu-utilization</td>
    <td>Percentuale di utilizzo della CPU verso il limite del contenitore.</td>
  </tr>
</table>


## Metriche del disco
{: #disk_metrics}

Le serie di metriche che vengono raccolte automaticamente per ogni applicazione CF includono i dati sulla dimensione del disco utilizzata, la dimensione totale del disco disponibile e la percentuale del disco utilizzata.


<table>
  <caption>Metriche del disco raccolte per un'applicazione CF</caption>
  <tr>
    <th>Metrica</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>disk-bytes-total</td>
    <td>La dimensione del disco del contenitore in cui è in esecuzione l'applicazione CF. Il valore è definito in byte.</td>
  </tr>
  <tr>
    <td>disk-bytes-used</td>
    <td>La dimensione del disco del contenitore utilizzata sul disco dall'applicazione CF. Il valore è definito in byte.</td>
  </tr>
  <tr>
    <td>disk-utilization</td>
    <td>La percentuale del disco utilizzata dall'applicazione CF.</td>
  </tr>
</table>

**Nota:** 

* Specifichi la dimensione del disco quando trasmetti l'applicazione CF.
* Quando disk-utilization raggiunge il 90%, considera di ridimensionare l'applicazione CF.

## Metriche della memoria
{: #mem_metrics}

Le serie di metriche che vengono raccolte automaticamente per ogni applicazione CF includono i dati sulla memoria utilizzata, la memoria totale disponibile e la percentuale di memoria utilizzata.

<table>
  <caption>Metriche della memoria raccolte per un'applicazione CF</caption>
  <tr>
    <th>Metrica</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>memory-bytes-total</td>
    <td>La memoria in byte disponibile per l'applicazione CF.</td>
  </tr>
  <tr>
    <td>memory-bytes-used</td>
    <td>La memoria in byte utilizzata dall'istanza dell'applicazione CF.</td>
  </tr>
  <tr>
    <td>memory-utilization</td>
    <td>La percentuale di memoria utilizzata dall'applicazione CF.</td>
  </tr>
</table>


## Formato delle query delle metriche
{: #query_format}


Le query che definisci in Grafana per monitorare un'applicazione Cloud Foundry devono rispettare il seguente formato: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

Ad esempio, consulta gli esempi delle serie di metriche raccolte per un'istanza dell'applicazione CF denominata logtester nella regione di Sydney:

```
ibmcloud.public.cloud-foundry.au-syd.logtester.0.container.cpu.utilization
ibmcloud.public.cloud-foundry.au-syd.logtester.0.container.disk.bytes-total
ibmcloud.public.cloud-foundry.au-syd.logtester.0.container.disk.bytes-used
ibmcloud.public.cloud-foundry.au-syd.logtester.0.container.disk.utilization
ibmcloud.public.cloud-foundry.au-syd.logtester.0.container.memory.bytes-total
ibmcloud.public.cloud-foundry.au-syd.logtester.0.container.memory.bytes-used
ibmcloud.public.cloud-foundry.au-syd.logtester.0.container.memory.utilization
```
{: screen}

Per ulteriori informazioni, vedi [Formato delle metriche delle applicazioni CF](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format).

**Nota:** non tutti i caratteri che sono consentiti nei nomi dell'applicazione CF lo sono nei nomi delle serie di metriche. Ad esempio, le lettere maiuscole non sono consentite. Il nome dell'applicazione CF che puoi visualizzare in Grafana quando definisci una query viene modificato con tutte lettere minuscole.




