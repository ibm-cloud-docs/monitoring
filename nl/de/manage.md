---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, manage

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

# Daten verwalten
{: #manage}

Verwenden Sie Bezeichnungen, um Infrastrukturressourcen in logische Hierarchien zu gruppieren, Daten herauszufiltern und zusammengefasste Daten in Segmente aufzuteilen. Passen Sie an, wie Daten aggregiert werden, wenn Sie ein Diagramm konfigurieren oder einen Alert für eine Metrik erstellen. Legen Sie den Geltungsbereich eines Dashboards, einer Anzeige oder eines Alerts fest, um Datenpunkte zu filtern. Beschränkten Sie den Zugriff auf Daten, indem der Datenzugriff der Benutzer durch die Teams verwaltet werden. 
{:shortdesc}



## Bezeichnungen
{: #manage_labels}

**Bezeichnungen** definieren die Merkmale einer Metrik. Sie können Bezeichnungen verwenden. um die Merkmale einer Metrik zu identifizieren und zu unterscheiden. 

Bezeichnungen werden als Infrastruktur- und Metrik-Deskriptor-Bezeichnungen klassifiziert. Jede Metrik verfügt über eine Reihe vordefinierter Bezeichnungen. Für benutzerdefinierte Metriken können Sie weitere Bezeichnungen konfigurieren. 

* Sie können **Infrastrukturbezeichnungen** verwenden, um Objekte innerhalb der Infrastruktur zu identifizieren. Diese Bezeichnungen werden aus der Infrastruktur abgerufen. Eine Bezeichnung kann z. B. *kubernetes.pod.name* sein.
* Sie können **Metrik-Deskriptor-Bezeichnungen** verwenden, um benutzerdefinierte Bezeichnungen zu definieren. Diese Bezeichnungen sind Schlüssel/Wert-Paare, die direkt auf Metriken angewendet werden und die aus den Integrationen wie StatsD, Prometheus und JMX stammen. 

## Gruppen
{: #manage_groups}

**Gruppen** organisieren Infrastrukturobjekte in logischen Hierarchien. Verwenden Sie Gruppen, um Ihre Infrastruktur zu strukturieren und die Überwachung Ihrer Umgebung zu vereinfachen.

In der *Erkunden*-Ansicht der Webbenutzerschnittstelle können Sie eine der folgenden Aktionen ausführen:

| Task                                                                                        | Beschreibung     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Eine Gruppe kopieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#copy_group)                | Kopieren Sie eine Gruppe in andere Teams. |
| [Eine Gruppe erstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#create_group)            | Erstellen Sie eine neue Gruppe. |
| [Eine Gruppe löschen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#delete_group)            | Löschen Sie eine Gruppe. |
| [Eine Gruppe umbenennen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#rename_group)            | Benennen Sie eine Gruppe. |
| [Eine Gruppe gemeinsam nutzen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#share_group)              | Geben Sie eine Gruppe für andere Mitglieder im Team frei. |
{: caption="Tabelle 1. Tasks zur Gruppierung von Bezeichnungen" caption-side="top"} 



## Aggregation
{: #manage_aggregation}

Die**Aggregation** von Daten erfolgt automatisch, wenn Sie ein Diagramm konfigurieren oder einen Alert für eine Metrik erstellen. Es gibt zwei Arten von Aggregation: Zeitaggregation und Gruppenaggregation. 
* Die Zeitaggregation wird immer vor der Gruppenaggregation ausgeführt.
* Sie können zusammengefasste Daten auch mithilfe von Bezeichnungen in kleinere Abschnitte aufteilen, die **Segmente** genannt werden, um mehrere Vergleiche und mehrere Alerts zu erstellen. 

Sysdig aggregiert Daten im Laufe der Zeit. Dann werden diese Datenpunkte verwendet und gruppiert, um die Daten in Metriken oder Dashboards anzuzeigen oder die Schwellenwerte für Alerts zu berechnen. 
{: tip}

Sie können anpassen, wie Daten aggregiert werden, wenn Sie ein Diagramm konfigurieren oder einen Alert für eine Metrik erstellen.

Es gibt zwei Formen der Aggregation für Metriken: 
* Zeitaggregation
* Gruppenaggregation

**Die Zeitaggregation wird immer vor der Gruppenaggregation ausgeführt.**


### Zeitaggregation
{: #manage_time_aggregation}

**Ein Sysdig-Agent erfasst und berichtet Metriken standardmäßig mit einer 10-Sekunden-Auflösung.**

Bei Zeitreihendiagrammen, die Daten für maximal fünf Minuten enthalten: 
* Datenpunkte werden bei einer Auflösung von 10 Sekunden aufgezeichnet.
* Es findet keine Zeitaggregation statt.

Die Zeitaggregation erfolgt automatisch in einer der folgenden Situationen:

* Bei Zeitreihendiagrammen, die Daten für einen Zeitraum von mehr als fünf Minuten enthalten, werden Datenpunkte als Aggregat für ein geeignetes Zeitintervall aufgezeichnet. Beispiel: Für ein Diagramm, das Daten für eine Stunde zeigt, stellt jeder Datenpunkt beispielsweise ein 1-Minuten-Intervall dar.
* Wenn Sie Protokolldaten anzeigen. Daten werden im Laufe der Zeit aufsummiert. Sie können auswählen, welche Datenpunkte verwendet werden sollen, wenn Sie ältere Daten anzeigen.

In der folgenden Tabelle werden verschiedene Aggregationstypen für Zeitreihendiagramme aufgelistet:

| Aggregationstyp | Beschreibung                                                              |
|------------------|--------------------------------------------------------------------------|
| average          | Durchschnitt der abgerufenen Metrikwerte über den gesamten ausgewerteten Zeitraum hinweg. |
| rate (timeAvg)   | Durchschnittlicher Wert der Metrik über den gesamten ausgewerteten Zeitraum hinweg.            |
| maximum	         | Höchster Wert während des ausgewerteten Zeitraums.                          |
| minimum	         | Geringster Wert während des ausgewerteten Zeitraums.                           |
| sum              | Kombinierte Summe der Metrik über den gesamten ausgewerteten Zeitraum.             |
{: caption="Tabelle 2. Aggregationstypen für Zeitreihendiagramme" caption-side="top"} 

**Hinweis:** Standardmäßig wird der Durchschnitt für die Anzeige von Datenpunkten für ein Zeitintervall verwendet.

Die Rate und der Durchschnitt sind sehr ähnliche Aggregationstypen. Sie liefern oft das gleiche Ergebnis. Die Berechnung unterscheidet sich jedoch. Wenn die Zeitaggregation auf eine Minute festgelegt wird, wird der Sysdig-Agent so eingestellt, dass er sechs Proben abruft, alle 10 Sekunden eine Probe. Beachten Sie, dass in einigen Fällen aufgrund von Verbindungstrennungen oder anderen Umständen keine Proben vorhanden sind.


### Gruppenaggregation
{: #manage_group_aggregation}

**Metriken, die auf eine Gruppe von Ressourcen angewendet werden, z. B. mehrere Container, Hosts oder Knoten, werden standardmäßig zwischen den Mitgliedern der Gruppe gemittelt.**

Wenn beispielsweise drei Hosts eine unterschiedliche CPU-Auslastung für ein Probenintervall melden, werden die drei Werte gemittelt und als einzelner Datenpunkt für diese Metrik in dem Diagramm aufgelistet.

In der folgenden Tabelle werden verschiedene Typen von Gruppenaggregationstypen aufgeführt:

| Aggregationstyp | Beschreibung                                        |
|------------------|----------------------------------------------------|
| average          | Der durchschnittliche Wert der Proben des Intervalls.           |
| maximum	         | Der höchste Wert der Proben des Intervalls.           |
| minimum	         | Der niedrigste Wert der Proben des Intervalls.            |
| sum              | Der kombinierte Wert der Proben des Intervalls.          |
{: caption="Tabelle 3. Aggregationstypen für Gruppenzusammenfassung" caption-side="top"} 


**Die Gruppenzusammenfassung hängt von der Segmentierung ab.** Für eine Ansicht, in der Metriken für eine Gruppe von Elementen angezeigt werden, wenn die Auswahl *Segment nach* so geändert wird, dass die einzelnen Elemente aufgegliedert werden, findet keine Gruppenaggregation statt.



## Geltungsbereich
{: #manage_scope}

Der **Geltungsbereich** ist eine Sammlung von Bezeichnungen, die die Bedingungen zum Filtern von Datenpunkten definieren, wenn Sie Dashboards und Anzeigen erstellen, Alerts konfigurieren und Teams anpassen. 

In der folgenden Tabelle werden die Tasks aufgelistet, die Sie ausführen können, um den Geltungsbereich im Überwachungsservice zu ändern:

| Task                                                                                        | Beschreibung     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Geltungsbereich eines Dashboards ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Ändern Sie den Geltungsbereich eines Dashboards, um Datenpunkte für alle Metriken zu filtern, die über Anzeigen im Dashboard angezeigt werden. |
| [Geltungsbereich einer Anzeige ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Ändern Sie den Geltungsbereich einer Anzeige, um Daten für eine bestimmte Metrik zu filtern, die über die Anzeige angezeigt wird. |
| [Geltungsbereich eines Teams ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope) | Ändern Sie den Geltungsbereich der Daten, die für Benutzer sichtbar sind, die Mitglieder eines Teams sind. |
{: caption="Tabelle 4. Tasks zum Ändern des Geltungsbereichs" caption-side="top"} 


## Teams
{: #manage_teams}

**Teams** gruppieren Benutzer und steuern die Daten sowie die Berechtigungen für die Arbeit mit Sysdig-Erfassungen und Infrastrukturereignissen für diese Benutzer. 

Ein Sysdig-Administrator kann eine beliebige Anzahl von Teams definieren. Er kann für jedes Team die folgenden Informationen konfigurieren:
* Das *Standardteam*: Sie können dieses Team als das Team festlegen, dem jeden Benutzer, der sich zum ersten Mal bei der Webbenutzerschnittstelle anmeldet, standardmäßig zugeordnet wird.
* Der *Standardeingangspunkt*: Sie können die Ansicht in der Webbenutzerschnittstelle angeben, die bei jeder Anmeldung eines Benutzers geöffnet wird. Gültige Eingangspunkte sind: Ansicht *Erkunden*, Ansicht *Dashboards*, Ansicht *Ereignisse*, Ansicht *Alerts* und Ansicht *Einstellungen*.
* Der Geltungsbereich: Sie können die Daten, die Benutzer anzeigen können, einschränken. Sie können *Host* oder *Container* auswählen, um die Ebene der Daten zu definieren, die sichtbar sein sollen. Anschließend können Sie eine oder mehrere Bedingungen hinzufügen. Wenn der Geltungsbereich auf *Host* festgelegt ist, können Benutzer alle Informationen auf der Host- und Containerebene anzeigen. Wenn der Geltungsbereich auf *Container* festgelegt ist, können Benutzer nur Informationen auf Containerebene anzeigen.
* Die Berechtigungen: Sie können die folgenden Funktionen aktivieren oder inaktivieren: *Sysdig-Erfassungen* und *Infrastrukturereignisse*. Erfassungsdateien sind nur für Mitglieder des Teams sichtbar. **Hinweis:** Erfassungen enthalten detaillierte Informationen aus jedem Container auf einem Host, unabhängig vom Geltungsbereich des Teams. Wenn die Infrastrukturereignisse aktiviert sind, können Benutzer alle angepassten Infrastrukturereignisse von jedem Benutzer und Sysdig-Agenten in der Instanz anzeigen.

Standardmäßig gibt es das Team **Operationen überwachen**, das für jede {{site.data.keyword.mon_full_notm}}-Instanz vordefiniert ist.
* Dieses Team kann nicht gelöscht werden.
* Benutzer werden automatisch als Mitglieder dieses Teams hinzugefügt und erhalten vollständigen Einblick in alle in der Instanz verfügbaren Ressourcen. 

**Hinweis:** 
* Ein Administrator muss in das Team *Operationen überwachen* wechseln, bevor er Teams erstellen oder die Einstellungen für andere Teams ändern kann.
* Nachdem sich ein Benutzer bei {{site.data.keyword.cloud_notm}} angemeldet und die Sysdig-Webbenutzerschnittstelle gestartet hat, kann ein Administrator diesen Benutzer in der Sysdig-Webbenutzerschnittstelle verwalten. Der Benutzer wird in der Sysdig-Datenbank erstellt, wenn sich der Benutzer zum ersten Mal an der Sysdig-Webbenutzerschnittstelle anmeldet. 

Um die Anzeigeberechtigungen für Benutzer einzuschränken, kann ein Administrator eine der folgenden Aktionen ausführen:
* Ändern Sie die Rolle des Benutzers im Standardteam *Operationen überwachen* zu einem *Leseberechtigten*. 
* Erstellen Sie ein Standardteam mit eingeschränktem Geltungsbereich und eingeschränkter Sichtbarkeit. Ordnen Sie dann Benutzer manuell anderen Teams zu. 

In der folgenden Tabelle sind die Tasks aufgelistet, die Sie ausführen können, wenn Sie mit Teams arbeiten:

| Task                                                                            | Beschreibung                 |
|---------------------------------------------------------------------------------|-----------------------------|
| [Team erstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_create)      | Erstellen Sie ein Team, um die Datensichtbarkeit zu steuern.  |
| [Team löschen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_delete)      | Löschen Sie ein Team. </br>**Hinweis:** Wenn Sie ein Team löschen, werden Benutzer, die nur zu diesem Team gehören, in das Standardteam verschoben. |
| [Teammitglieder hinzufügen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_users)   | Fügen Sie einem Team weitere Benutzer hinzu. |
| [Team bearbeiten ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope)          | Ändern Sie den Geltungsbereich der Daten, die für Benutzer sichtbar sind, die Mitglieder eines Teams sind.  |
{: caption="Tabelle 5. Tasks für die Arbeit mit Teams" caption-side="top"} 





    


