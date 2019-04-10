---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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


# Metriken für eine App analysieren, die in einem Kubernetes-Cluster implementiert ist
{: #kubernetes_cluster}

In diesem Lernprogramm erfahren Sie, wie Sie einen Cluster für die Weiterleitung von Metriken an den {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.cloud_notm}} konfigurieren.
{:shortdesc}

Sie können den {{site.data.keyword.mon_full_notm}}-Service zum Überwachen von Kubernetes-Cluster verwenden.

Wenn Sie einen Cluster für die Weiterleitung von Metriken konfigurieren möchten, müssen Sie einen Agenten auf jedem Workerknoten in Ihrem Kubernetes-Cluster mit einem DaemonSet installieren. Der Sysdig-Agent verwendet einen Zugriffsschlüssel (Token), um sich bei der {{site.data.keyword.mon_full_notm}}-Instanz zu authentifizieren. Der Sysdig-Agent agiert als Datenkollektor. Er erfasst automatisch Metriken wie *Worker-CPU* und Worker-Speicher*, *HTTP-Datenverkehr in und aus Ihren Containern* sowie mehrere Teile der allgemeinen Infrastruktur-Software. Darüber hinaus kann der Agent angepasste Anwendungsmetriken entweder mit einem Prometheus-kompatiblen Scraper oder mit einer statsd-Fassade erfassen. 

Sie können Metriken über die webbasierte Benutzeroberfläche von Sysdig anzeigen.

![Komponentenübersicht von {{site.data.keyword.cloud_notm}}](../images/kube.png "Komponentenübersicht von {{site.data.keyword.cloud_notm}}")



## Vorbemerkungen
{: #kubernetes_cluster_prereqs}

ZUm die Schritte in diesem Einführungslernprogramm abzuschließen, finden Sie Anweisungen, um eine Instanz von {{site.data.keyword.mon_full_notm}} in der Region "USA (Süden)" bereitzustellen. Sie können einen vorhandenen Cluster oder die neue **Clusterversion 1.10** verwenden. Der Cluster kann in einer anderen Region verfügbar sein.  

Lesen Sie mehr über {{site.data.keyword.mon_full_notm}}. Weitere Informationen finden Sie im Abschnitt [Informationen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Verwenden Sie eine Benutzer-ID, die Mitglied oder ein Eigentümer eines {{site.data.keyword.cloud_notm}}-Kontos ist. Gehen Sie zum Abrufen einer {{site.data.keyword.cloud_notm}}-Benutzer-ID zu [Registrierung ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}.

Ihrer {{site.data.keyword.IBM_notm}}-ID müssen IAM-Richtlinien für jede der folgenden Ressourcen zugeordnet sein: 

| Ressource                             | Geltungsbereich der Zugriffsrichtlinie | Rolle    | Region    | Informationen                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Ressourcengruppe **Standard**           |  Ressourcengruppe            | Anzeigeberechtigter  | us-south  | Diese Richtlinie ist erforderlich, damit der Benutzer die Serviceinstanzen in der Standardressourcengruppe anzeigen kann.    |
| {{site.data.keyword.mon_full_notm}}-Service |  Ressourcengruppe            | Editor  | us-south  | Diese Richtlinie ist erforderlich, damit der Benutzer den {{site.data.keyword.mon_full_notm}}-Service in der Standardressourcengruppe bereitstellen und verwalten kann.   |
| Kubernetes-Clusterinstanz          |  Ressource                 | Editor  | us-south  | Diese Richtlinie ist erforderlich, um den geheimen Schlüssel und den Sysdig-Agent im Kubernetes-Cluster zu konfigurieren. |
{: caption="Tabelle 1. Liste der IAM-Richtlinien, um das Lernprogramm abzuschließen" caption-side="top"} 

Weitere Informationen zu den {{site.data.keyword.containerlong}}-IAM-Rollen finden Sie im Abschnitt [Benutzerzugriffsberechtigungen](/docs/containers?topic=containers-access_reference#access_reference).

Installieren Sie die {{site.data.keyword.cloud_notm}}-CLI und das CLI-Plug-in für Kubernetes. Weitere Informationen finden Sie unter [Die {{site.data.keyword.cloud_notm}}-CLI installieren](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Schritt 1: Bereitstellen einer {{site.data.keyword.mon_full_notm}}-Instanz
{: #kubernetes_cluster_step1}

Führen Sie die folgenden Schritte aus, um eine Instanz von {{site.data.keyword.mon_full_notm}} über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle bereitzustellen:

1. Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an.

    Klicken Sie auf das [{{site.data.keyword.cloud_notm}}-Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}, um das {{site.data.keyword.cloud_notm}}-Dashboard zu starten.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie auf **Katalog**. Die Liste der Services, die in {{site.data.keyword.cloud_notm}} verfügbar sind, wird geöffnet.

3. Wenn Sie die Liste der angezeigten Services filtern möchten, wählen Sie die Kategorie **Entwicklertools** aus.

4. Klicken Sie auf die Kachel **{{site.data.keyword.mon_full_notm}}**. Das Dashboard *Beobachtbarkeit* wird geöffnet.

5. Wählen Sie **Instanz erstellen** aus. 

6. Geben Sie einen Namen für die Serviceinstanz ein.

7. Wählen Sie die Ressourcengruppe **Standard** aus. 

    Standardmäßig ist die Ressourcengruppe **Standard** festgelegt.

8. Wählen Sie den Serviceplan **Testversion** aus. 

    Standardmäßig ist der Plan **Testversion** festgelegt.

    Weitere Informationen zu anderen Serviceplänen finden Sie im Abschnitt [Preisstrukturpläne](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Klicken Sie auf **Erstellen**, um den {{site.data.keyword.mon_full_notm}}-Service in der {{site.data.keyword.cloud_notm}}-Ressourcengruppe, in der Sie angemeldet sind, bereitzustellen.

Nachdem Sie eine Instanz bereitgestellt haben, wird das Dashboard *Beobachtbarkeit* geöffnet. 


**Hinweis:** Wenn Sie eine Instanz über die Befehlszeilenschnittstelle (CLI) bereitstellen möchten, lesen Sie die Informationen [Eine Instanz über die {{site.data.keyword.cloud_notm}}-CLI bereitstellen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Schritt 2: Ihren Kubernetes-Cluster zum Senden von Metriken an Ihre Instanz konfigurieren
{: #kubernetes_cluster_step2}

Wenn Sie Ihren Kubernetes-Cluster so konfigurieren möchten, dass Metriken an Ihre {{site.data.keyword.mon_full_notm}}-Instanz gesendet werden, müssen Sie auf jedem Knoten des Clusters ein Sysdig-Agent-Pod installieren. Der Sysdig-Agent wird über einen DaemonSet installiert, der sicherstellt, dass auf jedem Workerknoten eine Instanz des Agenten ausgeführt wird. Der Sysdig-Agent erfasst Metriken aus dem Pod, wo er installiert ist, und leitet diese an Ihre Instanz weiter.

**Hinweis:** Damit die vollständige Systemmetrik bereitgestellt werden kann, muss der Sysdig-Agent einen privilegierten Status haben.

Führen Sie in der Befehlszeile die folgenden Schritte aus, um Ihren Kubernetes-Cluster so zu konfigurieren, dass Metriken an Ihre {{site.data.keyword.mon_full_notm}}-Instanz weitergeleitet werden:

1. Öffnen Sie ein Terminal. Melden Sie sich dann an der {{site.data.keyword.cloud_notm}} an. Führen Sie den folgenden Befehl aus und folgen Sie den Eingabeaufforderungen:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    Wählen Sie das Konto aus, in dem Sie die {{site.data.keyword.mon_full_notm}}-Instanz bereitgestellt haben.

2. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

3. Rufen Sie den Sysdig-Zugriffsschlüssel ab. Weitere Informationen finden Sie im Abschnitt [Zugriffsschlüssel über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

4. Rufen Sie die Aufnahme-URL ab. Weitere Informationen finden Sie unter [Sysdig-Collector-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

5. Stellen Sie den Sysdig-Agenten bereit. Führen Sie den folgenden Befehl aus:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * SYSDIG_ACCESS_KEY ist der Aufnahmeschlüssel für die Instanz.

    * COLLECTOR_ENDPOINT ist die Aufnahme-URL für die Region, in der die Überwachungsinstanz verfügbar ist.

    * TAG_DATA sind durch Kommas getrennte Tags, die als *TAG_NAME:TAG_VALUE* formatiert sind. Sie können Ihrem Sysdig-Agenten einen oder mehrere Tags zuordnen. Beispiel: *role:serviceX,location:us-south*. Später können Sie diese Tags verwenden, um Metriken aus der Umgebung zu identifizieren, in der der Agent ausgeführt wird.

    * Legen Sie **sysdig_capture_enabled** auf *false* fest, um die Sysdig-Erfassungsfunktion zu inaktivieren. Standardmäßig ist *true* festgelegt. Weitere Informationen finden Sie im Abschnitt [Mit Erfassungen arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

6. Stellen Sie sicher, dass der Sysdig-Agent und sein Status erfolgreich erstellt wurden. Führen Sie den folgenden Befehl aus:

    ```
    kubectl get pods
    ```
    {: codeblock}



## Schritt 3: Sysdig-Webbenutzerschnittstelle starten
{: #kubernetes_cluster_step3}

Führen Sie die folgenden Schritte aus, um die Webbenutzerschnittstelle zu starten:

1. Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an.

    Klicken Sie auf das [{{site.data.keyword.cloud_notm}}-Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}, um das {{site.data.keyword.cloud_notm}}-Dashboard zu starten.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird das {{site.data.keyword.cloud_notm}}-Dashboard geöffnet.

2. Wählen Sie im Navigationsmenü die Option **Beobachtbarkeit** aus. 

3. Wählen Sie **Überwachung** aus. 

    Die Liste der Instanzen, die unter {{site.data.keyword.cloud_notm}} verfügbar sind, wird angezeigt.

4. Wählen Sie Ihre Instanz aus. Klicken Sie dann auf **Sysdig anzeigen**.

Wenn der Sysdig-Agent erfolgreich konfiguriert wurde, wird die *ERKUNDEN*-Ansicht geöffnet.

Wenn der Sysdig-Agent jedoch nicht erfolgreich installiert wurde, wenn er auf den falschen Aufnahmeendpunkt verweist oder der Zugriffsschlüssel falsch ist, öffnet sich eine Seite und informiert Sie darüber, was als Nächstes getan werden soll.

Es kann nur eine Webbenutzerschnittstelle-Sitzung pro Browser geöffnet sein.
{: tip}


## Schritt 4: Ihren Cluster überwachen
{: #kubernetes_cluster_step4}

Sie können Ihren Cluster in der Ansicht **ERKUNDEN** überwachen, die über die Webbenutzerschnittstelle verfügbar ist. Diese Ansicht ist der Ausgangspunkt für die Fehlerbehebung und die Überwachung Ihrer Infrastruktur. Es handelt sich hierbei um die Standard-Homepage der Webbenutzerschnittstelle für Benutzer.

Im Abschnitt *Host und Container* können Sie die Liste der Worker in Ihrem Cluster anzeigen, die Metriken an die Überwachungsinstanz weiterleiten. Jeder Worker-Eintrag stellt eine Gruppe zusammengehöriger Infrastrukturobjekte für diesen Worker dar.

Klicken Sie auf **Host und Container** ![Host und Container](../images/switch_hosts.png), um die Datenquellen zu wechseln. Wählen Sie dann einen Worker aus. Die angezeigten Daten entsprechen dem von Ihnen ausgewählten Worker.

Wenn Sie auf **Zurück zur Erkundungstabelle** klicken, wird die *Erkundungstabelle* angezeigt. Jede Spalte zeigt eine andere Metrik an. Sie können jede Metrik einzeln konfigurieren. Sie können die Reihenfolge der Spalten ändern. Wenn Sie Änderungen an der Reihenfolge der vorhandenen Spalten vornehmen, wird die Änderung während der Anmeldung über verschiedene Gruppierungen hinweg persistent gespeichert. Wenn Sie eine Spalte hinzufügen oder entfernen, ist die Änderung permanent. Sie können auch Farben konfigurieren, um Werte hervorzuheben und die Lesbarkeit zu verbessern.

Führen Sie beispielsweise die folgenden Schritte aus, um die Farbcodierung für eine Spalte zu konfigurieren:

1. Wählen Sie eine Spalte aus. Bewegen Sie den Mauszeiger über den Spaltentitel. Wählen Sie dann das Stiftsymbol aus.
2. Schalten Sie den Balken ein, um die Farbcodierung zu aktivieren.
3. Legen Sie Werte für die verschiedenen Schwellenwerte fest.

Wenn Sie einen Worker auswählen, wird ein Standarddashboard angezeigt. Klicken Sie auf ![Dashboard wechseln](images/switch_dashboards_1.png) und erkunden Sie die verschiedenen Standarddashboards und Metriken. Beachten Sie, dass Sie nur Metriken und Dashboards auswählen können, die für den ausgewählten Worker relevant sind.


## Nächste Schritte
{: #kubernetes_cluster_next_steps}

Erstellen Sie ein angepasstes Dashboard. Weitere Informationen finden Sie im Abschnitt [Mit Dashboards arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Sie können auch Informationen zu Alerts erhalten. Weitere Informationen finden Sie im Abschnitt [Mit Alerts arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






