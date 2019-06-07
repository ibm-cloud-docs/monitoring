---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

subcollection: Sysdig

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

# Suministro de una instancia
{: #provision}

Para poder supervisar y gestionar las métricas con Sysdig, debe suministrar una instancia del servicio en {{site.data.keyword.cloud_notm}}.
{:shortdesc}


## Suministro de una instancia de Sysdig desde el catálogo
{: #provision_ui}

Para suministrar una instancia de Sysdig desde el catálogo de {{site.data.keyword.cloud_notm}}, siga los pasos siguientes:

1. Inicie una sesión en su cuenta de {{site.data.keyword.cloud_notm}}.

    Pulse el [panel de control de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window} para iniciar el panel de control de {{site.data.keyword.cloud_notm}}.

	Cuando inicia una sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.cloud_notm}}.

2. Pulse **Catálogo**. Se abre la lista de los servicios que están disponibles en {{site.data.keyword.cloud_notm}}.

3. Para filtrar la lista de servicios que se visualiza, seleccione la categoría **Herramientas de desarrollador**.

4. Pulse el mosaico **{{site.data.keyword.mon_full_notm}}**. Se abre el panel de control *Observabilidad*.

5. Seleccione **Crear instancia**. 

6. Seleccione un plan de servicio. De forma predeterminada, se selecciona el plan de **Prueba**.

    Para obtener más información sobre los planes de servicio, consulte [Planes de servicio](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

7. Seleccione un grupo de recursos. De forma predeterminada, está establecido el grupo de recursos predeterminado (**Default**).

8. Pulse **Crear**.

Después de suministrar una instancia, 

* Se abre el panel de control *Observabilidad*. 
* Se crea automáticamente un ID de servicio. Puede utilizar este ID de servicio para obtener la clave de acceso de Sysdig para la instancia.

A continuación, configure un origen de métrica añadiendo un agente de Sysdig. Este agente es el responsable de recopilar y de reenviar métricas a Sysdig. 



## Suministro de una instancia de Sysdig mediante la CLI
{: #provision_cli}

Para suministrar una instancia de Sysdig mediante la línea de mandatos, siga los pasos siguientes:

1. [Requisito previo] Instalación de la CLI de {{site.data.keyword.cloud_notm}}. Si la CLI está instalada, continúe en el paso siguiente.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

2. Inicie una sesión en {{site.data.keyword.cloud_notm}} donde desea suministrar la instancia. Ejecute el siguiente mandato: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Establezca el grupo de recursos en el que desea suministrar la instancia. Ejecute el siguiente mandato: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    De forma predeterminada, está establecido el grupo de recursos `default`.

4. Cree la instancia de Sysdig. Ejecute el mandato [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create):

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    Donde

    * NAME es el nombre de la instancia de Sysdig.
    
    * `sysdig-monitor` es el nombre del servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}.
    
    * SERVICE_PLAN_NAME es el tipo de plan. Los valores válidos son *lite* y *graduated-tier*.
    
    * LOCATION es la región en la que se crea la instancia.

    Por ejemplo, para suministrar una instancia con el plan de pago, ejecute el mandato siguiente:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

