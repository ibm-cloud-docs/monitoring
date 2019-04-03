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



# Supresión de métricas
{: #delete_metrics}

Puede suprimir métricas desde el servicio {{site.data.keyword.monitoringshort}} mediante [la API de métricas](https://console.bluemix.net/apidocs/monitoring-metrics-api).
{:shortdesc}

Después de [iniciar sesión en una región en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login), siga estos pasos para suprimir una notificación:


## Paso 1: Obtener la señal de seguridad
{: #step1_delete_metrics}

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
Señal de IAM:  Portador djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    Señal de UAA:  Portador eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
A continuación, exporte la variable *Token*:
	
```
export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
```
{: screen}
	
**Nota:** La señal excluye *Bearer*.
	
## Paso 2: Verificar los permisos para trabajar con métricas 
{: #step2_delete_metrics}

Dependiendo del dominio donde están disponibles las métricas, tenga en cuenta la información siguiente:

* Para trabajar con métricas disponibles en un dominio de espacio, el usuario necesita el rol de *desarrollador* en el espacio de Cloud Foundry asociado con el dominio. 
* Para trabajar con métricas disponibles en el dominio de la cuenta, el usuario necesita una política de IAM con el rol *administrador*, *operador* o *editor*.

Para verificar los permisos de usuario, siga estos pasos:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Verifique los permisos de acceso para trabajar con el servicio {{site.data.keyword.monitoringshort}}.


## Paso 3: Obtener el ID de espacio 
{: #step3_delete_metrics}

Este paso solo se aplica cuando desea suprimir métricas disponibles en un dominio de espacio.

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

	

## Paso 4: Listar las métricas
{: #step4_delete_metrics}


Ejecute el mandato cURL siguiente para obtener una lista de las métricas disponibles en un dominio de espacio:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*

```
{: screen}

Ejecute el mandato cURL siguiente para obtener una lista de las métricas disponibles en el dominio de la cuenta:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*
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

* *query* define el filtro que se aplica. Por ejemplo, `query=metric-service.*` hace una lista de todas las métricas que existen bajo la jerarquía `metric-service.*`, y `query=*` hace una lista de todas las métricas del dominio.


## Paso 5 - Opción 1: Suprimir todas las métricas
{: #step5_delete_metrics}
  

Ejecute el mandato cURL siguiente para suprimir todas las métricas de un dominio de espacio:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

Ejecute el mandato cURL siguiente para suprimir todas las métricas del dominio de la cuenta:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

donde
	
* *X-Auth-User-Token* es un parámetro que pasa la señal UAA de {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type es el prefijo que define el tipo de señal. Los valores válidos son: *uaa* para la señal de UAA, *iam* para la señal de IAM, y *api* para la clave de API.
	
* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio.
	
* *Token* representa la señal de seguridad.
	
* *Space* representa el GUID del espacio. 
	
* *METRICS_ENDPOINT* representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *query* define el filtro que se aplica. `query=*` indica todas las métricas del dominio.


## Paso 6 - Opción 2: Suprimir todas las métricas para un servicio
{: #step6_delete_metrics}
  

Ejecute el mandato cURL siguiente para suprimir todas las métricas para un servicio de un dominio de espacio:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

Ejecute el mandato cURL siguiente para suprimir todas las métricas del dominio de la cuenta:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

donde
	
* *X-Auth-User-Token* es un parámetro que pasa la señal UAA de {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type es el prefijo que define el tipo de señal. Los valores válidos son: *uaa* para la señal de UAA, *iam* para la señal de IAM, y *api* para la clave de API.
	
* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio.
	
* *Token* representa la señal de seguridad.
	
* *Space* representa el GUID del espacio. 
	
* *METRICS_ENDPOINT* representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *query* define el filtro que se aplica. `query=*` indica todas las métricas del dominio.

* *metric-service.** es el nombre de un servicio. Por ejemplo, `containers-kubernetes`.
