---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# Erfassungen verwalten
{: #captures}

Eine Erfassung ist eine Tracedatei, die Sie generieren können, um zu analysieren, was in einem Host während eines Zeitrahmens geschieht. Sie können diese beispielsweise verwenden, um Engpässe oder Komponenteninteraktionen zu analysieren. Im {{site.data.keyword.mon_full_notm}}-Service können Sie *Erfassungen* für einzelne Knoten erstellen, erkunden, herunterladen und löschen. 
{:shortdesc}

Weitere Informationen finden Sie in [Erfassungen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


## Eine Erfassung erstellen
{: #captures_create}

Sie können eine Erfassung in der Ansicht *Erkunden* erstellen.

Führen Sie die folgenden Schritte aus, um eine Erfassungsdatei zu erstellen:

1. Navigieren Sie zum *ERKUNDEN*-Abschnitt in der Webbenutzerschnittstelle. [Erfahren Sie mehr darüber](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. Klicken Sie auf das Symbol für den Switch-Host ![Symbol für den Switch-Host](images/switch_hosts.png).

3. Wählen Sie einen Host oder einen Container aus.

4. Klicken Sie auf das Aktionssymbol ![Drei-Punkte-Symbol](images/actions.png) und wählen Sie **Sysdig-Erfassung** aus.

    Das Fenster *Sysdig-Erfassung* wird geöffnet.

5. Definieren Sie im Fenster *Sysdig-Erfassung* die folgenden Parameter:

    1. Geben Sie im Feld *Pfad und Name erfassen* den Namen der Erfassungsdatei ein. Sie können den Standardwert beibehalten oder ändern. Der Standardname enthält das Datum und die Zeitmarke, wann die Erfassung erstellt wird. 

    2. Legen Sie einen *Zeitrahmen* fest, um zum Sammeln von Daten die Anzahl der Sekunden anzugeben. Die Standardzeit für die Erfassung beträgt 15 Sekunden. Die maximale Erfassungszeit beträgt 86400 Sekunden (24 Stunden). 

    3. (Optional) Fügen Sie einen Filter hinzu, um die Menge der erfassten Trace-Informationen zu begrenzen. 

6. Klicken Sie auf **Erfassung starten**. Der Sysdig-Agent wird aufgefordert, eine Erfassung zu starten und die resultierende Tracedatei zurückzusenden. 

7. Klicken Sie auf **Zur Erfassungsseite gehen**, um die Liste der Erfassungen im Abschnitt *Erfassungen* der Webbenutzerschnittstelle anzuzeigen. 

Auf der Seite *Erfassungen* wird eine Tabelle angezeigt, in der der Name der Erfassungsdatei, der Host, von dem sie abgerufen wurde, der Zeitrahmen und die Größe der Erfassung aufgelistet werden. 

Der Status einer Erfassungsdatei kann einen der folgenden Werte haben:
* `Angefordert`: Es wird eine Datei generiert.
* `Hochgeladen`: Eine Datei steht zum Herunterladen und zur Analyse zur Verfügung.
* `Fehler`: Eine Datei ist aufgrund einer Zeitlimitüberschreitung, aufgrund von Daten, die nie empfangen wurden, oder aufgrund eines Agentenfehlers nicht verfügbar.



## Eine Erfassung löschen
{: #captures_delete}

Führen Sie die folgenden Schritte aus, um eine Erfassungsdatei zu löschen:

1. Navigieren Sie zum *ERFASSUNGEN*-Abschnitt in der Webbenutzerschnittstelle. [Erfahren Sie mehr darüber](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Geben Sie die Erfassungsdatei, die Sie löschen möchten, an oder wählen Sie sie aus.
3. Klicken Sie auf **Löschen**.



## Eine Erfassung erkunden
{: #captures_explore}

Führen Sie die folgenden Schritte aus, um eine Erfassungsdatei zu erkunden:

1. Navigieren Sie zum *ERFASSUNGEN*-Abschnitt in der Webbenutzerschnittstelle. [Erfahren Sie mehr darüber](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Geben Sie die Erfassungsdatei, die die Daten für den Host enthält, den Sie analysieren möchten, an oder wählen Sie sie aus.
3. Klicken Sie auf **ERKUNDEN**.



## Eine Erfassung herunterladen
{: #captures_download}

Führen Sie die folgenden Schritte aus, um eine Erfassungsdatei herunterzuladen:

1. Navigieren Sie zum *ERFASSUNGEN*-Abschnitt in der Webbenutzerschnittstelle. [Erfahren Sie mehr darüber](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Geben Sie die Erfassungsdatei, die die Daten enthält, den Sie herunterladen möchten, an oder wählen Sie sie aus.
3. Klicken Sie auf **DOWNLOAD**.


## Chisel
{: #captures_chisels}

Ein Sysdig-Chisel ist ein Skript, das in der Scripting-Sprache Lua geschrieben ist. Sie können es verwenden, um Daten in einer Erfassungsdatei zu analysieren. 

Weitere Informationen hierzu finden Sie im Dokument [Chisels User Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}.



## Csysdig
{: #captures_csysdig}

Csysdig ist ein Open-Source-Tool für Linux, das für die Überwachung und das Debugging entwickelt wurde. Sie können es verwenden, um Erfassungsdateien zu analysieren. 

Weitere Informationen finden Sie in den folgenden Ressourcen:
* [Csysdig-Blog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Csysdig-Video ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


