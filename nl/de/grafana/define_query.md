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


# Metrikabfrage in Grafana konfigurieren
{: #define_query}

In {{site.data.keyword.Bluemix}} werden Metriken aus ausgewählten Cloud-Services automatisch erfasst. Um diese mit {{site.data.keyword.monitoringlong}} zu überwachen, müssen Sie eine Grafana-Abfrage definieren. 
{:shortdesc}

## Schritt 1: Daten für die CF-App oder den Service erfassen, die/der überwacht werden soll
{: #step18}

Rufen Sie die folgenden Informationen für die CF-App oder den Service ab, die/der überwacht werden soll:

* Die **Region**, in der die CF-App ausgeführt wird.
* Die **Organisation**, in der die CF-App ausgeführt wird. 	
* Den **Bereich**, in dem die CF-App ausgeführt wird. 
* Den **Namen der CF-App**, die überwacht werden soll, oder den **Servicenamen**. 


## Schritt 2: Grafana starten
{: #step27}

Starten Sie Grafana von einem Browser. Weitere Informationen finden Sie unter [Von einem Web-Browser zum Grafana-Dashboard navigieren](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

Stellen Sie in Grafana sicher, dass Sie bei dem Konto, der Organisation und dem Bereich angemeldet sind, für das/die/den die CF-App oder der Service ausgeführt wird. 


## Schritt 3: Abfrage in Grafana definieren
{: #step36}

Führen Sie die folgenden Schritte aus, um ein Grafana-Dashboard zu erstellen und eine Abfrage zu definieren:

1. Erstellen Sie ein neues Dashboard.

    * Wählen Sie das Steuerelement zum Hin- und Herschalten ![Grafana-Seitenmenüleiste](images/grafana_settings.gif "Grafana-Seitenmenüleiste") in der seitlichen Menüleiste aus.
    * Wählen Sie **Dashboards** aus.
    * Klicken Sie auf **Neu**

    Ein Dashboard wird geöffnet. Das Dashboard enthält eine leere Zeile, die konfiguriert werden kann.

2. Fügen Sie eine *Grafikanzeige* hinzu.

    1. Wählen Sie **Grafik** aus.

    2. Klicken Sie auf den Grafiktitel und wählen Sie anschließend **Bearbeiten** aus.

        Die Registerkarte *Metriken* wird angezeigt. Sie können hier die Standarddatenquelle sehen.

3. Definieren Sie die Abfrage, die die in der Grafik angezeigten Daten filtert. 

    Wählen Sie auf der Registerkarte *Metriken* die Option **Abfrage hinzufügen** aus. <br>Ein Abfrageeintrag wird hinzugefügt. Jede Abfrage wird mit einem Buchstaben gekennzeichnet.
    
    ![Neuer Abfrageeintrag](images/grafana4_query_f1.gif "Neuer Abfrageeintrag")
        
    1. Klicken Sie auf **Metrik auswählen** und wählen Sie die Quelle `ibmcloud` aus.
    
    2. Klicken Sie auf **Metrik auswählen** und wählen Sie den Cloudtyp `public` aus.
    
    3. Klicken Sie auf **Metrik auswählen** und wählen Sie den Servicenamen, beispielsweise `cloud-foundry` für CF-App-Metriken oder `message hub` für {{site.data.keyword.messagehub}}-Metriken, aus.
    
    4. Klicken Sie auf **Metrik auswählen** und wählen Sie dann die Region aus, in der Sie arbeiten, beispielsweise `ng` für die Region 'USA (Süden)'.
    
    5. Wählen Sie die Servicefelder aus, die für den Service oder die CF-App gelten, der/die überwacht werden soll.

        <table>
          <caption>Abfrageformate für Metriken pro Service oder CF-App</caption>
          <tr>
            <th>Servicename</th>
            <th>Link zum Abfrageformat der Metrik</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Abfrageformat für für Container erfasste CPU-Metriken](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers) </br>[Abfrageformat für für Worker erfasste Lademetriken](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers) </br>[Abfrageformat für für Container erfasste Speichermetriken](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)</td> 
          </tr>
          <tr>
            <td>CF-Apps</td>
            <td>[Abfrageformat für CF-Apps](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format)</td> 
          </tr>
        </table>

        Wählen Sie für eine CF-App beispielsweise Folgendes aus:
    
        Klicken Sie auf **Metrik auswählen** und wählen Sie dann den CF-App-Namen aus, beispielsweise `logtester`.
    
        Klicken Sie auf **Metrik auswählen** und wählen Sie dann den Index der CF-App-Instanz aus, beispielsweise `0`.

        Klicken Sie auf **Metrik auswählen** und wählen Sie dann `Container` aus.
    
    9. Klicken Sie auf **Metrik auswählen** und wählen Sie dann ein Metriktyp aus. Beispiel: **cpu** für CPU-Metriken, **memory** für Speichermetriken und **disk** für Plattenmetriken. 

        **Hinweis:** Überspringen Sie diesen Schritt für CF-Apps. 

    10. Klicken Sie auf **Metrik auswählen** und wählen Sie dann eine Metrik aus. 

        <table>
          <caption>Liste der Metriken pro Service oder CF-App</caption>
          <tr>
            <th>Servicename</th>
            <th>Link zu Metriken</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[CPU-Metriken](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Plattenmetriken](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[Speichermetriken](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>CF-Apps</td>
            <td>[CPU-Metriken](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics)  </br>[Plattenmetriken](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[Speichermetriken](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Metriken für einen Kafka-Abschnitt](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_topic_metrics) </br>[Metriken für eine Kafka-Partition](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. Klicken Sie auf das Pluszeichen ![Symbol für das Hinzufügen](images/grafana_plus_image.gif "Pluszeichen") und wählen Sie eine Funktion aus. Sie können eine Funktion zur Transformation, zur Kombination und zur Durchführung von Berechnungen mit den Daten hinzufügen, die für eine Metrik zur Verfügung stehen.
        
        Sie können zum Beispiel die Funktion **alias(newName)** hinzufügen, um einen Aliasnamen für eine Metrik hinzuzufügen. Dieser Aliasname wird verwendet, um einen Zeichenfolge anstelle des Metriknamens in der Legende anzuzeigen, die in der Grafik angezeigt wird.
        
        Um einen Aliasnamen für Ihre Metrik hinzuzufügen, führen Sie die folgenden Schritte aus:
        
        1. Klicken Sie auf das Pluszeichen.
        2. Wählen Sie **Spezieller Name** aus. 
        3 Wählen Sie **Aliasname** aus.
        4. Geben Sie eine Zeichenfolge ein. Zum Beispiel `My sample metric`.


## Schritt 4: Dashboard für spätere Wiederverwendung speichern
{: #step44}

Führen Sie die folgenden Schritte aus:

1. Klicken Sie auf die Dashboardabbildung zum Speichern ![Dashboardabbildung zum Speichern](images/grafana_save_image.gif "Dashboardabbildung zum Speichern").
2. Geben Sie den Namen des Dashboards ein.
3. Klicken Sie auf **Speichern**.
