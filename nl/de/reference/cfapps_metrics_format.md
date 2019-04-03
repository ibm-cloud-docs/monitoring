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


# CF-Apps
{: #cfapps_metrics_format}

Abfragen, die Sie in Grafana zum Überwachen einer Cloud Foundry-Anwendung definieren, die in {{site.data.keyword.Bluemix}} Public ausgeführt wird, müssen das folgende Format aufweisen: 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

Dabei gilt Folgendes:

<table>
  <caption>Allgemeine Felder in einer Abfrage</caption>
  <tr>
    <th>Feld</th>
	<th>Beschreibung</th>
	<th>Wert</th>
  </tr>
  <tr>
    <td>Source</td>
	<td>Dies ist ein reservierter Name. Metriken unter dieser Hierarchie kommen aus {{site.data.keyword.Bluemix_notm}}-Anwendungen und -Services.</td>
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
	<td>Definiert die Region, in der die Instanz der CF-App ausgeführt wird.</td>
	<td>Für die Region 'USA (Süden)' ist der Wert *us-south* <br>Für die Region 'Vereinigtes Königreich' lautet der Wert *eu-gb*  <br>Für Deutschland lautet der Wert *eu-de* <br>Für Sydney lautet der Wert *au-syd* </td>
  </tr>
  <tr>
    <td>CFapp Name</td>
	<td>Name der CF-Anwendung.</td>
	<td></td>
  </tr>
  <tr>
    <td>CFapp Index</td>
	  <td>Index der Instanz der CF-Anwendung.</td>
	  <td>Beispiel: *0* </br>Wenn Sie über eine CF-App mit einer Instanz verfügen, gibt es nur den Index 0. Wenn Sie die CF-App beispielsweise auf 10 Instanzen skalieren, stehen für den Index die Werte 0 bis 9 zur Verfügung.</td>
  </tr>
  <tr>
    <td>CFapp container</td>
	  <td>Fester Wert.</td>
	  <td>*container*</td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>Typ der Metrik. Platte, Speicher und CPU sind automatisch erfasste Metrikserien.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Anzuzeigende Metrik. </br>[CPU-Metriken](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[Plattenmetriken](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics) </br>[Speichermetriken](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Abfragefunktionen, die Sie zur Visualisierung einer Containermetrik in der Anzeige auswählen können. </td>
    <td>[Functions ![(Symbol für externen Link)](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




