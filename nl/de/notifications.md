---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# Mit Benachrichtigungskanälen arbeiten
{: #notifications}

Konfigurieren Sie Benachrichtigungskanäle, um benachrichtigt zu werden, wenn ein Alert ausgelöst wird. Sie können Benachrichtigungskanäle über die Anzeige *Einstellungen* in der Webbenutzerschnittstelle verwalten.
{:shortdesc}
 

## Einen Benachrichtigungskanal konfigurieren
{: #notifications_create}

Führen Sie die folgenden Schritte aus, um einen Benachrichtigungskanal hinzuzufügen:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Einstellungen** aus.

3. Wählen Sie **Benachrichtigungskanäle** aus.

4. Klicken Sie auf **MEINE KANÄLE** ![Hinzufügen-Symbol](../images/add.png). Wählen Sie dann einen Kanal aus.

    **Hinweis:** Wenn Sie zum ersten Mal einen Benachrichtigungskanal konfigurieren, klicken Sie auf einen der Kanäle.

5. Konfigurieren Sie einen Benachrichtigungskanal:

    * Geben Sie den Namen des Kanals ein.

    * Aktivieren Sie das Feld *Benachrichtigung, wenn OK*, um eine Benachrichtigung zu erhalten, wenn die Alertbedingung nicht mehr ausgelöst wird.

    * Aktivieren Sie die Bedingung *Benachrichtigen, wenn gelöst*, um eine Benachrichtigung zu erhalten, wenn der Alert manuell durch einen Benutzer aufgelöst wurde.

    * Fügen Sie für einen **E-Mail**-Benachrichtigungskanal die Liste der Empfänger als durch Kommas getrennte Liste hinzu.

    * Fügen Sie für einen **slack**-Benachrichtigungskanal den Namen des *Slack-Kanals* hinzu.

    * Fügen Sie für einen **Webhook**-Benachrichtigungskanal die *Webhook-URL* hinzu. **Hinweis:** Wenn ein Alert ausgelöst wird, wird die Benachrichtigung als POST im JSON-Format an Ihren Webhook-Endpunkt gesendet. Weitere Informationen hierzu finden Sie im Abschnitt [Webhook-Kanal konfigurieren![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}. Sysdig kann zum Beispiel mit einem angepassten Webhook in ServiceNow integriert werden. Weitere Informationen zum Konfigurieren von Sysdig mit ServiceNow finden Sie im Abschnitt [ServiceNow konfigurieren ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}.

    * Fügen Sie für den Benachrichtigungskanal **VictorOps** den *API-Schlüssel* und den *Routing-Schlüssel* hinzu.

    * Fügen Sie für den Benachrichtigungskanal **OpsGenie** den *OpsGenie-API-Schlüssel* hinzu. Beachten Sie, dass Sie in OpsGenie die Integration mit Sysdig konfigurieren müssen. Weitere Informationen finden Sie unter [Sysdig-Cloud-Integration in OpsGenie hinzufügen ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}.

    * Für den Benachrichtigungskanal **PagerDuty** müssen Sie zuerst Sysdig für die Integration in Ihr Konto autorisieren. Wenn Sie PagerDuty auswählen, wird ein Assistent zum Konfigurieren der Integration mit Sysdig geöffnet. Klicken Sie auf **Integration autorisieren** oder **Unter Verwendung des Identitätsproviders anmelden**, um PagerDuty zu autorisieren. Wählen Sie einen vorhandenen Service aus oder konfigurieren Sie einen neuen Service für Sysdig-Benachrichtigungen. Klicken Sie dann auf **Integration fertigstellen**. Wählen Sie die Eskalationsrichtlinie aus, die für Sysdig-Vorfälle verwendet werden soll. Bestätigen Sie dann auf der Registerkarte *Benachrichtigungen* Ihr PagerDuty-Konto, Ihren Servicenamen und den Serviceschlüssel. 

    * Aktivieren Sie optional bzw. für Integrationen, die Tests zulassen, die Bedingung *Testbenachrichtigung*, um eine Testbenachrichtigung zu erhalten. Wenn Sie innerhalb von 10 Minuten keine Testbenachrichtigung erhalten, überprüfen Sie Ihre Kanalkonfiguration. 

6. Klicken Sie auf **KANAL ERSTELLEN**. 



## Einen Benachrichtigungskanal ändern
{: #notifications_update}

Führen Sie die folgenden Schritte aus, um einen Benachrichtigungskanal zu ändern:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Einstellungen** aus.

3. Wählen Sie **Benachrichtigungskanäle** aus.

4. Geben Sie den Zielkanal an, den Sie ändern möchten, und klicken Sie auf **BEARBEITEN**.

5. Nachdem Sie Änderungen vorgenommen haben, klicken Sie auf **ÄNDERUNGEN SPEICHERN**.



## Einen Benachrichtigungskanal testen
{: #notifications_test}

Führen Sie die folgenden Schritte aus, um einen Benachrichtigungskanal zu testen:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Einstellungen** aus.

3. Wählen Sie **Benachrichtigungskanäle** aus.

4. Geben Sie den Zielkanal an, den Sie ändern möchten, und klicken Sie auf **TESTEN**.



## Einen Benachrichtigungskanal inaktivieren
{: #notifications_disable}

Führen Sie die folgenden Schritte aus, um einen Benachrichtigungskanal vorübergehend zu inaktivieren:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Einstellungen** aus.

3. Wählen Sie **Benachrichtigungskanäle** aus.

4. Aktivieren Sie im Abschnitt *Benachrichtigungen* die Option *Ausfallzeit*, um Alerts vorübergehend zu inaktivieren und alle Benachrichtigungen stumm zu schalten.

## Einen Benachrichtigungskanal löschen
{: #notifications_delete}

Führen Sie die folgenden Schritte aus, um einen Benachrichtigungskanal zu löschen:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Einstellungen** aus.

3. Wählen Sie **Benachrichtigungskanäle** aus.

4. Geben Sie den Zielkanal an, den Sie ändern möchten, und klicken Sie auf **BEARBEITEN**.

5. Klicken Sie auf **KANAL LÖSCHEN**.

6. Bestätigen Sie das Löschen des Kanals. Klicken Sie auf **ÄNDERUNGEN SPEICHERN**.




