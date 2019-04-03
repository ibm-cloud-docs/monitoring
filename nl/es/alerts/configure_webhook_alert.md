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


# Configuración de una alerta de Webhook mediante la API de {{site.data.keyword.monitoringshort}}
{: #configure_webhook_alert}

Para configurar una alerta de webhook en una métrica, defina una regla y una notificación de webhook. A continuación, registe la regla y el método de notificación con el servicio {{site.data.keyword.monitoringshort}}.
{:shortdesc}

Realice los siguientes pasos:

## Paso 1: Crear una regla
{: #step14}

Cree una regla para una consulta métrica que ha definido en Grafana. Para obtener más información, consulte [Creación de una regla](/docs/services/cloud-monitoring/alerts/rules.html#create).

Por ejemplo, cree el archivo de reglas `s-rule-1.json` en el directorio `~/cloud-monitoring/rules/`. 

```
{
    "name": "RULE_NAME",
    "description": "MH check Bytes In per second",
    "expression": "movingAverage(messagehub.65qser11-8034-1234-5678-c82fb42wdfgh.1.kafka-java-console-sample-topic.BytesInPerSec.15MinuteRate,\"5min\")",
    "enabled": true,
    "from": "-5min",
    "until": "now",
    "comparison": "above",
    "comparison_scope": "last",
    "error_level" : 27,
    "warning_level" : 25,
    "frequency": "1min",
    "dashboard_url": "https://metrics.ng.bluemix.net",
    "notifications": [
      "NOTIFICATION_NAME"
    ]
}
```
{: screen}

A continuación, exporte la variable *RULE_FILE*:
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## Paso 2: Registrar la regla en el servicio de supervisión
{: #step23}
	
En un terminal, siga los pasos siguientes:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Por ejemplo, para utilizar la señal de IAM, ejecute el siguiente mandato:

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	El resultado de este mandato es el siguiente:
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	A continuación, exporte la variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Nota:** La señal excluye *Bearer*.
	
3. Obtenga el GUID del espacio. El GUID debe tener el prefijo *s-* para identificar un espacio.

    Ejecute el mandato siguiente:
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	Donde *SpaceName* es el nombre del espacio donde va a definir una notificación.
	
	Por ejemplo, para obtener el GUID de un espacio con el nombre *dev*, ejecute el mandato siguiente:
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	El resultado de este mandato es el siguiente:
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	A continuación, exporte la variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Ejecute el mandato cURL siguiente para registrar una regla:
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	donde
	
	* RULE_FILE es el archivo JSON que define la regla de alerta.
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
	Para verificar que la regla se ha creado correctamente, ejecute el siguiente mandato:
	
	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	Por ejemplo:

    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## Paso 3: Crear una notificación de webhook
{: #step32}


Para crear un archivo de notificación, tenga en cuenta la siguiente información:

* Utilice la plantilla de notificación para las alertas de webhook. Para obtener más información, consulte [Plantillas de notificación](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template).
* Cree el archivo en un directorio local, por ejemplo, `~/cloud-monitoring/notifications`.

Por ejemplo, cree el archivo **webhook.json** mediante el editor vi: 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "Webhook",
"description" : "Fire this webhook when ....",
    "detail": "https://myendpoint.bluemix.net?key=abcd1234"
    }
```
{: codeblock}	

Para poder invocar un webhook, el campo *detail* debe estar establecido en el URL en el que se debe realizar la acción POST. Configure un webhook para puntos finales https y añada un parámetro.
	
Para obtener más información, consulte [Creación de una notificación](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create).
	
## Paso 4: Registrar el método de notificación en el servicio de supervisión
{: #step42}
	
En un terminal, siga los pasos siguientes:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Por ejemplo, para utilizar la señal de IAM, ejecute el siguiente mandato:

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	El resultado de este mandato es el siguiente:
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	A continuación, exporte la variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Nota:** La señal excluye *Bearer*.
	
3. Obtenga el GUID del espacio. El GUID debe tener el prefijo *s-* para identificar un espacio.

    Ejecute el mandato siguiente:
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	Donde *SpaceName* es el nombre del espacio donde va a definir una notificación.
	
	Por ejemplo, para obtener el GUID de un espacio con el nombre *dev*, ejecute el mandato siguiente:
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	El resultado de este mandato es el siguiente:
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	A continuación, exporte la variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Ejecute el mandato cURL siguiente para registrar una notificación:

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	donde
	
	* NOTIFICATION_FILE es el archivo JSON que define la notificación.
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Para verificar que la notificación se ha creado correctamente, ejecute el siguiente mandato:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
