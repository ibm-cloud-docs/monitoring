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


# Recuperación del historial de una alerta mediante la API de alertas
{: #retrieve_history}

Utilice la API de alertas para recuperar el historial de una alerta. 
{:shortdesc}


Para recuperar el historial de una alerta mediante la API de alertas, siga estos pasos:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
	En el mismo terminal en el que ha iniciado sesión en {{site.data.keyword.Bluemix_notm}}, establezca la variable Token para la señal.

    Por ejemplo, para utilizar la señal de IAM, ejecute el siguiente mandato:

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	El resultado de este mandato es el siguiente:
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	A continuación, exporte la variable *Token*:
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
	A continuación, exporte la variable *Space*. **Nota:** El GUID debe tener el prefijo *s-* para identificar un espacio.
	
	Por ejemplo:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Recuperar el historial de una regla

    * Para recuperar el historial de una regla por su nombre, consulte [Recuperación del historial de una regla utilizando su nombre](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_name).
	* Para recuperar el historial de una regla durante un periodo de tiempo, consulte [Recuperación del historial de una regla de las últimas 48 horas](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_time).
	* Para recuperar un número de entrada del historial de una regla, consulte [Recuperación de las últimas 3 entradas en el historial de una regla](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#number).
	
	
## Recuperación del historial de una regla por nombre de regla
{: #by_name}
	
Ejecute el mandato cURL siguiente para obtener el historial de una alerta:

```
curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/history?rule_name=RULE_NAME
```
{: codeblock}
	
donde
	
* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

    * *apikey* identifica que la señal es una clave de API.
	* *iam* identifica que la señal especificada es una señal generada por IAM.
	* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
* *Token* es la señal de autenticación de UAA o IAM, o la clave de API.
	
* *Space* es el GUID del espacio. 
	
* *RULE_NAME* es el nombre de la regla que se utiliza para desencadenar la alerta. El valor es el especificado en el campo *name*.
	
* *METRICS_ENDPOINT* representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    
Por ejemplo, el historial de la regla `highNginxCPU` es el siguiente:

```
curl -XGET --header "X-Auth-User-Token: iam ${Token}" --header "X-Auth-Scope-Id: ${Space}" https://metrics.ng.bluemix.net/v1/alert/history?rule_name=highNginxCPU
```
{: screen}

```
[
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T22.23.21.000",
 "value": 99.5,
 "from_level": "OK",
 "to_level": "ERROR"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.11.12.123",
 "value": 98.5,
 "from_level" : "OK",
 "to_level": "WARN"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.12.14.000",
 "value": 97.0,
 "from_level" : "WARN",
 "to_level": "OK"
 }
]
```
{: screen}


## Recuperación del historial de una regla de las últimas 48 horas
{: #by_time}

Ejecute el mandato cURL siguiente para obtener el historial de una alerta de las últimas 48 horas:

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?start=-48h
```
{: codeblock}

donde
	
* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

    * *apikey* identifica que la señal es una clave de API.
	* *iam* identifica que la señal especificada es una señal generada por IAM.
	* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
* *Token* es la señal de autenticación de UAA o IAM, o la clave de API.
	
* *Space* es el GUID del espacio. 
	
* *RULE_NAME* es el nombre de la regla que se utiliza para desencadenar la alerta. El valor es el especificado en el campo *name*.
	
* *METRICS_ENDPOINT* representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	

## Recuperación de las últimas 3 entrada en el historial de una regla
{: #number}

Ejecute el mandato cURL siguiente para obtener las últimas 3 entrada en el historial de una alerta:

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?max_results=3
```
{: codeblock}

donde
	
* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

    * *apikey* identifica que la señal es una clave de API.
	* *iam* identifica que la señal especificada es una señal generada por IAM.
	* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
* *Token* es la señal de autenticación de UAA o IAM, o la clave de API.
	
* *Space* es el GUID del espacio. 
	
* *RULE_NAME* es el nombre de la regla que se utiliza para desencadenar la alerta. El valor es el especificado en el campo *name*.
	
* *METRICS_ENDPOINT* representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
