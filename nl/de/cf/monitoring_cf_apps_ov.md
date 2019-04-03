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


# Cloud Foundry-Apps
 {:#monitoring_bluemix_apps}

In {{site.data.keyword.Bluemix}} werden Metriken automatisch für CF-Apps (CF, Cloud Foundry) erfasst, die in der Public-Region ausgeführt und an den {{site.data.keyword.monitoringlong}}-Service weitergeleitet werden. Sie können Grafana zur Analyse verwenden, um die Leistung der CF-Anwendung zu überwachen. Außerdem können Sie mithilfe der Metrik-API die Metriken für die CF-App abfragen und basierend auf den Daten entsprechende Maßnahmen ergreifen.
{:shortdesc}


## CF-Apps überwachen, die für Public ausgeführt werden
{: #public}


Wenn Sie mit dem {{site.data.keyword.monitoringshort}}-Service eine CF-App überwachen, berücksichtigen Sie die folgenden Informationen:

* Sie müssen den {{site.data.keyword.monitoringshort}}-Service in dem Bereich bereitstellen, in dem auch die CF-App ausgeführt wird.
* Metriken, die für eine CF-App erfasst werden, werden automatisch an die Bereichsdomäne im {{site.data.keyword.monitoringshort}}-Service weitergeleitet. 
* Metriken werden an eine Bereichsdomäne weitergeleitet. Die Bereichsdomäne entspricht der Domäne, in der die CF-App ausgeführt wird. 
* Außerdem können Sie mithilfe der Metrik-API die Metriken abfragen und basierend auf den Daten entsprechende Maßnahmen ergreifen. Sie können beispielsweise eine Automatisierung erstellen, mit der die CPU-Auslastung der CF-App abgefragt und eine entsprechende Skalierung vorgenommen wird, wenn die CPU zu hoch wird.

Die folgende Abbildung zeigt eine allgemeine Übersicht der Überwachung von CF-Apps in {{site.data.keyword.Bluemix_notm}}:

![Allgemeine Übersicht der Überwachung von CF-Apps in {{site.data.keyword.Bluemix_notm}}](images/cfapp_metrics_ov.png "Allgemeine Übersicht der Überwachung von CF-Apps in {{site.data.keyword.Bluemix_notm}}")

## CF-Apps überwachen, die außerhalb von {{site.data.keyword.Bluemix_notm}} ausgeführt werden
{: #outside}

Um CF-Apps zu überwachen, die außerhalb von {{site.data.keyword.Bluemix_notm}} ausgeführt werden, können Sie mithilfe der Metrik-API die Metriken der CF-App an den {{site.data.keyword.monitoringshort}}-Service weiterleiten.

* Weitere Informationen zur API finden Sie unter [Metrik-API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-metrics-api?&language=node#introduction).
* Weitere Informationen zur Verwendung der API finden Sie unter [Daten über die Metrik-API senden](/docs/services/cloud-monitoring/send-metrics/send_data_api.html#send_data_api).




## Metriken für CF-Apps anzeigen und analysieren
{: #monitoring_cfapps}

Verwenden Sie Grafana zum Überwachen der Leistung von CF-Anwendungen in {{site.data.keyword.Bluemix_notm}}. 

Der {{site.data.keyword.monitoringlong}}-Service verwendet Grafana, eine Open-Source-Analyse- und Darstellungsplattform, mit der Sie Ihre Metriken in einer Vielfalt von Grafiken (z. B. Diagramme und Tabellen) überwachen, durchsuchen, analysieren und visualisieren können.

Sie können Grafana von einem Browser starten. Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

**Hinweis:** Sie müssen Grafana in der {{site.data.keyword.Bluemix_notm}}-Region starten, in der die Instanz der CF-App ausgeführt wird.


Um CF-Anwendungen zu überwachen, müssen Sie mindestens eine Abfrage in Grafana definieren. Weitere Informationen finden Sie unter [Metrikabfrage in Grafana konfigurieren](/docs/services/cloud-monitoring/grafana/define_query.html#define_query). 

Außerdem können Sie Alerts für Abfragen definieren. Weitere Informationen finden Sie unter [Alerts konfigurieren ](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).



## CPU-Metriken
{: #cpu_metrics}

Die Metrikserien, die automatisch für jede CF-Anwendung erfasst werden, enthalten Daten zur CPU-Auslastung.


<table>
  <caption>Für eine CF-Anwendung erfasste CPU-Metriken</caption>
  <tr>
    <th>Metrik</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td>cpu-utilization</td>
    <td>Prozentsatz der CPU-Auslastung im Hinblick auf das Limit des Containers.</td>
  </tr>
</table>


## Plattenmetriken
{: #disk_metrics}

Die Metrikserien, die automatisch für jede CF-Anwendung erfasst werden, enthalten Daten zu der genutzten Plattengröße, der gesamten verfügbaren Plattengröße und dem Prozentsatz an genutzter Platte.


<table>
  <caption>Für eine CF-Anwendung erfasste Plattenmetriken</caption>
  <tr>
    <th>Metrik</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td>disk-bytes-total</td>
    <td>Plattengröße des Containers, in dem die CF-App ausgeführt wird. Werte sind in Byte angegeben.</td>
  </tr>
  <tr>
    <td>disk-bytes-used</td>
    <td>Plattengröße des Containers, die von der CF-App genutzt wird. Werte sind in Byte angegeben.</td>
  </tr>
  <tr>
    <td>disk-utilization</td>
    <td>Prozentsatz der Platte, die von der CF-App genutzt wird.</td>
  </tr>
</table>

**Anmerkung:** 

* Sie geben die Plattengröße an, wenn Sie für die CF-App eine Push-Operation durchführen.
* Erreicht die Plattennutzung 90 %, sollten Sie die CF-App skalieren.

## Speichermetriken
{: #mem_metrics}

Die Metrikserien, die automatisch für jede CF-Anwendung erfasst werden, enthalten Daten zum genutzten Speicher, zum gesamten verfügbaren Speicher und dem Prozentsatz an genutztem Speicher.

<table>
  <caption>Für eine CF-Anwendung erfasste Speichermetriken</caption>
  <tr>
    <th>Metrik</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td>memory-bytes-total</td>
    <td>Speicher in Byte, der für die CF-App verfügbar ist.</td>
  </tr>
  <tr>
    <td>memory-bytes-used</td>
    <td>Speicher in Byte, der von der Instanz der CF-App verwendet wird.</td>
  </tr>
  <tr>
    <td>memory-utilization</td>
    <td>Prozentsatz an Speicher, der von der CF-App verwendet wird.</td>
  </tr>
</table>


## Abfrageformat für Metriken
{: #query_format}


Abfragen, die Sie in Grafana zum Überwachen einer Cloud Foundry-Anwendung definieren, müssen das folgende Format aufweisen: 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

Nachfolgend finden Sie Beispiele für die Metrikserien, die beispielsweise von einer Instanz der CF-App namens 'logtester' in der Region 'Sydney' angezeigt werden:

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

Weitere Informationen finden Sie unter [Format der Metriken von CF-Apps](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format).

**Hinweis:** Nicht alle Zeichen, die in Namen von CF-Apps zulässig sind, dürfen in Namen von Metrikserien verwendet werden. Großschreibung sind beispielsweise nicht zulässig. Der in Grafana angezeigte CF-App-Name beim Definieren einer Abfrage wird vollständig in Kleinbuchstaben angezeigt.




