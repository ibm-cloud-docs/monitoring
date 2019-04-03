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


# Erstellen eines Grafana-Dashboards
{:#create_grafana_dashboard}

Erstellen Sie ein angepasstes Grafana-Dashboard, um Metriken für alle Container anzuzeigen, die in einem Bereich Ihrer {{site.data.keyword.Bluemix}}-Organisation ausgeführt werden.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um ein Grafana-Dashboard zu erstellen:

1. Starten Sie Grafana über einen Web-Browser. Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).

2. Speichern Sie das Standarddashboard.

    1. Klicken Sie in der Symbolleiste auf das Symbol 'Speichern'.
    2. Geben Sie einen Namen für das Dashboard ein.
    3. Klicken Sie neben dem Feld 'Name' auf das Symbol 'Speichern'.
   
3. Inaktivieren Sie die automatische Seitenaktualisierung, während Sie an Ihrem Dashboard arbeiten. 

    1. Klicken Sie auf das Zeitauswahlfeld im Header.
    2. Wählen Sie **Automatisches Aktualisieren** aus.
    3. Klicken Sie auf **Aus**.
 
 5. Löschen Sie die Beispielzeilen.
 
     1. Bewegen Sie den Cursor neben dem Header *Willkommen bei Grafana* auf den Menüschieberegler 'Zeile' und klicken Sie dann auf das Menüsymbol 'Zeile', das hinausgeschoben wird.
     2. Klicken Sie auf **Zeile löschen** und danach auf **Ja**.
     
     Wiederholen Sie diese Schritte, um die Dokumentationslinks und die Zeilen 'Erste Grafik' zu entfernen. 
     
     Passen Sie in der Seitenüberschrift das Zeitauswahlfeld an, um sicherzustellen, dass Sie Daten anzeigen können. Der Standardwert liegt zwischen vor 6 Stunden und vor einigen Sekunden. Wählen Sie **Letzte 30 Tage** aus.
     
6. Fügen Sie eine Visualisierung hinzu.

    * Informationen zum Hinzufügen einer Visualisierung des CPU-Leerlaufs finden Sie unter [Visualisierung des CPU-Leerlaufs hinzufügen](/docs/services/cloud-monitoring/grafana/create_grafana_dashboard.html#grafana_add_cpu).
    * Informationen zum Hinzufügen einer Visualisierung der Speicherbelegung finden Sie unter [Visualisierung der Speicherbelegung hinzufügen](/docs/services/cloud-monitoring/grafana/create_grafana_dashboard.html#grafana_add_mem).
        
7. Speichern Sie das angepasste Dashboard.

    1. Klicken Sie in der Symbolleiste auf das Symbol 'Speichern'.
    2. Geben Sie einen Namen für das Dashboard ein.
    3. Klicken Sie neben dem Feld 'Name' auf das Symbol 'Speichern'.
    

## Visualisierung des CPU-Leerlaufs hinzufügen
{:#grafana_add_cpu}

Führen Sie die folgenden Schritte aus, um eine Grafik für den CPU-Leerlauf von allen Containern in Ihrem Bereich hinzuzufügen:

1. Klicken Sie auf die Schaltfläche **Eine Zeile hinzufügen**. An der Seite der Zeile wird der Menüschieberegler 'Zeile' angezeigt.
    
2. Bewegen Sie den Cursor auf den Menüschieberegler für die Zeile und klicken Sie dann auf das Menüsymbol 'Zeile', das hinausgeschoben wird.

3. Klicken Sie auf **Anzeige hinzufügen**. Klicken Sie anschließend auf **Grafik**.

4. Klicken Sie auf den Titel der Grafik, um das Anzeigemenü zu öffnen, und klicken Sie dann auf **Bearbeiten**. 

    Der Rest des Dashboards ist ausgeblendet. Nur der Editor für diese Grafik und eine Vorschau der Grafik werden angezeigt.
    
5. Auf der Registerkarte 'Metriken' erstellen Sie eine Abfrage, um Daten für die Grafik zu erfassen. 

    Wenn Sie beispielsweise mit Containern arbeiten, die in einer {{site.data.keyword.Bluemix_notm}}-verwalteten Cloudinfrastruktur bereitgestellt sind, enthält das Abfrageformat die Bereichs-ID, eine Containergruppen-ID und eine einzelne Containerinstanz-ID in folgendem Format: `space_ID.group_ID.instance_ID.metric`
        
    1. Klicken Sie in der Zeile A auf **Metrik auswählen**. Wählen Sie dann Ihre Bereichs-ID aus.
    2. Klicken Sie auf **Metrik auswählen** und wählen Sie den Stern (\*) aus.
    
    Wenn Sie (\*) auswählen, enthalten die Daten Metriken von jeder Containergruppe im Bereich. Optional können Sie dieses Format mit einem regulären Ausdruck verändern, um nur Metriken von bestimmen Containern einzuschließen. Wenn Sie nur die Metriken einzelner Container anzeigen und Containergruppen ausschließen möchten, klicken Sie auf **Metrik auswählen** und wählen **0000** aus.
        
    3. Klicken Sie auf **Metrik auswählen** und wählen Sie erneut den Stern (\*) aus. Dieses Format enthält Metriken aus allen einzelnen Containern in dem Bereich.
        
    4. Klicken Sie auf **Metrik auswählen** und auf **cpu-0**.
        
    5. Klicken Sie auf **Metrik auswählen** und auf **cpu-idle**. Die Grafikvorschau wird aktualisiert und zeigt die Metriken an, die mit dieser Abfrage übereinstimmen.
    
6. Optional: Passen Sie die Anzeige der Grafik an.
    
    * Um der Grafik einen Namen zu geben, klicken Sie auf die Registerkarte 'Allgemein' und geben im Feld 'Titel' einen Namen für die Grafik ein. Zum Beispiel: CPU-Leerlauf
    * Um der vertikalen Achse einen Namen zu geben, klicken Sie auf die Registerkarte für Achsen und Raster und geben im Abschnitt für die linke Y-Achse im Feld 'Bezeichnung' die Bezeichnung 'CPU' ein.
    * Um die Hintergrundfarbe der Grafik zu ändern, klicken Sie im Abschnitt für Rasterschwellenwerte für Ebene 2 auf das Auswahlsymbol für die Hintergrundfarbe und ändern die Hintergrundfarbe von weiß in hellgrau.
    
    Klicken Sie im Header auf **Zurück zum Dashboard**.
    
7. Um die Änderungen, die Sie an diesem Dashboard vorgenommen haben, im Header zu speichern, klicken Sie auf das Symbol 'Speichern' und anschließend auf das Symbol 'Speichern' im Menü.


## Visualisierung der Speicherbelegung hinzufügen
{:#grafana_add_mem}

Führen Sie die folgenden Schritte aus, um eine Visualisierung der Speicherbelegung hinzuzufügen:

1. Klicken Sie auf die Schaltfläche zum Hinzufügen einer Zeile. Der Menüschieberegler 'Zeile' wird an der Seite der Zeile angezeigt.
   
2. Bewegen Sie den Cursor auf den Menüschieberegler für die Zeile und klicken Sie dann auf das Menüsymbol 'Zeile', das hinausgeschoben wird.

    1. Klicken Sie auf 'Anzeige hinzufügen' > Grafik.
    2. Klicken Sie auf 'Bearbeiten'. Der Rest des Dashboards ist ausgeblendet. Nur der Editor für diese Grafik und eine Vorschau der Grafik werden angezeigt.
    
3. Auf der Registerkarte 'Metriken' erstellen Sie eine Abfrage, um Daten für die Grafik zu erfassen. 

    Wenn Sie beispielsweise mit Containern arbeiten, die in einer {{site.data.keyword.Bluemix_notm}}-verwalteten Cloudinfrastruktur bereitgestellt sind, enthält das Abfrageformat die Bereichs-ID, eine Containergruppen-ID und eine einzelne Containerinstanz-ID in folgendem Format:
        
    1. Klicken Sie in der Zeile A auf **Metrik auswählen**. Wählen Sie dann Ihre Bereichs-ID aus.
    2. Klicken Sie auf **Metrik auswählen** und wählen Sie den Stern (\*) aus.
    
    Wenn Sie (\*) auswählen, enthalten die Daten Metriken von jeder Containergruppe im Bereich. Optional können Sie dieses Format mit einem regulären Ausdruck verändern, um nur Metriken von bestimmen Containern einzuschließen. Wenn Sie nur die Metriken einzelner Container anzeigen und Containergruppen ausschließen möchten, klicken Sie auf **Metrik auswählen** und wählen **0000** aus.
    
    3. Klicken Sie auf **Metrik auswählen** und wählen Sie erneut den Stern (\*) aus. Dieses Format enthält Metriken aus allen einzelnen Containern in dem Bereich.
        
    4. Klicken Sie auf **Metrik auswählen** und auf **memory**.
        
    5. Klicken Sie auf **Metrik auswählen** und auf **memory-used**. Die Grafikvorschau wird aktualisiert und zeigt die Metriken an, die mit dieser Abfrage übereinstimmen.
    
6. Optional: Passen Sie die Anzeige der Grafik an.
    
    * Um der Grafik einen Namen zu geben, klicken Sie auf die Registerkarte 'Allgemein' und geben im Feld 'Titel' einen Namen für die Grafik ein. Zum Beispiel: Speicherbelegung
    *  Um das Format der vertikalen Achsenwerte zu ändern, klicken Sie auf die Registerkarte für Achsen und Raster und wählen im Abschnitt für die linke Y-Achse im Feld für das Format 'Bytes' aus.
    * Um der vertikalen Achse eine Bezeichnung zu geben, geben Sie im Feld 'Bezeichnung' die Bezeichnung 'Speicher' ein.
    * Um die Hintergrundfarbe der Grafik zu ändern, klicken Sie im Abschnitt für Rasterschwellenwerte für Ebene 2 auf das Auswahlsymbol für die Hintergrundfarbe und ändern die Hintergrundfarbe von weiß in hellgrau.
    
    Klicken Sie im Header auf **Zurück zum Dashboard**.

7. Um die Änderungen, die Sie an diesem Dashboard vorgenommen haben, im Header zu speichern, klicken Sie auf das Symbol 'Speichern' und anschließend auf das Symbol 'Speichern' im Menü.

