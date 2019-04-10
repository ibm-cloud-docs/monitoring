---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring

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

# Ihre Umgebung überwachen
{: #monitoring}

Sie können Ihre Infrastruktur überwachen. Die Anwendungen, die mit dem {{site.data.keyword.mon_full_notm}}-Service ausgeführt in der Infrastruktur ausgeführt werden, können überwacht werden. Sie können eine Erfassung anfordern, um zu analysieren, was während eines Zeitrahmens in einem Knoten geschieht.
{:shortdesc}

Nachdem Sie eine Instanz des {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.Bluemix}} bereitgestellt und Sysdig-Agenten für Ihre Metrikquellen konfiguriert haben, können Sie Daten über die Webbenutzerschnittstelle des Service anzeigen, überwachen und verwalten.

Die Daten für Standardmetriken werden automatisch erfasst. Sie können angepasste Metriken konfigurieren und Bezeichnungen zu diesen Metriken hinzufügen, um deren Merkmale zu beschreiben. Die Daten für diese angepassten Metriken werden ebenfalls automatisch erfasst.

Sie können Daten auf der Registerkarte *Erkunden* und auf der Registerkarte *Dashboard* der Webbenutzerschnittstelle analysieren. Sie überwachen die Daten über Metrikansichten und Dashboards. 

* Verwenden Sie eine Metrikansicht, um eine bestimmte Metrik zu überwachen.
* Verwenden Sie Dashboards, um einen spezialisierten Einblick in Netzdaten, Anwendungsdaten, Topologie, Services, Hosts und Container zu erhalten, indem Daten über Anzeigen überwacht werden. In einer Anzeige wird eine Metrik oder eine Gruppe von Metriken in einem Dashboard angezeigt.

Für jede Metrikansicht und jedes Dashboard können Sie beispielsweise den Geltungsbereich der Daten definieren und festlegen, wie Daten zusammengefasst und welche Zeit- und Gruppenfilter auf die Daten angewendet werden sollen. Weitere Informationen hierzu finden Sie im Abschnitt [Daten verwalten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

Auf der Registerkarte *Erkunden* können Sie Daten mithilfe von Standardmetriken und Standarddashboards überwachen. Sie können Bezeichnungen verwenden, um neue Infrastrukturgruppen zu definieren, die Sie dann verwenden können, um Daten auf unterschiedliche Weise zusammenzufassen und Ihre Umgebung zu überwachen. Sie können auch benutzerdefinierte Dashboards verwenden, die Sie über die Registerkarte *Dashboard* definieren.

Auf der Registerkarte *Dashboards* können Sie Daten überwachen, indem Sie eines der Standarddashboards verwenden oder neue Dashboards erstellen.

Sie können ein Standarddashboard als Standardeingangspunkt für ein Team konfigurieren und somit die Erfahrung eines Teams vereinheitlichen und es den Benutzern ermöglichen, ihre unmittelbare Aufmerksamkeit auf die für sie relevantesten Informationen zu richten. 
{: tip}

Sie können Alerts verwenden, um Benutzer über Probleme zu benachrichtigen, die über einen oder mehrere Benachrichtigungskanäle Aufmerksamkeit erfordern.
* Der Abschnitt *Alerts* in der Webbenutzerschnittstelle zeigt die Liste der vordefinierten Alerts an. Aus dieser Ansicht können Sie vordefinierte Alerts aktivieren und inaktivieren. Sie können vorhandene Alerts ändern und neue Alerts erstellen.
* Der Abschnitt *Einstellungen* in der Webbenutzerschnittstelle ist die Position, an der Sie Benachrichtigungskanäle konfigurieren.
 
Sie können eine Erfassung auf einem Knoten anfordern, um zu analysieren, was in diesem Knoten während eines Zeitrahmens geschieht. Sie können diese beispielsweise verwenden, um Engpässe oder Komponenteninteraktionen zu analysieren.

## Metriken
{: #monitoring_metrics}

Eine Metrik ist eine quantitative Kennzahl, die mindestens eine Bezeichnung zum Definieren seiner Merkmale aufweist. Verwenden Sie Metriken, um statistische Daten zu analysieren, die numerische Werte aufweisen. 

Eine Metrik wird durch Zeitreihen dargestellt. Eine Zeitreihe ist eine Gruppe von numerischen Datenpunkten über einen bestimmten Zeitraum. 

Metriken werden in zwei Gruppen eingeteilt: 

* [Standardmetriken](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [Angepasste Metriken](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

Bezeichnungen werden als Infrastruktur- und Metrik-Deskriptor-Bezeichnungen klassifiziert. Jede Metrik verfügt über eine Reihe vordefinierter Bezeichnungen. Für benutzerdefinierte Metriken können Sie weitere Bezeichnungen konfigurieren. 

Sie können Bezeichnungen verwenden, um die Merkmale einer Metrik zu identifizieren und zu unterscheiden, wie z. B.:
* Sie können Infrastrukturobjekte in logische Hierarchien gruppieren. 
* Sie können Daten herausfiltern. 
* Sie können zusammengefasste Daten in Segmente aufteilen. 

Weitere Informationen finden Sie unter [Bezeichnungen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels).

## Anzeigen
{: #monitoring_panels}

In einer Anzeige wird eine Metrik oder eine Gruppe von Metriken in einem Dashboard angezeigt. 

Sie können einen der folgenden Anzeigentypen verwenden, um Metriken zu visualisieren:

| Typ | Beschreibung |
|------|-------------|
| Zeile | Verwenden Sie diese Anzeige, um Trends für eine oder mehrere Metriken im Laufe der Zeit anzuzeigen.  |
| Bereich | Verwenden Sie diese Anzeige, um Trends für eine oder mehrere Metriken im Laufe der Zeit anzuzeigen.  |
| Top-Liste | Verwenden Sie diese Anzeige, um eine Metrik über mehrere Gruppen von Entitäten hinweg zu vergleichen. Das Balkendiagramm ist in absteigender Reihenfolge sortiert.  |
| Histogramm | Verwenden Sie diese Anzeige, um die Häufigkeitsverteilung einer Metrik in Buckets anzuzeigen.  |
| Topologie | Verwenden Sie diese Anzeige, um die Infrastruktur als Topologiemap sowie die Beziehungen zwischen Entitäten in der Map darzustellen.  |
| Zahl | Verwenden Sie diese Anzeige, um eine einzelne Zahl anzuzeigen, die den Wert einer Aggregationsmetrik für eine oder mehrere Entitäten im Laufe der Zeit darstellt.  |
| Tabelle | Verwenden Sie diese Anzeige, um numerische Daten für Ihre Infrastruktur basierend auf Metriken und Segmenten anzuzeigen.  |
| Text | Verwenden Sie diese Anzeige, um Text hinzuzufügen. Verwenden Sie Markdown, um Ihren Text hinzuzufügen.  |
{: caption="Tabelle 3. Anzeigentypen" caption-side="top"} 

Sie können Anzeigen kopieren, ihren Geltungsbereich ändern, die Anzeigen duplizieren, löschen, exportieren und erkunden.

Sie können Daten aus einer Anzeige exportieren. Beachten Sie beim Exportieren von Daten die folgenden Informationen:

* Sie können Daten aus einem Kurvendiagramm in eine **JSON-Datei** exportieren.
* Sie können Daten aus einem Tabellendiagramm oder aus einem Kurvendiagramm in eine **CSV-Datei** exportieren.


In der folgenden Tabelle sind die Tasks aufgelistet, die Sie mit Anzeigen ausführen können:

| Task | Beschreibung |
|------|-------------|
| [Anzeige kopieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | Kopieren Sie eine Anzeige in ein neues Dashboard.  |
| [Geltungsbereich ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Ändern Sie den Geltungsbereich einer Anzeige. |
| [Anzeige duplizieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | Kopieren Sie eine Anzeige in dasselbe Dashboard.  |
| [Anzeige löschen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | Löschen Sie eine Anzeige aus dem Dashboard.  |
| [Daten exportieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | Exportieren Sie Daten aus einer Anzeige in eine CSV- oder JSON-Datei.  |
| [Alert erstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | Definieren Sie einen Alert für eine Metrik. |
{: caption="Tabelle 4. Anzeigentasks" caption-side="top"} 


## Dashboards
{: #monitoring_dashboards}

Ein **Dashboard** zeigt Gruppen von Metriken an, die einen Bericht über den Zustand, die Leistung und den Status Ihrer Infrastruktur, Anwendungen und Services für einen einzelnen Host oder für eine Gruppe von Hosts erstellen. Dashboards bieten einen spezialisierten Einblick in Netzdaten, Anwendungsdaten, Topologie, Services, Hosts und Container. Verwenden Sie Dashboards, um Ihre Infrastruktur, Anwendungen und Services zu überwachen.


Im Abschnitt **DASHBOARDS** der Webbenutzerschnittstelle sind Dashboards in drei Hauptgruppen unterteilt:

* *Meine Dashboards*: Dies sind die Dashboards, die von dem Benutzer erstellt werden, der momentan angemeldet ist.
* *Meine gemeinsam genutzten Dashboards*: Dies sind die Dashboards, die von dem Benutzer erstellt werden, der momentan angemeldet ist, und die mit anderen Benutzern gemeinsam genutzt werden.
* *Mit mir gemeinsam genutzte Dashboards*: Dies sind die Dashboards, die von anderen Benutzern erstellt wurden und mit dem aktuellen Benutzer gemeinsam genutzt werden.

Im Abschnitt **ERKUNDEN** der Webbenutzerschnittstelle sind Dashboards in zwei Gruppen unterteilt:
* *Standarddashboards*: Dies sind vordefinierte Dashboards.
* *Meine Dashboards*: Dies sind die Dashboards, die von dem Benutzer erstellt werden, der momentan angemeldet ist.

Sie können vordefinierte Dashboards verwenden. Sie können auch benutzerdefinierte Dashboards über die Webbenutzerschnittstelle oder programmgesteuert erstellen. Sie können Dashboards sichern und wiederherstellen, indem Sie Python-Scripts oder die Sysdig-REST-API verwenden.

Sie können Dashboards auch über die Webbenutzerschnittstelle kopieren und gemeinsam nutzen. 

In der folgenden Tabelle werden die Tasks aufgeführt, die Sie ausführen können, um mit Dashboards von der Benutzerschnittstelle aus zu arbeiten:

| Task | Beschreibung |
|------|-------------|
| [Dashboard erstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | Erstellen Sie in der Webbenutzerschnittstelle ein angepasstes Dashboard. |
| [Dashboard kopieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | Erstellen Sie eine Kopie eines Dashboards im aktuellen Team, in dem das Dashboard verfügbar ist, oder kopieren Sie ein Dashboard in ein anderes Team. |
| [Geltungsbereich ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Ändern Sie den Geltungsbereich eines Dashboards.       |
| [Dashboard löschen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  Löschen Sie ein Dashboard. |
| [Dashboard gemeinsam nutzen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | Nutzen Sie Dashboards zwischen Benutzern in einem Team und extern gemeinsam, indem Sie eine öffentliche URL für das Dashboard konfigurieren. |
{: caption="Tabelle 1. Dashboardtasks, die Sie in der Webbenutzerschnittstelle ausführen können" caption-side="top"} 

In der folgenden Tabelle werden die Tasks aufgeführt, die Sie programmgesteuert ausführen können, um mit Dashboards zu arbeiten:

| Task                    |	REST-API verwenden                |
|-------------------------|-------------------------------|
| Dashboard erstellen      | [Dashboard mithilfe der API erstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Dashboard löschen      | [Dashboard mithilfe der API löschen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Dashboards speichern       | [Dashboards eines Teams mithilfe der API speichern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabelle 2. Tasks zum programmgesteuerten Verwalten von Dashboards" caption-side="top"} 



## Ereignisse
{: #monitoring_events}

Ein Ereignis ist eine Benachrichtigung, die darüber informiert, dass in einem der Knoten, die Daten an Ihre {{site.data.keyword.mon_full_notm}}-Instanz weiterleiten, etwas aufgetreten ist. Verwenden Sie Ereignisse, um Probleme zu überprüfen, zu verfolgen und zu beheben. 

Es gibt verschiedene Arten von Ereignissen: 

* *Alertereignisse* sind Ereignisse, die durch vom Benutzer konfigurierte Alerts ausgelöst werden. Weitere Informationen finden Sie im Abschnitt [Mit Alerts arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* *Infrastrukturbasierte Ereignisse* sind Ereignisse, die von Docker- und Kubernetes-Knoten erfasst werden. Standardmäßig erkennt der Sysdig-Agent automatisch Daten aus einer ausgewählten Gruppe von Ereignissen und erfasst diese. Sie können die Agentenkonfigurationsdatei bearbeiten, um weitere Ereignisse zu aktivieren.
* *Angepasste Ereignisse*, die Sie über eine der folgenden Integrationen konfigurieren: Slackbot, vordefinierte Python-Scripts, angepasste und vom Benutzer erstellte Python-Scripts oder cURL-Anforderungen.

Ein Ereignis hat standardmäßig einen Status: 
* *Aktiv*: Dieser Status zeigt an, dass die Umstände, die das Ereignis ausgelöst haben, weiterhin vorhanden sind, z. B. wenn ein Knoten weiterhin inaktiv ist.
* *OK*: Dieser Status zeigt an, dass die Situation wieder normal ist, z. B. wenn ein Knoten wieder betriebsbereit ist.

Ereignisse werden im Abschnitt *Ereignisse* der Webbenutzerschnittstelle verwaltet. 
* Sie können Alertereignisse über die Registerkarte *Alertereignisse* anzeigen.
* Sie können infrastrukturbasierte Ereignisse über die Registerkarte *Angepasste Ereignisse* anzeigen.
* Sie können angepasste Ereignisse über die Registerkarte *Angepasste Ereignisse* anzeigen.
* Sie können angepasste Ereignisse mithilfe des [API-Token für dieses Team](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token) an jedes Ihrer Teams senden. Weitere Informationen finden Sie unter [Angepasste Ereignisse ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.

Sie können die Situation lösen, die ein Ereignis ausgelöst hat. Während Sie warten, bis die Bedingung, die das Ereignis ausgelöst hat, erneut ausgeführt wird, und den Status auf *OK* setzen, können Sie das Ereignis als **Gelöst** festlegen, um grafisch anzuzeigen, dass das Problem behoben wurde. 
{: #tip}



## Alerts
{: #monitoring_alerts}

Ein Alert ist ein Benachrichtigungsereignis, das Sie verwenden können, um vor Situationen zu warnen, die Aufmerksamkeit erfordern. Jeder Alert hat einen Prioritätsstatus. Dieser Status informiert Sie über die Kritikalität der Informationen, die gemeldet werden. 

Wenn Sie einen Alert definieren, müssen Sie die Bedingung, die die Benachrichtigung auslöst, einen oder mehrere Benachrichtigungskanäle, über die Sie benachrichtigt werden möchten, die Prioritätsstufe des Alerts und den Typ des Alerts definieren. 

Sie können Alerts für einen der folgenden Alerttypen definieren:

| Typ              | Beschreibung |
|-------------------|-------------|
| Anomalieerkennung | Verwenden Sie diese Option, um Hosts auf der Basis ihres Langzeitverhaltens zu überwachen, und um Benachrichtigungen zu erhalten, wenn sie abweichen. |
| Ausfallzeit          | Verwenden Sie diese Option, um einen beliebigen Entitätstyp zu überwachen, z. B. Host, Container, Prozess oder Service, und um Benachrichtigungen zu erhalten, wenn die Entität ausfällt. |
| Ereignis             | Verwenden Sie diese Option, um das Auftreten bestimmter Ereignisse zu überwachen und Benachrichtigungen zu erhalten, wenn die Gesamtzahl der Vorkommen einen Schwellenwert nicht einhält. Sie können sie beispielsweise verwenden, um auf Neustarts und Bereitstellungen von Containern, Orchestrierungen und Serviceereignissen hinzuweisen.|
| Gruppen-Ausreißer     | Verwenden Sie diese Option, um eine Gruppe von Hosts zu überwachen und Benachrichtigungen zu erhalten, wenn eine Gruppe anders als die übrigen agiert. |
| Metrik            | Verwenden Sie diese Option, um Zeitreihenmetriken zu überwachen und Benachrichtigungen zu erhalten, wenn sie gegen benutzerdefinierte Schwellenwerte verstoßen. |
{: caption="Tabelle 5. Alerttypen" caption-side="top"} 

Die Priorität ist standardmäßig auf *Warnung* festgelegt. Sie können die Priorität eines Alerts auf einen der folgenden Werte festlegen: *Notfall*, *Alert*, *Kritisch*, *Fehler*, *Warnung*, *Hinweis*, *Information*, Debug* 

Sie können einen oder mehrere Benachrichtigungskanäle für eine der folgenden Benachrichtigungsintegrationen definieren:
* E-Mail-Benachrichtigungen
* PagerDuty-Benachrichtigungen
* Slack-Benachrichtigungen
* VictorOps-Benachrichtigungen
* OpsGenie-Benachrichtigungen
* Webhook-Kanal konfigurieren

Weitere Informationen hierzu finden Sie im Abschnitt [Einen Benachrichtigungskanal konfigurieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create).


Sie können in der Webbenutzerschnittstelle und mithilfe der Sysdig-API vordefinierte Alerts aktivieren, Alerts ändern und angepasste Alerts erstellen.

Sie verwalten Alerts in der Ansicht *Alerts* der Webbenutzerschnittstelle. Sie können die Tabellenspalten konfigurieren, die in der Ansicht *Alerts* angezeigt werden. Gültige Spaltenoptionen: *Name*, *Geltungsbereich*, *Alert, wenn*, *Segment nach*, *Benachrichtigungen*, *Aktiviert*, *Geändert*, *Erfassungen*, *Kanäle*, *Erstellt*, *Beschreibung*, *E-Mail-Empfänger*, *Für mindestens*, *OpsGenie*, *PagerDuty*, *Priorität*, *Slack*, *WebHook*, *SNS-Topics*, *Typ*, *VictorOps*

In der folgenden Liste werden die wichtigsten Tasks bei der Arbeit mit Alerts beschrieben:
* [Alert konfigurieren ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [Alert aktivieren oder inaktivieren ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [Nach einem Alert suchen ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [Alert ändern ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [Alert in dasselbe Team kopieren ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [Alert in ein anderes Team kopieren ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [Alert exportieren ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [Alert löschen ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [Alertschwellenwerte als angepasste Boolesche Ausdrücke definieren ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## Erfassungen
{: #monitoring_captures}

Eine Erfassung ist eine Tracedatei, die Sie generieren können, um zu analysieren, was in einem Knoten während eines Zeitrahmens geschieht. Die Größenbeschränkung der Aufzeichnungsdatei beträgt 100 MB. Sie können diese beispielsweise verwenden, um Engpässe oder Komponenteninteraktionen zu analysieren. 

Erfassungen enthalten Systemaufrufe und andere Betriebssystemereignisse wie Latenzzeiten auf Systemebene, Dauer von Stapeljobs, Unterbrechungszeiten für Implementierungen, Latenzzeiten für die automatische Skalierung, Container-Startzeiten oder Anwendungstransaktionszeiten. Erfassungen enthalten detaillierte Informationen aus jedem Container für einen Knoten. 

In Abhängigkeit von den Richtlinien Ihrer Organisation können Sie Erfassungen inaktivieren. Standardmäßig sind Erfassungen aktiviert, wenn Sie einen Sysdig-Agenten in einem Knoten konfigurieren.
{: tip}

Sie können *Erfassungen* für einzelne Knoten erstellen, erkunden, herunterladen und löschen. Ein Knoten kann ein Host, ein Container, eine virtuelle Maschine, ein Bare Metal oder eine Metrikquelle sein, in der Sie einen Sysdig-Agenten installieren. 

* In der Webbenutzerschnittstelle erstellen Sie Erfassungen im Abschnitt *Erkunden* und verwalten die Erfassungsdateien über den Abschnitt *Erfassungen*.
* Sie können Daten aus einer Erfassung mithilfe von *Csysdig* (der Curses-basierten Befehlszeilenbenutzerschnittstelle für Sysdig) oder mit den Open-Source-Sysdig-Dienstprogrammen visualisieren, um die Daten in einer Erfassung zu analysieren.
* Sie können Daten in einer Erfassung mithilfe von Filtern durchsuchen.
* Sie können Daten in einer Erfassung mithilfe von Chisels (Scripts) bearbeiten. 

Wenn Sie die Erfassungsfunktion für ein Team aktivieren, sind die Erfassungsdateien nur für Mitglieder dieses Teams sichtbar.

In der folgenden Liste werden die wichtigsten Tasks bei der Arbeit mit Erfassungen beschrieben:
* [Erfassung erstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [Erfassung löschen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [Erfassung erkunden](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [Erfassung herunterladen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

Weitere Informationen finden Sie im Abschnitt [Mit Erfassungen arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


