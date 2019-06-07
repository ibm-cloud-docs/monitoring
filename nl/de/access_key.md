---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# Zugriffsschlüssel verwalten
{: #access_key}

Der **Zugriffsschlüssel** ist ein Token, das Sie zum Konfigurieren von Sysdig-Agenten verwenden müssen, um Daten erfolgreich an Ihre {{site.data.keyword.mon_full_notm}}-Instanz in {{site.data.keyword.cloud_notm}} weiterzuleiten.   
{:shortdesc}


## Zugriffsschlüssel über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abrufen
{: #access_key_ibm_cloud_ui}

Führen Sie die folgenden Schritte aus, um den Zugriffsschlüssel für eine {{site.data.keyword.mon_full_notm}}-Instanz über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abzurufen:

1. Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an.

    Klicken Sie auf das [{{site.data.keyword.cloud_notm}}-Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}, um das {{site.data.keyword.cloud_notm}}-Dashboard zu starten.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle geöffnet.

2. Wählen Sie im Navigationsmenü die Option **Beobachtbarkeit** aus. 

3. Wählen Sie **Überwachung** aus. Das {{site.data.keyword.mon_full_notm}}-Dashboard wird geöffnet. Die Liste der Überwachungsinstanzen, die unter {{site.data.keyword.cloud_notm}} verfügbar sind, wird angezeigt.

3. Geben Sie die Instanz an, für die Sie den Zugriffsschlüssel abrufen möchten, und klicken Sie auf **Zugriffsschlüssel anzeigen**.

4. Es wird ein Popup-Fenster geöffnet, in dem Sie auf **Anzeigen** klicken können, um den Zugriffsschlüssel anzuzeigen.



## Zugriffsschlüssel über die Befehlszeilenschnittstelle (CLI) abrufen
{: #access_key_cli}

Führen Sie die folgenden Schritte aus, um den Zugriffsschlüssel für eine Sysdig-Instanz über die Befehlszeile abzurufen:

1. [Voraussetzung] Installieren Sie die {{site.data.keyword.cloud_notm}}-CLI.

   Weitere Informationen finden Sie unter [Die {{site.data.keyword.cloud_notm}}-CLI installieren](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

   Wenn die Befehlszeilenschnittstelle (CLI) installiert ist, fahren Sie mit dem nächsten Schritt fort.

2. Melden Sie sich an der Region in {{site.data.keyword.cloud_notm}} an, in der die Sysdig-Instanz ausgeführt wird. Führen Sie den folgenden Befehl aus: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Legen Sie die Ressourcengruppe fest, in der die Sysdig-Instanz ausgeführt wird. Führen Sie den folgenden Befehl aus: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Standardmäßig ist die Ressourcengruppe `Standard` festgelegt.

4. Rufen Sie den Instanznamen ab. Führen Sie den folgenden Befehl aus: [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Rufen Sie den Namen des API-Schlüssels ab, der der Sysdig-Instanz zugeordnet ist. Führen Sie den Befehl [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) aus:

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    Dabei ist INSTANCE_NAME der Name der Instanz, die Sie im vorherigen Schritt abgerufen haben.

6. Rufen Sie den Zugriffsschlüssel ab. Führen Sie den Befehl [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) aus:

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    Dabei ist APIKEY_NAME der Name des API-Schlüssels.
 
    Die Ausgabe dieses Befehls enthält das Feld **Sysdig-Zugriffsschlüssel**, das den Zugriffsschlüssel für die Instanz enthält.


Der folgende Befehl zeigt z. B. die Ausgabe einer Beispiel-Service-ID an:

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Abrufen von Serviceschlüssel {{site.data.keyword.mon_full_notm}}-shg-key-admin in Ressourcengruppe "Standard" unter Konto Beispielkonto als sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf
Erstellt um:   Fri Nov  2 13:40:39 UTC 2018
Status:         active
Berechtigungsnachweise:
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777
               Sysdig-Zugriffsschlüssel:    xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
               Sysdig-Kunden-ID:            111
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf
               Sysdig-Collector-Endpunkt:   ingest.us-south.monitoring.test.cloud.ibm.com
               Sysdig-Endpunkt:             https://us-south.monitoring.test.cloud.ibm.com
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameter:
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## Zugriffsschlüssel zurücksetzen 
{: #access_key_reset}

Wenn der Zugriffsschlüssel kompromittiert wurde oder Sie über eine Richtlinie verfügen, den Zugriffsschlüssel nach einigen Tagen zu erneuern, können Sie einen neuen Schlüssel generieren und den alten löschen.

Führen Sie die folgenden Schritte aus, um den Zugriffsschlüssel für eine {{site.data.keyword.mon_full_notm}}-Instanz zu verlängern:

1. Starten Sie die {{site.data.keyword.mon_full_notm}}-Webbenutzerschnittstelle. Weitere Informationen finden Sie unter [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. Wählen Sie in der Navigationsleiste mithilfe der *Auswahltaste* die Option **Einstellungen** aus.

2. Klicken Sie im Abschnitt *Kennwortmanagement* auf **Kennwort zurücksetzen**.

**Hinweis:** Nachdem Sie den Sysdig-Zugriffsschlüssel zurückgesetzt haben, müssen Sie den Zugriffsschlüssel für alle Protokollquellen aktualisieren, die Metriken an diese {{site.data.keyword.mon_full_notm}}-Instanz weiterleiten.
