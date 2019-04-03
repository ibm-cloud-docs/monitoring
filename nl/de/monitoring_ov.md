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


# Informationen
{: #monitoring_ov}

Verwenden Sie den {{site.data.keyword.monitoringlong}}-Service zur Erweiterung Ihrer Erfassungs- und Aufbewahrungsfunktionen, wenn Sie mit Metriken arbeiten, und um Regeln und Alerts definieren zu können, die Sie über Bedingungen informieren, die Ihre Aufmerksamkeit erfordern. Stärken Sie Ihr DevOps-Team durch Features, die Ihnen Einblick in die Leistung und den Ressourcenverbrauch Ihrer Apps bieten. So identifizieren Sie schnell aktuelle Trends und können Probleme sofort erkennen und diagnostizieren. Dies amortisiert sich sofort und ist eine Investition mit geringen Anschaffungs- und Betriebskosten. Verwenden Sie Grafana, um Ihre Umgebung zu überwachen. 
{:shortdesc}

Die folgende Abbildung zeigt eine Übersicht der unterschiedlichen Ressourcen, von denen aus Sie Metriken zur Analyse an den {{site.data.keyword.monitoringshort}}-Service senden können.

![Allgemeine Komponentenübersicht im {{site.data.keyword.monitoringlong}}-Service](images/cloud_monitoring_ov.png "Allgemeine Komponentenübersicht im {{site.data.keyword.monitoringlong}}-Service")

{{site.data.keyword.Bluemix}} erfasst standardmäßig Metriken zur CPU-Nutzung, Speicherauslastung und Netzein-/-ausgabe für den {{site.data.keyword.containershort}} und zeigt diese an. Sie können den {{site.data.keyword.monitoringshort}}-Service in {{site.data.keyword.Bluemix_notm}} verwenden, um Schlüsselmesswerte in Ihrer Umgebung und Ihren Anwendungen automatisch zu erfassen und zu messen. Es ist keine spezielle Instrumentierung erforderlich, um Metriken zu erfassen. Sie können beispielsweise Informationen, die von Leistungsmetriken bereitgestellt wurden, verwenden, um zu überwachen, wie ein Service in der Cloud ausgeführt wird. Sie können Ressourcenengpässe erkennen und das Service-Level-Agreement (SLA) im Blick behalten. Wenn Sie Leistungsdaten für einen Service analysieren, können Sie Situationen erkennen, die zu einem Ressourcenengpass führen können und folglich Ihr Service-SLA mit Ihren Kunden betreffen. Indem Sie in einem frühen Stadium Maßnahmen ergreifen, können Sie verhindern, dass solche Situationen Ihr Geschäft beeinträchtigen.  

Sie können Metriken für Ihre Cloud Foundry-Anwendungen (CF-Anwendungen) und virtuellen Maschinen (VM) an den {{site.data.keyword.monitoringshort}}-Service senden. Weitere Informationen zur Vorgehensweise beim Senden von Metriken finden Sie unter [Metriken an den {{site.data.keyword.monitoringshort}}-Service senden.](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#send_retrieve_metrics_ov)

Sie können den {{site.data.keyword.monitoringshort}}-Service über den {{site.data.keyword.Bluemix_notm}}-Katalog bereitstellen.  

Sie können vom {{site.data.keyword.monitoringshort}}-Service erfasste Metriken über das {{site.data.keyword.Bluemix_notm}}-Dashboard anzeigen und analysieren.  

## Gründe für die Verwendung des Überwachungsservice
{: #value}

1. **Investieren Sie weniger Zeit in die Instrumentierung Ihrer Anwendung und mehr Zeit in die Verbesserung des Nutzwerts.**

    Der {{site.data.keyword.monitoringlong_notm}}-Service erfasst automatisch Metrikdaten von den {{site.data.keyword.IBM_notm}} Cloud-Services und macht so Agenten überflüssig. APIs erleichtern das Hinzufügen von angepassten Metriken und das Abfragen Ihrer Überwachungsdaten. 
	
	Der {{site.data.keyword.monitoringlong_notm}}-Service bietet eine Erfassung von Metriken in Intervallen von einer Minute.  Im Rahmen des Lite-Plans werden die Metriken bei vollständiger Auflösung für 15 Tage gespeichert.  Im Rahmen des Premium-Plans werden die Metriken bei vollständiger Auflösung für 45 Tage gespeichert.

2. **Sie können die Überwachung ohne großen Aufwand in Ihrer Anwendung mit APIs erweitern**

    Integrieren Sie Ihre Überwachungsdaten über die {{site.data.keyword.monitoringshort}}-Service-APIs in Ihre Anwendungen und Operationen. Verwenden Sie die APIs, um relevante Anwendungs- und Geschäftsmetriken zu Ihren Cloud-Überwachungsdaten hinzuzufügen. Darüber hinaus können Sie die APIs verwenden, um Metrikdaten von außerhalb der {{site.data.keyword.IBM_notm}}-Cloud in den {{site.data.keyword.monitoringshort}}-Service zu importieren.

3. **Gewinnen Sie Einblicke in Ihre Umgebung, um Probleme schnell zu erkennen, zu diagnostizieren und zu identifizieren.**

    Visualisieren Sie den Impuls Ihrer Anwendung und Infrastruktur mit flexiblen und vom Benutzer angepassten Dashboards. {{site.data.keyword.monitoringlong_notm}} bietet Ihnen das Potenzial, die Flexibilität und die Vertrautheit von Grafana bei der schnellen Erstellung und Adaption Ihres Dashboards an die Bedürfnisse Ihrer Anwendung.
	
4. **Erstellen Sie wiederverwendbare Dashboards und machen Sie sie interaktiv.**

    Die Grafana-Bereitstellung des {{site.data.keyword.monitoringlong_notm}}-Service bietet Unterstützung für die Erstellung benutzerdefinierter Dashboards mit einer großen Palette an Visualisierungsoptionen.  Machen Sie Dashboards durch den Einsatz von Vorlagen dynamisch, indem Sie Metrikabfragen mit Variablen verwenden.

5. **Erhalten Sie Alerts.**

    Definiert Regeln zur Benachrichtigung bei Bedingungen, die Ihre Aufmerksamkeit erfordern. Der {{site.data.keyword.monitoringlong_notm}}-Service bietet eine API, die es Ihnen ermöglicht, Leistungsschwellenwerte festzulegen und Benachrichtigungen bei der Überschreitung dieser Schwellenwerte zu erhalten. Definieren Sie Alertregeln für eine einzelne Service- oder App-Instanz sowie Alertregeln für eine Gruppe von Instanzen. Wenn ein Alert ausgelöst wird, können Sie sich per E-Mail, PagerDuty-Ereignis, Webhook-Benachrichtigung oder eine beliebige Kombination der drei Möglichkeiten benachrichtigen lassen.

6. **Wählen Sie den Serviceplan aus, der Ihren Anforderungen entspricht.** 

    Abhängig von den jeweiligen Nutzungsanforderungen können Sie den Lite- oder den Premium-Serviceplan auswählen.  Der Lite-Plan bietet eine grundlegende Plattformmetrikerfassung und die zugehörige Alertfunktionalität.  Alternativ dazu können Sie den Premium-Plan auswählen, der eine umfassendere Metrikverarbeitung mit längerer Aufbewahrungsdauer, eine größere Anzahl definierbarer Alerts - einschließlich Alerts für mehrere Services und Apps - und Zugriff auf die Service-APIs ermöglicht.

 
## Servicepläne
{: #plan}

Der {{site.data.keyword.monitoringshort}}-Service bietet mehrere Pläne. Jeder Plan weist eine andere Funktionalität bei der Metrikzusammenstellung, Aufbewahrung und Alertdefinition auf. 

Sie können einen Plan über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder über die Befehlszeile ändern. Sie können Ihren Plan jederzeit aktualisieren oder reduzieren. Weitere Informationen zu Serviceplanupgrades in {{site.data.keyword.Bluemix_notm}} finden Sie in [Plan ändern](/docs/services/cloud-monitoring/plan/change_plan.html#change_plan). 

In der folgenden Tabelle sind die Pläne aufgeführt, die bei der Bereitstellung des {{site.data.keyword.monitoringshort}}-Service in einem Bereich verfügbar sind:

<table>
    <caption>Tabelle 1. Zusammenfassung der Pläne für den {{site.data.keyword.monitoringshort}}-Service pro Bereich.</caption>
      <tr>
        <th>Plan</th>
        <th>Senden der Metriken mithilfe der API</th>
        <th>Aufbewahrungsdauer für Metriken</th>
        <th>Alerts</th>
		    <th>Benachrichtigungsmethoden</th>
      </tr>
      <tr>
        <td>Lite (Standard)</td>
        <td>Nicht verfügbar</td>
        <td>15 Tage</td>
        <td>Sie können bis zu 10 Alertregeln für einzelne Metrikabfragen oder eine einzelne Alertregel mit einem Platzhalter definieren.</td>
		    <td>E-Mail</td>
      </tr>
      <tr>
        <td>Premium</td>
        <td>Verfügbar</td>
        <td>45 Tage</td>
        <td>Sie können Alertregeln einschließlich Regeln mit Platzhaltern definieren.</td>
		    <td>E-Mail, Webhook, PagerDuty</td>
      </tr>
</table>

**Hinweis:** Der Lite-Plan bietet dieselben Features wie die in {{site.data.keyword.Bluemix_notm}} integrierten Überwachungsfunktionen. Die Kontodomäne bietet wiederum dieselben Features wie der Lite-Plan.


## Aufbewahrungsdauer für Metriken
{: #metrics_retention}

In der folgenden Tabelle ist die Aufbewahrungsdauer auf der Basis Ihres Serviceplans zusammengefasst.

<table>
    <caption>Tabelle 2. Zusammenfassung der Aufbewahrungsdauer für den {{site.data.keyword.monitoringshort}}-Service.</caption>
      <tr>
        <th>Plan</th>
        <th>Aufbewahrungsdauer</th>
      </tr>
      <tr>
        <td>Lite (Standard)</td>
        <td>Metriken werden jede Minute gespeichert und 15 Tage aufbewahrt. (1m:15d)</td>
      </tr>
      <tr>
        <td>Premium</td>
        <td>Metriken werden jede Minute gespeichert und 45 Tage aufbewahrt. (1m:45d)</td>
      </tr>
</table>

Metriken, die in den letzten 7 Tagen keine Daten erhalten haben, werden gelöscht. Der {{site.data.keyword.monitoringshort}}-Service löscht alle Daten für einen Metrikpfad, der von transienter Natur zu sein scheint, indem er Metriken identifiziert, in die in den letzten 7 Tagen nicht geschrieben wurde. Beispiel:

* Wenn ein Container gelöscht wurde, bleiben die Metriken, die zu diesem Container gehörten, 7 Tage nach dem Löschen der Metriken erhalten.
* Wenn Sie eine statsd-Messanzeige mit dem Namen `<space_id>.test.statsd.gauge-hello` haben und eine Woche lang nicht in diese schreiben, wird diese Metrik zusammen mit allen archivierten Informationen gelöscht. 

## Bereitstellungs- und Überwachungsservice
{: #provision1}

Im {{site.data.keyword.Bluemix_notm}}-Katalog können Sie den {{site.data.keyword.monitoringshort}}-Service im **DevOps**-Abschnitt finden. Weitere Informationen zur Bereitstellung eines Service in {{site.data.keyword.Bluemix_notm}} finden Sie in [{{site.data.keyword.monitoringshort}}-Service bereitstellen](/docs/services/cloud-monitoring/how-to/provision.html#provision).

Beachten Sie die folgenden Informationen zum {{site.data.keyword.monitoringshort}}-Service:

* Sie können nur eine Instanz des {{site.data.keyword.monitoringshort}}-Service pro Bereich bereitstellen.
* Um Metriken für die Cloudressourcen zu erfassen, die in einem Cloud Foundry-Bereich ausgeführt werden, müssen Sie den Service in demselben Bereich zur Verfügung stellen, in dem die Ressourcen ausgeführt werden.




## Regionen
{: #regions}

Der {{site.data.keyword.monitoringshort}}-Service steht in den folgenden Regionen zur Verfügung:

* Deutschland
* Sydney
* Vereinigtes Königreich
* USA (Süden)




## URLs für den Überwachungsservice
{: #region}

Der {{site.data.keyword.monitoringshort}}-Service steht jeder Person mit einer {{site.data.keyword.Bluemix_notm}}-ID und Berechtigungen zum Arbeiten mit dem Service in {{site.data.keyword.Bluemix_notm}} zur Verfügung.

* Für jede Region, in der der {{site.data.keyword.monitoringshort}}-Service verfügbar ist, gibt es eine andere Gruppe von Endpunkten. 
* Es gibt eine einzelne URL, die von den Endpunkten für die Aufnahme und die API-/Webbenutzerschnittstelle gemeinsam genutzt wird.
* Port 443 ist ein TLS-Port, der für den Zugriff auf Metriken über die API und die Web-Benutzerschnittstelle (Grafana) verwendet wird.

In der folgenden Tabelle sind die URLs nach Region aufgelistet:

<table>
  <caption>Tabelle 3. Liste der Endpunkte zur Verwendung mit dem {{site.data.keyword.monitoringshort}}-Service.</caption>
  <tr>
    <th>Region</th>
	<th>Endpunkt</th>
  </tr>
  <tr>
    <td>Deutschland</td>
	<td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
  </tr>
  <tr>
    <td>Sydney</td>
	<td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
  </tr>
  <tr>
    <td>Vereinigtes Königreich</td>
	<td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
  </tr>
  <tr>
    <td>USA (Süden)</td>
	<td>[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)</td>
  </tr>
</table>



