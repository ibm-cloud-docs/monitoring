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


# Formato generale
{: #metrics_format}

Le query che definisci in Grafana per monitorare un servizio {{site.data.keyword.Bluemix}} devono rispettare il seguente formato: 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

dove [service fields] rappresenta i campi specifici della query della metrica di un servizio o un'applicazione CF. 

<table>
  <caption>Campi comuni in una query</caption>
  <tr>
    <th>Campo</th>
	<th>Descrizione</th>
	<th>Valore</th>
  </tr>
  <tr>
    <td>Origine</td>
	<td>Questo è un nome riservato. Le metriche in questa gerarchia provengono dai servizi {{site.data.keyword.Bluemix_notm}}.</td>
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
	  <td>Per {{site.data.keyword.containershort}}, il valore è: *containers-kubernetes*</td>
  </tr>
  <tr>
    <td>Regione</td>
	  <td>Definisce la regione in cui il contenitore è in esecuzione.</td>
	  <td>Per la regione Stati Uniti Sud, il valore è: *us-south* <br>Per la regione Regno Unito, il valore è: *united-kingdom*  <br>Per la Germania, il valore è: *frankfurt* <br>Per Sydney, il valore è: *sydney* </td>
  </tr>
  <tr>
    <td>Tipo di metrica</td>
	<td>Tipo di metrica.</td>
	<td>*cpu* <br>*load* <br>*memory*</td>
  </tr>
  <tr>
    <td>Tipo secondario della metrica</td>
	<td>Il tipo secondario della metrica.</td>
	<td>Ad esempio: *usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Funzioni</td>
    <td>Funzioni della query che puoi selezionare per visualizzare una metrica del contenitore nel pannello. </td>
    <td>[Functions ![(Icona link esterno)](../../../icons/launch-glyph.svg "Icona link esterno")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




