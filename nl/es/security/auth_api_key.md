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


# Trabajo con claves de API
{: #auth_api_key}

Puede obtener una API mediante la CLI de {{site.data.keyword.Bluemix}} o la IU de {{site.data.keyword.Bluemix_notm}}. La clave de API no caduca. Si una API está en peligro, puede revocarla y generar una nueva.
{:shortdesc}

## Generación de una clave de API IAM mediante la CLI de IBM Cloud
{: #iam_apikey_cli}

Complete los pasos siguientes para generar una clave de API utilizando la CLI de {{site.data.keyword.Bluemix_notm}}:

1. (Requisito previo) Instalar la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa).
   
   Si la CLI está instalada, continúe en el paso siguiente.
	
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
 
3. Ejecute el mandato `ibmcloud iam api-key-create` para crear una clave de API.

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	donde
	
	* NAME es el nombre de la clave de API que se va a crear.
	* DESCRIPTION es el texto que utilizará para describir la clave de API.
	* FILE es el nombre del archivo en el que se guarda la clave.
	
    Por ejemplo, para crear una clave de API *MyKey*, ejecute el siguiente mandato:
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## Generación de una clave de API IAM mediante la IU de IBM Cloud
{: #iam_apikey_ui}

Complete los pasos siguientes para generar una clave de API mediante la IU de {{site.data.keyword.Bluemix_notm}}:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús de la consola, pulse **Gestionar > Seguridad > Claves de API de IBM Cloud**.

3. Pulse **Crear una clave de API**.

4. Especifique un nombre y una descripción para su clave de API. A continuación, pulse **Crear clave de API**.

5. Guarde la clave de API. Pulse **Descargar clave de API**.

    Pulse **Mostrar** para ver la clave de API.  

**Nota:** La clave de API únicamente está disponible para ser mostrada o descargada en el momento de su creación. Si se pierde la clave de API, deberá crear una nueva clave de API.  


	
## Revocación de una clave de API mediante la interfaz de usuario de IBM Cloud
{: #revoke_ui}
	
Siga estos pasos para revocar una clave de API IAM mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús de la consola, pulse **Gestionar > Seguridad > Claves de API de IBM Cloud**.

3. Pulse **Acciones** y, a continuación, **Suprimir clave**.





	

	
	
	
	
	
	
