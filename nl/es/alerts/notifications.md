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


# Notificaciones CRUD
{: #notifications}

Utilice la API de alertas para crear, suprimir y actualizar una notificación, para mostrar los detalles de una notificación y para listar las notificaciones que se definen en un espacio.
{:shortdesc}

## Creación de una notificación
{: #notifications_create}

Para
crear una notificación, siga los pasos siguientes:

1. Cree un archivo de notificación.

    1. Utilice una plantilla de notificación para crear un archivo de notificación. Para obtener más información, consulte [Plantillas de notificación](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template).
	
	2. Actualice el archivo:
	
	    * Escriba un nombre exclusivo en el campo *name*. El valor de este campo se utiliza más adelante para actualizar, suprimir y mostrar los detalles de la notificación.
		* Entre una descripción.
		* Escriba una dirección de correo electrónico, punto final de URL o clave de PagerDuty válidos.
		
	3. Guarde el archivo. Por ejemplo, utilice un prefijo como *s-* para las notificaciones que defina para las consultas que se ejecutan en un espacio.
	
	    **Consejo:** Cree su archivo de notificaciones en el siguiente directorio: *~/cloud-monitoring/notifications/* para agrupar los recursos del servicio {{site.data.keyword.monitoringshort_notm}}. 
	
	4. Exporte la variable *NOTIFICATION_FILE*:
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

3. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
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
	
5. Registre una notificación con el servicio {{site.data.keyword.monitoringshort}}.

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	donde
	
	* NOTIFICATION_FILE es el archivo JSON que define la notificación.
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-Scope-Id* es un parámetro que pasa el GUID de espacio. El GUID debe tener el prefijo *s-* para identificar un espacio. Esta cabecera es necesaria si utiliza una autenticación de señal de UAA. Si utiliza una señal de autenticación de IAM, esta cabecera es opcional y se utiliza la información de dominio enlazada con la señal.
	
	* La señal es la señal de UAA, la señal de IAM o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    Por ejemplo, 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## Supresión de una notificación
{: #notifications_delete}

Para suprimir una notificación, siga los pasos siguientes:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
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
	
	A continuación, exporte la variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Ejecute el siguiente mandato cURL para suprimir una notificación:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	donde
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}. La señal o la clave de API deben llevar uno de los siguientes prefijos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
		
	* La señal es la señal de UAA, la señal de IAM o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* Notification_Name es el nombre de la notificación, es decir, el valor del campo *name* cuando genera una lista de las propiedades de una notificación.
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	


## Listado de todas las notificaciones
{: #notifications_list}

Para obtener una lista de todas las notificaciones, siga estos pasos:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
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
	
	A continuación, exporte la variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Ejecute el siguiente mandato cURL para obtener una lista de todas las notificaciones:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	donde
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
		
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}. La señal o la clave de API deben llevar uno de los siguientes prefijos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
		
	* La señal es la señal de UAA, la señal de IAM o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

			

## Muestra de los detalles de una notificación
{: #show}


Para mostrar la información sobre una notificación, siga los siguientes pasos:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
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
	
	A continuación, exporte la variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Ejecute el siguiente mandato cURL para mostrar los detalles de una notificación:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	donde
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
		
	* La señal es la señal de UAA, la señal de IAM o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* NOTIFICATION_NAME es el nombre de la notificación, es decir, el valor del campo *name* cuando genera una lista de las propiedades de una notificación.
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
     
		

			
## Prueba de una notificación
{: #test}	
			
Para probar una notificación, siga los pasos siguientes:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
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
	
	A continuación, exporte la variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Ejecute el siguiente mandato cURL para probar una notificación:

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	donde
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de {{site.data.keyword.Bluemix_notm}}. La señal o la clave de API deben llevar uno de los siguientes prefijos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
		
	* La señal es la señal de UAA, la señal de IAM o la clave de API.
	
	* Space es el GUID del espacio. 
	
	* NOTIFICATION_NAME es el nombre de la notificación, es decir, el valor del campo *name* cuando genera una lista de las propiedades de una notificación.
	
	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	


## Actualización de una notificación
{: #notifications_update}

Para actualizar una notificación, siga los pasos siguientes:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenga la señal de seguridad. Puede utilizar una señal de UAA, una señal de IAM o una clave de API. Elija uno de los métodos siguientes para obtener la señal de seguridad:
	
	* Para obtener una señal UAA, consulte [Obtención de la señal de UAA mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Para obtener una señal de IAM, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
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
	
	A continuación, exporte la variable *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Ejecute el siguiente mandato cURL para actualizar una notificación:

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	donde
	
	* NOTIFICATION_FILE es el archivo JSON que define la notificación.
	
	* *Auth_Type* es el prefijo que define el tipo de señal o de clave de API. En la lista siguiente se muestran los valores válidos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
	
	* El valor *X-Auth-User-Token* es un parámetro que pasa la señal de UAA, la señal de IAM o la clave de API de bluemix. La señal o la clave de API deben llevar uno de los siguientes prefijos: *apikey*, *iam* o *uaa*, donde

        * *apikey* identifica que la señal es una clave de API.
		* *iam* identifica que la señal especificada es una señal generada por IAM.
		* *uaa* identifica que la señal especificada es una señal generada por UAA.
		
	* La señal es la señal de UAA, la señal de IAM o la clave de API.
	
	* Space es el GUID del espacio. 

	* METRICS_ENDPOINT representa el punto de entrada al servicio. Cada región tiene un URL diferente. Para obtener la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
        

