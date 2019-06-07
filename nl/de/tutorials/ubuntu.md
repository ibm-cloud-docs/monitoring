---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# Metriken für einen Ubuntu-Host analysieren
{: #ubuntu}

In diesem Lernprogramm erfahren Sie, wie Sie einen Ubuntu-Host konfigurieren, um Metriken an den {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.cloud_notm}} weiterzuleiten.
{:shortdesc}

Wenn Sie einen Ubuntu-Server für die Weiterleitung von Metriken konfigurieren möchten, müssen Sie einen Sysdig-Agenten installieren. Der Agent verwendet einen Zugriffsschlüssel (Token), um sich bei der {{site.data.keyword.mon_full_notm}}-Instanz zu authentifizieren. Der Sysdig-Agent agiert als Datenkollektor. Die Messdaten werden automatisch erfasst.

Sie können Metriken über die webbasierte Benutzeroberfläche von Sysdig anzeigen.

![Komponentenübersicht von {{site.data.keyword.cloud_notm}}](../images/ubuntu.png "Komponentenübersicht von {{site.data.keyword.cloud_notm}}")



## Vorbemerkungen
{: #ubuntu_prereqs}

Arbeiten Sie mit der Region "USA (Süden)". 

Lesen Sie mehr über {{site.data.keyword.mon_full_notm}}. Weitere Informationen finden Sie im Abschnitt [Informationen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Verwenden Sie eine Benutzer-ID, die Mitglied oder ein Eigentümer eines {{site.data.keyword.cloud_notm}}-Kontos ist. Gehen Sie zum Abrufen einer {{site.data.keyword.cloud_notm}}-Benutzer-ID zu [Registrierung ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/login){:new_window}.

Ihrer {{site.data.keyword.IBM_notm}}-ID müssen IAM-Richtlinien für jede der folgenden Ressourcen zugeordnet sein: 

| Ressource                             | Geltungsbereich der Zugriffsrichtlinie | Rolle    | Region    | Informationen                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Ressourcengruppe **Standard**           |  Ressourcengruppe            | Anzeigeberechtigter  | `Us-south`  | Diese Richtlinie ist erforderlich, damit der Benutzer die Serviceinstanzen in der Standardressourcengruppe anzeigen kann.    |
| {{site.data.keyword.mon_full_notm}}-Service |  Ressourcengruppe            | Editor  | `Us-south`  | Diese Richtlinie ist erforderlich, damit der Benutzer den {{site.data.keyword.mon_full_notm}}-Service in der Standardressourcengruppe bereitstellen und verwalten kann.   |
{: caption="Tabelle 1. Liste der IAM-Richtlinien, um das Lernprogramm abzuschließen" caption-side="top"} 

Installieren Sie die {{site.data.keyword.cloud_notm}}-CLI. Weitere Informationen finden Sie unter [Die {{site.data.keyword.cloud_notm}}-CLI installieren](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Schritt 1: Bereitstellen einer {{site.data.keyword.mon_full_notm}}-Instanz
{: #ubuntu_step1}

Führen Sie die folgenden Schritte aus, um eine Instanz von {{site.data.keyword.mon_full_notm}} über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle bereitzustellen:

1. [Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/login){:new_window}.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie auf **Katalog**. Die Liste der Services, die in {{site.data.keyword.cloud_notm}} verfügbar sind, wird geöffnet.

3. Wenn Sie die Liste der angezeigten Services filtern möchten, wählen Sie die Kategorie **Entwicklertools** aus.

4. Klicken Sie auf die Kachel **{{site.data.keyword.mon_full_notm}}**. Das Dashboard *Beobachtbarkeit* wird geöffnet.

5. Wählen Sie **Instanz erstellen** aus. 

6. Geben Sie einen Namen für die Serviceinstanz ein.

7. Wählen Sie die Ressourcengruppe **Standard** aus. 

    Standardmäßig ist die Ressourcengruppe **Standard** festgelegt.

8. Wählen Sie den Serviceplan **Lite** aus. 

    Standardmäßig ist der **Lite**-Plan festgelegt.

    Weitere Informationen zu anderen Serviceplänen finden Sie im Abschnitt [Preisstrukturpläne](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Klicken Sie auf **Erstellen**, um den {{site.data.keyword.mon_full_notm}}-Service in der {{site.data.keyword.cloud_notm}}-Ressourcengruppe, in der Sie angemeldet sind, bereitzustellen.

Nachdem Sie eine Instanz bereitgestellt haben, wird das Dashboard *Beobachtbarkeit* geöffnet. 


**Hinweis:** Wenn Sie eine Instanz über die Befehlszeilenschnittstelle (CLI) bereitstellen möchten, lesen Sie die Informationen [Eine Instanz über die {{site.data.keyword.cloud_notm}}-CLI bereitstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Schritt 2: Ihren Ubuntu-Server zum Senden von Metriken an Ihre Instanz konfigurieren
{: #ubuntu_step2}

Um Ihren Ubuntu-Server zu konfigurieren, um Metriken an Ihre {{site.data.keyword.mon_full_notm}}-Instanz zu senden, müssen Sie einen Sysdig-Agenten installieren. 

Führen Sie in der Befehlszeile die folgenden Schritte aus:

1. Öffnen Sie ein Terminal. Melden Sie sich dann an der {{site.data.keyword.cloud_notm}} an. Führen Sie den folgenden Befehl aus und folgen Sie den Eingabeaufforderungen:

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    Wählen Sie das Konto aus, in dem die {{site.data.keyword.mon_full_notm}}-Instanz verfügbar ist.

2. Rufen Sie den Sysdig-Zugriffsschlüssel ab. Weitere Informationen finden Sie im Abschnitt [Zugriffsschlüssel über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

3. Rufen Sie die Aufnahme-URL ab. Weitere Informationen finden Sie unter [Sysdig-Collector-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

4. Stellen Sie den Sysdig-Agenten bereit. Führen Sie den folgenden Befehl aus:

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * SYSDIG_ACCESS_KEY ist der Aufnahmeschlüssel für die Instanz.

    * COLLECTOR_ENDPOINT ist die Aufnahme-URL für die Region, in der die Überwachungsinstanz verfügbar ist.

    * TAG_DATA sind durch Kommas getrennte Tags, die als *TAG_NAME:TAG_VALUE* formatiert sind. Sie können Ihrem Sysdig-Agenten einen oder mehrere Tags zuordnen. Beispiel: *role:serviceX,location:us-south*.Später können Sie diese Tags verwenden, um Metriken aus der Umgebung zu identifizieren, in der der Agent ausgeführt wird.

    * Legen Sie **sysdig_capture_enabled** auf *false* fest, um die Sysdig-Erfassungsfunktion zu inaktivieren. Standardmäßig ist *true* festgelegt. Weitere Informationen finden Sie im Abschnitt [Mit Erfassungen arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

Wenn der Sysdig-Agent nicht ordnungsgemäß installiert werden kann, installieren Sie die Kernel-Header manuell. Wählen Sie eine Distribution aus und führen Sie den Befehl für diese Distribution aus. Wiederholen Sie anschließend die Bereitstellung des Sysdig-Agenten.

* Für **Debian- und Ubuntu-Linux-Distributionen** führen Sie den folgenden Befehl aus:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* Für **RHEL-, CentOS- und Fedora-Linux-Distributionen** führen Sie den folgenden Befehl aus:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## Schritt 3: Sysdig-Webbenutzerschnittstelle starten
{: #ubuntu_step3}

Führen Sie die folgenden Schritte aus, um die Webbenutzerschnittstelle zu starten:

1. [Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/login){:new_window}.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird das {{site.data.keyword.cloud_notm}}-Dashboard geöffnet.

2. Wählen Sie im Navigationsmenü die Option **Beobachtbarkeit** aus. 

3. Wählen Sie **Überwachung** aus. 

    Die Liste der Instanzen, die unter {{site.data.keyword.cloud_notm}} verfügbar sind, wird angezeigt.

4. Wählen Sie Ihre Instanz aus. Klicken Sie dann auf **Sysdig anzeigen**.

Wenn der Sysdig-Agent erfolgreich konfiguriert wurde, wird die *ERKUNDEN*-Ansicht geöffnet.

Wenn der Sysdig-Agent jedoch nicht erfolgreich installiert wurde, wenn er auf den falschen Aufnahmeendpunkt verweist oder der Zugriffsschlüssel falsch ist, öffnet sich eine Seite und informiert Sie darüber, was als Nächstes getan werden soll.

Es kann nur eine Webbenutzerschnittstellensitzung pro Browser geöffnet sein.
{: tip}


## Schritt 4. Ihren Ubuntu-Server überwachen
{: #ubuntu_step4}

Sie können Ihren Ubuntu-Server in der Ansicht **ERKUNDEN** überwachen, die über die Webbenutzerschnittstelle verfügbar ist. Diese Ansicht ist der Ausgangspunkt für die Fehlerbehebung und die Überwachung Ihrer Infrastruktur. Es handelt sich hierbei um die Standard-Homepage der Webbenutzerschnittstelle für Benutzer.

Sie finden im Abschnitt *Host und Container* den Eintrag für Ihren Ubuntu-Server. Klicken Sie auf **Host und Container** ![Host und Container](../images/switch_hosts.png), um die Datenquellen zu wechseln. Wählen Sie dann Ihren Ubuntu-Server aus. Die angezeigten Daten entsprechen dem von Ihnen ausgewählten Ubuntu-Server.

Führen Sie beispielsweise die folgenden Schritte aus, um die Farbcodierung für eine Spalte zu konfigurieren:

1. Wählen Sie eine Spalte aus. Bewegen Sie den Mauszeiger über den Spaltentitel. Wählen Sie dann das Stiftsymbol aus.
2. Schalten Sie den Balken ein, um die Farbcodierung zu aktivieren.
3. Legen Sie Werte für die verschiedenen Schwellenwerte fest.



## Nächste Schritte
{: #ubuntu_next_steps}

Erstellen Sie ein angepasstes Dashboard. Weitere Informationen finden Sie im Abschnitt [Mit Dashboards arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Sie können auch Informationen zu Alerts erhalten. Weitere Informationen finden Sie im Abschnitt [Mit Alerts arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






