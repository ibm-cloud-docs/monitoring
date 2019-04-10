---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, dashboards

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


# Mit Dashboards arbeiten
{: #dashboards}

Verwenden Sie Dashboards, um Ihre Infrastruktur, Anwendungen und Services zu überwachen. Sie können vordefinierte Dashboards verwenden. Sie können auch benutzerdefinierte Dashboards über die Webbenutzerschnittstelle oder programmgesteuert erstellen. Sie können Dashboards mithilfe von Python-Scripts sichern und wiederherstellen.
{:shortdesc}

Ein **Dashboard** zeigt Gruppen von Metriken an, die einen Bericht über den Zustand, die Leistung und den Status Ihrer Infrastruktur, Anwendungen und Services für einen einzelnen Host oder für eine Gruppe von Hosts erstellen. Dashboards bieten einen spezialisierten Einblick in Netzdaten, Anwendungsdaten, Topologie, Services, Hosts und Container.

Im Abschnitt **DASHBOARDS** der Webbenutzerschnittstelle sind Dashboards in drei Hauptgruppen unterteilt:

* *Meine Dashboards*: Dies sind die Dashboards, die von dem Benutzer erstellt werden, der momentan angemeldet ist.
* *Meine gemeinsam genutzten Dashboards*: Dies sind die Dashboards, die von dem Benutzer erstellt werden, der momentan angemeldet ist, und die mit anderen Benutzern gemeinsam genutzt werden.
* *Mit mir gemeinsam genutzte Dashboards*: Dies sind die Dashboards, die von anderen Benutzern erstellt wurden und mit dem aktuellen Benutzer gemeinsam genutzt werden.

Im Abschnitt **ERKUNDEN** der Webbenutzerschnittstelle sind Dashboards in zwei Gruppen unterteilt:
* *Standarddashboards*: Dies sind vordefinierte Dashboards.
* *Meine Dashboards*: Dies sind die Dashboards, die von dem Benutzer erstellt werden, der momentan angemeldet ist.

Sie können Dashboards über die Webbenutzerschnittstelle kopieren und gemeinsam nutzen. 

Sie können Scripts ausführen, um eine der folgenden Aktionen programmgesteuert auszuführen:
* Speichern Sie vorhandene Dashboards in einer lokalen Datei.
* Erstellen Sie neue Dashboards, die mit den Dashboards identisch sind, die Sie speichern.
* Stellen Sie Dashboards wieder her.



## Vordefinierte Dashboards
{: #dashboards_predefined}

Vordefinierte Dashboards werden für verschiedene unterstützte Anwendungen, Netztopologien, Infrastrukturlayouts und Services entworfen. 

Vordefinierte Dashboards enthalten eine Reihe von Anzeigen, die bereits konfiguriert sind.

In der folgenden Tabelle sind die verschiedenen Typen vordefinierter Dashboards aufgelistet:

| Typ | Beschreibung | Weitere Informationen | 
|------|-------------|------------------|
| Anwendungen | Dashboards, die Sie verwenden können, um Ihre Anwendungen und Infrastrukturkomponenten zu überwachen.  | [Anwendungsdashboards](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_applications) |
| Host and Container | Dashboards, die Sie verwenden können, um die Ressourcennutzung und die Systemaktivität auf Ihren Hosts und in Ihren Containern zu überwachen. | [Host- und Container-Dashboards](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_host_container) |
| Netz | Dashboards, die Sie verwenden können, um Ihre Netzverbindungen und die Aktivität zu überwachen. | [Netz-Dashboards](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_network) |
| Service | Dashboards, die Sie verwenden können, um die Leistung Ihrer Services zu überwachen, selbst wenn diese Services in orchestrierten Containern bereitgestellt sind. | [Service-Dashboards](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_service) |
| Topologie | Dashboards, die Sie verwenden können, um die logischen Abhängigkeiten Ihrer Anwendungsschichten und Overlay-Metriken zu überwachen. | [Topologie-Dashboards](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_topology) |
{: caption="Tabelle 1. Liste vordefinierter Dashboards" caption-side="top"} 



## Angepasste Dashboards in der Webbenutzerschnittstelle erstellen
{: #dashboards_create}

Wenn Sie ein angepasstes Dashboard erstellen, können Sie mit einer Schablone beginnen, wie z. B. einem vordefinierten Dashboard, oder ein leeres Dashboard auswählen. Ein Dashboard enthält Anzeigen, die so konfiguriert sind, dass bestimmte Daten in einer Reihe unterschiedlicher Formate angezeigt werden. Außerdem legen Sie fest, wie Daten zusammengefasst werden. Der **Geltungsbereich** definiert, welche Daten für die Zusammenfassung verwendet und angezeigt werden. Sie können den Geltungsbereich auf Dashboardebene festlegen oder für einzelne Anzeigen überschreiben. 

Führen Sie die folgenden Schritte aus, um ein angepasstes Dashboard zu erstellen:

1. Navigieren Sie zum Abschnitt *DASHBOARD** in der Webbenutzerschnittstelle, und wählen Sie **Dashboard hinzufügen** aus. Die Seite *"Neues Dashboard erstellen" wird geöffnet.

    1. Wählen Sie ein vordefiniertes Dashboard aus oder wählen Sie *Leeres Dashboard* aus. 

    2. Geben Sie einen Namen für Ihr Dashboard ein.

    3. Klicken Sie auf **Dashboard erstellen**.

2. Legen Sie den Geltungsbereich des Dashboards fest. Klicken Sie auf **Geltungsbereich bearbeiten**, um den Standardgeltungsbereich zu ändern. Standardmäßig ist die Option **Überall** ausgewählt.
    
    1. Wählen Sie den Geltungsbereich aus. 

    2. Klicken Sie optional auf **Angepasste Anzeigengeltungsbereiche überschreiben**, um den Geltungsbereich für alle Anzeigen zu überschreiben, für die derzeit ein angepasster Geltungsbereich definiert ist. **Hinweis: Diese Aktion kann nicht rückgängig gemacht werden.** 

    **Hinweis:** Wählen Sie **Überall** aus, um den Dashboard-Geltungsbereich auf die gesamte Infrastruktur zurückzusetzen oder um den Geltungsbereich eines vorhandenen Dashboards auf die gesamte Infrastruktur zu aktualisieren.

    3. Klicken Sie auf **Speichern**.

3. Konfigurieren Sie Anzeigen. Wiederholen Sie diesen Schritt für alle Anzeigen in dem Dashboard, die Sie ändern möchten.

    1. Geben Sie die Anzeige an, die Sie ändern möchten.

    2. Wählen Sie **Anzeige bearbeiten** aus. Dies ist das Stiftsymbol.
    
    3. Ändern Sie den Diagrammtyp.

    4. Ändern Sie die Metrik und die Rate. Die Rate definiert den Typ der Zusammenfassung, die für die Daten ausgeführt wird.

    5. Ändern Sie den Geltungsbereich der Anzeige. Klicken Sie auf **Dashboard-Geltungsbereich überschreiben**. Ändern Sie dann den Geltungsbereich. Wenn Sie den Geltungsbereich des Dashboards in der Anzeige wiederherstellen müssen, wählen Sie **Dashboard-Geltungsbereich wiederherstellen** aus.

    6. Klicken Sie im Feld *Vergleichen mit* auf **Konfigurieren**. Legt den Zeitraum für den Vergleich fest.

    7. Legen Sie die Hintergrundfarbe für die Anzeige auf der Basis von Metrik-Schwellenwerten fest. Klicken Sie auf **Farbcode überschreiben** und dann auf **Aktivieren**. Legen Sie Werte für die verschiedenen Schwellenwerte fest.

    8. Klicken Sie auf **Speichern**.


## Geltungsbereich ändern
{: #dashboards_scope}

Anstatt den Geltungsbereich eines vordefinierten Dashboards zu ändern, kopieren Sie das Dashboard und ändern Sie den Geltungsbereich im kopierten Dashboard.
{: tip}

Führen Sie die folgenden Schritte aus, um den Geltungsbereich eines Dashboards zu ändern:

1. Navigieren Sie zum Abschnitt **DASHBOARD** in der Webbenutzerschnittstelle und wählen Sie ein Dashboard aus.

2. Klicken Sie auf **Geltungsbereich bearbeiten**, um den Standardgeltungsbereich zu ändern. 

    Standardmäßig ist die Option **Überall** ausgewählt.
    
3. Wählen Sie den Geltungsbereich aus. 

4. Klicken Sie optional auf **Angepasste Anzeigengeltungsbereiche überschreiben**, um den Geltungsbereich für alle Anzeigen zu überschreiben, für die derzeit ein angepasster Geltungsbereich definiert ist. 

    **Hinweis: Diese Aktion kann nicht rückgängig gemacht werden.** 

    Wählen Sie **Überall** aus, um den Dashboard-Geltungsbereich auf die gesamte Infrastruktur zurückzusetzen oder um den Geltungsbereich eines vorhandenen Dashboards auf die gesamte Infrastruktur zu aktualisieren.
    {: tip}

5. Klicken Sie auf **Speichern**.



## Ein Dashboard kopieren
{: #dashboards_copy}

Wenn Sie ein Dashboard kopieren, erstellen Sie ein Duplikat.

In der folgenden Tabelle werden die verschiedenen Aktionen und Benutzerberechtigungen beschrieben, die Benutzer zum Kopieren eines Dashboards benötigen:

| Aktion     |	Wer kann kopieren?     |	Dashboard-Instanz	   | Wer kann das Dashboard anzeigen?     | Wer kann das Dashboard bearbeiten?  |
|------------|-------------------|-------------------------|--------------------------------|-----------------------------|
| In aktuelles Team kopieren    |	Benutzer im Team mit Editorberechtigungen | Neue Dashboardinstanz  | Teammitglieder mit Anzeigeberechtigung	 | Benutzer im Team mit Editorberechtigungen |
| In anderes Team kopieren    | Benutzer im Team mit Editorberechtigungen in beiden Teams | Neue Dashboardinstanz  | Wenn das ursprüngliche Dashboard nicht gemeinsam genutzt wird, hat nur der Benutzer Zugriff, der das Dashboard kopiert hat. </br>Wenn das ursprüngliche Dashboard gemeinsam genutzt wird, haben alle Teammitglieder Zugriff. | Wenn das ursprüngliche Dashboard nicht gemeinsam genutzt wird, nur der Benutzer, der das Dashboard kopiert hat. </br>Wenn das ursprüngliche Dashboard gemeinsam genutzt wird, alle Teammitglieder mit Editorberechtigungen. |
{: caption="Tabelle 2. Informationen zu Benutzern und Dashboards in Bezug auf das Kopieren von Dashboards" caption-side="top"} 

Führen Sie die folgenden Schritte aus, um ein Dashboard in der Webbenutzerschnittstelle zu kopieren:

1. Navigieren Sie zum Abschnitt *DASHBOARDS* in der Webbenutzerschnittstelle.
2. Wählen Sie das Dashboard aus der linken Anzeige aus.
3. Klicken Sie auf **Einstellungen** (Drei-Punkte-Symbol) und wählen Sie **Dashboard kopieren** aus. 
4. Wählen Sie aus, wo das Dashboard kopiert werden soll.

    1. Wählen Sie **Aktuelles Team** aus, um das Dashboard in das aktuelle Team zu kopieren.
    
    2. Wählen Sie **Andere Teams** aus, um das Dashboard in andere Teams zu kopieren. Wählen Sie die Teams aus, in die Sie das Dashboard kopieren möchten.

    3. Geben Sie einen Namen für das Dashboard ein.

    4. Klicken Sie auf **Kopie senden**.
    
    5. Überprüfen Sie, ob der Geltungsbereich des Dashboards im neuen Team auf der Basis der Berechtigungen des Zielteams aktualisiert wird.

## Ein Dashboard löschen
{: #dashboards_delete}

Führen Sie die folgenden Schritte aus, um ein Dashboard in der Webbenutzerschnittstelle zu löschen:

1. Navigieren Sie zum Abschnitt *DASHBOARDS* in der Webbenutzerschnittstelle.
2. Wählen Sie das Dashboard aus der linken Anzeige aus.
3. Klicken Sie auf **Einstellungen** ![Drei-Punkte-Symbol](images/actions.png) und wählen Sie **Dashboard löschen** aus. 
4. Bestätigen Sie das Löschen, indem Sie auf **Ja, Dashboard löschen** klicken.


## Dashboard gemeinsam nutzen
{: #dashboards_share}

Sie können Dashboards zwischen Benutzern in einem Team und extern gemeinsam nutzen, indem Sie eine öffentliche URL für das Dashboard konfigurieren.  

In der folgenden Tabelle sind die verschiedenen Aktionen und Benutzerberechtigungen aufgeführt, die für Benutzer erforderlich sind, um ein gemeinsam genutztes Dashboard gemeinsam zu nutzen oder mit einem gemeinsam genutzten Dashboard zu arbeiten:

| Aktion      |	Wer kann gemeinsam nutzen?        |	Dashboard-Instanz	       | Wer kann das Dashboard anzeigen?        | Wer kann das Dashboard bearbeiten?  |
|-------------|-------------------|-----------------------------|------------------------------------|-----------------------------|
| Mit aktuellem Team gemeinsam nutzen |	Dashboard-Ersteller         |	Dieselbe Dashboardinstanz gemeinsam nutzen   | Teammitglieder mit Anzeigeberechtigung  | Teammitglieder mit Editorberechtigung   |
| Als URL öffentlich freigeben	  | Jeder Benutzer mit Bearbeitungszugriff im Team |	Dieselbe Dashboardinstanz gemeinsam nutzen   | Jeder     | Keiner                      |
{: caption="Tabelle 3. Informationen zu Benutzern und Dashboards in Bezug auf die gemeinsame Nutzung von Dashboards" caption-side="top"} 


Führen Sie die folgenden Schritte aus, um ein Dashboard in der Webbenutzerschnittstelle gemeinsam zu nutzen:

1. Navigieren Sie zum Abschnitt *DASHBOARDS* in der Webbenutzerschnittstelle.
2. Wählen Sie das Dashboard aus der linken Anzeige aus.
3. Klicken Sie auf **Einstellungen** ![Drei-Punkte-Symbol](images/actions.png) und wählen Sie **Gemeinsam nutzen** aus.
4. Wählen Sie aus, wie das Dashboard gemeinsam genutzt werden soll:

    * Aktivieren Sie den Schieberegler **Mit Team gemeinsam nutzen**, um das Dashboard mit dem aktuellen Team gemeinsam zu nutzen. Das Team, in dem das Dashboard gemeinsam genutzt wird, wird angezeigt.

    * Aktivieren Sie den Schieberegler **Öffentliche URL freigeben**, um die angepasste öffentliche URL anzuzeigen.

5. Klicken Sie auf **Schließen**.

Geben Sie ein Dashboard extern frei, um externen Benutzern die Anzeige der Dashboard-Metriken zu ermöglichen, während Sie den Zugriff auf die Änderung von Anzeigen und Konfigurationen einschränken.
{: tip}


## Dashboards programmgesteuert verwalten
{: #dashboards_programmatically}

Verwenden Sie die Sysdig-REST-API, um Routineaufgaben zu automatisieren und Benachrichtigungen zu überwachen. Sie können auch die Sysdig-Python-Bibliothek verwenden. 

**Hinweis:** Die Python-Bibliothek macht einen Teil der Funktionalität der Sysdig-REST-API zugänglich. 


Wenn Sie die API aus Ihren angepassten Scripts oder Programmen verwenden, müssen Sie ein Sysdig-Token verwenden, um sich bei der {{site.data.keyword.mon_full_notm}}-Instanz zu authentifizieren. Weitere Informationen finden Sie im Abschnitt [Mit API-Tokens arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token).


| Task                    | REST-API verwenden                |
|-------------------------|-------------------------------|
| Dashboard erstellen      | [Dashboard mithilfe der API erstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Dashboard löschen      | [Dashboard mithilfe der API löschen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Dashboards speichern       | [Dashboards eines Teams mithilfe der API speichern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabelle 4. Tasks zum programmgesteuerten Verwalten von Dashboards" caption-side="top"} 


