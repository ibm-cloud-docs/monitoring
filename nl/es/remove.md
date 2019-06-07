---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# Eliminación de una instancia
{: #remove}

Puede eliminar una instancia del servicio {{site.data.keyword.mon_full_notm}} desde la interfaz de usuario de {{site.data.keyword.Bluemix}} o a través de la línea de mandatos.
{:shortdesc}

Cuando elimine una instancia de {{site.data.keyword.cloud_notm}}, tenga en cuenta la siguiente información:

1. Anote la lista de orígenes que reenvían métricas a la instancia de {{site.data.keyword.mon_full_notm}} que desea eliminar. Debe eliminar el agente de Sysdig de cada origen.
2. Elimine los permisos otorgados a los usuarios para que trabajen con la instancia. 

    Si utiliza un grupo de acceso para gestionar permisos para acceder a la instancia, debe eliminar el grupo de acceso.

    Si utiliza un grupo de acceso para gestionar permisos para acceder a diferentes instancias de servicio, debe eliminar las políticas que otorgan permisos a la instancia que desea eliminar.
    
    Si otorga políticas individuales a los usuarios, debe reunir la información de cada usuario que tenga acceso a la instancia. Luego debe eliminar una por una las políticas relacionadas con la instancia que desea suprimir.


A continuación, suprima la instancia del panel de control de {{site.data.keyword.cloud_notm}}.


## Eliminación de una instancia mediante la interfaz de usuario de {{site.data.keyword.cloud_notm}}
{: #remove_ui}

Para eliminar una instancia de {{site.data.keyword.mon_full_notm}} mediante la interfaz de usuario de {{site.data.keyword.cloud_notm}}, siga los pasos siguientes:

1. [Inicie una sesión en su cuenta de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window}.

	Cuando inicia una sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.cloud_notm}}.

2. Seleccione **Observabilidad**. 

3. Seleccione **Supervisión**. Se muestra la lista de instancias.

4. Seleccione la instancia que desea suprimir.

5. En el menú *Acción*, seleccione **Eliminar**.


## Eliminación de una instancia mediante la CLI
{: #remove_cli}

Para eliminar una instancia de {{site.data.keyword.mon_full_notm}} mediante la línea de mandatos, siga los pasos siguientes:

1. [Requisito previo] Instalación de la CLI de {{site.data.keyword.cloud_notm}}. Si la CLI está instalada, continúe en el paso siguiente.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

2. Inicie una sesión en {{site.data.keyword.cloud_notm}} donde desea suministrar la instancia. Ejecute el siguiente mandato: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Establezca el grupo de recursos en el que se ha suministrado la instancia. Ejecute el siguiente mandato: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    De forma predeterminada, está establecido el grupo de recursos `default`.

4. Elimine la instancia. Ejecute el mandato [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete):

    ```
    ibmcloud resource service-instance-delete NAME 
    ```
    {: codeblock}

    Donde NAME es el nombre de la instancia

    Por ejemplo, para eliminar una instancia, ejecute el mandato siguiente:

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
