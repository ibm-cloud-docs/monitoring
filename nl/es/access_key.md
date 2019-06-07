---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# Gestión de claves de acceso
{: #access_key}

La **clave de acceso** es una señal que debe utilizar para configurar los agentes de Sysdig para que puedan enviar correctamente datos a la instancia de {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}.   
{:shortdesc}


## Obtención de la clave de acceso mediante la IU de {{site.data.keyword.cloud_notm}}
{: #access_key_ibm_cloud_ui}

Para obtener la clave de acceso para una instancia de {{site.data.keyword.mon_full_notm}} mediante la interfaz de usuario de {{site.data.keyword.cloud_notm}}, siga estos pasos:

1. Inicie una sesión en su cuenta de {{site.data.keyword.cloud_notm}}.

    Pulse el [panel de control de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window} para iniciar el panel de control de {{site.data.keyword.cloud_notm}}.

	Cuando inicia una sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.cloud_notm}}.

2. En el menú de navegación, seleccione **Observabilidad**. 

3. Seleccione **Supervisión**. Se abre el panel de control de {{site.data.keyword.mon_full_notm}}. Verá la lista de instancias de supervisión que están disponibles en {{site.data.keyword.cloud_notm}}.

3. Identifique la instancia para la que desea obtener la clave de acceso y pulse **Ver clave de acceso**.

4. Se abrirá una ventana emergente donde puede pulsar **Mostrar** para ver la clave de acceso.



## Obtención de la clave de acceso mediante la CLI
{: #access_key_cli}

Para obtener la clave de acceso para una instancia de Sysdig mediante la línea de mandatos, siga los pasos siguientes:

1. [Requisito previo] Instale la CLI de {{site.data.keyword.cloud_notm}}.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

   Si la CLI está instalada, continúe en el paso siguiente.

2. Inicie una sesión en la región de {{site.data.keyword.cloud_notm}} donde se ejecuta la instancia de Sysdig. Ejecute el siguiente mandato: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Establezca el grupo de recursos en el que se ejecuta la instancia de Sysdig. Ejecute el siguiente mandato: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    De forma predeterminada, está establecido el grupo de recursos `default`.

4. Obtenga el nombre de instancia. Ejecute el siguiente mandato: [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Obtenga el nombre de la clave de API que está asociada a la instancia de Sysdig. Ejecute el mandato [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances):

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    donde INSTANCE_NAME es el nombre de la instancia que ha obtenido en el paso anterior.

6. Obtenga la clave de acceso. Ejecute el mandato [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key):

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    donde APIKEY_NAME es el nombre de la clave de API.
 
    La salida de este mandato incluye el campo **Sysdig Access Key**, que contiene la clave de acceso de la instancia.


Por ejemplo, el mandato siguiente muestra la salida de un ID de servicio de ejemplo:

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf 
Created At:    Fri Nov  2 13:40:39 UTC 2018
State:         active
Credentials:
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
               Sysdig Customer Id:          111
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## Restablecimiento de la clave de acceso 
{: #access_key_reset}

Si la clave de acceso se ve comprometida o si tiene una política para renovarla transcurridos un cierto número de días, puede generar una nueva clave y suprimir la antigua.

Para renovar la clave de acceso para una instancia de {{site.data.keyword.mon_full_notm}}, siga estos pasos:

1. Inicie la interfaz de usuario web de {{site.data.keyword.mon_full_notm}}. Para obtener más información, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. En el botón *Selector* de la barra de navegación, seleccione **Valores**.

2. En la sección *Gestión de contraseñas*, pulse **Restablecer la contraseña**.

**Nota:** después de restablecer la clave de acceso de Sysdig, debe actualizar la clave de acceso para cualquier origen de registro que reenvíe métricas a esta instancia de {{site.data.keyword.mon_full_notm}}.
