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

# Alerts in Grafana konfigurieren
{: #config_alerts_grafana}

Der {{site.data.keyword.monitoringshort}}-Service stellt ein abfragebasiertes Alertausgabesystem zur Verfügung. Sie können Alerts in Grafana für Dashboards konfigurieren, die nicht über Vorlagenvariablen verfügen. 
{:shortdesc}

Führen Sie die folgenden Schritte aus, um einen Alert für eine Metrikabfrage über die Gafana-Benutzerschnittstelle zu konfigurieren:

1. Starten Sie Grafana.
2. Definieren Sie mindestens einen Benachrichtigungskanal.
3. Erstellen Sie ein Grafana-Dashboard, das eine Grafik und mindestens eine Abfragemetrik umfasst. 
4. Konfigurieren Sie den Alert über die Registerkarte **Alerts** für eine Grafana-Grafik.

## Schritt 1: Grafana starten
{: #step1_cag1}

Starten Sie Grafana von einem Browser. Geben Sie beispielsweise die folgende URL ein, um Grafana in der Region 'USA (Süden)' zu öffnen: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

Eine Liste der Grafana-URLs nach Region finden Sie unter [URLs für den {{site.data.keyword.monitoringshort}}-Service](/docs/services/cloud-monitoring/monitoring_ov.html#region).

## Schritt 2: Mindestens einen Benachrichtigungskanal definieren
{: #step2_cag2}

Führen Sie die folgenden Schritte aus:

1. Wählen Sie in Grafana die Seitenmenüleiste aus.

2. Wählen Sie **Alerting > Benachrichtigungskanäle > Neuer Kanal** aus.

3. Geben Sie die Daten für den neuen Kanal ein. Fügen Sie beispielsweise einen Benachrichtungskanal für E-Mails hinzu.

<table>
  <caption>E-Mail-Benachrichtigungsmethode und Daten, die Sie zum Erstellen eines neuen Kanals eingeben müssen</caption>
  <tr>
     <th>Feld</th>
     <th>Beschreibung</th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Name des Benachrichtigungskanals. Dieser Wert muss eindeutig sein.</td>
  </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Zusätzliche Informationen, die für Dokumentationszwecke eingeschlossen werden können.</td>
  </tr>
  <tr>
    <td>Typ</td>
    <td>Wählen Sie **E-Mail** aus.</td>
  </tr>
  <tr>
    <td>E-Mail-ID</td>
    <td>Geben Sie die E-Mail-Adresse des Empfängers ein. </br>Sie können mehrere, durch Kommas getrennte E-Mail-Adressen angeben.</td>
  </tr>
</table>

<table>
  <caption>Webhook-Benachrichtigungsmethode und Daten, die Sie zum Erstellen eines neuen Kanals eingeben müssen</caption>
  <tr>
     <th>Feld</th>
     <th>Beschreibung</th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Name des Benachrichtigungskanals. Dieser Wert muss eindeutig sein.</td>
  </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Zusätzliche Informationen, die für Dokumentationszwecke eingeschlossen werden können.</td>
  </tr>
  <tr>
    <td>Typ</td>
    <td>Wählen Sie **Webhook** aus.</td>
  </tr>
  <tr>
    <td>Webhook-POST-URL</td>
    <td>Geben Sie die URL ein, bei der der POST vorgenommen werden soll.</td>
  </tr>
  <tr>
    <td>Webhook-Header</td>
    <td>Geben Sie alle Header ein.</td>
  </tr>
  <tr>
    <td>Webhook-Abfrageparameter</td>
    <td>Geben Sie alle Abfrageparameter ein.</td>
  </tr>
</table>

<table>
  <caption>PagerDuty-Benachrichtigungsmethode und Daten, die Sie zum Erstellen eines neuen Kanals eingeben müssen</caption>
  <tr>
     <th>Feld</th>
     <th>Beschreibung</th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Name des Benachrichtigungskanals. Dieser Wert muss eindeutig sein.</td>
  </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Zusätzliche Informationen, die für Dokumentationszwecke eingeschlossen werden können.</td>
  </tr>
  <tr>
    <td>Typ</td>
    <td>Wählen Sie **PagerDuty** aus.</td>
  </tr>
  <tr>
    <td>PagerDuty-API-Schlüssel</td>
    <td>Geben Sie den PagerDuty-Schlüssel ein.</td>
  </tr>
</table>

## Schritt 3: Metrik definieren
{: #step3_cag3}

Führen Sie die folgenden Schritte aus, um ein neues Dashboard zu erstellen:

1. Wählen Sie das Steuerelement zum Hin- und Herschalten ![Grafana-Seitenmenüleiste](images/grafana_settings.gif "Grafana-Seitenmenüleiste") in der seitlichen Menüleiste aus.
2. Wählen Sie **Dashboards** aus.
3. Klicken Sie auf **Neu**

Ein Dashboard wird geöffnet. Das Dashboard enthält eine leere Zeile, die konfiguriert werden kann. 

Fügen Sie als Nächstes eine Metrikabfrage hinzu:

1. Fügen Sie eine *Grafikanzeige* hinzu.
2. Wählen Sie **Grafik** aus.
3. Klicken Sie auf den Grafiktitel und wählen Sie anschließend **Bearbeiten** aus.
    
    Die Registerkarte *Metriken* wird angezeigt. Sie können hier die Standarddatenquelle sehen.
    
4. Definieren Sie die Metrikabfrage, die die in der Grafik angezeigten Daten filtert. 


## Schritt 4: Alert definieren
{: #step4_cag4}

Führen Sie die folgenden Schritte aus, um einen Alert in der Grafana-Benutzerschnittstelle zu definieren:

1. Wählen Sie die Registerkarte **Alert** aus.
2. Definieren Sie im Abschnitt für die **Alertkonfiguration** die Regel, die die Bedingungen festlegt, unter denen eine Alertdefinition generiert wird.

    Konfigurieren Sie das Feld **Alle bewerten** und den Abschnitt mit den **Bedingungen**.

3. Wählen Sie im Abschnitt für die **Benachrichtigungen** mindestens einen Benachrichtigungskanal aus.

**Anmerkung:** 

* Wenn eine Bedingung festgelegt wurde, wird in der Grafik eine rote Linie angezeigt, die den Schwellenwertsatz definiert. Sie können sie zum Ändern in die Grafik ziehen.
* Sobald der Alert erstellt wurde, können Sie ihn bei Bedarf über die Alert-API ändern.
* Wenn Sie **Löschen** wählen, wird der Alert gelöscht.

## Nächster Schritt: Sicherstellen, dass ein Alert generiert wird
{: #next_cag5}

Wenn Sie beispielsweise einen Benachrichtigungskanal für E-Mails erstellt haben, überprüfen Sie Ihre E-Mails.

Suchen Sie nach E-Mails mit dem Absender **IBM Cloud Monitoring**.

Eine E-Mail enthält Informationen zu dem ausgelösten Alert und einen Link zum Grafana-Dashboard, in dem Sie sich die Situation ansehen können.

Beispiel:

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


