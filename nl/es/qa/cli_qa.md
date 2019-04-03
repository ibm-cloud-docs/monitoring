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



# Preguntas frecuentes de la CLI de IBM Cloud
{: #cli_qa}

Aquí encontrará las respuestas a preguntas comunes sobre el uso de la CLI de {{site.data.keyword.Bluemix}} con el servicio {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [¿Cómo iniciar sesión en {{site.data.keyword.Bluemix_notm}}?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)
* [¿Cómo se instala la CLI de {{site.data.keyword.Bluemix_notm}}?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#install_bmx_cli)
* [¿Cómo se obtiene el GUID de una cuenta?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#account_guid)
* [¿Cómo se obtiene el GUID de una organización?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#org_guid)
* [¿Cómo se obtiene el GUID de un espacio?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid)

## ¿Cómo iniciar sesión en IBM Cloud?
{: #login}

Ejecute el siguiente mandato para iniciar una sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}:

```
ibmcloud login -a Endpoint
```
{: codeblock}
	
Donde *Endpoint* es el URL para iniciar sesión en {{site.data.keyword.Bluemix_notm}}. Este URL es diferente según la región.
	
<table>
    <caption>Lista de puntos finales para acceder a {{site.data.keyword.Bluemix_notm}}</caption>
	<tr>
	  <th>Región</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>Alemania</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>Sídney</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>Reino Unido</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
	<tr>
	  <td>EE.UU. sur</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
</table>

Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

Siga las instrucciones. 

A continuación, establezca la organización y el espacio. Ejecute el mandato siguiente:

```
ibmcloud target -o OrgName -s SpaceName
```
{: codeblock}

donde

* OrgName es el nombre de la organización.
* SpaceName es el nombre del espacio.

	
## ¿Cómo se instala la CLI de IBM Cloud?
{: #install_bmx_cli}

Consulte [Descargar e instalar la CLI de {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview).

## ¿Cómo se obtiene el GUID de una cuenta?
{: #account_guid}
	
Siga estos pasos para obtener el GUID de una cuenta:
	
1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. Ejecute el mandato:

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	Donde *Endpoint* es el URL para iniciar sesión en {{site.data.keyword.Bluemix_notm}}. Este URL es diferente según la región.
	
	<table>
	    <caption>Lista de puntos finales para acceder a {{site.data.keyword.Bluemix_notm}}</caption>
		<tr>
		  <th>Región</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>EE.UU. sur</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>Reino Unido</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Siga las instrucciones. Escriba sus credenciales de {{site.data.keyword.Bluemix_notm}}, seleccione una organización y un espacio.
	
	Para los **ID de usuario federados**, ejecute el mandato siguiente y siga las instrucciones:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. Ejecute el mandato `ibmcloud iam accounts` para obtener el GUID de una cuenta.

    ```
	ibmcloud iam accounts
	```
	{: codeblock} 
	
	Por ejemplo, para recuperar todas las cuentas con sus correspondientes GUID para el usuario xxx@yyy.com, ejecute el mandato:
	
	```
	ibmcloud iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## ¿Cómo se obtiene el GUID de una organización?
{: #org_guid}

Siga los pasos siguientes para obtener el GUID de una organización:
	
1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. Ejecute el mandato:

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	Donde *Endpoint* es el URL para iniciar sesión en {{site.data.keyword.Bluemix_notm}}. Este URL es diferente según la región.
	
	<table>
	    <caption>Lista de puntos finales para acceder a {{site.data.keyword.Bluemix_notm}}</caption>
		<tr>
		  <th>Región</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>EE.UU. sur</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>Reino Unido</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Siga las instrucciones. Escriba sus credenciales de {{site.data.keyword.Bluemix_notm}}, seleccione una organización y un espacio.
	
	Para los ID de usuario federados, ejecute el mandato siguiente y siga las instrucciones:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}

2. Ejecute el mandato `ibmcloud iam org` para obtener el GUID de organización. 

    ```
    ibmcloud iam org NAME --guid
    ```
    {: codeblock}
	
    donde NAME es el nombre de la organización de {{site.data.keyword.Bluemix_notm}}.        
		
## ¿Cómo se obtiene el GUID de un espacio?
{: #space_guid}
	
Siga estos pasos para obtener el GUID de un espacio:
	
1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. Ejecute el mandato:

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	Donde *Endpoint* es el URL para iniciar sesión en {{site.data.keyword.Bluemix_notm}}. Este URL es diferente según la región.
	
	<table>
	    <caption>Lista de puntos finales para acceder a {{site.data.keyword.Bluemix_notm}}</caption>
		<tr>
		  <th>Región</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>EE.UU. sur</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>Reino Unido</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Siga las instrucciones. Escriba sus credenciales de {{site.data.keyword.Bluemix_notm}}, seleccione una organización y un espacio.
	
	Para los ID de usuario federados, ejecute el mandato siguiente y siga las instrucciones:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. Ejecute el mandato `ibmcloud iam space` para obtener el GUID del espacio. 

    ```
    ibmcloud iam space NAME --guid
    ```
    {: codeblock}
	
    donde NAME es el nombre de un espacio de {{site.data.keyword.Bluemix_notm}}. 
	
    Por ejemplo, para obtener la GUID del espacio *dev*, ejecute el mandato siguiente:
	
    ```
    ibmcloud iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		
