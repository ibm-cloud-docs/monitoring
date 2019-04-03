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


# Reglas CRUD
{: #rules}

Utilice la API de alertas para crear, suprimir o actualizar una regla, para mostrar los detalles de una regla y para generar una lista de las reglas definidas en un espacio.
{:shortdesc}


## Creación de una regla
{: #create}

Para configurar una regla en el servicio {{site.data.keyword.monitoringshort}}, cree un archivo de regla que incluya los detalles de regla y registre la regla con el servicio {{site.data.keyword.monitoringshort}}.

Realice los siguientes pasos:

1. Cree un archivo de reglas que contenga un archivo JSON válido. Guarde el archivo. 

    Por ejemplo, para guardar el archivo, utilice un prefijo como *s-* para las reglas que defina para las consultas que se ejecutan en un espacio.
	
	**Consejos:** 
	
	* Defina distintas reglas para una consulta para alertar acerca de errores o avisos mediante distintos métodos de notificación. 
	* Cree su archivo de reglas en el directorio siguiente: *~/cloud-monitoring/roles/* para agrupar los recursos del servicio {{site.data.keyword.monitoringshort_notm}}. 

    Escriba la siguiente información en el archivo de la regla:
	
	* *name*: Especifique un nombre exclusivo. El valor de este campo se utiliza más adelante para actualizar, suprimir y mostrar los detalles de la regla.
	* *description*: Especifique una descripción.
	* *expression*: Escriba la consulta que desea supervisar.
	* *enabled*: Establezca el valor *true* para habilitar la regla.
	* *from*: Punto inicial en el tiempo que se utiliza para analizar los datos en función de los valores de umbral.
	* *until*: Punto final en el tiempo que se utiliza para analizar los datos en función de los valores de umbral.
	* *comparison*: Operación de comparación que se utiliza para identificar el tipo de comprobación que se va a realizar, por ejemplo *below*.
	* *error_level*: Define el umbral que establece para desencadenar una alerta de error.
	* *warning_level*: Define el umbral que establece para desencadenar una alerta de aviso.
	* *frequency*: Define la frecuencia con la que comprueba los datos.
	* *dashboard_url*: Define un URL que muestra en Grafana un panel de control con la consulta.
	* *notifications*: El método de notificación en el caso de que se desencadene la alerta descrita con esta regla.
	
	Por ejemplo, el archivo de regla myrulefile.json tiene el siguiente aspecto:
	
	```
	{
    "name": "checkbytesin",
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
      "emailXXX"
    ]
    }
    ```
	{: screen}
	
	A continuación, exporte la variable *RULE_FILE*:
	
	```
	export RULE_FILE="myrulefile.json"
	```
	{: screen}
	
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}.

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

3. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal de UAA, consulte [Obtención de una señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
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
	
4. Obtenga el GUID del espacio. El GUID debe tener el prefijo *s-* para identificar un espacio.

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
	
5. Ejecute el mandato cURL siguiente para registrar la regla en el servicio {{site.data.keyword.monitoringshort}}:

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
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
	
    Por ejemplo, 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## Supresión de una regla
{: #delete}

Para suprimir una regla, siga los pasos siguientes:

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
		
4. Ejecute el siguiente mandato cURL para suprimir una regla:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	donde
	
    * *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* Rule_Name es el nombre de la regla especificada en el campo *name*.
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    
	
## Listado de todas las reglas
{: #list}

Para obtener una lista de todas las reglas, siga estos pasos:

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
	
4. Ejecute el siguiente mandato cURL para obtener una lista de todas las reglas de un espacio:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	donde
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

	
	

## Cómo mostrar los detalles de una regla
{: show}

Para mostrar los detalles de una regla, siga estos pasos:

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
	
4. Ejecute el siguiente mandato cURL para mostrar los detalles de una regla:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	donde
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* Rule_Name es el nombre de la regla especificada en el campo *name*.
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

## Actualización de una regla
{: #update}

Para actualizar una regla, modifíquela mediante la actualización del archivo de regla y, a continuación, siga estos pasos:

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
	
4. Ejecute el siguiente mandato cURL para actualizar una regla:

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	donde
	
	* RULE_FILE es el archivo JSON que define la regla de alerta.
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* La señal es la señal de autenticación de UAA o IAM, o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

	
	
