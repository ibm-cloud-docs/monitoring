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


# Allgemeines Format
{: #metrics_format}

Abfragen, die Sie in Grafana zum Überwachen eines {{site.data.keyword.Bluemix}}-Service definieren, müssen das folgende Format aufweisen: 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

Dabei steht [service fields] für die speziellen Felder der Metrikabfrage eines Service oder einer CF-App. 

<table>
  <caption>Allgemeine Felder in einer Abfrage</caption>
  <tr>
    <th>Feld</th>
	<th>Beschreibung</th>
	<th>Wert</th>
  </tr>
  <tr>
    <td>Source</td>
	<td>Dies ist ein reservierter Name. Metriken unter dieser Hierarchie kommen aus {{site.data.keyword.Bluemix_notm}}-Services.</td>
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
	  <td>Für den {{site.data.keyword.containershort}} lautet der Wert *containers-kubernetes*.</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Definiert die Region, in der der Container ausgeführt wird.</td>
	  <td>Für die Region 'USA (Süden)' ist der Wert *us-south* <br>Für die Region 'Vereinigtes Königreich' lautet der Wert *united-kingdom*  <br>Für Deutschland lautet der Wert *frankfurt* <br>Für Sydney lautet der Wert *sydney* </td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>Typ der Metrik.</td>
	<td>*cpu* <br>*load* <br>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	<td>Untertyp der Metrik.</td>
	<td>Beispiel: *usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Abfragefunktionen, die Sie zur Visualisierung einer Containermetrik in der Anzeige auswählen können. </td>
    <td>[Functions ![(Symbol für externen Link)](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




