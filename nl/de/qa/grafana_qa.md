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



# Häufig gestellte Fragen zur Verwendung von Grafana
{: #grafana_qa}

Hier sind die Antworten auf häufig gestellte Fragen zur Verwendung von Grafana mit dem {{site.data.keyword.monitoringshort}}-Service. 
{:shortdesc}

* [Ich kann Alerts nicht im Grafana-Dashboard sehen, die ich mithilfe der Alert-API definiert habe](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#alerts1)
* [Ich erhalte den Fehler BXNMSAL41E, wenn ich versuche, eine Änderung am Grafana-Dashboard zu speichern](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL41E)
* [Ich erhalte den Fehler BXNMSAL36E, wenn ich versuche, eine Änderung zu speichern, nachdem ich einen Alert zum Grafana-Dashboard hinzugefügt habe](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL36E)
* [Ich erhalte den Fehler 404, wenn ich mich bei der Webbenutzerschnittstelle des Überwachungsservice anmelde](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#404)
* [Ich habe gerade JSON-Daten für ein Grafana-Dashboard hochgeladen. Warum wird meine Bildlaufleiste nicht mehr angezeigt?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#2)


## Ich kann Alerts nicht im Grafana-Dashboard sehen, die ich mithilfe der Alert-API definiert habe
{: #alerts1}

Alerts, die Sie mithilfe der Alert-API definieren, werden nicht auf der Registerkarte mit den Alerts in Grafana angezeigt. Um Alerts in Grafana sehen zu können, müssen Sie sie direkt in einem Grafana-Dashboard definieren.

Weitere Informationen finden Sie unter [Alerts in Grafana konfigurieren](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-config_alerts_grafana#config_alerts_grafana).

## Ich erhalte den Fehler BXNMSAL41E, wenn ich versuche, eine Änderung am Grafana-Dashboard zu speichern
{: #BXNMSAL41E}

Sie können Benachrichtigungskanäle und Alerts in Grafana definieren. Wenn Sie einen Benachrichtigungskanal in Grafana löschen und Sie die Regel zum Entfernen dieser Benachrichtigung nicht aktualisiert haben, erhalten Sie den Fehler **BXNMSAL41E**, wenn Sie versuchen, das Grafana-Dashboard zu speichern.

Um das Problem zu beheben, aktualisieren Sie die Regel mithilfe der Alert-API und versuchen Sie, das Dashboard erneut zu speichern. Wenn Sie die Regel aktualisieren, entfernen Sie den Benachrichtigungskanal, der gelöscht wurde.

Weitere Informationen finden Sie unter [Alert-API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction).

## Ich erhalte den Fehler BXNMSAL36E, wenn ich versuche, eine Änderung zu speichern, nachdem ich einen Alert zum Grafana-Dashboard hinzugefügt habe
{: #BXNMSAL36E}

Wenn Sie das Kontingent für die Domäne erschöpfen, für die Sie Metriken im {{site.data.keyword.monitoringshort}}-Service überwachen, erhalten Sie den folgenden Fehler: **BXNMSAL36E**

Aktualisieren Sie Ihren Plan und versuchen Sie es erneut.

Weitere Informationen zur Vorgehensweise beim Aktualisieren des Plans finden Sie unter [Plan ändern](/docs/services/cloud-monitoring/plan?topic=cloud-monitoring-change_plan#change_plan).


## Ich erhalte den Fehler 404, wenn ich mich bei der Webbenutzerschnittstelle des Überwachungsservice mit dem UUA-Authentifizierungsmodell anmelde
{: #404}

Wenn Sie den Fehler 404 erhalten, nachdem Sie versucht haben, sich bei der Webbenutzerschnittstelle (Grafana) des {{site.data.keyword.monitoringshort}}-Service anzumelden, überprüfen Sie, dass der Bereich vorhanden ist und dass Sie darauf zugreifen dürfen.

Wenn Sie das [UAA-Authentifizierungsmodell](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa) für den Zugriff auf den {{site.data.keyword.monitoringshort}}-Service verwenden, müssen Sie dieselbe Benutzer-ID und dasselbe Kennwort wie für die Anmeldung bei der {{site.data.keyword.Bluemix_notm}}-Konsole verwenden. 

Um zu überprüfen, dass Sie Zugriff auf das Konto, die Organisation und den Bereich haben, in dem Sie sich anmelden möchten, melden Sie sich an der {{site.data.keyword.Bluemix_notm}}-Konsole an und wechseln in den betreffenden Bereich. 

Sie können auch die Befehlszeile verwenden, um zu überprüfen, ob Sie Zugriff auf diesen Bereich haben. Führen Sie folgenden Befehl aus, um sich in einer Region, einer Organisation und einem Bereich von {{site.data.keyword.Bluemix_notm}} anzumelden:

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

Befolgen Sie die Anweisungen. Geben Sie Ihre {{site.data.keyword.Bluemix_notm}}-Berechtigungsnachweise ein, wählen Sie eine Organisation und einen Bereich aus.


## Ich habe gerade JSON-Daten für ein Grafana-Dashboard hochgeladen. Warum wird meine Bildlaufleiste nicht mehr angezeigt?
{: #2}

Dies ist ein Fehler in Grafana, der die Bildlaufleiste nach dem Import eines Dashboards ausblendet. 

Speichern Sie das Dashboard nach dem Importieren, um die Bildlaufleiste wieder einzublenden. 








