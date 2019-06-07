---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, panels

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


# Anzeigen verwalten
{: #panels}

Verwenden Sie eine Anzeige, um eine Metrik oder eine Gruppe von Metriken in einem Dashboard anzuzeigen. Sie können Anzeigen kopieren, ihren Geltungsbereich ändern, die Anzeigen duplizieren, löschen, exportieren und erkunden.
{:shortdesc}

Sie können einen der folgenden Anzeigentypen verwenden:

| Typ | Beschreibung |
|------|-------------|
| `Linie` | Verwenden Sie diese Anzeige, um Trends für eine oder mehrere Metriken im Laufe der Zeit anzuzeigen.  |
| `Bereich` | Verwenden Sie diese Anzeige, um Trends für eine oder mehrere Metriken im Laufe der Zeit anzuzeigen.  |
| `Top-Liste` | Verwenden Sie diese Anzeige, um eine Metrik über mehrere Gruppen von Entitäten hinweg zu vergleichen. Das Balkendiagramm ist in absteigender Reihenfolge sortiert.  |
| `Histogramm` | Verwenden Sie diese Anzeige, um die Häufigkeitsverteilung einer Metrik in Buckets anzuzeigen.  |
| `Topologie` | Verwenden Sie diese Anzeige, um die Infrastruktur als Topologiemap sowie die Beziehungen zwischen Entitäten in der Map darzustellen.  |
| `Zahl` | Verwenden Sie diese Anzeige, um eine einzelne Zahl anzuzeigen, die den Wert einer Aggregationsmetrik für eine oder mehrere Entitäten im Laufe der Zeit darstellt.  |
| `Tabelle` | Verwenden Sie diese Anzeige, um numerische Daten für Ihre Infrastruktur basierend auf Metriken und Segmenten anzuzeigen.  |
| `Text` | Verwenden Sie diese Anzeige, um Text hinzuzufügen. Verwenden Sie Markdown, um Ihren Text hinzuzufügen.  |
{: caption="Tabelle 1. Anzeigentypen" caption-side="top"} 



## Anzeige in ein Dashboard kopieren
{: #panels_copy}

Führen Sie die folgenden Schritte aus, um eine Anzeige zu kopieren:

1. Navigieren Sie zum Abschnitt *DASHBOARD** in der Webbenutzerschnittstelle. Wählen Sie ein Dashboard aus. Geben Sie dann die Anzeige an, in der die Metrik angezeigt wird, den Sie kopieren möchten.

2. Wählen Sie das Symbol *Weitere Optionen* ![DRei-Punkte-Symbol](images/actions.png) aus und wählen Sie **Anzeige kopieren** ![Kopieren-Symbol](images/actions.png) aus.

3. Wählen Sie eines der aufgelisteten Dashboards aus oder geben Sie einen Namen für ein neues Dashboard ein. 

4. Klicken Sie auf **Kopieren und öffnen**.



## Geltungsbereich einer Anzeige ändern
{: #panels_scope}

Führen Sie die folgenden Schritte aus, um den Geltungsbereich einer Anzeige zu ändern:

1. Navigieren Sie zum Abschnitt *DASHBOARD** in der Webbenutzerschnittstelle. Wählen Sie ein Dashboard aus. Geben Sie anschließend die Anzeige an, in der die Metrik angezeigt wird, für die Sie den Geltungsbereich ändern möchten.

2. Klicken Sie in der Anzeige auf **Geltungsbereich bearbeiten**, um den Standardgeltungsbereich zu ändern. 

    Standardmäßig ist die Option **Überall** ausgewählt.
    
3. Wählen Sie den Geltungsbereich aus. 

4. Klicken Sie optional auf **Angepasste Anzeigengeltungsbereiche überschreiben**, um den Geltungsbereich für alle Anzeigen zu überschreiben, für die ein angepasster Geltungsbereich definiert ist.  

    **Hinweis: Diese Aktion kann nicht rückgängig gemacht werden.** 

    Wählen Sie **Überall** aus, um den Dashboard-Geltungsbereich auf die gesamte Infrastruktur zurückzusetzen oder um den Geltungsbereich eines vorhandenen Dashboards auf die gesamte Infrastruktur zu aktualisieren.
    {: tip}

5. Klicken Sie auf **Speichern**.



## Eine Anzeige duplizieren
{: #panels_duplicate}

Führen Sie die folgenden Schritte aus, um eine Anzeige im aktuellen Dashboard zu duplizieren:

1. Navigieren Sie zum Abschnitt *DASHBOARD** in der Webbenutzerschnittstelle. Wählen Sie ein Dashboard aus. Geben Sie dann die Anzeige an, in der die Metrik angezeigt wird, den Sie kopieren möchten.

2. Wählen Sie das Symbol *Weitere Optionen* ![Drei-Punkte-Symbol](images/actions.png) und wählen Sie **Anzeige duplizieren** ![Kopieren-Symbol](images/duplicate.png) aus.


## Eine Anzeige löschen
{: #panels_delete}

Führen Sie die folgenden Schritte aus, um eine Anzeige aus dem aktuellen Dashboard zu löschen:

1. Navigieren Sie zum Abschnitt *DASHBOARD** in der Webbenutzerschnittstelle. Wählen Sie ein Dashboard aus. Geben Sie dann die Anzeige an, in der die Metrik angezeigt wird, den Sie kopieren möchten.

2. Wählen Sie das Symbol *Weitere Optionen* ![Drei-Punkte-Symbol](images/actions.png) aus und wählen Sie **Eine Anzeige löschen** ![Kopieren-Symbol](images/delete.png) aus.

3. Klicken Sie auf **Ja, Anzeige löschen**, um das Löschen der Anzeige zu bestätigen.



## Daten aus einer Anzeige exportieren
{: #panels_export}

Beachten Sie beim Exportieren von Daten die folgenden Informationen:

* Sie können Daten aus einem Kurvendiagramm in eine **JSON-Datei** exportieren.
* Sie können Daten aus einem Tabellendiagramm oder aus einem Kurvendiagramm in eine **CSV-Datei** exportieren.

Führen Sie die folgenden Schritte aus, um Daten aus einer Anzeige zu exportieren:

1. Navigieren Sie zum Abschnitt *DASHBOARD** in der Webbenutzerschnittstelle. Wählen Sie ein Dashboard aus. Geben Sie dann die Anzeige an, in der die Metrik angezeigt wird, den Sie kopieren möchten.

2. Wählen Sie das Symbol *Weitere Optionen* ![Drei-Punkte-Symbol](images/actions.png) aus.

3. Wählen Sie eine der folgenden Optionen aus:

    * Wählen Sie **JSON exportieren** aus, um Daten in eine JSON-formatierte Datei zu exportieren.

    * Wählen Sie **CSV exportieren** aus, um Daten in eine CSV-formatierte Datei zu exportieren.

4. Klicken Sie auf **Datei speichern**.




## Einen Alert erstellen
{: #panels_alert}

Sie können Alerts direkt über eine Anzeige erstellen.

Führen Sie die folgenden Schritte aus, um einen Alert zu erstellen:

1. Navigieren Sie zum Abschnitt *DASHBOARD** in der Webbenutzerschnittstelle. Wählen Sie ein Dashboard aus. Geben Sie dann die Anzeige an, in der die Metrik angezeigt wird, den Sie kopieren möchten.

2. Wählen Sie das Symbol *Weitere Optionen* ![Drei-Punkte-Symbol](images/actions.png) aus.

3. Wählen Sie **Alert erstellen** aus.

4. Konfigurieren Sie den Alert.

5. Klicken Sie auf **Erstellen**.


