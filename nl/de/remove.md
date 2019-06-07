---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# Eine Instanz entfernen
{: #remove}

Sie können eine Instanz des {{site.data.keyword.mon_full_notm}}-Service über die {{site.data.keyword.Bluemix}}-Benutzerschnittstelle oder über die Befehlszeile entfernen.
{:shortdesc}

Wenn Sie eine Instanz aus {{site.data.keyword.cloud_notm}} entfernen, müssen Sie die folgenden Informationen beachten:

1. Notieren Sie die Liste der Quellen, die Metriken an die {{site.data.keyword.mon_full_notm}}-Instanz weiterleiten, die Sie entfernen möchten. Sie müssen den Sysdig-Agenten aus jeder Quelle entfernen.
2. Entfernen Sie die Berechtigungen, die Benutzern erteilt wurden, um mit der Instanz zu arbeiten. 

    Wenn Sie eine Zugriffsgruppe verwenden, um die Berechtigungen für den Zugriff auf die Instanz zu verwalten, müssen Sie die Zugriffsgruppe entfernen.

    Wenn Sie eine Zugriffsgruppe verwenden, um die Berechtigungen für den Zugriff auf verschiedene Serviceinstanzen zu verwalten, müssen Sie die Richtlinien entfernen, die Berechtigungen für die Instanz erteilen, die Sie entfernen möchten.
    
    Wenn Sie Benutzern einzelne Richtlinien erteilt haben, müssen Sie die Informationen jedes Benutzers mit Zugriff auf die Instanz zusammenstellen. Dann müssen Sie eine Richtlinie nach der anderen entfernen, die sich auf die Instanz beziehen, die Sie löschen möchten.


Löschen Sie anschließend die Instanz aus dem {{site.data.keyword.cloud_notm}}-Dashboard.


## Eine Instanz über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle entfernen
{: #remove_ui}

Führen Sie die folgenden Schritte aus, um eine Instanz von {{site.data.keyword.mon_full_notm}} mit der {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle zu entfernen:

1. [Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/login){:new_window}.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle geöffnet.

2. Wählen Sie **Beobachtbarkeit** aus. 

3. Wählen Sie **Überwachung** aus. Die Liste der Instanzen wird angezeigt.

4. Wählen Sie die Instanz aus, die Sie löschen möchten.

5. Wählen Sie im Menü *Aktion* die Option **Entfernen** aus.


## Entfernen einer Instanz über die Befehlszeilenschnittstelle
{: #remove_cli}

Führen Sie die folgenden Schritte aus, um eine Instanz von {{site.data.keyword.mon_full_notm}} über die Befehlszeile zu entfernen:

1. [Voraussetzung] Installieren Sie die {{site.data.keyword.cloud_notm}}-CLI. Wenn die Befehlszeilenschnittstelle (CLI) installiert ist, fahren Sie mit dem nächsten Schritt fort.

   Weitere Informationen finden Sie unter [Die {{site.data.keyword.cloud_notm}}-CLI installieren](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

2. Melden Sie sich an der Region in {{site.data.keyword.cloud_notm}} an, in der die Sysdig-Instanz ausgeführt werden soll. Führen Sie den folgenden Befehl aus: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Legen Sie die Ressourcengruppe fest, in der die Instanz bereitgestellt wird. Führen Sie den folgenden Befehl aus: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Standardmäßig ist die Ressourcengruppe `Standard` festgelegt.

4. Entfernen Sie die Instanz. Führen Sie den Befehl [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete) aus:

    ```
    ibmcloud resource service-instance-delete NAME 
    ```
    {: codeblock}

    Dabei steht NAME für den Namen der Instanz.

    Wenn Sie beispielsweise eine Instanz entfernen möchten, führen Sie den folgenden Befehl aus:

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
