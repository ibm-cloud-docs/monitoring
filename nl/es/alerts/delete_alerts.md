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



# Supresión de alertas
{: #delete_alerts}

Puede suprimir alertas desde el servicio {{site.data.keyword.monitoringshort}} mediante [la API de alertas](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window}.
{:shortdesc}


Después de [iniciar sesión en una región en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login), siga estos pasos para suprimir una notificación:


## Paso 1: Obtener la señal de seguridad
{: #step1_delete_alerts}

Puede utilizar una señal de UAA, una señal de IAM o una clave de API. 

Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
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
IAM token:  Bearer djn.._l_HWtlNTibmcloudsl0qjBI9GqCnuQ
UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
A continuación, exporte la variable *Token*:
	
```
export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
```
{: screen}
	
**Nota:** La señal excluye *Bearer*.
	

## Paso 2: Obtener el ID de espacio 
{: #step2_delete_alerts}

Este paso solo se aplica cuando desea suprimir alertas disponibles en un dominio de espacio.

Para obtener el GUID de espacio, ejecute el mandato siguiente:
	
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
	
A continuación, exporte la variable *Space*. El GUID debe tener el prefijo *s-* para identificar un espacio.
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## Paso 3: Listar las reglas
{: #step3_delete_alerts}


Ejecute el mandato cURL siguiente para obtener una lista de las reglas definidas en un dominio de espacio:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules

```
{: screen}

Ejecute el mandato cURL siguiente para obtener una lista de las notificaciones del dominio de la cuenta:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules
```
{: screen}

donde
	
* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

    * *apikey* identifica que la señal es una clave de API.
	* *iam* identifica que la señal especificada es una señal generada por IAM.
	* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. 
	
* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
* Space es el GUID del espacio. 
	
* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).


## Paso 4: Suprimir una regla de alerta
{: #step4_delete_alerts}
  

Ejecute el mandato cURL siguiente para suprimir una regla de un dominio de espacio:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

Ejecute el mandato cURL siguiente para suprimir una regla del dominio de la cuenta:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

	
donde
	
* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

    * *apikey* identifica que la señal es una clave de API.
	* *iam* identifica que la señal especificada es una señal generada por IAM.
	* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. 
	
* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
* Space es el GUID del espacio. 
	
* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *name* es el nombre de la regla que desea suprimir.
	
