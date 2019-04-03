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



# {{site.data.keyword.messagehub}}
{: #monitoring_mh_ov}

In {{site.data.keyword.Bluemix}} werden {{site.data.keyword.messagehub}}-Metriken automatisch erfasst. Die Anzahl der ankommenden und abgehenden Bytes eines Abschnitts wird erfasst. Alle 15 Minuten wird ein Prüfpunkt erstellt. Sie können Grafana verwenden, um diese Metriken zu visualisieren. 
{:shortdesc}


**Hinweis:** {{site.data.keyword.messagehub}}-Metriken sind im Rahmen des {{site.data.keyword.messagehub}}-Standardplans nur in den Regionen USA (Süden), Vereinigtes Königreich und Sydney verfügbar.  




## Metriken anzeigen und analysieren
{: #view}

Verwenden Sie Grafana zum Überwachen der Leistung von {{site.data.keyword.messagehub}} in {{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.messagehub}} stellt ein Dashboard bereit, über das Sie die Leistung Ihrer Abschnitte anzeigen und überwachen können.

Der {{site.data.keyword.monitoringlong}}-Service verwendet Grafana, eine Open-Source-Analyse- und Darstellungsplattform, mit der Sie Ihre Metriken in einer Vielfalt von Grafiken (z. B. Diagramme und Tabellen) überwachen, durchsuchen, analysieren und visualisieren können. 

Sie können Grafana auf eine der folgenden Weisen starten:

* Sie können in der {{site.data.keyword.Bluemix_notm}}-Konsole im {{site.data.keyword.messagehub}}-Dashboard auf die Schaltfläche **Grafana** klicken.

    Grafana wird im Kontext des Bereichs in {{site.data.keyword.Bluemix_notm}} geöffnet, in dem {{site.data.keyword.messagehub}} ausgeführt wird.
    
* Sie können Grafana direkt über einen Web-Browser starten.

    Stellen Sie sicher, dass Sie sich in der richtigen Organisation und im richtigen Bereich befinden, in der bzw. in dem die {{site.data.keyword.messagehub}}-Instanz ausgeführt wird.
    
    Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).
    

Beachten Sie die folgenden Informationen:

* Sie müssen Grafana in derselben {{site.data.keyword.Bluemix_notm}}-Region starten, in der auch die {{site.data.keyword.messagehub}}-Instanz ausgeführt wird.
* Verwenden Sie das Grafana-Dashboard, das standardmäßig bereitgestellt wird, um mit der Überwachung Ihrer {{site.data.keyword.messagehub}}-Instanz zu beginnen.
* Erstellen Sie benutzerdefinierte Grafana-Dashboards, um Ad-hoc-Dashboards zu erstellen. Sie können eine oder mehrere Metrikabfragen in einem Grafana-Dashboard definieren, um eine {{site.data.keyword.messagehub}}-Instanz zu überwachen. Weitere Informationen finden Sie unter [Metrikabfrage in Grafana konfigurieren](/docs/services/cloud-monitoring/grafana/define_query.html#define_query).
* Außerdem können Sie Alerts für Abfragen definieren. Weitere Informationen finden Sie unter [Alerts konfigurieren ](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).


## Metriken für einen Kafka-Abschnitt
{: #kafka_topic_metrics}

Für jeden definierten Kafka-Abschnitt werden die folgenden Metriken erfasst:


<table>
  <caption>Metriken pro Kafka-Abschnitt</caption>
  <tr>
    <th>Metrik</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Rate der Bytes, die von Kafka-Clientanwendungen an den Abschnitt gesendet werden.</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Rate der Bytes, die von Kafka-Clientanwendungen von einem Abschnitt empfangen werden.</td>
  </tr>
</table>



## Metriken für eine Kafka-Partition
{: #kafka_partition_metrics}

Für jede Kafka-Partition mit einer Cloudspeicherbrücke, die Nachrichten verarbeitet, werden die folgenden Metriken erfasst:


<table>
  <caption>Metriken für Kafka-Partitionen</caption>
  <tr>
    <th>Metrik</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>Das Offset für den letzten Kafka-Datensatz, der von der Cloudspeicherbrücke verarbeitet wird.</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>Das festgeschriebene Offset für Kafka-Datensätze, die von der Cloudspeicherbrücke verarbeitet werden.</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Anzahl der Nachrichten, die von einer Cloudspeicherbrückeninstanz von einem Kafka-Abschnitt empfangen werden. Zählt nur die Nachrichten, die gültigen JSON-Code enthalten, der nicht von der Brücke verarbeitet werden kann.</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Anzahl der Nachrichten, die von einer Cloudspeicherbrückeninstanz von einem Kafka-Abschnitt empfangen werden. Zählt nur Nachrichten, die Daten enthalten, die nicht geparst werden konnten, da die Daten kein gültiges JSON-Dokument sind.</td>
  </tr>
</table>




## Referenzinformationen
{: #mhlinks}

* [Einführung in Message Hub](/docs/services/EventStreams/index.html#getting_started)
* [Überwachung und Protokollierung](/docs/services/EventStreams/messagehub072.html#monitoring)

