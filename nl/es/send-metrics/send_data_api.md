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

# Envío de datos mediante la API de métricas
{: #send_data_api}

Puede enviar métricas al servicio {{site.data.keyword.monitoringshort}} mediante la API de métricas. 
{:shortdesc}


Para los contenedores {{site.data.keyword.Bluemix_notm}} Docker, se recopilan automáticamente métricas básicas del sistema. Para aplicaciones Cloud Foundry y apps que se ejecutan en una máquina virtual (VM), las métricas se deben enviar directamente desde la app mediante [la API de métricas](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}. 



## Envío de métricas a un dominio de espacio
{: #space_uaa}

Para enviar métricas a un espacio mediante cURL, siga estos pasos:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API.

    Elija uno de los métodos siguientes para obtener la señal de seguridad que necesita para enviar métricas:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli);
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	En el mismo terminal en el que ha iniciado sesión en {{site.data.keyword.Bluemix_notm}}, establezca la variable *Token* para la señal.

    Por ejemplo, establezca una señal de UAA y elimine la parte *Bearer* del valor de señal:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
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
	
5. Ejecute el siguiente mandato cURL para enviar métricas:

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	donde
	
	* Metrics_File representa el archivo JSON que incluye la definición de las métricas que se envían al servicio {{site.data.keyword.monitoringshort}}.
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de seguridad.
	
	* *Auth_Type* es el prefijo que define el tipo de señal. Los valores válidos son: *uaa* para la señal de UAA, *iam* para la señal de IAM, y *api* para la clave de API.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio.
	
	* Token representa la señal de seguridad o la clave de API.
	
	* Space representa el GUID del espacio. 
	
	* Endpoint representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
	Por ejemplo, puede ejecutar el siguiente mandato para enviar 2 métricas, `myhost.cpu.idle` y `myapp.login.attempts`, al servicio {{site.data.keyword.monitoringshort}}:
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	El archivo de ejemplo *metric.json* se define así:

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
