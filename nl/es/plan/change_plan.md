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


# Cambio del plan
{: #change_plan}

Puede cambiar su plan de servicio de {{site.data.keyword.monitoringshort}} a través del panel de control de {{site.data.keyword.monitoringlong_notm}} o ejecutando el mandato `cf update-service`. Puede actualizar o reducir el plan siempre que lo desee.
{:shortdesc}

## Cambio del plan de servicio mediante la interfaz de usuario
{: #change_plan_ui}

Para cambiar el plan de servicio en el panel de control de {{site.data.keyword.monitoringlong_notm}}, siga estos pasos:

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}} y pulse el servicio {{site.data.keyword.monitoringshort}} en el panel de control. 

    Se abre el panel de control del servicio {{site.data.keyword.monitoringshort}}.
    
2. Seleccione el separador **Plan**.

    Aparecerá información sobre el plan actual.
	
3. Seleccione un nuevo plan para actualizar o reducir su plan. 

4. Pulse **Guardar**.



## Cambio del plan de servicio mediante la CLI
{: #change_plan_cli}

Para cambiar el plan de servicio en {{site.data.keyword.Bluemix_notm}} a través de la CLI, siga estos pasos:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
	
2. Ejecute el mandato `ibmcloud service list` para comprobar su plan actual y para obtener el nombre del servicio {{site.data.keyword.loganalysisshort}} de la lista de servicios disponibles en el espacio. 

    El valor del campo **name** es el que debe utilizar para cambiar el plan. 

    Por ejemplo,
	
	```
	$ ibmcloud service list
	Getting services in org MyOrg / space dev as xxx@yyy.com...
	OK
	name            service      plan   bound apps   last operation
	Monitoring-0c   Monitoring   premium             create succeeded
    ```
	{: screen}
    
3. Actualice o reduzca su plan. Ejecute el mandato `ibmcloud service update`.
    
	```
	ibmcloud service update service_name [-p new_plan]
	```
	{: codeblock}
	
	donde 
	
	* *service_name* es el nombre del servicio. 
	* *new_plan* es el nombre del plan.
	
	En la tabla siguiente se muestran los distintos planes y los valores que admiten:
	
	<table>
	  <caption>Tabla 1. Lista de planes.</caption>
	  <tr>
	    <th>Plan</th>
		<th>Características</th>
	    <th>Nombre</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>Supervisión gratuita.</td>
		<td>lite</td>
	  </tr>
	  <tr>
	    <td>Premium</td>
	    <td>Supervisión Premium.</td>
		<td>premium</td>
	  </tr>
	</table>
	
	Por ejemplo, para reducir su plan al plan *Lite*, ejecute el siguiente mandato:
	
	```
	ibmcloud service update "Monitoring-0c" -p lite
    Updating service instance Monitoring-0c as xxx@yyy.com...
    OK
	```
	{: screen}

4. Verifique que el plan se ha modificado. Ejecute el mandato `ibmcloud service list`.

    ```
	ibmcloud service list
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service       plan   bound apps   last operation
    Monitoring-0c     Monitoring    lite                create succeeded
	```
	{: screen}






