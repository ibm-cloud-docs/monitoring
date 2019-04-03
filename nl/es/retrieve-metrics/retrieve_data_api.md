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

# Recuperación de métricas
{: #retrieve_data_api}

Puede recuperar métricas desde el servicio {{site.data.keyword.monitoringshort}} mediante la [API de métricas](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}.
{:shortdesc}


## Recuperación de métricas de un espacio
{: #uaa}

Para recuperar métricas desde un espacio, siga estos pasos:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Establezca la señal de seguridad o la clave de API
  
    Debe establecer el campo **X-Auth-User-Token** con una señal de seguridad, o una clave de API. Puede utilizar una señal de UAA, una señal de IAM o una clave de API.

    En primer lugar, elija uno de los métodos siguientes para obtener la señal de seguridad que necesita para enviar métricas:
	
    * Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
    
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
    
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key). 

    Una señal o clave de API debe tener como prefijo uno de los valores siguientes: `apikey`, `iam` o `uaa` 

    donde 

    * *apikey* identifica que la señal es una clave de API.
    * *iam* identifica que la señal especificada es una señal generada por IAM.
    * *uaa* identifica que la señal especificada es una señal generada por UAA.

    Por ejemplo, puede establecer la cabecera siguiente para una clave de API: `X-Auth-User-Token: apikey SomeIAMGeneratedKey`
	
	A continuación, en el mismo terminal en el que ha iniciado sesión en {{site.data.keyword.Bluemix_notm}}, establezca la variable Token para la señal.

    Por ejemplo, establezca una señal de UAA y elimine la parte *Bearer* del valor de señal:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. Obtenga el ID de espacio.

    Para recuperar métricas, es necesario el campo de cabecera **X-Auth-Scope-Id**, y debe establecerse en el GUID de espacio. 

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

4. Ejecute el siguiente mandato cURL para enviar métricas:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	donde
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal UAA de {{site.data.keyword.Bluemix_notm}}.
	
	* Auth_Type es el prefijo que define el tipo de señal. Los valores válidos son: *uaa* para la señal de UAA, *iam* para la señal de IAM, y *api* para la clave de API.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera solo es necesaria si utiliza la autenticación de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* *Token* representa la señal de seguridad.
	
	* *Space* representa el GUID del espacio. 
	
	* *Start_Time* define el inicio de la solicitud. Esta información se utiliza para calcular el periodo de tiempo relativo o absoluto. *End_Time* define el final de la solicitud. Esta información se utiliza para calcular el periodo de tiempo relativo o absoluto. Para obtener más información, consulte [Establecimiento de un período de tiempo](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#time).
	
	* *Path* identifica una o varias métricas. Opcionalmente, puede aplicar funciones a cada métrica. En las vías de acceso también se admiten los comodines, que permiten identificar más de una métrica en una sola vía de acceso. Para obtener más información, consulte [Definición de las métricas](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#metrics).
	
	* *METRICS_ENDPOINT* representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

	
## Definición de métricas
{: #metrics}

Para recuperar datos para una métrica, debe especificar la vía de acceso de la métrica desde la raíz del árbol de métricas hasta la métrica, y debe separar cada paso con un punto (.).

La vía de acceso se especifica en el parámetro **Target**. Se pueden especificar un máximo de 5 destinos por solicitud.  

Opcionalmente, puede aplicar funciones a la métrica. Para obtener más información acerca de las funciones admitidas, consulte [Funciones de Graphite 0.9.15 ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://graphite.readthedocs.io/en/latest/functions.html).

Puede utilizar comodines para definir una vía de acceso. Al utilizar comodines, puede identificar más de una métrica en una sola vía de acceso. 

* **Asterisco**: Puede utilizar un asterisco (*) para hacer coincidan cero más caracteres. 

    Puede incluir más de un asterisco dentro de un único elemento de vía de acceso, por ejemplo: `servers.sp*aeg*r.cpu.total.*` Este ejemplo devuelve datos sobre la CPU total para todos los servidores que coincidan con el patrón.

* **Lista o rangos de caracteres**: Puede definir los caracteres entre corchetes ([...]) para especificar una única posición de carácter en la serie de la vía de acceso. 

    Puede definir un rango inclusivo de caracteres especificando dos caracteres separados por un guión (-). Coincidirá con cualquier carácter entre estos dos caracteres. 
	
	Puede definir una o varios rangos de caracteres entre corchetes. 
	
	Cuando los caracteres incluidos dentro de un conjunto de corchetes no se puedan leer como un rango, se tratan como una lista de valores. 
	
	Puede incluir un guión (-) como carácter en una lista de valores poniéndolo al principio o al final dentro de los corchetes.

* **Value list**: Puede establecer valores separador por comas en el corchete para definir listas de valores. 

    Por ejemplo, para descargar las métricas de las siguientes vías de acceso: `servers.myserver.cpu.total.user` y `servers.myserver.cpu.total.system`, puede establecer una única vía de acceso para ambos tipos: `servers.myserver.cpu.total.{user,system}`



## Establecimiento de un período de tiempo
{: #time}

De forma opcional, especifique un período de tiempo utilizando un tiempo relativo o absoluto. Debe definir los parámetros de consulta **From** y **Until**.  

* Cuando se omite el inicio del periodo de tiempo, el valor predeterminado es hace 24 horas. 

* Cuando se omite el tiempo final del periodo de tiempo, el valor predeterminado es la hora actual *now*.

**Relative time** siempre va precedido del signo menos (-) y seguido de una unidad de tiempo. 

En la tabla siguiente se muestran las diferentes abreviaturas de tiempo relativo que puede utilizar:


| Abreviatura | Descripción |
|--------------|-------------|
| s            | Segundos     |
| min          | Minutos     |
| h            | Horas       |
| d            | Días        |
| w            | Semanas       |
| mon          | Meses      |
| now          | Hora actual |


Puede utilizar cualquiera de los formatos siguientes para definir **Absolute time**: `HH:MM_YYMMDD`, `YYYYMMDD`, `MM/DD/YY`

| Abreviatura | Descripción |
|--------------|-------------|
| YYYY         | Año con cuatro dígitos |
| MM           | Mes con dos dígitos (01=En etc) |
| DD           | Día del mes con dos dígitos (01 a 31) |
| hh           | Dos dígitos de hora (00 a 23) |
| mm           | Dos dígitos de minuto (00 a 59) |
| ss           | Dos dígitos de segundo (00 a 59) |

**Ejemplo**

La tabla siguiente muestra distintos ejemplos sobre cómo definir diferentes periodos de tiempo estableciendo los parámetros *from* y *until*:

<table>
  <caption>Tabla 1. Distintos ejemplos que muestran cómo establecer diferentes periodos de tiempo estableciendo los parámetros *from* y *until*</caption>
  <tr>
    <th>Ejemplo</th>
	<th>Descripción</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>Periodo de tiempo que incluye datos desde el último lunes hasta ahora.</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>Periodo de tiempo establecido en un mes, por ejemplo, noviembre </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>Para mostrar datos dentro de un ciclo de 24 horas, por ejemplo, desde las 02:00 hasta las 14:00 del 1 de julio de 2017</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>Para mostrar el mismo día de la semana, por ejemplo, la última semana</td>
  </tr>
  
</table>


