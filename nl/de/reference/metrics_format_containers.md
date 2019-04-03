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

Abfragen, die Sie in Grafana zum Überwachen des {{site.data.keyword.containershort_notm}}-Service definiert werden, folgen dem folgendem Muster: 
{:shortdesc}



## Abfrageformat für für Container erfasste CPU-Metriken
{: #cpu_containers}

Das Format einer Abfrage, die Sie in Grafana zum Überwachen einer CPU-Metrik für einen Container definieren, der für den {{site.data.keyword.containershort_notm}}-Service ausgeführt wird, sieht folgendermaßen aus: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

Dabei gilt Folgendes:

<table>
  <caption>Erforderliche Felder zum Definieren einer CPU-Metrik für einen Container </caption>
  <tr>
    <th>Feld</th>
	  <th>Beschreibung</th>
	  <th>Wert</th>
  </tr>
  <tr>
    <td>Source</td>
	  <td>Dies ist ein reservierter Name. Metriken unter dieser Hierachie kommen aus {{site.data.keyword.Bluemix_notm}}-Anwendungen und -Services.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	  <td>Gibt den Typ der Cloud an. </td>
	  <td>Für die {{site.data.keyword.Bluemix_notm}} Public Cloud lautet der Wert *public*.</td>
  </tr>
  <tr>
    <td>Service Name</td>
	  <td>Gibt den Namen des Service in {{site.data.keyword.Bluemix_notm}} an.</td>
	  <td>Für CF-Apps ist der Wert *cloud-foundry*.</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Definiert die Region, in der der Container ausgeführt wird.</td>
	  <td>Für die Region 'USA (Süden)' ist der Wert *us-south* <br>Für die Region 'Vereinigtes Königreich' lautet der Wert *united-kingdom*  <br>Für Deutschland lautet der Wert *frankfurt* <br>Für Sydney lautet der Wert *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	  <td>Name des zu überwachenden Clusters.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	  <td>Quelle der Daten.</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>Namensbereich, in dem der Container in einem Kubernetes-Cluster bereitgestellt wird.</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>Name des Pods.</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	<td>Name des Containers.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>Typ der Metrik.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Anzuzeigende Metrik.</td>
	  <td>*usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Abfragefunktionen, die Sie zur Visualisierung einer Containermetrik in der Anzeige auswählen können. </td>
    <td>[Functions ![(Symbol für externen Link)](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Beispielsweise wird eine Abfrage zum Überwachen der CPU-Auslastung für einen Container, der in einem Kubernetes-Cluster in der Region 'USA (Süden)' ausgeführt wird, folgendermaßen definiert:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## Abfrageformat für für Worker erfasste Lademetriken
{: #load_workers}

Das Format einer Abfrage, die Sie in Grafana zum Überwachen einer Lademetrik für einen Worker definieren, der für den {{site.data.keyword.containershort_notm}}-Service ausgeführt wird, sieht folgendermaßen aus: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

Dabei gilt Folgendes:

<table>
  <caption>Erforderliche Felder zum Definieren einer Auslastungsmetrik für einen Worker </caption>
  <tr>
    <th>Feld</th>
	<th>Beschreibung</th>
	<th>Wert</th>
  </tr>
  <tr>
    <td>Source</td>
	  <td>Dies ist ein reservierter Name. Metriken unter dieser Hierachie kommen aus {{site.data.keyword.Bluemix_notm}}-Anwendungen und -Services.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	  <td>Gibt den Typ der Cloud an. </td>
	  <td>Für die {{site.data.keyword.Bluemix_notm}} Public Cloud lautet der Wert *public*.</td>
  </tr>
  <tr>
    <td>Service Name</td>
	  <td>Gibt den Namen des Service in {{site.data.keyword.Bluemix_notm}} an.</td>
	  <td>Für CF-Apps ist der Wert *cloud-foundry*.</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Definiert die Region, in der der Container ausgeführt wird.</td>
	  <td>Für die Region 'USA (Süden)' ist der Wert *us-south* <br>Für die Region 'Vereinigtes Königreich' lautet der Wert *united-kingdom*  <br>Für Deutschland lautet der Wert *frankfurt* <br>Für Sydney lautet der Wert *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>Name des zu überwachenden Clusters.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>Quelle der Daten.</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>Worker Name</td>
	<td>Name des Workers.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>Typ der Metrik.</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Anzuzeigende Metrik.</td>
	  <td>*avg-1*, *avg-5*, *avg-15*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Abfragefunktionen, die Sie zur Visualisierung einer Containermetrik in der Anzeige auswählen können. </td>
    <td>[Functions ![(Symbol für externen Link)](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Beispielsweise wird eine Abfrage zum Überwachen der CPU-Auslastung für einen Worker, der in einem Kubernetes-Cluster in der Region 'USA (Süden)' ausgeführt wird, folgendermaßen definiert:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## Abfrageformat für für Container erfasste Speichermetriken
{: #mem_containers}

Das Format einer Abfrage, die Sie in Grafana zum Überwachen einer Speichermetrik für einen Container definieren, der für den {{site.data.keyword.containershort_notm}}-Service ausgeführt wird, sieht folgendermaßen aus: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

Dabei gilt Folgendes:

<table>
  <caption>Erforderliche Felder zum Definieren einer Speichermetrik für einen Container</caption>
  <tr>
    <th>Feld</th>
	<th>Beschreibung</th>
	<th>Wert</th>
  </tr>
  <tr>
    <td>Source</td>
	  <td>Dies ist ein reservierter Name. Metriken unter dieser Hierachie kommen aus {{site.data.keyword.Bluemix_notm}}-Anwendungen und -Services.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	  <td>Gibt den Typ der Cloud an. </td>
	  <td>Für die {{site.data.keyword.Bluemix_notm}} Public Cloud lautet der Wert *public*.</td>
  </tr>
  <tr>
    <td>Service Name</td>
	  <td>Gibt den Namen des Service in {{site.data.keyword.Bluemix_notm}} an.</td>
	  <td>Für CF-Apps ist der Wert *cloud-foundry*.</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Definiert die Region, in der der Container ausgeführt wird.</td>
	  <td>Für die Region 'USA (Süden)' ist der Wert *us-south* <br>Für die Region 'Vereinigtes Königreich' lautet der Wert *united-kingdom*  <br>Für Deutschland lautet der Wert *frankfurt* <br>Für Sydney lautet der Wert *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>Name des zu überwachenden Clusters.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>Quelle der Daten.</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>Namensbereich, in dem der Container in einem Kubernetes-Cluster bereitgestellt wird.</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>Name des Pods.</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	  <td>Name des Containers.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
  	<td>Typ der Metrik.</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Anzuzeigende Metrik.</td>
	  <td>*limit*, *current*, *usage-pct*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Abfragefunktionen, die Sie zur Visualisierung einer Containermetrik in der Anzeige auswählen können. </td>
    <td>[Functions ![(Symbol für externen Link)](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Beispielsweise wird eine Abfrage zum Überwachen der Speicherbelegung für einen Container, der in einem Kubernetes-Cluster in der Region 'USA (Süden)' ausgeführt wird, folgendermaßen definiert:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
