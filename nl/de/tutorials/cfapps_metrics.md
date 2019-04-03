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


# Metriken in Grafana für eine CF-App analysieren
{: #cfapps_metrics}

In diesem Lernprogramm erfahren Sie, wie Sie mit dem {{site.data.keyword.monitoringlong}}-Service die Leistung einer CF-App (Cloud Foundry) überwachen können, die in {{site.data.keyword.Bluemix_notm}} Public ausgeführt wird. 
{:shortdesc}


## Lernziele
{: #objectives}

Erfahren Sie, wie Sie nach Metriken für eine CF-App suchen und diese analysieren:

1. Stellen Sie eine CF-App bereit.
2. Starten Sie Grafana und legen Sie die {{site.data.keyword.monitoringshort}}-Domäne fest, in der Sie die Metriken für die CF-App anzeigen können.
3. Suchen und analysieren Sie Metriken für eine CF-App, die in einem Bereich von {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Für dieses Lernprogramm wird angenommen, dass Sie in der Region 'USA (Süden)' arbeiten.


## Voraussetzungen
{: #cfapps_prereqs}

1. Sie müssen ein Mitglied oder ein Eigner eines {{site.data.keyword.Bluemix_notm}}-Kontos mit Berechtigungen zum Bereitstellen von Services in einem Bereich, Bereitstellen von CF-Apps und Abfragen von Metriken in {{site.data.keyword.Bluemix_notm}} über den {{site.data.keyword.monitoringshort}}-Service sein.

    Ihre Benutzer-ID für {{site.data.keyword.Bluemix_notm}} muss über eine CF-Rolle für den Bereich verfügen, in dem der {{site.data.keyword.monitoringshort}}-Service und die CF-App bereitgestellt werden. Die dafür erforderlich Rolle ist der *Entwickler*.
    
    Weitere Informationen finden Sie unter [Einem Benutzer eine CF-Rolle über die IBM Cloud-Benutzerschnittstelle zuweisen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#grant_permissions_ui_space).

2. Stellen Sie den {{site.data.keyword.monitoringshort}}-Service in einem Bereich bereit, für den Sie über Berechtigungen zum Bereitstellen von Services in der Region 'USA (Süden)' verfügen.

    Weitere Informationen finden Sie in [{{site.data.keyword.monitoringshort}}-Service bereitstellen](/docs/services/cloud-monitoring/how-to?topic=cloud-monitoring-provision#provision).

## Schritt 1: Dem Benutzer Berechtigungen für die Arbeit mit CF-Apps und dem {{site.data.keyword.monitoringshort}}-Service erteilen
{: #cfapps_step1}

Um einem Benutzer Berechtigungen für die Bereitstellung von CF-Apps in einem Bereich oder zum Anzeigen von Metriken in einer Bereichsdomäne zu erteilen, müssen Sie diesem Benutzer eine CF-Rolle zuweisen, die die Aktionen beschreibt, die der Benutzer mithilfe des {{site.data.keyword.monitoringshort}}-Service in dem Bereich und in {{site.data.keyword.Bluemix_notm}} durchführen kann. 

**Hinweis:** Im Rahmen dieses Lernprogramms wird angenommen, dass Sie der Kontoeigner sind oder über Berechtigungen zum Hinzufügen von Rollen zu Ihrer Benutzer-ID verfügen. Wenn Sie diese Berechtigungen nicht haben, bitten Sie den Kontoeigner, diesen Schritt durchzuführen.

Führen Sie die folgenden Schritte aus, um einem Benutzer entsprechende Berechtigungen zum Durchführen des Lernprogramms zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten>Konto>Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste der Benutzer mit ihren E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Suchen Sie in der Liste nach Ihrem Benutzernamen und klicken Sie im Menü *Aktionen* auf **Benutzer verwalten**.

4. Wählen Sie **Cloud Foundry-Zugriff** und anschließend **Organisation zuweisen** aus.

5. Geben Sie die folgenden Werte ein: 

    <table>
      <caption>Liste der auszuwählenden Werte</caption>
      <tr>
        <th>Feld</th>
        <th>Wert</th>
      </tr>
      <tr>
        <td>Organisation</td>
        <td>MyOrg</td>
      </tr>
      <tr>
        <td>Organisationsrolle</td>
        <td>Keine Organisationsrolle</td>
      </tr>
      <tr>
        <td>Region</td>
        <td>USA (Süden)</td>
      </tr>
      <tr>
        <td>Bereich</td>
        <td>dev</td>
      </tr>
      <tr>
        <td>Bereichsrolle</td>
        <td>Entwickler</td>
      </tr>
    </table>
	
6. Klicken Sie auf **Rolle speichern**.
 

## Step 2: CF-App bereitstellen
{: #cfapps_step2}

Führen Sie die folgenden Schritte über die {{site.data.keyword.Bluemix_notm}}-Konsole aus:

1. Klicken Sie in der {{site.data.keyword.Bluemix_notm}}-Symbolleiste auf **Katalog**.

2. Klicken Sie auf **Cloud Foundry-Apps > Liberty for Java**. 

3. Geben Sie die folgenden Informationen ein:

    * **App-Name**: Name der Anwendung. Dieser muss eindeutig sein.
    * **Region**: Wählen Sie 'USA (Süden)' aus.
    * **Organisation**: Wählen Sie die Organisation aus, in der Sie den {{site.data.keyword.monitoringshort}}-Service bereitgestellt haben.
    * **Bereich**: Wählen Sie den Bereich aus, in dem Sie den {{site.data.keyword.monitoringshort}}-Service bereitgestellt haben.

3. Klicken Sie auf **Erstellen**.

Sobald die CF-App ausgeführt wird, werden Metriken erfasst und an den {{site.data.keyword.monitoringshort}}-Service weitergeleitet.

## Schritt 3: Grafana starten und die Metrikdomäne festlegen
{: #cfapps_step3}

Starten Sie Grafana über einen Browser und legen Sie die {{site.data.keyword.monitoringshort}}-Domäne fest, in der Sie die Metriken für die CF-App anzeigen können.

1. Starten Sie Grafana über einen Browser. 

    Geben Sie die URL für den {{site.data.keyword.monitoringshort}}-Service für die Region an, in der der {{site.data.keyword.monitoringshort}}-Service bereitgestellt wurde.
    
    Informationen zum Abrufen der URLs nach Region finden Sie unter [URLs für den Überwachungsservice](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

    Starten Sie zum Beispiel für die Region 'USA (Süden)': [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Legen Sie die {{site.data.keyword.monitoringshort}}-Domäne fest, in der Sie die Clustermetriken anzeigen können.

    Wählen Sie in Grafana Ihre ID aus. Stellen Sie dann sicher, dass Sie sich im richtigen Konto befinden, und wählen Sie `Domäne = Bereich` aus.

    Stellen Sie sicher, dass der Organisationsname und der Bereichsname den Namen entsprechen, für die Sie die CF-Apps und den {{site.data.keyword.monitoringshort}}-Service bereitstellt haben.


## Schritt 4: Grafana-Dashboard für die Überwachung einer Metrik erstellen
{: #cfapps_step4}


Führen Sie die folgenden Schritte aus, um ein neues Dashboard in Grafana zu erstellen:

1. Wählen Sie das Steuerelement zum Hin- und Herschalten ![Grafana-Seitenmenüleiste](images/grafana_settings.gif "Grafana-Seitenmenüleiste") in der seitlichen Menüleiste aus.
2. Wählen Sie **Dashboards** aus.
3. Klicken Sie auf **Neu**

Ein Dashboard wird geöffnet. Das Dashboard enthält eine leere Zeile, die konfiguriert werden kann.

![Grafana-Dashboard](images/grafana4_f1.gif "Grafana-Dashboard")

Fügen Sie in Grafana Zeilen hinzu, um das Dashboard in Abschnitte zu unterteilen. Eine Zeile gruppiert eine oder mehrere Anzeigen. Innerhalb einer Zeile ist eine Anzeige die kleinste Visualisierungseinheit, die Sie für die Anzeige von Daten für eine Metrik konfigurieren können. Sie können zum Beispiel eine Diagrammanzeige oder eine Tabellenanzeige auswählen. Sie können Anzeigen ziehen und übergeben, um sie in einem Dashboard neu anzuordnen. Die in den Anzeigen angezeigten Daten werden über Abfragen konfiguriert. Sie können eine oder mehrere Abfragen in einer Anzeige definieren. Jede Abfrage stellt eine andere Gruppe von Daten dar. Sie können auch den Zeitraum für eine Anzeige festlegen. Normalerweise wird der Zeitraum durch das Zeitauswahlfeld im *Dashboard* festgelegt.

Definieren Sie die Abfrage, die die in der Grafik angezeigten Daten filtert. Mit dieser Abfrage wird der Prozentsatz der CPU-Auslastung im Hinblick auf das Limit des Containers überwacht.

Informationen zum Format der Abfrage finden Sie unter [Grafana-Abfrageformat für CF-Apps](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-cfapps_metrics_format#cfapps_metrics_format).
    
1. Fügen Sie eine *Grafik*anzeige hinzu, um die Nanosekunden der CPU-Zeit über alle zentralen Bestandteile für einen Container zu überwachen.
    
    1. Wählen Sie **Grafik** aus.
    
    2. Klicken Sie auf den Grafiktitel und wählen Sie anschließend **Bearbeiten** aus.
    
        Die Registerkarte *Metriken* wird angezeigt. Sie können hier die Standarddatenquelle sehen.
    
        ![Grafikanzeige mit Konfigurationsregisterkarten](images/grafana4_f2.gif "Grafikanzeige mit Konfigurationsregisterkarten")
    
2. Definieren Sie die Abfrage, die die in der Grafik angezeigten Daten filtert. 
    
    Wählen Sie auf der Registerkarte *Metriken* die Option **Abfrage hinzufügen** aus. <br>Ein Abfrageeintrag wird hinzugefügt. Jede Abfrage wird mit einem Buchstaben gekennzeichnet.
    
    ![Neuer Abfrageeintrag](images/grafana4_query_f1.gif "Neuer Abfrageeintrag")
        
    1. Klicken Sie auf **Metrik auswählen** und wählen Sie die Quelle `ibmcloud` aus.
    
    2. Klicken Sie auf **Metrik auswählen** und wählen Sie den Cloudtyp `public` aus.
    
    3. Klicken Sie auf **Metrik auswählen** und wählen Sie dann `cloud-foundry` aus.
    
    4. Klicken Sie auf **Metrik auswählen** und wählen Sie dann die Region aus, in der Sie arbeiten, beispielsweise `us-south` für die Region 'USA (Süden)'.
    
    5. Klicken Sie auf **Metrik auswählen** und wählen Sie dann den CF-App-Namen aus, beispielsweise `logtester`.
    
    6. Klicken Sie auf **Metrik auswählen** und wählen Sie dann den Index der CF-App-Instanz aus, beispielsweise `0`.

    7. Klicken Sie auf **Metrik auswählen** und wählen Sie dann `container` aus.
    
    9. Klicken Sie auf **Metrik auswählen** und wählen Sie dann eine Metrik aus. Um den *Prozentsatz der CPU-Auslastung* eines Containers, wählen Sie `cpu-utilization` aus.

    10. Klicken Sie auf das Pluszeichen ![Symbol für das Hinzufügen](images/grafana_plus_image.gif "Pluszeichen") und wählen Sie eine Funktion aus. Sie können eine Funktion zur Transformation, zur Kombination und zur Durchführung von Berechnungen mit den Daten hinzufügen, die für eine Metrik zur Verfügung stehen.
        
        Sie können zum Beispiel die Funktion **alias(newName)** hinzufügen, um einen Aliasnamen für eine Metrik hinzuzufügen. Dieser Aliasname wird verwendet, um einen Zeichenfolge anstelle des Metriknamens in der Legende anzuzeigen, die in der Grafik angezeigt wird.
        
        Um einen Aliasnamen für Ihre Metrik hinzuzufügen, führen Sie die folgenden Schritte aus:
        
        1. Klicken Sie auf das Pluszeichen.
        2. Wählen Sie **Spezieller Name** aus. 
        3 Wählen Sie **Aliasname** aus.
        4. Geben Sie eine Zeichenfolge ein. Zum Beispiel `My sample metric`.
        

## Schritt 5: Dashboard speichern
{: #cfapps_step5}

Speichern Sie das Dashboard zur späteren Wiederverwendung.

1. Klicken Sie auf die Dashboardabbildung zum Speichern ![Dashboardabbildung zum Speichern](images/grafana_save_image.gif "Dashboardabbildung zum Speichern").

    ![Dashboard speichern](images/grafana_save_dashboard.gif "Dashboard speichern")

2. Geben Sie den Namen des Dashboards ein.
3. Klicken Sie auf **Speichern**.


## Nächste Schritte
{: #cfapps_next_steps}

Definieren Sie einen Alert für eine Metrik. Weitere Informationen finden Sie unter [Alerts konfigurieren ](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).
