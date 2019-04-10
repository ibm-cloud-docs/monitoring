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


# Utilisation de l'API REST Sysdig
{: #api}

Utilisez l'API REST Sysdig pour automatiser des tâches de routine et surveiller des notifications.
{:shortdesc}

Lorsque vous utilisez l'API à partir de vos programmes ou scripts personnalisés, vous devez vous servir d'un jeton Sysdig pour vous authentifier sur l'instance {{site.data.keyword.mon_full_notm}}. 
{: tip}

## Création d'un tableau de bord à l'aide de l'API
{: #api_create_dashboard}

Vous pouvez créer un tableau de bord en dupliquant un tableau de bord existant.  

Pour créer un tableau de bord, procédez comme suit :

1. Obtenez le jeton d'API Sysdig pour l'équipe dont vous voulez sauvegarder les tableaux de bord. Pour plus d'informations, voir [Obtention du jeton d'API Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Créez le fichier JSON qui décrit le tableau de bord. Les zones suivantes doivent être définies comme indiqué :

    * *name* : saisissez le nom du tableau de bord.

    * *id* : définissez ce paramètre sur *null*.

    * *version* : définissez ce paramètre sur *null*.

    * username : affectez à ce paramètre l'adresse électronique associée à votre IBMid.

    * *isShared* : définissez ce paramètre sur true pour partager le tableau de bord avec d'autres membres de l'équipe.

    * *isPublic* : définissez ce paramètre sur true si vous voulez que le tableau de bord soit public.

    * Configurez des filtres pour définir la portée du tableau de bord.
    
3. Créez le tableau de bord. Exécutez la commande cURL suivante :

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    où

    * *ENDPOINT* est l'URL de la région où se trouve l'instance de surveillance. Pour plus d'informations, voir [Noeuds finaux Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* est le jeton d'API que vous avez obtenu à l'étape précédente.

    * *dashboard.json* est le fichier qui décrit le nouveau tableau de bord, notamment les panneaux et les métriques.

Par exemple, pour créer un tableau de bord, un exemple de fichier JSON se présente comme suit :
```
{
  "dashboard": {
    "filterExpression": null,
    "name": "Mon nouveau tableau de bord",
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
        "name": "Utilisation de l'UC",
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



## Sauvegarde des tableaux de bord d'une équipe à l'aide de l'API
{: #api_save_dashboard}

Procédez comme suit pour télécharger les tableaux de bord à la disposition d'une équipe :

1. Obtenez le jeton d'API Sysdig pour l'équipe dont vous voulez sauvegarder les tableaux de bord. Pour plus d'informations, voir [Obtention du jeton d'API Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Exécutez la commande cURL suivante :

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    où

    * *ENDPOINT* est l'URL de la région où se trouve l'instance de surveillance. Pour plus d'informations, voir [Noeuds finaux Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* est le jeton d'API que vous avez obtenu à l'étape précédente.

Par exemple, pour télécharger les tableaux de bord d'une équipe travaillant dans la région Sud des Etats-Unis, vous pouvez exécuter la commande suivante :

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

La sortie est un fichier JSON dans lequel chaque tableau de bord commence par la zone **id**. Le nom du tableau de bord est spécifié dans la zone **name**.


## Suppression d'un tableau de bord à l'aide de l'API
{: #api_delete_dashboard}

Procédez comme suit pour supprimer un tableau de bord de la liste des tableaux de bord à disposition d'une équipe :

1. Obtenez le jeton d'API Sysdig pour l'équipe dont vous voulez sauvegarder les tableaux de bord. Pour plus d'informations, voir [Obtention du jeton d'API Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Affichez tous les tableaux de bord disponibles pour l'équipe. Pour plus d'informations, voir [Sauvegarde des tableaux de bord à l'aide de l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard).

3. Trouvez l'ID du tableau de bord à supprimer. Recherchez la valeur **id** qui est associée au  **nom** du tableau de bord à supprimer.

4. Exécutez la commande cURL suivante :

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    où

    * *ID* est l'ID du tableau de bord à supprimer.

    * *ENDPOINT* est l'URL de la région où se trouve l'instance de surveillance. Pour plus d'informations, voir [Noeuds finaux Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* est le jeton d'API que vous avez obtenu à l'étape précédente.

Par exemple, pour supprimer le tableau portant l'ID *391* de la liste des tableaux de bord d'une équipe travaillant dans la région Sud des Etats-Unis, vous pouvez exécuter la commande suivante :

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




