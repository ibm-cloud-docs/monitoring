---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, overview

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


# {{site.data.keyword.mon_full_notm}}
{: #about}

{{site.data.keyword.mon_full}} ist ein für die Cloud natives Container-Intelligence-Managementsystem eines Drittanbieters, das Sie als Teil Ihrer {{site.data.keyword.cloud_notm}}-Architektur verwenden können. Nutzen Sie es, um Einblick in die Leistung und den Status Ihrer Anwendungen, Services und Plattformen zu erhalten. Es bietet Administratoren, DevOps-Teams und Entwicklern eine vollständige Stack-Telemetrie mit erweiterten Funktionen zum Überwachen und Beheben von Fehlern, zum Definieren von Alerts und zum Entwerfen angepasster Dashboards. {{site.data.keyword.mon_full_notm}} wird von Sysdig in Partnerschaft mit {{site.data.keyword.IBM_notm}} betrieben.
{:shortdesc}


Um Überwachungsfunktionen mit {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}} hinzuzufügen, müssen Sie eine Instanz des {{site.data.keyword.mon_full_notm}}-Service bereitstellen.

Bevor Sie eine Instanz bereitstellen, sollten Sie die folgenden Informationen beachten:

* Ihre Daten werden an einen Drittanbieter gesendet.
* Der Kontoeigner kann eine Instanz eines Service in {{site.data.keyword.cloud_notm}} erstellen, anzeigen und löschen. Er kann auch anderen Benutzern die Berechtigung erteilen, mit dem {{site.data.keyword.mon_full_notm}}-Service zu arbeiten.
* Andere {{site.data.keyword.cloud_notm}}-Benutzer mit `Administrator`- oder `Editor`-Berechtigungen können den {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.cloud_notm}} verwalten. Diese Benutzer müssen außerdem über die Plattform-Berechtigungen verfügen, um Ressourcen im Kontext der Ressourcengruppe zu erstellen, in der sie die Instanz bereitstellen wollen.

Sie können eine Instanz im Kontexts einer Ressourcengruppe bereitstellen. Mit einer Ressourcengruppe können Sie Ihre Services für die Zugriffssteuerung und die Abrechnung organisieren. Sie können die {{site.data.keyword.mon_full_notm}}-Instanz in der *Standard*-Ressourcengruppe oder in einer angepassten Ressourcengruppe bereitstellen.

Wenn Sie [eine Instanz bereitstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision), erhalten Sie automatisch einen Aufnahmeschlüssel, der auch als [Sysdig-Zugriffsschlüssel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key) bezeichnet wird.

Nachdem Sie eine Instanz bereitgestellt haben, müssen Sie einen {{site.data.keyword.mon_full_notm}}-Agenten für jede Metrikquelle konfigurieren. Eine Metrikquelle ist die Cloudressource, die Sie überwachen und deren Leistung und Status Sie steuern möchten. Sie müssen in jeder Umgebung, die Sie überwachen wollen, einen {{site.data.keyword.mon_full_notm}}-Agenten konfigurieren. Eine Metrikquelle kann z. B. ein Kubernetes-Cluster sein. Sie verwenden den Sysdig-Zugriffsschlüssel, um den Sysdig-Agenten zu konfigurieren, der für die Erfassung und Weiterleitung von Metriken an Ihre Instanz verantwortlich ist.

Nachdem der {{site.data.keyword.mon_full_notm}}-Agent in einer Metrikquelle bereitgestellt wurde, wird die Erfassung und Weiterleitung von Metriken an die Instanz automatisch ausgeführt. Der {{site.data.keyword.mon_full_notm}}-Agent erfasst und berichtet automatisch über vordefinierte Metriken. Sie können konfigurieren, welche Metriken in einer Umgebung überwacht werden sollen.

Sie können Daten über die {{site.data.keyword.mon_full_notm}}-Webbenutzerschnittstelle [überwachen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring) und [verwalten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).  

Die folgende Abbildung zeigt die Komponentenübersicht für den {{site.data.keyword.mon_full_notm}}-Service, der unter {{site.data.keyword.cloud_notm}} ausgeführt wird:

![{{site.data.keyword.mon_full_notm}} Komponentenübersicht von {{site.data.keyword.cloud_notm}}](images/components.png "{{site.data.keyword.mon_full_notm}} Komponentenübersicht von {{site.data.keyword.cloud_notm}}")



## Datenerfassung
{: #overview_collection}

Wenn Sie einen Sysdig-Agenten für die Erfassung und Weiterleitung von Daten an eine {{site.data.keyword.mon_full_notm}}-Instanz konfigurieren, werden die Daten automatisch erfasst und sind zur Analyse über die Webbenutzerschnittstelle verfügbar.

Die Daten werden mit einer Frequenz von 10 Sekunden erfasst. 

## Datenverfügbarkeit
{: #overview_availability}

Die Daten sind für maximal 15 Monate verfügbar.

Nachdem Sie einen Sysdig-Agenten aus einem Host oder Container entfernt haben, werden die Protokolldaten nicht gelöscht. Die Daten sind für die Analyse über die Webbenutzerschnittstelle für den Zeitraum verfügbar, in dem der Agent installiert und berichtet wurde.

Nachdem Sie eine Instanz des {{site.data.keyword.mon_full_notm}}-Service gelöscht haben, stehen keine Daten mehr für die Suche und Analyse zur Verfügung.



## Datenspeicherung
{: #overview_retention}

Die Daten werden für jede Instanz werden auf der Basis einer *Rollup*-Richtlinie aufbewahrt.

Im Laufe der Zeit werden die Daten innerhalb von 3 Monaten von einer feinen Granularität zu einer gröberen aufsummiert.

Die Rollup-Richtlinie beschreibt die Granularität der Daten im Laufe der Zeit:

* Die Daten werden für die ersten 6 Stunden mit einer 10-Sekunden-Auflösung aufbewahrt.
* Die Daten werden für 2 Tage mit einer 1-Minuten-Auflösung aufbewahrt.
* Die Daten werden für 2 Wochen mit einer 10-Minuten-Auflösung aufbewahrt.
* Die Daten werden für 3 Monate mit einer 1-Stunden-Auflösung aufbewahrt.
* Die Daten werden für 1 Jahr mit einer 1-Tag-Auflösung aufbewahrt.

## Datenlöschung
{: #overview_data_deletion}

Wenn Sie eine Instanz von {{site.data.keyword.mon_full_notm}} aus {{site.data.keyword.cloud_notm}} löschen, müssen Sie einen Supportfall öffnen, damit das Löschen der Daten anzufordern. Weitere Informationen erhalten Sie im Abschnitt [Unterstützung anfordern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp).

Wenn Sie eine Erfassung löschen, wird die Datendatei für diese Erfassung automatisch gelöscht.

Das Löschen von Daten, die von einem einzigen Sysdig-Agenten in einer {{site.data.keyword.mon_short}}-Instanz erfasst werden, wird nicht unterstützt.
{: note}



## Datenposition
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}} erfasst und fasst Metriken zusammen. 

* Metrikdaten werden in {{site.data.keyword.cloud_notm}} bereitgestellt.
* Jede Region mit mehreren Zonen (MZR) erfasst und fasst Metriken für jede Instanz von {{site.data.keyword.mon_full_notm}} zusammen, die an dieser Position ausgeführt wird.
* Die Daten befinden sich in der Region, in der die {{site.data.keyword.mon_full_notm}}-Instanz bereitgestellt ist. Zum Beispiel werden Metrikdaten für eine Instanz, die in der Region "USA (Süden)" bereitgestellt wird, in der Region "USA (Süden)" gehostet.



## {{site.data.keyword.mon_full_notm}}-Agenten
{: #overview_sysdig_agent}

Der {{site.data.keyword.mon_full_notm}}-Agent erfasst und berichtet automatisch über vordefinierte Metriken. 

In der folgenden Liste sind die verfügbaren {{site.data.keyword.mon_full_notm}}-Agenten aufgeführt:

* {{site.data.keyword.mon_full_notm}}-Agent für Kubernetes, GKE und OpenShift.
* {{site.data.keyword.mon_full_notm}}-Agent für Docker-Container oder nicht-containerbasierte Services.
* {{site.data.keyword.mon_full_notm}}-Agent für Mesos, Marathon und DCOS.
* {{site.data.keyword.mon_full_notm}}-Agent für manuelle Linux-Installationen.

Weitere Informationen hierzu finden Sie in den Abschnitten [Einen Sysdig-Agenten konfigurieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) und [Einen Sysdig-Agenten entfernen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove).


## Die Nutzung anzeigen
{: #overview_usage}

Weitere Informationen zur Überwachung der Nutzung und Kosten Ihres Service finden Sie im Abschnitt [Ihre Nutzung anzeigen](/docs/billing-usage/viewing_usage.html#viewingusage).


## Servicepläne
{: #overview_plans}

Es sind verschiedene Preisstrukturpläne für eine {{site.data.keyword.mon_full_notm}}-Instanz verfügbar. [Erfahren Sie mehr darüber](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).


## Sicherheitsaspekte
{: #overview_security}

**Erfassungen**

Eine Erfassung ist eine Tracedatei, die Sie generieren können, um zu analysieren, was in einem Host während eines Zeitrahmens geschieht. Erfassungen enthalten Systemaufrufe und andere Betriebssystemereignisse. Sie können diese Funktion pro Knoten aktivieren oder inaktivieren, wenn Sie den Sysdig-Agenten konfigurieren, der Metriken von diesem Knoten erfasst. Standardmäßig sind *Erfassungen* aktiviert, wenn Sie einen Sysdig-Agenten konfigurieren. Ein Knoten kann ein Host, ein Container, eine virtuelle Maschine, ein Bare Metal oder eine Metrikquelle sein, in der Sie einen Sysdig-Agenten installieren.

Wenn Erfassungen aktiviert sind, ist es möglich, dass Sysdig einen tiefen Einblick in Ihre Operationen hat. Um einen Sicherheitsvorfall und möglicherweise den Zugang von außerhalb Ihres Unternehmens auf Daten zu vermeiden, müssen Sie die Sicherheitsrichtlinien Ihres Unternehmens überprüfen, bevor Sie die Erfassung auf einem Knoten aktivieren. Ziehen Sie die Inaktivierung der *Erfassungsfunktion* für alle Sysdig-Agenten in Betracht.
{: important}

