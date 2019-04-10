---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, metrics

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

# Mit Metriken arbeiten
{: #metrics}

Nachdem Sie eine Instanz des {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.Bluemix}} bereitgestellt und einen Sysdig-Agenten für eine Metrikquelle konfiguriert haben, können Sie Metriken über die {{site.data.keyword.mon_full_notm}}-Webbenutzerschnittstelle anzeigen, überwachen und verwalten. Verwenden Sie Metriken, um statistische Daten zu analysieren, die numerische Werte aufweisen. 
{:shortdesc}


**Eine Metrik ist eine quantitative Kennzahl, die mindestens eine Bezeichnung zum Definieren seiner Merkmale aufweist.**

Eine Metrik wird durch Zeitreihen dargestellt. 

Eine Zeitreihe ist eine Gruppe von numerischen Datenpunkten über einen bestimmten Zeitraum. 

Metriken werden in zwei Gruppen eingeteilt: 

* Standardmetriken 
* Angepasste Metriken


## Bezeichnungen
{: #metrics_labels}

**Bezeichnungen definieren die Merkmale einer Metrik.**

Bezeichnungen werden als Infrastruktur- und Metrik-Deskriptor-Bezeichnungen klassifiziert. Jede Metrik verfügt über eine Reihe vordefinierter Bezeichnungen. Für benutzerdefinierte Metriken können Sie weitere Bezeichnungen konfigurieren. 

Sie können Bezeichnungen verwenden, um die Merkmale einer Metrik zu identifizieren und zu unterscheiden, wie z. B.:
* Sie können Infrastrukturobjekte in logische Hierarchien gruppieren. 
* Sie können Daten herausfiltern. 
* Sie können zusammengefasste Daten in Segmente aufteilen. 


## Standardmetriken 
{: #metrics_default}

**Standardmetriken berichten über das System, den Orchestrator und die Netzinfrastruktur.**

Der Überwachungsservice fügt jeder Metrik automatisch Bezeichnungen hinzu.


## Angepasste Metriken
{: #metrics_custom}

**Angepasste Metriken variieren je nach Typ der Infrastruktur und nach den Anwendungen, die Sie überwachen. Einige Beispiele sind JMX, Prometheus und StatsD.**

Diese Metriken verfügen über eine Reihe vordefinierter Bezeichnungen. Sie können zusätzliche angepasste Bezeichnungen hinzufügen.

Der Überwachungsservice verwaltet einen Index aller angepassten Metriken und angepassten Bezeichnungen, die in den letzten 14 Tagen Daten gemeldet haben. Sie können diese Metriken verwenden, um Dashboards, Geltungsbereiche und Alerts zu konfigurieren.

Berücksichtigen Sie die folgenden Informationen, wie der Überwachungsservice die Indexeinträge verwaltet:
*  Eine Metrik wird automatisch aus dem Überwachungsserviceindex entfernt und als fehlend markiert, wenn eine der folgenden Bedingungen auftritt:
    
    * Der Überwachungsservice empfängt seit mehr als 14 Tagen keine Daten für eine Metrik oder eine Bezeichnung.
    
    * Eine Metrik oder eine Bezeichnung hat nie Daten gemeldet.

* Sie können keine neuen Artefakte mit einer fehlenden Metrik oder einer fehlenden Bezeichnung konfigurieren. 
* Sie können vorhandene Artefakte erst dann aktualisieren, wenn die fehlenden Metriken und Bezeichnungen aus der aktuellen Konfiguration entfernt wurden.
* Sie können eine fehlende Metrik oder eine fehlende Bezeichnung für Datenabfragen und Diagramme verwenden. 
* Ihre vorhandenen Artefakte sind nicht betroffen, wenn sie eine fehlende Metrik oder eine fehlende Bezeichnung enthalten.
* Wenn Daten für eine fehlende Metrik oder eine fehlende Bezeichnung empfangen werden, wird dem Index die Metrik oder die Bezeichnung erneut hinzugefügt.



