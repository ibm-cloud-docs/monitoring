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


# Metriken in Grafana für einen Kubernetes-Cluster analysieren
{: #container_service_metrics}

In diesem Lernprogramm erfahren Sie, wie Sie den {{site.data.keyword.monitoringlong}}-Service zum Überwachen der Leistung Ihres Containers verwenden. 
{:shortdesc}


## Lernziele
{: #ks_objectives}

Sie erfahren, wie Sie nach Containermetriken für eine App suchen, die in einem Kubernetes-Cluster bereitgestellt ist, und wie Sie diese Metriken analysieren:

1. Ermitteln Sie, wo Metriken, die in einem Cluster erfasst werden, an den {{site.data.keyword.monitoringshort}}-Service weitergeleitet werden. 
2. Starten Sie Grafana und legen Sie die {{site.data.keyword.monitoringshort}}-Domäne fest, in der Sie die Clustermetriken anzeigen können.
3. Suchen und analysieren Sie Containermetriken für eine App, die in einem Kubernetes-Cluster in {{site.data.keyword.Bluemix_notm}} bereitgestellt wird.

Dieses Lernprogramm führt Sie durch die erforderlichen Schritte zum Erzielen des folgenden End-to-End-Szenarios bei der Arbeit in {{site.data.keyword.Bluemix_notm}}: Bereitstellen eines Clusters, ermitteln, wo der Cluster Metriken an den {{site.data.keyword.monitoringshort}}-Service in {{site.data.keyword.Bluemix_notm}} sendet, Bereitstellen einer App im Cluster und Verwenden von Grafana zum Anzeigen und Filtern von Containermetriken für diesen Cluster.


**Hinweis:** Zum Absolvieren dieses Lernprogramms müssen Sie die Voraussetzungen erfüllen und die Lernprogramme durchführen, die aus verschiedenen Schritten verlinkt sind.


## Voraussetzungen
{: #ks_prereqs}

1. Sie müssen ein Mitglied oder ein Eigner eines {{site.data.keyword.Bluemix_notm}}-Kontos mit der Berechtigung zum Erstellen von Kubernetes-Standardclustern, Bereitstellen von Apps in Clustern und zum Abfragen der Metriken in {{site.data.keyword.Bluemix_notm}} für die Überwachung in Grafana sein.

    Ihrer Benutzer-ID in {{site.data.keyword.Bluemix_notm}} müssen die folgenden Richtlinien zugewiesen sein:
    
    * Eine IAM-Richtlinie für den {{site.data.keyword.containershort}} mit der Berechtigung *Operator* oder *Administrator*.
    
    Weitere Informationen finden Sie in [Einem Benutzer eine IAM-Richtlinie über die IBM Cloud-Benutzerschnittstelle zuweisen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui).

2. Öffnen Sie eine Terminalsitzung, von der aus Sie die Kubernetes-Cluster verwalten und die Apps über die Befehlszeile bereitstellen können. Die Beispiele in diesem Lernprogramm gelten für ein Ubuntu Linux-System.

3. Installieren Sie die CLIs für die Arbeit mit dem {{site.data.keyword.containershort}} in Ihrem Ubuntu-System.

    * Installieren Sie die {{site.data.keyword.Bluemix_notm}}-CLI. 
    * Installieren Sie die {{site.data.keyword.containershort}}-CLI zum Erstellen und Verwalten Ihrer Kubernetes-Cluster in {{site.data.keyword.containershort}} und zum Bereitstellen containerisierten Apps im Cluster.
    
    Weitere Informationen dazu finden Sie unter [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview).
    
    

    
 

## Schritt 1: Kubernetes-Cluster bereitstellen
{: #ks_step1}

Führen Sie die folgenden Schritte aus:

1. Erstellen Sie einen Kubernetes-Standardcluster. Weitere Informationen finden Sie in [Kubernetes-Standardcluster erstellen](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial).

2. Richten Sie den Clusterkontext in einem Terminal ein. Nach der Konfiguration des Kontexts können Sie den Kubernetes-Cluster verwalten und die Anwendung im Kubernetes-Cluster bereitstellen.

    Melden Sie sich bei der Region, der Organisation und dem Bereich in {{site.data.keyword.Bluemix_notm}} an, die/der dem von Ihnen erstellten Cluster zugeordnet ist. Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).

	Initialisieren Sie das {{site.data.keyword.containershort}}-Service-Plug-in.

	```
	ibmcloud cs init
	```
	{: codeblock}

    Legen Sie den Terminalkontext für den Cluster fest.
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    Die Ausgabe dieses Befehls stellt den Befehl bereit, den Sie in Ihrem Terminal ausführen müssen, um den Pfad zur Konfigurationsdatei anzugeben. Beispiel:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Kopieren Sie den Befehl und fügen Sie ihn ein, um die Umgebungsvariable in Ihrem Terminal festzulegen, und drücken Sie dann die **Eingabetaste**.



## Schritt 2: Dem Benutzer Berechtigungen zum Anzeigen von Metriken in der Kontodomäne erteilen
{: #ks_step2}

Um einem Benutzer Berechtigungen zum Anzeigen von Metriken in einer Kontodomäne zu erteilen, müssen Sie dem Benutzer eine IAM-Richtlinie für den {{site.data.keyword.monitoringshort}}-Service mit der Rolle **Anzeigeberechtigter** zuweisen.

Führen Sie die folgenden Schritte aus, um einem Benutzer die Berechtigung zum Arbeiten mit dem {{site.data.keyword.monitoringshort}}-Service zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten>Konto>Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste der Benutzer mit ihren E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Wenn der Benutzer Mitglied des Kontos ist, wählen Sie den Benutzernamen in der Liste aus oder klicken Sie im Menü *Aktionen* auf **Benutzer verwalten**.

    Wenn der Benutzer kein Mitglied des Kontos ist, finden Sie weitere Informationen unter [Benutzer einladen](/docs/iam?topic=iam-iamuserinv#iamuserinv).

4. Wählen Sie **Zugriffsrichtlinien > Zugriff zuweisen > Zugriff auf Ressourcen zuweisen** aus.

5. Wählen Sie den Service **{{site.data.keyword.monitoringlong}}**, die Region, in der der Cluster verfügbar ist (**USA (Süden)** für dieses Lernprogramm), und eine Rolle (**Anzeigeberechtigter**) aus.



## Schritt 3: Berechtigungen für den Eigner des {{site.data.keyword.containershort_notm}} erteilen
{: #ks_step3}

Wenn der Cluster Metriken an die Kontodomäne weiterleiten soll, muss der Eigner des {{site.data.keyword.containershort}}-Schlüssels über die folgenden IAM-Richtlinien verfügen:

* IAM-Richtlinie mit **Bearbeitungsberechtigungen** für den {{site.data.keyword.monitoringshort}}-Service.
* IAM-Richtlinie mit **Administratorberechtigungen** für {{site.data.keyword.containershort}}.


Führen Sie die folgenden Schritte aus, um die {{site.data.keyword.containershort}}-Schlüsseleignerberechtigungen zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten>Konto>Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste der Benutzer mit ihren E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Suchen Sie nach der Benutzer-ID des Eigners des {{site.data.keyword.containershort}}.

    Führen Sie den Befehl `ibmcloud cs api-key-info ClusterName` aus, um die Benutzer-ID des Eigners des {{site.data.keyword.containershort}} abzurufen.

4. Wählen Sie **Zugriffsrichtlinien > Zugriff zuweisen > Zugriff auf Ressourcen zuweisen** aus.

5. Wählen Sie den Service **{{site.data.keyword.monitoringlong}}**, die Region, in der der Cluster verfügbar ist (**USA (Süden)** für dieses Lernprogramm), und eine Rolle (**Bearbeiter**) aus.	

6. Wiederholen Sie die Schritte 2 bis 4 und wählen Sie den {{site.data.keyword.containershort}}-Service aus. Wählen Sie **Alle Regionen** und die Rolle **Administrator** aus.	




## Schritt 4: Beispielapp im Kubernetes-Cluster bereitstellen
{: #ks_step4}

Stellen Sie die Beispielapp im Kubernetes-Cluster bereit und führen Sie sie aus. Führen Sie die Schritte im folgenden Lernprogramm aus, um die Beispielapp bereitzustellen: [Lerneinheit 1: Einzelne Instanzapps in Kubernetes-Clustern bereitstellen](/docs/containers?topic=containers-cs_apps_tutorial#cs_apps_tutorial_lesson1).

Die App ist eine 'Hello World'-Node.js-App:

```
var express = require('express')
    var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

Wenn Sie in dieser Beispiel-App die App in einem Browser testen, schreibt die App die folgende Nachricht an 'stdout': `Sample app is listening on port 8080.`


## Schritt 5: Grafana starten und die Metrikdomäne festlegen
{: #ks_step5}

Starten Sie Grafana über einen Browser und legen Sie die {{site.data.keyword.monitoringshort}}-Domäne fest, in der Sie die Clustermetriken anzeigen können.

Zum Analysieren von Metriken für einen Cluster müssen Sie auf Grafana in der öffentlichen Cloud-Region zugreifen, in der der Cluster erstellt wird. Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).

1. Starten Sie Grafana über einen Browser. 

    Geben Sie die {{site.data.keyword.monitoringshort}}-Service-URL für die Region ein, in der Sie den Cluster erstellt haben. 
    
    Informationen zum Abrufen der URLs nach Region finden Sie unter [URLs für den Überwachungsservice](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

    Starten Sie zum Beispiel für die Region 'USA (Süden)': [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Legen Sie für die Domäne {{site.data.keyword.monitoringshort}} den Wert **Konto** fest.

    Wählen Sie in Grafana Ihre ID aus. Stellen Sie dann sicher, dass Sie sich im richtigen Konto befinden und wählen Sie eine Domäne aus. Wählen Sie `Domäne = Konto` aus.

    Cluster leiten Metriken an die Kontometrikdomäne weiter. 

## Schritt 6: Cluster in Grafana überwachen
{: #ks_step6}

Der {{site.data.keyword.containershort}} stellt ein Grafana-Dashboard bereit, über das Sie Ihre Clustermetriken überwachen können. 

Führen Sie die folgenden Schritte aus, um das Beispieldashboard zu öffnen:

1. Wählen Sie das Steuerelement zum Hin- und Herschalten ![Grafana-Seitenmenüleiste](images/grafana_settings.gif "Grafana-Seitenmenüleiste") in der seitlichen Menüleiste aus.
2. Wählen Sie **Dashboards** aus.
3. Klicken Sie auf **Öffnen**.
4. Wählen Sie **ClusterMonitoringDashboard_v1** aus.

Das Beispieldashboard wird geöffnet. 

![Grafana-Beispieldashboard](images/cluster_grafana_sample_dashboard.png "Grafana-Beispieldashboard")



## Nächste Schritte
{: #ks_next_steps}

Definieren Sie einen Alert für eine Metrik. Weitere Informationen finden Sie unter [Alerts konfigurieren ](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).
