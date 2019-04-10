---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, teams

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

# Mit Teams arbeiten
{: #teams}

Ein Administrator oder ein Manager einer {{site.data.keyword.mon_full_notm}}-Instanz kann Mitglieder erstellen, löschen, hinzufügen und den Geltungsbereich von Teams in dieser Instanz ändern. 
{:shortdesc} 

Ein Administrator oder Manager einer {{site.data.keyword.mon_full_notm}}-Instanz muss in das Team *Operationen überwachen* wechseln, bevor er Teams erstellen und vorhandene Teams verwalten kann.
{: tip}

## Ein Team erstellen
{: #teams_create}

Führen Sie die folgenden Schritte aus, um ein Team zu erstellen:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Operationen überwachen** aus. Wählen Sie dann **Einstellungen** aus.

3. Wählen Sie **Teams** aus. Die Liste der vorhandenen Teams wird angezeigt.

4. Klicken Sie auf **Team hinzufügen**. Die Teamkonfigurationsseite wird angezeigt.

5. Konfigurieren Sie die Teamdetails. 

    * Wählen Sie eine Farbe aus.

    * Geben Sie den Namen des Teams ein.

    * [Optional] Geben Sie eine Beschreibung für dieses Team ein.

    * [Optional] Legen Sie den Parameter **Standardteam** fest, wenn dieses Team das Standardteam für neue Benutzer werden soll.

    * Legen Sie den **Standardeingangspunkt** fest, um die Ansicht in der Webbenutzerschnittstelle anzugeben, die sich bei jeder Anmeldung eines Benutzers öffnet. Gültige Eingangspunkte sind: Ansicht *Erkunden*, Ansicht *Dashboards*, Ansicht *Ereignisse*, Ansicht *Alerts* und Ansicht *Einstellungen*. Standardmäßig ist die Ansicht *Erkunden* festgelegt.

6. Konfigurieren Sie den Geltungsbereich für das Team. 

    * [Optional] Legen Sie **Geltungsbereich nach** fest, um die Datenebene anzugeben, auf die Mitglieder des Teams Zugriff haben. Gültige Werte sind *host* und *container*. Wenn der Parameter auf *Host* festgelegt ist, können die Mitglied alle Informationen auf Hostebene und auf Containerebene anzeigen. Wenn der Parameter auf *Container* festgelegt ist, können die Mitglied nur Informationen auf Containerebene anzeigen.

    * Legen Sie den **Geltungsbereich** fest, um einzuschränken, welche Daten Benutzern angezeigt werden. Sie können eine oder mehrere Bedingungen festlegen, indem Sie Ausdrücke für Metriken angeben. Der Geltungsbereich ist standardmäßig auf *Überall* festgelegt.
	
    * [Optional] Aktivieren oder inaktivieren Sie **Sysdig-Erfassungen**. Aktivieren Sie dieses Kontrollkästchen, damit dieses Team Sysdig-Erfassungen aufzeichnen darf. Erfassungsdateien sind nur für Mitglieder dieses Teams sichtbar. **Hinweis:** Erfassungen enthalten detaillierte Informationen aus jedem Container auf einem Host, unabhängig vom Geltungsbereich des Teams.

    * [Optional] Aktivieren oder inaktivieren Sie **Infrastrukturereignisse**. Aktivieren Sie dieses Kontrollkästchen, um alle angepassten Infrastrukturereignisse von jedem Benutzer und Sysdig-Agenten anzuzeigen. Wenn diese Option nicht aktiviert ist, können die Benutzer die Infrastrukturereignisse sehen, die speziell an dieses Team gesendet werden. 

6. Fügen Sie dem Team Mitglieder hinzu. Klicken Sie auf **Benutzer zuordnen**. Suchen Sie einen Benutzer und fügen Sie ihn hinzu.



## Geltungsbereich eines Teams ändern
{: #teams_scope}

Führen Sie die folgenden Schritte aus, um den Geltungsbereich der Daten zu ändern, die für die Mitglieder eines Teams sichtbar sind: 

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Operationen überwachen** aus. Wählen Sie dann **Einstellungen** aus.

3. Wählen Sie **Teams** aus. Die Liste der vorhandenen Teams wird angezeigt.

4. Suchen Sie das Team und wählen Sie es aus. Die Details des Teams werden angezeigt.

5. Ändern Sie die Konfigurationsdetails im Abschnitt *Sichtbarkeit*.

6. Klicken Sie auf **Speichern**. 


## Einem Team Benutzer hinzufügen
{: #teams_users}

Führen Sie die folgenden Schritte aus, um Mitglieder zu einem Team hinzuzufügen: 

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Operationen überwachen** aus. Wählen Sie dann **Einstellungen** aus.

3. Wählen Sie **Teams** aus. Die Liste der vorhandenen Teams wird angezeigt.

4. Suchen Sie das Team und wählen Sie es aus. Die Details des Teams werden angezeigt.

5. Klicken Sie im Abschnitt *Team-Benutzer* auf **Benutzer zuordnen**.

6. Klicken Sie auf **Speichern**. 


## Ein Team löschen
{: #teams_delete}

Das Standardteam (**Operationen überwachen**) kann nicht gelöscht werden. 

Führen Sie die folgenden Schritte aus, um ein Team zu löschen:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Operationen überwachen** aus. Wählen Sie dann **Einstellungen** aus.

3. Wählen Sie **Teams** aus. Die Liste der vorhandenen Teams wird angezeigt.

4. Suchen Sie das Team, das Sie löschen möchten, und wählen Sie es aus. Die Details des Teams werden angezeigt.

5. Klicken Sie auf **Team löschen**.

**Hinweis:** Wenn Sie ein Team löschen, werden Benutzer, die nur zu diesem Team gehören, in das Standardteam verschoben.



