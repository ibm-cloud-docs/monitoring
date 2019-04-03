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



# Speichermetriken für einen Container in Grafana konfigurieren
{: #config_mem_container}

In {{site.data.keyword.Bluemix}} werden ausgewählte Speichermetriken für einen Container automatisch erfasst. Um diese mit {{site.data.keyword.monitoringlong}} zu überwachen, müssen Sie eine Grafana-Abfrage definieren. 
{:shortdesc}

Eine Liste der Speichermetriken finden Sie unter [Speichermetriken](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics).


## Schritt 1: Daten für den Container erfassen, der überwacht werden soll
{: #step17}

Rufen Sie die folgenden Informationen für den Container ab, der überwacht werden soll:

* Die **Region**, in der der Cluster ausgeführt wird.
* Den **Clusternnamen** des Clusters, in dem der Container ausgeführt wird. 
* Den **Namensbereich**, in dem der Container bereitgestellt wird. 

    Ein Namensbereich wird zum Gruppieren von Clusterressourcen verwendet.
	
* Den **Podnamen**, der dem zu überwachenden Container zugeordnet ist. 

    Ein Pod definiert eine Gruppe mit mindestens einem Container mit gemeinsam genutztem Speicher und Netz. Außerdem enthält er Details darüber, wie die Container im Cluster ausgeführt werden sollen.
	
* Den **Containernamen** des Containers, der überwacht werden soll.

Ermitteln Sie, ob Metriken an eine Bereichsdomäne oder an die Kontodomäne weitergeleitet werden.

Um herauszufinden, wohin der Cluster Metriken weiterleitet, führen Sie den folgenden Befehl aus:

```
$ ibmcloud cs cluster-get ClusterName --json
```
{: codeblock}

Dabei ist *ClusterName* der Name des Clusters.

In der Ausgabe enthalten die folgenden Felder die Informationen darüber, wohin Metriken weitergeleitet werden:

* **logOrg** definiert die ID einer CF-Organisation.
* **logOrgName** definiert den Namen einer CF-Organisation.
* **logSpace** definiert die ID eines CF-Bereichs.
* **logSpaceName** definiert den Namen eines CF-Bereichs.

Wenn die Felder leer sind, werden Metriken an die Kontodomäne weitergeleitet.
Wenn in den Feldern eine CF-Organisation und ein CF-Bereich angegeben ist, werden Metriken an die Bereichsdomäne weitergeleitet, die diesem Bereich zugeordnet ist.

## Schritt 2: Grafana starten
{: #step26}

Starten Sie Grafana von einem Browser. Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

Stellen Sie in Grafana sicher, dass Sie bei dem Konto angemeldet sind, für das der Cluster ausgeführt wird. 

1. Starten Sie Grafana über einen Browser. 

    Geben Sie die {{site.data.keyword.monitoringshort}}-Service-URL für die Region ein, in der Sie den Cluster erstellt haben. 
    
    Informationen zum Abrufen der URLs nach Region finden Sie unter [URLs für den Überwachungsservice](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Starten Sie zum Beispiel für die Region 'USA (Süden)': [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Legen Sie die {{site.data.keyword.monitoringshort}-Domäne fest, in der Sie die Clustermetriken anzeigen können.

    Wählen Sie in Grafana Ihre ID aus. Stellen Sie dann sicher, dass Sie sich im richtigen Konto befinden und wählen Sie eine Domäne aus.

    Cluster, denen ein CF-Bereich zugeordnet ist, leiten Metriken an die Bereichsmetrikdomäne weiter. Wählen Sie `Domäne = Bereich` sowie die Organisation und den Bereich aus, die/der dem Cluster zugeordnet ist.

    Cluster, die auf Kontoebene erstellt werden, leiten Metriken an die Kontometrikdomäne weiter. Wählen Sie `Domäne = Konto` aus.




## Schritt 3: Abfrage in Grafana für eine CPU-Metrik definieren
{: #step35}

Führen Sie die folgenden Schritte aus, um ein Grafana-Dashboard zu erstellen und eine Abfrage zum Überwachen der CPU-Auslastung eines Workers zu erstellen:

1. Erstellen Sie ein neues Dashboard.

    * Wählen Sie das Steuerelement zum Hin- und Herschalten ![Grafana-Seitenmenüleiste](images/grafana_settings.gif "Grafana-Seitenmenüleiste") in der seitlichen Menüleiste aus.
    * Wählen Sie **Dashboards** aus.
    * Klicken Sie auf **Neu**

    Ein Dashboard wird geöffnet. Das Dashboard enthält eine leere Zeile, die konfiguriert werden kann.

2. Fügen Sie eine *Grafikanzeige* hinzu, um die CPU-Metrik für einen Pod zu überwachen.

    1. Wählen Sie **Grafik** aus.

    2. Klicken Sie auf den Grafiktitel und wählen Sie anschließend **Bearbeiten** aus.

        Die Registerkarte *Metriken* wird angezeigt. Sie können hier die Standarddatenquelle sehen.

3. Definieren Sie die Abfrage, die die in der Grafik angezeigten Daten filtert. 

    Weitere Informationen zum Format der Abfrage finden Sie unter [Abfrageformat für für Container erfasste Speichermetriken](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers).

    Wählen Sie auf der Registerkarte *Metriken* die Option **Abfrage hinzufügen** aus. <br>Ein Abfrageeintrag wird hinzugefügt. Jede Abfrage wird mit einem Buchstaben gekennzeichnet.
	
	Führen Sie die folgenden Schritte aus, um die Abfrage zu definieren:

    1. Klicken Sie auf **Metrik auswählen**, um die Quelle anzugeben, und wählen Sie dann `ibmcloud` aus.
    
    2. Klicken Sie auf **Metrik auswählen**, um den Cloudtyp anzugeben, und wählen Sie dann `public` aus.
    
    3. Klicken Sie auf **Metrik auswählen**, um den Servicenamen anzugeben, und wählen Sie dann `containers-kubernetes` aus.
	
    4. Klicken Sie auf **Metrik auswählen**, um die Region anzugeben, und wählen Sie dann die Region aus, in der Ihr Cluster ausgeführt wird. Wählen Sie beispielsweise `us-south` für einen Cluster aus, der in der Region 'USA (Süden)' verfügbar ist.
    
    5. Klicken Sie auf **Metrik auswählen**, um den Clusternamen anzugeben, und wählen Sie dann den Namen des Clusters aus, in dem der Container ausgeführt wird.
		
	6. Klicken Sie auf **Metrik auswählen**, um die Metrikquelle anzugeben. Wählen Sie **Container** aus.
		
	7. Klicken Sie auf **Metrik auswählen**, um den Namensbereich anzugeben. Geben Sie dann den Namen des Namensbereichs in Ihrem Cluster ein, der dem Container zugeordnet ist.
		
	8. Klicken Sie auf **Metrik auswählen**, um den Podnamen anzugeben.
	
	9. Klicken Sie auf **Metrik auswählen**, um den Containernamen des Containers anzugeben, der überwacht werden soll.
	
	10. Klicken Sie auf **Metrik auswählen**, um den Metriktyp auszuwählen, und klicken Sie dann auf **Metrik auswählen**, um den Metrikuntertyp festzulegen.
	
	    Um beispielsweise dem Byteumfang des Speichers zu überwachen, die aktuell von einem Container belegt wird, wählen Sie als Typ **Speicher** und **aktuell** als Untertyp aus.
	
	    Eine Liste der Speichermetriken finden Sie unter [Speichermetriken für Container](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics) 
	
	11. Klicken Sie auf das Pluszeichen ![Symbol für das Hinzufügen](images/grafana_plus_image.gif "Pluszeichen") und wählen Sie eine Funktion aus. Sie können eine Funktion zur Transformation, zur Kombination und zur Durchführung von Berechnungen mit den Daten hinzufügen, die für eine Metrik zur Verfügung stehen.

        Sie können zum Beispiel die Funktion **alias(newName)** hinzufügen, um einen Aliasnamen für eine Metrik hinzuzufügen. Dieser Aliasname wird verwendet, um einen Zeichenfolge anstelle des Metriknamens in der Legende anzuzeigen, die in der Grafik angezeigt wird.

        Um einen Aliasnamen für Ihre Metrik hinzuzufügen, führen Sie die folgenden Schritte aus:

        1. Klicken Sie auf das Pluszeichen.
        2. Wählen Sie **Spezieller Name** aus.
        3 Wählen Sie **Aliasname** aus.
        4. Geben Sie eine Zeichenfolge ein. Zum Beispiel `My sample metric`.

4. Speichern Sie das Dashboard zur späteren Wiederverwendung.

    1. Klicken Sie auf die Dashboardabbildung zum Speichern ![Dashboardabbildung zum Speichern](images/grafana_save_image.gif "Dashboardabbildung zum Speichern").
    2. Geben Sie den Namen des Dashboards ein.
    3. Klicken Sie auf **Speichern**.

	
