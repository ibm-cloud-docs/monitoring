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


# Grafana-Dashboard für die Überwachung eines Kubernetes-Clusters erstellen
{: #container_grafana_dashboard}


In diesem Lernprogramm erfahren Sie, wie Sie ein Grafana-Dashboard im {{site.data.keyword.monitoringlong}}-Service für die Überwachung der Leistung Ihres Clusters erstellen. 
{:shortdesc}


## Lernziele
{: #cgd_objectives}

Sie erfahren, wie Sie nach Containermetriken für eine App suchen, die in einem Kubernetes-Cluster bereitgestellt ist, und wie Sie diese Metriken analysieren:

1. Starten Sie Grafana und legen Sie die {{site.data.keyword.monitoringshort}}-Domäne fest, in der Sie die Clustermetriken anzeigen können.
2. Erstellen Sie ein Grafana-Dashboard und definieren Sie eine Metrik, mit der die CPU-Auslastung eines Containers überwacht werden kann.


## Annahmen
{: #cgd_assumptions}

Für dieses Lernprogramm wird Folgendes angenommen:

* Es ist ein Cluster in der Region 'USA (Süden)' verfügbar. 
* Ihre Benutzer-ID verfügt über eine IAM-Richtlinie für den {{site.data.keyword.monitoringshort}}-Service mit **Anzeigeberechtigung**.

Um dieses Lernprogramm durchzuführen, müssen Sie das Lernprogramm [Metriken in Grafana für eine in einem Kubernetes-Cluster bereitgestellte App analysieren](/docs/services/cloud-monitoring/tutorials?topic=cloud-monitoring-container_service_metrics#container_service_metrics) absolvieren oder es muss ein Cluster mit mindestens einer bereitgestellten Anwendung eingerichtet sein.



## Schritt 1: Grafana starten
{: #cgd_step1}

Starten Sie Grafana über einen Browser und legen Sie die {{site.data.keyword.monitoringshort}}-Domäne fest, in der Sie die Clustermetriken anzeigen können.

Zum Analysieren von Metriken für einen Cluster müssen Sie auf Grafana in der öffentlichen Cloud-Region zugreifen, in der der Cluster erstellt wird. Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).

1. Starten Sie Grafana über einen Browser. 

    Geben Sie die {{site.data.keyword.monitoringshort}}-Service-URL für die Region ein, in der Sie den Cluster erstellt haben. 
    
    Informationen zum Abrufen der URLs nach Region finden Sie unter [URLs für den Überwachungsservice](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

    Starten Sie zum Beispiel für die Region 'USA (Süden)': [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Legen Sie die {{site.data.keyword.monitoringshort}}-Domäne auf **account** fest.

    Wählen Sie in Grafana Ihre ID aus. Stellen Sie dann sicher, dass Sie sich im richtigen Konto befinden, und wählen Sie `Domain = account` aus.


## Schritt 2: Grafana-Dashboard erstellen
{: #cgd_step2}

Führen Sie die folgenden Schritte aus, um ein neues Dashboard zu erstellen:

1. Wählen Sie das Steuerelement zum Hin- und Herschalten ![Grafana-Seitenmenüleiste](images/grafana_settings.gif "Grafana-Seitenmenüleiste") in der seitlichen Menüleiste aus.
2. Wählen Sie **Dashboards** aus.
3. Klicken Sie auf **Neu**

Ein Dashboard wird geöffnet. Das Dashboard enthält eine leere Zeile, die konfiguriert werden kann.

![Grafana-Dashboard](images/grafana4_f1.gif "Grafana-Dashboard")

Fügen Sie in Grafana Zeilen hinzu, um das Dashboard in Abschnitte zu unterteilen. Eine Zeile gruppiert eine oder mehrere Anzeigen. Innerhalb einer Zeile ist eine Anzeige die kleinste Visualisierungseinheit, die Sie für die Anzeige von Daten für eine Metrik konfigurieren können. Sie können zum Beispiel eine Diagrammanzeige oder eine Tabellenanzeige auswählen. Sie können Anzeigen ziehen und übergeben, um sie in einem Dashboard neu anzuordnen. Die in den Anzeigen angezeigten Daten werden über Abfragen konfiguriert. Sie können eine oder mehrere Abfragen in einer Anzeige definieren. Jede Abfrage stellt eine andere Gruppe von Daten dar. Sie können auch den Zeitraum für eine Anzeige festlegen. Normalerweise wird der Zeitraum durch das Zeitauswahlfeld im *Dashboard* festgelegt.

## Schritt 3: Grafik zum Überwachen einer Metrik zum Dashboard hinzufügen
{: #cgd_step3}

Führen Sie die folgenden Schritte aus:

1. Wählen Sie **Grafik** aus.

2. Klicken Sie auf den Grafiktitel und wählen Sie anschließend **Bearbeiten** aus.

    Die Registerkarte *Metriken* wird angezeigt. Sie können hier die Standarddatenquelle sehen.


![Grafikanzeige mit Konfigurationsregisterkarten](images/grafana4_f2.gif "Grafikanzeige mit Konfigurationsregisterkarten")


## Schritt 4: Eine Metrikabfrage definieren
{: #cgd_step4}

Definieren Sie die Abfrage, die die in der Grafik angezeigten Daten filtert. Diese Abfrage überwacht die Nanosekunden der CPU-Zeit über alle zentralen Bestandteile hinweg für einen Container.

Weitere Informationen zum Format der Abfrage finden Sie unter [Abfrageformat für für Container erfasste CPU-Metriken](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers).
 
Wählen Sie auf der Registerkarte *Metriken* die Option **Abfrage hinzufügen** aus. <br>Ein Abfrageeintrag wird hinzugefügt. Jede Abfrage wird mit einem Buchstaben gekennzeichnet. 

![Neuer Abfrageeintrag](images/grafana4_query_f1.gif "Neuer Abfrageeintrag") 
	
Führen Sie die folgenden Schritte aus, um die Abfrage zu definieren:
        
1. Klicken Sie auf **Metrik auswählen**, um die Quelle anzugeben, und wählen Sie dann `ibmcloud` aus.
    
2. Klicken Sie auf **Metrik auswählen**, um den Cloudtyp anzugeben, und wählen Sie dann `public` aus.
    
3. Klicken Sie auf **Metrik auswählen**, um den Servicenamen anzugeben, und wählen Sie dann `containers-kubernetes` aus.
	
4. Klicken Sie auf **Metrik auswählen**, um die Region anzugeben, und wählen Sie dann die Region aus, in der Ihr Cluster ausgeführt wird. Beispiel: `us-south`.
    
5. Klicken Sie auf **Metrik auswählen**, um den Clusternamen anzugeben, und wählen Sie dann den Namen des Clusters aus, in dem der Container ausgeführt wird.
		
6. Klicken Sie auf **Metrik auswählen**, um die Metrikquelle anzugeben. Wählen Sie **container** aus.
		
7. Klicken Sie auf **Metrik auswählen**, um den Namensbereich anzugeben. Geben Sie dann den Namen des Namensbereichs in Ihrem Cluster ein, der dem Container zugeordnet ist.
		
8. Klicken Sie auf **Metrik auswählen**, um den Podnamen anzugeben.
	
9. Klicken Sie auf **Metrik auswählen**, um den Containernamen des Containers anzugeben, der überwacht werden soll.
	
10. Klicken Sie auf **Metrik auswählen**, um den Metriktyp auszuwählen, und klicken Sie dann auf **Metrik auswählen**, um den Metrikuntertyp festzulegen.
	
    Um beispielsweise die Nanosekunden der CPU-Zeit über alle zentralen Bestandteile hinweg für einen Container zu überwachen, wählen Sie als Typ **cpu** und als Untertyp **usage** aus.
		
	Eine Liste der CPU-Metriken finden Sie unter [CPU-Metriken für Container](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers).
    
11. Klicken Sie auf das Pluszeichen ![Symbol für das Hinzufügen](images/grafana_plus_image.gif "Pluszeichen") und wählen Sie eine Funktion aus. Sie können eine Funktion zur Transformation, zur Kombination und zur Durchführung von Berechnungen mit den Daten hinzufügen, die für eine Metrik zur Verfügung stehen.

    Sie können zum Beispiel die Funktion **alias(newName)** hinzufügen, um einen Aliasnamen für eine Metrik hinzuzufügen. Dieser Aliasname wird verwendet, um einen Zeichenfolge anstelle des Metriknamens in der Legende anzuzeigen, die in der Grafik angezeigt wird.

    Um einen Aliasnamen für Ihre Metrik hinzuzufügen, führen Sie die folgenden Schritte aus:

    1. Klicken Sie auf das Pluszeichen.
    2. Wählen Sie **Spezieller Name** aus.
    3 Wählen Sie **Aliasname** aus.
    4. Geben Sie eine Zeichenfolge ein. Zum Beispiel `My sample metric`.

## Schritt 5: Dashboard speichern
{: #cgd_step5}

Speichern Sie das Dashboard zur späteren Wiederverwendung.

1. Klicken Sie auf die Dashboardabbildung zum Speichern ![Dashboardabbildung zum Speichern](images/grafana_save_image.gif "Dashboardabbildung zum Speichern").

    ![Dashboard speichern](images/grafana_save_dashboard.gif "Dashboard speichern")

2. Geben Sie den Namen des Dashboards ein.
3. Klicken Sie auf **Speichern**.



## Nächste Schritte
{: #cgd_next_steps}

Definieren Sie einen Alert für eine Metrik. Weitere Informationen finden Sie unter [Alerts konfigurieren ](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).
