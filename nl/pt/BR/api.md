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


# Gerenciando a API de REST do Sysdig
{: #api}

Use a API de REST do Sysdig para automatizar tarefas de rotina e monitorar notificações.
{:shortdesc}

Ao usar a API por meio de scripts ou programas customizados, deve-se usar um token do Sysdig para ser autenticado com a instância do {{site.data.keyword.mon_full_notm}}. 
{: tip}

## Criando um painel usando a API
{: #api_create_dashboard}

É possível criar um painel duplicando um painel existente.  

Conclua as etapas a seguir para criar um painel:

1. Obtenha o token da API do Sysdig para a equipe cujos painéis você deseja salvar. Para obter mais informações, consulte [Obtendo o token da API do Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Crie o arquivo json que descreve o painel. Os campos a seguir devem ser configurados conforme indicado:

    * `name`: insira o nome do painel.

    * ` id `: configurado como  * null *.

    * ` version `: configure como  * null *.

    * `username`: configure como o e-mail associado ao seu IBMid.

    * `isShared`: configure como true para compartilhar o painel com outros membros da equipe.

    * `isPublic`: configure como true se você desejar que o painel esteja disponível publicamente.

    * Configure filtros para definir o escopo do painel.
    
3. Crie o painel. Execute o comando cURL a seguir:

    ```
    curl -X POST ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json -d @dashboard.json' 
    ```
    {: codeblock}

    Em que

    * *ENDPOINT* é a URL da região na qual a instância de monitoramento está disponível. Para obter mais informações, consulte [Terminais Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* é o token da API que você recebeu na etapa anterior.

    * *dashboard.json* é o arquivo que descreve o novo painel, incluindo painéis e métricas.

Por exemplo, para criar um painel, um arquivo json de amostra se parece com o seguinte:
```
{
  "dashboard": {
    "filterExpression": null,
    "name": "My new dashboard",
    "items": [
      {
        "customDisplayOptions": {
          "yAxisLeftDomain": {
            "para": nulo, "de": 0
          },
          "yAxisScale": "linear",
          "yAxisRightDomain": {
            "para": nulo, "de": 0
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
          "filtros": {
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



## Salvando os painéis de uma equipe usando a API
{: #api_save_dashboard}

Conclua as etapas a seguir para fazer download dos painéis que estão disponíveis para uma equipe:

1. Obtenha o token da API do Sysdig para a equipe cujos painéis você deseja salvar. Para obter mais informações, consulte [Obtendo o token da API do Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Execute o comando cURL a seguir:

    ```
    curl -X GET ENDPOINT/ui/dashboards -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Em que

    * *ENDPOINT* é a URL da região na qual a instância de monitoramento está disponível. Para obter mais informações, consulte [Terminais Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* é o token da API que você recebeu na etapa anterior.

Por exemplo, para fazer download dos painéis para uma equipe que trabalha na região Sul dos EUA, é possível executar o comando a seguir:

```
curl -X GET https://us-south.monitoring.cloud.ibm.com/ui/dashboards -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json'
```
{: screen}

A saída é um arquivo JSON no qual cada painel se inicia com o campo **id**. O nome do painel é especificado no campo **name**.


## Excluindo um painel usando a API
{: #api_delete_dashboard}

Conclua as etapas a seguir para excluir um painel da lista de painéis que está disponível para uma equipe:

1. Obtenha o token da API do Sysdig para a equipe cujos painéis você deseja salvar. Para obter mais informações, consulte [Obtendo o token da API do Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token_get).

2. Obtenha todos os painéis que estão disponíveis para a equipe. Para obter mais informações, consulte [Salvando painéis usando a API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard).

3. Localize o ID do painel que você deseja excluir. Procure o valor **id** que está associado ao **name** do painel que você deseja excluir.

4. Execute o comando cURL a seguir:

    ```
    curl -X DELETE ENDPOINT/ui/dashboards/ID -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'Content-Type: application/json' 
    ```
    {: codeblock}

    Em que

    * *ID* é o ID do painel que você deseja excluir.

    * *ENDPOINT* é a URL da região na qual a instância de monitoramento está disponível. Para obter mais informações, consulte [Terminais Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints).

    * *SYSDIG_API_TOKEN* é o token da API que você recebeu na etapa anterior.

Por exemplo, para excluir o painel com o ID *391* da lista de painéis para uma equipe
que trabalha na região Sul dos EUA, é possível executar o comando a seguir:

```
curl -X DELETE https://us-south.monitoring.cloud.ibm.com/ui/dashboards/391 -H 'Authorization: Bearer xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' -H 'Content-Type: application/json' 
```
{: screen}




