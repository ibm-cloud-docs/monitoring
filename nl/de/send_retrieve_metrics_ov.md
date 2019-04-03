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


# Senden und Abrufen von Daten
{: #send_retrieve_metrics_ov}

Sie können Metriken mithilfe der Metrik-API oder durch Konfiguration des {{site.data.keyword.monitoringshort}}-Plug-ins (bei dem es sich um ein 'collectd'-Plug-in handelt) an einen Bereich senden. Sie können Metriken über die Metrik-API abrufen.
{:shortdesc}


		
## Metriken senden
{: #send}

Die folgende Abbildung zeigt eine Übersicht der unterschiedlichen Datenquellen, von denen aus Sie Metriken an den {{site.data.keyword.monitoringshort}}-Service senden können:

![Allgemeine Ansicht der Ressourcen, die Metriken an den {{site.data.keyword.monitoringlong}}-Service senden können](images/monitoring_ov_f1.gif)

Für Container, die in einem Kubernetes-Cluster in {{site.data.keyword.Bluemix_notm}} ausgeführt werden, sowie für ausgewählte Services werden grundlegende Systemmetriken automatisch erfasst. 
Sie können auch weitere Metriken erfassen oder Metriken von außerhalb der {{site.data.keyword.IBM_notm}} Cloud an den {{site.data.keyword.monitoringshort}}-Service senden. Es stehen unterschiedliche Methoden zur Verfügung. In den folgenden Tabellen sind die Methoden nach Metrikquelle aufgelistet:

<table>
  <caption>Tabelle 1. Methoden zum Senden von Metriken an den {{site.data.keyword.monitoringshort}}-Service für {{site.data.keyword.IBM_notm}} Cloud-Ressourcen.</caption>
  <tr>
    <th>Metrikquelle</th>
	<th>Metrik-API</th>
    <th>{{site.data.keyword.monitoringshort}}-Plug-in (collectd)</th>	
	<th>Weitere Informationen</th>
  </tr>
  <tr>
    <td>Container, die in einem Kubernetes-Cluster in {{site.data.keyword.Bluemix_notm}} ausgeführt werden</td>
	<td>Ja</td>
	<td>Ja</td>
	<td>Basissystemmetriken werden automatisch erfasst. Sie können 'collectd' explizit installieren und erweiterte oder angepassten Metriken senden, die nicht standardmäßig bereitgestellt werden.</td>
  </tr>
  <tr>
    <td>Cloud Foundry-Anwendungen</td>
	<td>Ja</td>
	<td>Nein</td>
	<td></td>
  </tr>
  <tr>
    <td>Virtuelle
Server </td>
	<td>Ja</td>
	<td>Ja</td>
	<td>**Hinweis:** Wird für Windows nicht unterstützt.</td>
  </tr>
</table>

<table>
  <caption>Tabelle 2. Methoden zum Senden von Metriken an den {{site.data.keyword.monitoringshort}}-Service von außerhalb der {{site.data.keyword.IBM_notm}} Cloud.</caption>
  <tr>
    <th>Metrikquelle</th>
	<th>Metrik-API</th>
    <th>{{site.data.keyword.monitoringshort}}-Plug-in (collectd)</th>	
	<th>Weitere Informationen</th>
  </tr>
  <tr>
    <td>Container</td>
	<td>Ja</td>
	<td>Ja</td>
	<td>Sie können *supervisord* als Container-Endpunkt zum Ausführen und Verwalten sowohl Ihrer App als auch von 'collectd' verwenden.</td>
  </tr>
  <tr>
    <td>Anwendungen</td>
	<td>Ja</td>
	<td>Nein</td>
	<td></td>
  </tr>
  <tr>
    <td>Services</td>
	<td>Ja</td>
	<td>Nein</td>
	<td></td>
  </tr>
  <tr>
    <td>Virtuelle Maschinen (VM)</td>
	<td>Ja</td>
	<td>Ja</td>
	<td>**Hinweis:** Wird für Windows nicht unterstützt.</td>
  </tr>
</table>


Beachten Sie beim Senden von Metriken an den {{site.data.keyword.monitoringshort}}-Service die folgenden Informationen: 

* Sie müssen den Bereich angeben, an den Sie Metriken senden möchten.

* Sie müssen ein Sicherheitstoken oder einen API-Schlüssel für die Verwendung des {{site.data.keyword.monitoringshort}}-Service angeben. 

* Die {{site.data.keyword.IBM_notm}}-ID des Benutzers, der Metriken sendet, muss über eine IAM-Richtlinie verfügen, die dem {{site.data.keyword.monitoringshort}}-Service zugewiesen wurde. Folgende IAM-Rollen ermöglichen dem Benutzer das Senden von Metriken: *Administrator*, *Editor* und *Operator*.

* Sie müssen den API-Endpunkt angeben, an den Sie Metriken senden. Es gibt einen Endpunkt pro Region. Für die Region 'USA (Süden)' ist der Endpunkt beispielsweise der folgende: `https://metrics.ng.bluemix.net/v1/metrics`. Weitere Informationen zu den Endpunkten finden Sie unter [URLs für den {{site.data.keyword.monitoringshort}}-Service](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region){: new_window}.


Sie können Metriken an den {{site.data.keyword.monitoringshort}}-Service senden, indem Sie eine der folgenden Methoden verwenden:

* *Methode 1: Konfigurieren Sie das {{site.data.keyword.monitoringshort}}-Plug-in. *

    Weitere Informationen finden Sie in [{{site.data.keyword.monitoringshort}}-Plug-in konfigurieren](/docs/services/cloud-monitoring/send-metrics?topic=cloud-monitoring-conf_monitoring_plugin#conf_monitoring_plugin).

    Die folgende Abbildung zeigt eine Übersicht über die Verwendung des {{site.data.keyword.monitoringshort}}-Plug-ins zum Senden von Metriken an den {{site.data.keyword.monitoringshort}}-Service:

    ![Übersicht über die Verwendung des {{site.data.keyword.monitoringshort}}-Plug-ins](images/monitoring_plugin_ov.png "Übersicht über die Verwendung des {{site.data.keyword.monitoringshort}}-Plug-ins")

* *Methode 2: Verwenden Sie die Metrik-API. *

    Weitere Informationen finden Sie unter [Metriken über die Metrik-API senden](/docs/services/cloud-monitoring/send-metrics?topic=cloud-monitoring-send_data_api#send_data_api).


## Metriken abrufen
{: #retrieve}

Wenn Sie eine weitere Analyse außerhalb des {{site.data.keyword.monitoringshort}}-Service vornehmen müssen oder wenn Ihre Anwendung Metriken erfordert, um Entscheidungen treffen zu können, so können Sie über die Metrik-API bis zu fünf Metriken pro Anforderung abzurufen. 

* Weitere Informationen zur Vorgehensweise beim Abrufen von Metriken finden Sie unter [Metriken aus einer Domäne abrufen](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#retrieve_data_api)
* Weitere Informationen zur Metrik-API finden Sie unter [Metrik-API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}.

Beachten Sie beim Abrufen von Metriken die folgenden Informationen: 

* Sie müssen den Bereich festlegen, von dem aus die Daten abgerufen werden sollen. 
* Sie müssen ein Sicherheitstoken oder einen API-Schlüssel für die Verwendung des {{site.data.keyword.monitoringshort}}-Service angeben. 
* Sie müssen einen Pfad für eine oder mehrere Metriken angeben. Weitere Informationen finden Sie in [Metriken definieren](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#metrics).
* Optional können Sie einen benutzerdefinierten Zeitraum angeben. Wenn Sie keinen Zeitraum angeben, entsprechen die abgerufenen Daten standardmäßig den letzten 24 Stunden. Weitere Informationen finden Sie in [Zeitraum konfigurieren](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#time).


## Metriken auflisten
{: #show_metrics}


Sie können die Metriken auflisten, die in einem Bereich verfügbar sind.

Beachten Sie beim Auflisten der Metriken die folgenden Informationen: 

* Sie müssen den {{site.data.keyword.Bluemix_notm}}-Bereich festlegen, für den die verfügbaren Metriken aufgelistet werden sollen.

* Sie müssen ein Sicherheitstoken oder einen API-Schlüssel für die Verwendung des {{site.data.keyword.monitoringshort}}-Service angeben. 

* Sie müssen eine Abfrage angeben, die den Pfad definiert, der die aufzulistenden Metriken enthält. Wenn Sie beispielsweise alle Metriken in einem Bereich auflisten möchten, können Sie die Abfrage auf `query= *` festlegen. 

    Der Standardwert ist `*`. Dieser gibt den Startpunkt in der Stammverzeichnisebene für den Bereich an.
	
* Sie können den API-Aufruf `Endpoint/v1/metrics/list` verwenden, wobei 'Endpoint' den Eingangspunkt zum Service darstellt. 

    Jede Region verfügt über eine andere URL. Für die Region 'USA (Süden)' können Sie z. B. den API-Endpunkt `https://metrics.ng.bluemix.net/v1/metrics/list` verwenden. 

    Informationen zum Abrufen der Liste der Endpunkte nach Region finden Sie unter [Endpunkte](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

    Weitere Informationen zur API finden Sie im Abschnitt [Metrik-API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}.



## Endpunkte zum Senden von Metriken
{: #endpoints}

 In der folgenden Tabelle sind die Endpunkte nach Region aufgelistet:
	
<table>
    <caption>Liste der Endpunkte</caption>
	<tr>
	  <th>Region</th>
	  <th>URL</th>
	  <th>Port für 'collectd'</th>
	</tr>
	<tr>
	  <td>Deutschland</td>
	  <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
	  <td>9095</td>
	</tr>
	<tr>
	  <td>Sydney</td>
	  <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
	  <td>9095</td>
	</tr>
	<tr>
	  <td>Vereinigtes Königreich</td>
	  <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
	  <td>9095</td>
	</tr>
	<tr>
	  <td>USA (Süden)</td>
	  <td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
	  <td>9095</td>
	</tr>
</table>






 
