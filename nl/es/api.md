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


# Cómo trabajar con la API REST de Sysdig
{: #api}

Utilice la API REST de Sysdig para automatizar las tareas rutinarias y supervisar las notificaciones.
{:shortdesc}

Cuando utilice la API desde scripts o programas personalizados, debe utilizar una señal de Sysdig para autenticarse con la instancia de {{site.data.keyword.mon_full_notm}}. 
{: tip}

## Creación de un panel de control mediante la API
{: #api_create_dashboard}

Puede crear un panel de control duplicando un panel de control existente.  

Siga los pasos siguientes para crear un panel de control:

1. Obtenga la señal de API de Sysdig correspondiente al equipo cuyos paneles de control desea guardar. Para obtener más información, consulte [Obtención de la señal de API de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Cree el archivo json que describe el panel de control. Los campos siguientes se deben establecer tal como se indica:

    * *name*: escriba el nombre del panel de control.

    * *id*: establézcalo en *null*.

    * *version*: establézcalo en *null*.

    * username: establézcalo en el correo electrónico asociado a su IBMid.

    * *isShared*: establézcalo en true para compartir el panel de control con otros miembros del equipo.

    * *isPublic*: establézcalo en true si desea que el panel de control esté disponible a nivel público.

    * Configure filtros para definir el ámbito del panel de control.
    
3. Cree el panel de control. Ejecute el siguiente mandato cURL:

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    donde

    * *ENDPOINT* es el URL de la región en la que está disponible la instancia de supervisión. Para obtener más información, consulte [Puntos finales de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* es la señal de API que se ha obtenido en el paso anterior.

    * *dashboard.json* es el archivo que describe el nuevo panel de control, incluidos los paneles y las métricas.

Por ejemplo, para crear un panel de control, un archivo json de ejemplo tiene el siguiente aspecto:
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



## Cómo guardar los paneles de control de un equipo mediante la API
{: #api_save_dashboard}

Siga los pasos siguientes para descargar los paneles de control que están disponibles para un equipo:

1. Obtenga la señal de API de Sysdig correspondiente al equipo cuyos paneles de control desea guardar. Para obtener más información, consulte [Obtención de la señal de API de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Ejecute el siguiente mandato cURL:

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    donde

    * *ENDPOINT* es el URL de la región en la que está disponible la instancia de supervisión. Para obtener más información, consulte [Puntos finales de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* es la señal de API que se ha obtenido en el paso anterior.

Por ejemplo, para descargar los paneles de control correspondientes a un equipo que trabaja en la región EE. UU. sur, ejecute el siguiente mandato:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

La salida es un archivo JSON en el que cada panel de control comienza por el campo **id**. El nombre del panel de control se especifica en el campo **name**.


## Supresión de un panel de control mediante la API
{: #api_delete_dashboard}

Siga los pasos siguientes para suprimir un panel de control de la lista de paneles de control que están disponibles para un equipo:

1. Obtenga la señal de API de Sysdig correspondiente al equipo cuyos paneles de control desea guardar. Para obtener más información, consulte [Obtención de la señal de API de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Obtenga todos los paneles de control que están disponibles para el equipo. Para obtener más información, consulte [Cómo guardar paneles de control mediante la API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard).

3. Busque el ID del panel de control que desea suprimir. Busque el valor de **id** que está asociado al panel de control **name** que desea suprimir.

4. Ejecute el siguiente mandato cURL:

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    donde

    * *ID* es el ID del panel de control que desea suprimir.

    * *ENDPOINT* es el URL de la región en la que está disponible la instancia de supervisión. Para obtener más información, consulte [Puntos finales de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* es la señal de API que se ha obtenido en el paso anterior.

Por ejemplo, para suprimir el panel de control con el ID *391* de la lista de paneles de control de un equipo que trabaja en la región EE. UU. sur, ejecute el mandato siguiente:

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




