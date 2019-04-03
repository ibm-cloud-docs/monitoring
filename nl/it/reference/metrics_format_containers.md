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


# {{site.data.keyword.containershort_notm}}
{: #metrics_format_containers}

Le query che definisci in Grafana per monitorare il servizio {{site.data.keyword.containershort_notm}} rispettano il seguente modello: 
{:shortdesc}



## Formato della query per le metriche della CPU raccolte per i contenitori
{: #cpu_containers}

Il formato di una query che definisci in Grafana per monitorare una metrica della CPU per un contenitore in esecuzione nel servizio {{site.data.keyword.containershort_notm}} viene descritta nel seguente modo: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

dove

<table>
  <caption>Campi obbligatori per definire una metrica della CPU per un contenitore. </caption>
  <tr>
    <th>Campo</th>
	  <th>Descrizione</th>
	  <th>Valore</th>
  </tr>
  <tr>
    <td>Origine</td>
	  <td>Questo è un nome riservato. Le metriche in questa gerarchia provengono dai servizi e dalle applicazioni {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo di cloud</td>
	  <td>Indica il tipo di cloud. </td>
	  <td>Per il cloud pubblico di {{site.data.keyword.Bluemix_notm}}, il valore è: *public*</td>
  </tr>
  <tr>
    <td>Nome del servizio</td>
	  <td>Definisce il nome del servizio in {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Per le applicazioni CF, il valore è: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Regione</td>
	  <td>Definisce la regione in cui il contenitore è in esecuzione.</td>
	  <td>Per la regione Stati Uniti Sud, il valore è: *us-south* <br>Per la regione Regno Unito, il valore è: *united-kingdom*  <br>Per la Germania, il valore è: *frankfurt* <br>Per Sydney, il valore è: *sydney* </td>
  </tr>
  <tr>
    <td>Nome del cluster</td>
	  <td>Il nome del cluster da monitorare.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Origine della metrica</td>
	  <td>L'origine dei dati.</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>Spazio dei nomi</td>
	<td>Lo spazio dei nomi in cui viene distribuito il contenitore.</td>
	<td></td>
  </tr>
   <tr>
    <td>Nome del pod</td>
	<td>Il nome del pod.</td>
	<td></td>
  </tr>
  <tr>
    <td>Nome del contenitore</td>
	<td>Il nome del contenitore.</td>
	<td></td>
  </tr>
  <tr>
    <td>Tipo di metrica</td>
	  <td>Tipo di metrica.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Tipo secondario della metrica</td>
	  <td>Metrica da visualizzare.</td>
	  <td>*usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Funzioni</td>
    <td>Funzioni della query che puoi selezionare per visualizzare una metrica del contenitore nel pannello. </td>
    <td>[Functions ![(Icona link esterno)](../../../icons/launch-glyph.svg "Icona link esterno")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Ad esempio, una query per monitorare l'utilizzo della CPU per un contenitore in esecuzione in un cluster Kubernetes nella regione Stati Uniti Sud è definita nel seguente modo:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## Formato della query delle metriche del carico per i nodi di lavoro
{: #load_workers}

Il formato di una query che definisci in Grafana per monitorare una metrica del carico per un nodo di lavoro in esecuzione nel servizio {{site.data.keyword.containershort_notm}} viene descritta nel seguente modo: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

dove

<table>
  <caption>Campi obbligatori per definire una metrica del carico per un nodo di lavoro. </caption>
  <tr>
    <th>Campo</th>
	<th>Descrizione</th>
	<th>Valore</th>
  </tr>
  <tr>
    <td>Origine</td>
	  <td>Questo è un nome riservato. Le metriche in questa gerarchia provengono dai servizi e dalle applicazioni {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo di cloud</td>
	  <td>Indica il tipo di cloud. </td>
	  <td>Per il cloud pubblico di {{site.data.keyword.Bluemix_notm}}, il valore è: *public*</td>
  </tr>
  <tr>
    <td>Nome del servizio</td>
	  <td>Definisce il nome del servizio in {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Per le applicazioni CF, il valore è: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Regione</td>
	  <td>Definisce la regione in cui il contenitore è in esecuzione.</td>
	  <td>Per la regione Stati Uniti Sud, il valore è: *us-south* <br>Per la regione Regno Unito, il valore è: *united-kingdom*  <br>Per la Germania, il valore è: *frankfurt* <br>Per Sydney, il valore è: *sydney* </td>
  </tr>
  <tr>
    <td>Nome del cluster</td>
	<td>Il nome del cluster da monitorare.</td>
	<td></td>
  </tr>
  <tr>
    <td>Origine della metrica</td>
	<td>L'origine dei dati.</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>Nome del nodo di lavoro</td>
	<td>Il nome del nodo di lavoro.</td>
	<td></td>
  </tr>
  <tr>
    <td>Tipo di metrica</td>
	<td>Tipo di metrica.</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>Tipo secondario della metrica</td>
	  <td>Metrica da visualizzare.</td>
	  <td>*avg-1*, *avg-5*, *avg-15*</td>
  </tr>
  <tr>
    <td>Funzioni</td>
    <td>Funzioni della query che puoi selezionare per visualizzare una metrica del contenitore nel pannello. </td>
    <td>[Functions ![(Icona link esterno)](../../../icons/launch-glyph.svg "Icona link esterno")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Ad esempio, una query per monitorare l'utilizzo della CPU per un nodo di lavoro in esecuzione in un cluster Kubernetes nella regione Stati Uniti Sud è definita nel seguente modo:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## Formato della query per le metriche della memoria raccolte per i contenitori
{: #mem_containers}

Il formato di una query che definisci in Grafana per monitorare una metrica della memoria per un contenitore in esecuzione nel servizio {{site.data.keyword.containershort_notm}} viene descritta nel seguente modo: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

dove

<table>
  <caption>Campi obbligatori per definire una metrica della memoria per un contenitore.</caption>
  <tr>
    <th>Campo</th>
	<th>Descrizione</th>
	<th>Valore</th>
  </tr>
  <tr>
    <td>Origine</td>
	  <td>Questo è un nome riservato. Le metriche in questa gerarchia provengono dai servizi e dalle applicazioni {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo di cloud</td>
	  <td>Indica il tipo di cloud. </td>
	  <td>Per il cloud pubblico di {{site.data.keyword.Bluemix_notm}}, il valore è: *public*</td>
  </tr>
  <tr>
    <td>Nome del servizio</td>
	  <td>Definisce il nome del servizio in {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Per le applicazioni CF, il valore è: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Regione</td>
	  <td>Definisce la regione in cui il contenitore è in esecuzione.</td>
	  <td>Per la regione Stati Uniti Sud, il valore è: *us-south* <br>Per la regione Regno Unito, il valore è: *united-kingdom*  <br>Per la Germania, il valore è: *frankfurt* <br>Per Sydney, il valore è: *sydney* </td>
  </tr>
  <tr>
    <td>Nome del cluster</td>
	<td>Il nome del cluster da monitorare.</td>
	<td></td>
  </tr>
  <tr>
    <td>Origine della metrica</td>
	<td>L'origine dei dati.</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>Spazio dei nomi</td>
	<td>Lo spazio dei nomi in cui viene distribuito il contenitore.</td>
	<td></td>
  </tr>
   <tr>
    <td>Nome del pod</td>
	<td>Il nome del pod.</td>
	<td></td>
  </tr>
  <tr>
    <td>Nome del contenitore</td>
	  <td>Il nome del contenitore.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Tipo di metrica</td>
  	<td>Tipo di metrica.</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>Tipo secondario della metrica</td>
	  <td>Metrica da visualizzare.</td>
	  <td>*limit*, *current*, *usage-pct*</td>
  </tr>
  <tr>
    <td>Funzioni</td>
    <td>Funzioni della query che puoi selezionare per visualizzare una metrica del contenitore nel pannello. </td>
    <td>[Functions ![(Icona link esterno)](../../../icons/launch-glyph.svg "Icona link esterno")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Ad esempio, una query per monitorare l'utilizzo della memoria per un contenitore in esecuzione in un cluster Kubernetes nella regione Stati Uniti Sud è definita nel seguente modo:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
