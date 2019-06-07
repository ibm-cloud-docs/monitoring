---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# Eine Instanz bereitstellen
{: #provision}

Bevor Sie Metriken mit Sysdig überwachen und verwalten können, müssen Sie eine Instanz des Service in {{site.data.keyword.cloud_notm}} bereitstellen.
{:shortdesc}


## Eine Sysdig-Instanz aus dem Katalog bereitstellen
{: #provision_ui}

Führen Sie die folgenden Schritte aus, um eine Instanz von Sysdig aus dem {{site.data.keyword.cloud_notm}}-Katalog bereitzustellen:

1. Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an.

    Klicken Sie auf das [{{site.data.keyword.cloud_notm}}-Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}, um das {{site.data.keyword.cloud_notm}}-Dashboard zu starten.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie auf **Katalog**. Die Liste der Services, die on {{site.data.keyword.cloud_notm}} verfügbar sind, wird geöffnet.

3. Wenn Sie die Liste der angezeigten Services filtern möchten, wählen Sie die Kategorie **Entwicklertools** aus.

4. Klicken Sie auf die Kachel **{{site.data.keyword.mon_full_notm}}**. Das Dashboard *Beobachtbarkeit* wird geöffnet.

5. Wählen Sie **Instanz erstellen** aus. 

6. Wählen Sie einen Serviceplan aus. Standardmäßig ist der Plan **Testversion** festgelegt.

    Weitere Informationen zu den Serviceplänen finden Sie im Abschnitt [Servicepläne](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

7. Wählen Sie eine Ressourcengruppe aus. Standardmäßig ist die Ressourcengruppe **Standard** festgelegt.

8. Klicken Sie auf **Erstellen**.

Nachdem Sie eine Instanz bereitgestellt haben: 

* Das Dashboard *Beobachtbarkeit* wird geöffnet. 
* Eine Service-ID wird automatisch erstellt. Sie können diese Service-ID verwenden, um den Sysdig-Zugriffsschlüssel für Ihre Instanz abzurufen.

Als Nächstes konfigurieren Sie eine Metrikquelle, indem Sie einen Sysdig-Agenten hinzufügen. Dieser Agent ist für die Erfassung und Weiterleitung von Metriken an Sysdig verantwortlich. 



## Eine Sysdig-Instanz über die Befehlszeilenschnittstelle bereitstellen
{: #provision_cli}

Führen Sie die folgenden Schritte aus, um eine Instanz von Sysig über die Befehlszeile bereitzustellen:

1. [Voraussetzung] Installieren Sie die {{site.data.keyword.cloud_notm}}-CLI. Wenn die Befehlszeilenschnittstelle (CLI) installiert ist, fahren Sie mit dem nächsten Schritt fort.

   Weitere Informationen finden Sie unter [Die {{site.data.keyword.cloud_notm}}-CLI installieren](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

2. Melden Sie sich an der Region in {{site.data.keyword.cloud_notm}} an, in der die Sysdig-Instanz ausgeführt werden soll. Führen Sie den folgenden Befehl aus: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Legen Sie die Ressourcengruppe fest, in der die Instanz bereitgestellt werden soll. Führen Sie den folgenden Befehl aus: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Standardmäßig ist die Ressourcengruppe `Standard` festgelegt.

4. Erstellen Sie die Sysdig-Instanz. Führen Sie den Befehl [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) aus:

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * NAME ist der Name der Sysdig-Instanz.
    
    * `sysdig-monitor` ist der Name des {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.cloud_notm}}.
    
    * SERVICE_PLAN_NAME ist der Typ des Plans. Gültige Werte sind *lite* und *graduated-tier*. 
    
    * LOCATION ist die Region, in der die Instanz erstellt wird.

    Wenn Sie beispielsweise eine Instanz mit dem bezahlten Plan bereitstellen möchten, führen Sie den folgenden Befehl aus:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

