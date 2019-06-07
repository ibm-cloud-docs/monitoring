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


# Gestione dell'API REST Sysdig
{: #api}

Utilizza l'API REST Sysdig per automatizzare le attività di routine e monitorare le notifiche.
{:shortdesc}

Quando utilizzi l'API dai tuoi script o programmi personalizzati, devi utilizzare un token Sysdig per l'autenticazione con l'istanza {{site.data.keyword.mon_full_notm}}. 
{: tip}

## Creazione di un dashboard utilizzando l'API
{: #api_create_dashboard}

Puoi creare un dashboard duplicandone uno esistente.  

Completa la seguente procedura per creare un dashboard:

1. Ottieni il token API Sysdig per il team di cui vuoi salvare i dashboard. Per ulteriori informazioni, consulta [Ottenimento del token API Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Crea il file JSON che descrive il dashboard. I seguenti campi devono essere configurati come indicato:

    * `name`: immetti il nome del dashboard.

    * `id`: imposta su *null*.

    * `version`: imposta su *null*.

    * `username`: imposta sull'email associata al tuo ID IBM.

    * `isShared`: imposta su true per condividere il dashboard con altri membri del team.

    * `isPublic`: imposta su true se vuoi che il dashboard sia disponibile pubblicamente.

    * Configura i filtri per definire l'ambito del dashboard.
    
3. Crea il dashboard. Immetti il seguente comando cURL:

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    Dove

    * *ENDPOINT* è l'URL per la regione in cui è disponibile l'istanza di monitoraggio. Per ulteriori informazioni, consulta [Endpoint Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* è il token API che hai ottenuto nel passo precedente.

    * *dashboard.json* è il file che descrive il nuovo dashboard, che include i pannelli e le metriche.

Ad esempio, per creare un dashboard, un file JSON di esempio è simile al seguente:
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



## Salvataggio dei dashboard di un team utilizzando l'API
{: #api_save_dashboard}

Completa la seguente procedura per scaricare i dashboard disponibili per un team:

1. Ottieni il token API Sysdig per il team di cui vuoi salvare i dashboard. Per ulteriori informazioni, consulta [Ottenimento del token API Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Immetti il seguente comando cURL:

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Dove

    * *ENDPOINT* è l'URL per la regione in cui è disponibile l'istanza di monitoraggio. Per ulteriori informazioni, consulta [Endpoint Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* è il token API che hai ottenuto nel passo precedente.

Ad esempio, per scaricare i dashboard per un team che lavora nella regione Stati Uniti Sud, puoi immettere il seguente comando:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

L'output è un file JSON in cui ogni dashboard inizia con il campo **id**. Il nome del dashboard viene specificato nel campo **name**.


## Eliminazione di un dashboard utilizzando l'API
{: #api_delete_dashboard}

Completa la seguente procedura per eliminare un dashboard dall'elenco dei dashboard disponibili per un team:

1. Ottieni il token API Sysdig per il team di cui vuoi salvare i dashboard. Per ulteriori informazioni, consulta [Ottenimento del token API Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Ottieni tutti i dashboard disponibili per il team. Per ulteriori informazioni, consulta [Salvataggio dei dashboard utilizzando l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard).

3. Trova l'ID del dashboard che vuoi eliminare. Ricerca il valore **id** associato al dashboard **name** che vuoi eliminare.

4. Immetti il seguente comando cURL:

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Dove

    * *ID* è l'ID del dashboard che vuoi eliminare.

    * *ENDPOINT* è l'URL per la regione in cui è disponibile l'istanza di monitoraggio. Per ulteriori informazioni, consulta [Endpoint Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* è il token API che hai ottenuto nel passo precedente.

Ad esempio, per eliminare il dashboard con ID *391* dall'elenco dei dashboard per un team che lavora nella regione Stati Uniti Sud, puoi immettere il seguente comando:

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




