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


# Suministro del servicio de supervisión
{: #provision}

Puede suministrar el servicio {{site.data.keyword.monitoringshort}} desde la interfaz de usuario de {{site.data.keyword.Bluemix}}, o desde la línea de mandatos.
{:shortdesc}


## Suministro desde la interfaz de usuario
{: #ui}

Siga estos pasos para suministrar una instancia del servicio {{site.data.keyword.monitoringshort}} en {{site.data.keyword.Bluemix_notm}}:

1. Inicie sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}.

    El panel de control de {{site.data.keyword.Bluemix_notm}} se puede encontrar en: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}.
    
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. Pulse **Catálogo**. Se abre la lista de los servicios que están disponibles en {{site.data.keyword.Bluemix_notm}}.

3. Seleccione la categoría **DevOps** para filtrar la lista de servicios que se muestra.

4. Pulse el mosaico **Supervisión**.

5. Seleccione un plan de servicio. 

    * Para recopilar y acceder a las métricas durante un máximo de 45 días, y para definir reglas de alertas, incluidas reglas con caracteres comodín, seleccione el plan **Premium**. 
	
	* De forma predeterminada, se establece el plan **Lite**, que le autoriza para recopilar métricas de plataforma en el espacio donde suministra el servicio y permite un periodo de retención de 15 días para dichas métricas. 

    Para obtener más información acerca de los planes de servicio, consulte [Planes de servicio](/docs/services/cloud-monitoring/monitoring_ov.html#plan).
	
6. Pulse **Crear** para suministrar el servicio {{site.data.keyword.monitoringshort}} en el espacio de {{site.data.keyword.Bluemix_notm}} en el que ha iniciado la sesión.
  
 

## Suministro desde la CLI
{: #cli}

Siga estos pasos para suministrar una instancia del servicio {{site.data.keyword.monitoringshort}} en {{site.data.keyword.Bluemix_notm}} mediante la línea de mandatos:

1. [Requisito previo] Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
3. Ejecute el mandato `ibmcloud service create` para suministrar una instancia.

    ```
	ibmcloud service create service_name service_plan service_instance_name
	```
	{: codeblock}
    
    donde
    	
    * *service_name* es **Supervisión**.
    * *service_plan* es el nombre del plan de servicio. Para recopilar y acceder a las métricas durante un máximo de 45 días, y para definir reglas de alertas, incluidas reglas con caracteres comodín, seleccione el plan **Premium**. De forma predeterminada, se establece el plan **Lite**, que le autoriza para recopilar métricas de plataforma en el espacio donde suministra el servicio y permite un periodo de retención de 15 días para dichas métricas. Para ver una lista de planes, consulte [Planes de servicio de {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/monitoring_ov.html#plan).
    * *service_instance_name* es el nombre que desea utilizar para la nueva instancia del servicio que crea.
    
    Por ejemplo, para crear una instancia del servicio {{site.data.keyword.monitoringshort}} con un plan premium, ejecute el mandato siguiente:
    
	```
	ibmcloud service create Monitoring premium my_monitoring_svc
	```
	{: codeblock}
    
4. Verifique que el servicio se ha creado correctamente. Ejecute el mandato siguiente:

    ```	
	ibmcloud service list
	```
	{: codeblock}
	
	La salida de la ejecución del mandato tiene el siguiente aspecto:
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_monitoring_svc              Monitoring               premium                                        create succeeded
	```
	{: screen}

	



