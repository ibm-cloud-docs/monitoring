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


# Zum Grafana-Dashboard navigieren
{:#navigating_grafana}

In {{site.data.keyword.Bluemix}} können Sie Grafana, eine Open-Source-Analyse- und Darstellungsplattform, verwenden, um Ihre Metriken in einer Vielfalt von Grafiken (z. B. Diagramme und Tabellen) zu überwachen, zu durchsuchen, zu analysieren und zu visualisieren. Verwenden Sie Grafana, um erweiterte Analysetasks durchzuführen.
{:shortdesc}

Sie können Grafana auf eine der folgenden Weisen starten:

* Über {{site.data.keyword.Bluemix_notm}}

    Sie können für Ihre spezifischen Docker-Container Metriken in Grafana im Kontext dieser spezifischen Container starten. Dieses Feature gilt nur für Container, die in der {{site.data.keyword.Bluemix_notm}}-verwalteten Infrastruktur bereitgestellt sind. 
    
    Weitere Informationen finden Sie in [Vom {{site.data.keyword.Bluemix_notm}}-Dashboard zum
    Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_bluemix). 

* Von einem direkten Browser-Link

    Sie können Grafana starten, so dass die angezeigten Daten Protokolle von Services innerhalb des bereitgestellten {{site.data.keyword.Bluemix_notm}}-Bereichs zusammenfassen.
    
    Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).
    
Weitere Informationen zu Grafana finden Sie im [Grafana Benutzerhandbuch![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Vom IBM Cloud-Dashboard zum Grafana-Dashboard navigieren
{: #launch_grafana_from_bluemix}

**Hinweis:** Dieses Feature gilt nur für Container, die in der {{site.data.keyword.Bluemix_notm}}-verwalteten Infrastruktur bereitgestellt sind. 

Die Abfrage wird verwendet, um die Daten zu filtern, die in Grafana angezeigt werden. Grafana ruft Daten für die {{site.data.keyword.Bluemix_notm}}-Container ab, von denen Sie Kibana starten. 

Führen Sie die folgenden Schritte aus, um die Metriken eines Docker-Containers in Grafana anzuzeigen:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie anschließend vom *Dashboard* aus auf den Container. 
    
2. Klicken Sie in der Navigationsleiste auf **Überwachung und Protokolle**. Die Registerkarte für die Überwachung wird angezeigt. 
    
3. Klicken Sie auf **Erweiterte Ansicht**. Das **Grafana**-Dashboard wird angezeigt.


##  Von einem Web-Browser zum Grafana-Dashboard navigieren
{: #launch_grafana_from_browser}

Die Abfrage wird verwendet, um die Daten zu filtern, die in Grafana angezeigt werden. Grafana ruft Daten für einen Bereich in der {{site.data.keyword.Bluemix_notm}}-Organisation ab. Die Informationen zu Metriken, die Grafana anzeigt, umfassen Datensätze für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix_notm}}-Organisation bereitgestellt wurden, bei der Sie angemeldet sind.

Führen Sie die folgenden Schritte aus, um Grafana von einem Browser zu starten:

1. Öffnen Sie einen Web-Browser. 
2. Geben Sie die URL für die Region ein, in der Sie Metriken überwachen wollen. 

    In der folgenden Tabelle sind die URLs nach Region aufgelistet:
	<table>
      <caption>URLs zum Starten von Grafana in verschiedenen Regionen</caption>
      <tr>
        <th>Region</th>
	    <th>Endpunkt</th>
      </tr>
      <tr>
        <td>Deutschland</td>
	    <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
      </tr>
      <tr>
        <td>Vereinigtes Königreich</td>
	    <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
      </tr>
      <tr>
        <td>USA (Süden)</td>
    	<td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
      </tr>
      <tr>
        <td>Vereinigtes Königreich</td>
	    <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
      </tr>
      
    </table>
	
2. Wählen Sie **Grafana** aus.
     

