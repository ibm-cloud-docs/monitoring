---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring,  predefined dashboards

subcollection: Sysdig

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


# Vordefinierte Dashboards
{: #default_dashboards}
Sie können eines der folgenden vordefinierten Dashboards auswählen, um Ihre Infrastruktur zu überwachen:
{:shortdesc}


## Anwendungen
{: #default_dashboards_applications}

In der folgenden Tabelle sind die vordefinierten Dashboards aufgeführt, die Sie für die Überwachung Ihrer Anwendungen und Infrastrukturkomponenten auswählen können:

| Dashboard-Name        | Beschreibung                                                            | Nutzung             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| HTTP-Übersicht         | Verwenden Sie dieses Dashboard, um den Status Ihres Webservers zu überwachen. Es zeigt die Last auf dem Server und seine Fähigkeit an, Anforderungen zeitnah zu bedienen. | Verwenden Sie die Anzeigen "Anzahl der Anforderungen" und "Durchschn./Max. Anfragezeit", um die gesamte Auslastung Ihres Servers zu messen. </br>Suchen Sie nach Korrelationen zwischen URLs, um Möglichkeiten zu finden, die Leistung zu verbessern. </br>Verwenden Sie die Statuscodes-Metrik, um die Fehlercodes 4xx und 5xx zu überwachen. |  
| HTTP-Top-Requests  |  Verwenden Sie dieses Dashboard, um die oben angeforderten URLs für Ihren Web-Server zu überwachen, wie z. B. die Gesamtzahl der Anforderungen, die durchschnittliche und die maximale Zeit zur Handhabung von Anforderungen und die Menge des in den Anforderungen und Antworten enthaltenen Datenverkehrs. |   |
| MongoDB  | Verwenden Sie dieses Dashboard, um zu überwachen, wie ausgelastet Ihr MongoDB-Dienst ist, welche Datensammlungen am meisten nachgefragt werden und welche Datensammlungen die geringste Leistung aufweisen.  |  Erfahren Sie, welche Datensammlungen von einer Optimierung der Abfrage- und Indexleistung profitieren können. |
| MySQL/PostgreSQL  | Verwenden Sie dieses Dashboard, um die gesamte Last und den Leistungsstatus Ihrer SQL-Datenbanktransaktionen zu überwachen. Informieren Sie sich über die Anzahl der Anfragen und wie schnell sie bearbeitet werden.  | Verbessern Sie die Leistung. Überwachen Sie z. B. die Antwortzeiten für die langsamsten Abfragen und identifizieren Sie die Änderungen, die Sie an der Abfrage oder den Indizes für die Tabellen vornehmen.  |
| MySQL/PostgreSQL Top  | Verwenden Sie dieses Dashboard, um die wichtigsten SQL-Abfragen zu überwachen. Zeigen Sie die Anzahl der empfangenen Abfragen und die Menge an Datenverkehr an, die für die Abfrage gesendet und empfangen wurden.   | Informieren Sie sich über die langsamsten Abfragen, die Abfragen mit der längsten Zeitdauer und Abfragen mit hohem Datenverkehr.  |
| Nginx  | Verwenden Sie dieses Dashboard, um Hostressourcen, HTTP-Verbindungen, wichtigste und langsamste URLs und Host-Antwortcodes zu überwachen. | Ermitteln Sie die Lastausgleichsanpassungen, indem Sie die folgenden Metriken überwachen: Schreiben, Lesen, Warten auf Verbindungen, CPU-Belastung nach Maschine, Netz-Byte-Aktivität, Anforderungen pro Sekunde. </br>Suchen Sie nach Seiten, die optimiert werden könnten, indem Sie die Metrik "Langsamste URLs" prüfen. </br>Suchen Sie nach Problemen, indem Sie Antwortcodes prüfen.  |
{: caption="Tabelle 1. Liste der vordefinierten Dashboards für Anwendungen und Infrastrukturkomponenten" caption-side="top"} 


## Host- und Container-Dashboards
{: #default_dashboards_host_container}

In der folgenden Tabelle sind die vordefinierten Dashboards aufgelistet, die Sie zur Überwachung der Ressourcennutzung und der Systemaktivität auf Ihren Hosts und in Ihren Containern verwenden können:


| Dashboard-Name        | Beschreibung                                                            | Nutzung             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| *Containerbegrenzungen*    | Verwenden Sie dieses Dashboard, um die CPU- und Speichermetriken anzuzeigen, die relativ zu den Hostressourcen und den einzelnen Containern zugeordnet sind. | |
| *Dateisystem*         | Verwenden Sie dieses Dashboard zum Anzeigen von Verzeichnismountpunkten, Dateisystemeinheiten sowie Kapazitäts- und Nutzungsinformationen für die Dateisysteme, die der Instanz angehängt sind.  </br>Dateisysteme mit einem Mount auf einem fernen System werden standardmäßig nicht aufgelistet. Fügen Sie zum Anzeigen der Daten für diese Dateisysteme zum folgenden Eintrag **remotefs.enabled = true** in die Datei */opt/draios/bin/dragent.properties* für jede Instanz hinzu. </br>Wenn Gruppen ausgewählt werden, sind die Metriken Durchschnittswerte für ähnliche Mountpunkte des Dateisystems.| Erfahren Sie, welche Dateisysteme gefüllt werden und welche nicht ausgelastet sind. Sortieren Sie nach *fs.bytes.used*.|
| *Übersicht nach Container* | Verwenden Sie dieses Dashboard, um Statistiken zur Ressourcennutzung anzuzeigen, z. B. CPU-Prozentsatz, Prozentsatz der Speicherbelegung, Gesamtanzahl der Netzbytes und Gesamtanzahl der Dateibytes für Container, die in der ausgewählten Gruppe oder Instanz ausgeführt werden.  </br>Verwenden Sie die Funktion *Reisezeit* mit der Funktion *Vergleichen* in dieser Ansicht, um historische Informationen anzuzeigen. Überprüfen Sie anhand der Daten, ob die Prozesse wie erwartet ausgeführt werden, ob sie falsch sind oder mehr Ressourcen benötigen. | Finden Sie heraus, welche Container viele Ressourcen belegen.  </br>Verwenden Sie die Informationen, um festzustellen, ob eine Anwendung auf einen anderen Host verschoben werden soll. |
| *Übersicht nach Container-Image* | Verwenden Sie dieses Dashboard, um eine Übersicht über die Größe, die Leistung und die Einschränkungen der Services zu erhalten, die im Container-Image definiert sind. | |
| Übersicht nach Host | Verwenden Sie dieses Dashboard, um allgemeine Ressourcennutzungsstatistikdaten für einen Host anzuzeigen, wie CPU-Prozentsatz, Prozentsatz der Speicherbelegung, Gesamtanzahl der Netzbyte, Anzahl der Netzverbindungen, Gesamtanzahl der Dateibyte, Plattenbelegung. </br>Sie können dieses Dashboard auch verwenden, um eine Gruppe von Instanzen zu überwachen. </br>Verwenden Sie die Funktion *Reisezeit* mit der Funktion *Vergleichen* in dieser Ansicht, um historische Informationen anzuzeigen. Überprüfen Sie anhand der Daten, ob die Prozesse wie erwartet ausgeführt werden, ob sie falsch sind oder mehr Ressourcen benötigen. | Finden Sie heraus, welche Hosts nicht verwendet werden oder die in einer Gruppe von Hosts mit ähnlichen Jobfunktionen überbelegt sind. | 
| Übersicht nach Prozess | Verwenden Sie dieses Dashboard, um allgemeine Ressourcennutzungsstatistikdaten für die wichtigsten Prozesse eines Hosts anzuzeigen, wie CPU-Prozentsatz, Prozentsatz der Speicherbelegung, Gesamtanzahl der Netzbyte, Anzahl der Netzverbindungen, Gesamtanzahl der Dateibyte, Plattenbelegung. </br>Sie können dieses Dashboard auch verwenden, um eine Gruppe von Instanzen zu überwachen. </br>Verwenden Sie die Funktion *Reisezeit* mit der Funktion *Vergleichen* in dieser Ansicht, um historische Informationen anzuzeigen. Überprüfen Sie anhand der Daten, ob die Prozesse wie erwartet ausgeführt werden, ob sie falsch sind oder mehr Ressourcen benötigen. | Finden Sie heraus, welche Prozesse viele Ressourcen belegen.  </br>Verwenden Sie die Informationen, um festzustellen, ob eine Anwendung auf einen anderen Host verschoben werden soll. |
| Sysdig-Agent-Zusammenfassung | Verwenden Sie dieses Dashboard, um die Anzahl der Sysdig-Agenten anzuzeigen, die in Ihrer Umgebung und ihren Versionen bereitgestellt sind. |  | 
| Häufigste Dateien | Verwenden Sie dieses Dashboard, um die Liste der häufigsten Dateien anzuzeigen. Sie können den Dateinamen, die Gesamtanzahl der Dateibyte, die Zeit in der Datei-E/A und die Dateifehleranzahl anzeigen. | Erfahren Sie, welche die Platten die größten Konsumenten sind, wenn Sie nach Größe sortieren. </br>Erfahren Sie, welche die Dateien am aktivsten sind, wenn Sie nach Größe sortieren. </br>Identifizieren Sie potenzielle Fehler, indem Sie die Daten in der Spalte *Dateifehleranzahl* überwachen. |
| Häufigste Prozesse | Verwenden Sie dieses Dashboard, um die Liste der häufigsten Prozesse anzuzeigen, die in einem Host oder einer Gruppe von Hosts ausgeführt werden. Sie können den Prozessnamen, seinen Pfad und alle Argumente anzeigen. </br>Verwenden Sie die Filterfunktion, um die aufgelisteten Prozesse einzuschränken. | Finden Sie heraus, welche Prozesse zu den höchsten Konsumenten in einer Umgebung gehören, in der derselbe Prozess mehrmals gestartet wird. |
| Top-Server-Prozesse | Verwenden Sie dieses Dashboard, um den Ressourcenverbrauch für Prozesse anzuzeigen, die nur als serverorientiert identifiziert werden (HTTPD, Java, NTPD usw.).. | Informieren Sie sich über die Ressourcennutzung für Serverprozesse. |
{: caption="Tabelle 2. Liste der vordefinierten Dashboards für Host und Container" caption-side="top"} 

## Netz
{: #default_dashboards_network}

In der folgenden Tabelle sind die vordefinierten Dashboards aufgeführt, die Sie auswählen können, um Ihre Netzverbindungen und die Aktivität zu überwachen:

| Dashboard-Name        | Beschreibung                                                            | Nutzung             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| Verbindungstabelle     | Verwenden Sie dieses Dashboard, um die Verbindungen zwischen Ihren Instanzen und fernen Knoten anzuzeigen. Überwachen Sie den Datenverkehr für jede Verbindung. | Erfahren Sie, welche Elemente in Ihrem Netz den höchsten Datenverkehr verursachen. |
| Übersicht              |  Verwenden Sie dieses Dashboard, um die gesamte Netzauslastung nach Anweisung, Anwendung, Prozess und Host im Laufe der Zeit anzuzeigen.| Geben Sie an, welche Ressourcen die Antwortleistung am meisten beeinflussen. |
| Antwortzeiten vs. Ressourcennutzung | Verwenden Sie dieses Dashboard, um die Metriken der Hostressource im Vergleich zur Antwortzeit des Hosts bei der Verarbeitung von Netzanforderungen anzuzeigen. |  |
| Häufigste Ports             |  Verwenden Sie dieses Dashboard, um eingehende, ausgehende und gesamte Byte pro Port sowie die Anzahl der Verbindungen zu den einzelnen Portnummern anzuzeigen. |  |
{: caption="Tabelle 3. Liste der vorab definierten Netz-Dashboards" caption-side="top"} 



## Service
{: #default_dashboards_service}


In der folgenden Tabelle sind die vordefinierten Dashboards aufgelistet, die Sie verwenden können, um die Leistung Ihrer Services zu überwachen, selbst wenn diese Services in orchestrierten Containern bereitgestellt sind:

| Dashboard-Name        | Beschreibung                                                            | 
|-----------------------|------------------------------------------------------------------------|
| Übersicht nach Service   | Verwenden Sie dieses Dashboard, um die Größe, die Leistung und die Einschränkungen der Services anzuzeigen, die in demselben Container-Image ausgeführt werden. | 
| Serviceübersicht      | Verwenden Sie dieses Dashboard, um die Ressourcenauslastung und die Antwortzeiten eines einzelnen Service anzuzeigen. | 
{: caption="Tabelle 4. Liste der vordefinierten Dashboards für Services" caption-side="top"} 



## Topologie
{: #default_dashboards_topology}

In der folgenden Tabelle sind die vordefinierten Dashboards aufgeführt, die Sie zum Überwachen der logischen Abhängigkeiten Ihrer Anwendungsschichten verwenden können:

| Dashboard-Name        | Beschreibung                                                            | 
|-----------------------|------------------------------------------------------------------------|
| CPU-Belastung             | Verwenden Sie dieses Dashboard, um die Interaktion zwischen Ihrem Host und der übrigen Infrastruktur zu überwachen.  | 
| Netzverkehr       | Verwenden Sie dieses Dashboard, um die Bandbreitennutzung der ausgewählten Instanz zwischen lokalen Prozessen und Prozessen auf fernen Knoten zu überwachen. |
| Antwortzeiten        | Verwenden Sie dieses Dashboard, um die Kommunikations- und Netzantwortmetriken zwischen allen Prozessen auf den ausgewählten Hosts zu überwachen. </br>Die Antwortanzahl und Antwortzeiten werden im Durchschnitt bis zu einer Sekunde Granularität angezeigt.  |
{: caption="Tabelle 5. Liste der vordefinierten Dashboards für die Topologie" caption-side="top"} 

**Hinweis:** Alle diese Dashboards zeigen gestrichelte Linien und graue Felder für Instanzen an, auf denen der Sysdig-Agent nicht installiert ist und für die eine Kommunikation erkannt wird.















