---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, sysdig rest api

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


# Die Sysdig-REST-API verwalten
{: #api}

Verwenden Sie die Sysdig-REST-API, um Routineaufgaben zu automatisieren und Benachrichtigungen zu überwachen.
{:shortdesc}

Wenn Sie die API aus Ihren angepassten Scripts oder Programmen verwenden, müssen Sie ein Sysdig-Token verwenden, um sich bei der {{site.data.keyword.mon_full_notm}}-Instanz zu authentifizieren. 
{: tip}

## Dashboard mithilfe der API erstellen
{: #api_create_dashboard}

Sie können ein Dashboard erstellen, indem Sie ein vorhandenes Dashboard duplizieren.  

Führen Sie die folgenden Schritte aus, um ein Dashboard zu erstellen:

1. Rufen Sie das Sysdig-API-Token für das Team ab, dessen Dashboards gespeichert werden sollen. Weitere Informationen finden Sie im Abschnitt [Das Sysdig-API-Token abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Erstellen Sie die JSON-Datei, die das Dashboard beschreibt. Die folgenden Felder müssen wie angegeben festgelegt werden:

    * `name`: Geben Sie den Namen des Dashboards ein.

    * `id`: Legen Sie *null* fest.

    * `version`: Legen Sie *null* fest.

    * `username`: Legen Sie die E-Mail auf die E-Mail fest, die Ihrer IBMid zugeordnet ist.

    * `isShared`: Legen Sie diese Option auf "true" fest, um das Dashboard mit anderen Teammitgliedern gemeinsam zu nutzen.

    * `isPublic`: Legen Sie diese Option auf "true" fest, wenn das Dashboard öffentlich verfügbar sein soll.

    * Konfigurieren Sie Filter, um den Geltungsbereich des Dashboards zu definieren.
    
3. Erstellen Sie das Dashboard. Führen Sie den folgenden cURL-Befehl aus:

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * *ENDPOINT* ist die URL für die Region, in der die Überwachungsinstanz verfügbar ist. Weitere Informationen finden Sie unter [Sysdig-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* ist das API-Token, das Sie im vorherigen Schritt abgerufen haben.

    * *dashboard.json* ist die Datei, die das neue Dashboard, einschließlich Anzeigen und Metriken, beschreibt.

Wenn Sie ein Dashboard erstellen möchten, sieht eine JSON-Beispieldatei beispielsweise wie folgt aus:
```
{
  "dashboard": {
    "filterExpression": null,
    "name": "My new dashboard",
    "items": [
      {
        "customDisplayOptions": {
          "yAxisLeftDomain": {
            "to": null,
            "from": 0
          },
          "yAxisScale": "linear",
          "yAxisRightDomain": {
            "to": null,
            "from": 0
          },
          "valueLimit": {
            "count": 10,
            "direction": "desc"
          },
          "histogram": {
            "numberOfBuckets": 10
          },
          "xAxis": {
            "to": null,
            "from": 0
          }
        },
        "name": "CPU usage",
        "overrideFilter": true,
        "showAsType": "line",
        "showAs": "timeSeries",
        "groupId": "My new cpu dashboardcontainer.namecarboncache1",
        "metrics": [
          {
            "propertyName": "k0",
            "metricId": "timestamp"
          },
          {
            "propertyName": "v0",
            "metricId": "cpu.used.percent",
            "aggregation": "avg",
            "groupAggregation": "avg"
          }
        ],
        "paging": {
          "to": 9,
          "from": 0
        },
        "compareToConfig": null,
        "gridConfiguration": {
          "size_y": 4,
          "size_x": 6,
          "col": 1,
          "row": 1
        },
        "filter": {
          "filters": {
            "filters": [
              {
                "metric": "container.name",
                "filters": null,
                "value": "carboncache",
                "op": "="
              }
            ],
            "logic": "and"
          }
        }
      }
    ],
    "isPublic": false,
    "annotations": {
      "createdByEngine": true
    },
    "username": "ENTER YOUR EMAIL ADDRESS",
    "version": null,
    "layout": [
      {
        "size_y": 4,
        "size_x": 6,
        "col": 1,
        "row": 1
      }
    ],
    "schema": 1,
    "id": null,
    "isShared": false
  }
}
```
{: screen}



## Dashboards eines Teams mithilfe der API speichern
{: #api_save_dashboard}

Führen Sie die folgenden Schritte aus, um die für ein Team verfügbaren Dashboards herunterzuladen:

1. Rufen Sie das Sysdig-API-Token für das Team ab, dessen Dashboards gespeichert werden sollen. Weitere Informationen finden Sie im Abschnitt [Das Sysdig-API-Token abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Führen Sie den folgenden cURL-Befehl aus:

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * *ENDPOINT* ist die URL für die Region, in der die Überwachungsinstanz verfügbar ist. Weitere Informationen finden Sie unter [Sysdig-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* ist das API-Token, das Sie im vorherigen Schritt abgerufen haben.

Um beispielsweise die Dashboards für ein Team herunterzuladen, das in der Region "USA (Süden)" arbeitet, können Sie den folgenden Befehl ausführen:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

Bei der Ausgabe handelt es sich um eine JSON-Datei, in der jedes Dashboard mit dem Feld **id** beginnt. Der Name des Dashboards wird im Feld **Name** angegeben.


## Dashboard mithilfe der API löschen
{: #api_delete_dashboard}

Führen Sie die folgenden Schritte aus, um ein Dashboard aus der Liste der Dashboards zu löschen, die für ein Team verfügbar sind:

1. Rufen Sie das Sysdig-API-Token für das Team ab, dessen Dashboards gespeichert werden sollen. Weitere Informationen finden Sie im Abschnitt [Das Sysdig-API-Token abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Rufen Sie alle Dashboards ab, die für das Team verfügbar sind. Weitere Informationen finden Sie im Abschnitt [Dashboards mithilfe der API speichern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard).

3. Suchen Sie die ID des Dashboards, das Sie löschen möchten. Suchen Sie nach dem Wert **id**, der dem Dashboard **Name** zugeordnet ist, das Sie löschen möchten.

4. Führen Sie den folgenden cURL-Befehl aus:

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * *ID* ist die ID des Dashboards, das Sie löschen möchten.

    * *ENDPOINT* ist die URL für die Region, in der die Überwachungsinstanz verfügbar ist. Weitere Informationen finden Sie unter [Sysdig-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* ist das API-Token, das Sie im vorherigen Schritt abgerufen haben.

Wenn Sie beispielsweise das Dashboard mit der ID *391* aus der Liste der Dashboards für ein Team löschen möchten, das in der Region "USA (Süden)" arbeitet, können Sie den folgenden Befehl ausführen:

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




