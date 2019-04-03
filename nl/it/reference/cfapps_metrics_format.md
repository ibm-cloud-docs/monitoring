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


# Applicazioni CF
{: #cfapps_metrics_format}

Le query che definisci in Grafana per monitorare un'applicazione Cloud Foundry in esecuzione in {{site.data.keyword.Bluemix}} Pubblico devono rispettare il seguente formato: 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

dove

<table>
  <caption>Campi comuni in una query</caption>
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
	<td>Definisce la regione in cui l'istanza dell'applicazione CF è in esecuzione:</td>
	<td>Per la regione Stati Uniti Sud, il valore è: *us-south* <br>Per la regione Regno Unito, il valore è: *eu-gb*  <br>Per la Germania, il valore è: *eu-de* <br>Per Sydney, il valore è: *au-syd* </td>
  </tr>
  <tr>
    <td>Nome dell'applicazione CF</td>
	<td>Il nome dell'applicazione CF.</td>
	<td></td>
  </tr>
  <tr>
    <td>Indice dell'applicazione CF</td>
	  <td>L'indice dell'istanza dell'applicazione CF.</td>
	  <td>Ad esempio: *0* </br>Se disponi di un'applicazione CF con una istanza, c'è solo l'indice 0. Se ridimensioni l'applicazione CF, ad esempio a 10 istanze, disponi dei valori di indice da 0 a 9.</td>
  </tr>
  <tr>
    <td>Contenitore CFapp</td>
	  <td>Valore fisso.</td>
	  <td>*container*</td>
  </tr>
  <tr>
    <td>Tipo di metrica</td>
	  <td>Tipo di metrica. Disco, memoria e CPU sono le serie di metriche raccolte automaticamente.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Tipo secondario della metrica</td>
	  <td>Metrica da visualizzare. </br>[Metriche CPU](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Metriche del disco](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[Metriche della memoria](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>Funzioni</td>
    <td>Funzioni della query che puoi selezionare per visualizzare una metrica del contenitore nel pannello. </td>
    <td>[Functions ![(Icona link esterno)](../../../icons/launch-glyph.svg "Icona link esterno")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




