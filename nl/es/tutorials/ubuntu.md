---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# Análisis de métricas para un host Ubuntu
{: #ubuntu}

Utilice esta guía de aprendizaje para aprender a configurar un host Ubuntu para que reenvíe métricas al servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Para configurar un servidor Ubuntu para que reenvíe métricas, debe instalar un agente de Sysdig. El agente utiliza una clave de acceso (señal) para autenticarse con la instancia de {{site.data.keyword.mon_full_notm}}. El agente de Sysdig actúa como recopilador de datos. Recopila métricas de forma automática.

Las métricas se visualizan en una interfaz de usuario web de Sysdig.

![Visión general de los componentes de {{site.data.keyword.cloud_notm}}](../images/ubuntu.png "Visión general de los componentes de {{site.data.keyword.cloud_notm}}")



## Antes de empezar
{: #ubuntu_prereqs}

Trabaje en la región EE. UU. sur. 

Obtenga más información sobre {{site.data.keyword.mon_full_notm}}. Encontrará detalles en la sección [Acerca de](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Utilice un ID de usuario que sea miembro o propietario de una cuenta de {{site.data.keyword.cloud_notm}}. Para obtener un ID de usuario de {{site.data.keyword.cloud_notm}}, vaya a: [Registro ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window}.

El ID de {{site.data.keyword.IBM_notm}} debe tener asignadas políticas de IAM para cada uno de los siguientes recursos: 

| Recurso                             | Ámbito de la política de acceso | Rol    | Región    | Información                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Grupo de recursos **predeterminado**           |  Grupo de recursos            | Visor  | us-south  | Esta política es necesaria para permitir que el usuario vea las instancias de servicio en el grupo de recursos predeterminado.    |
| Servicio {{site.data.keyword.mon_full_notm}} |  Grupo de recursos            | Editor  | us-south  | Esta política es necesaria para permitir que el usuario suministre y administre el servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos predeterminado.   |
{: caption="Tabla 1. Lista de políticas de IAM necesarias para completar la guía de aprendizaje" caption-side="top"} 

Instale la CLI de {{site.data.keyword.cloud_notm}}. Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Paso 1: Suministrar una instancia de {{site.data.keyword.mon_full_notm}}
{: #ubuntu_step1}

Para suministrar una instancia de {{site.data.keyword.mon_full_notm}} mediante la interfaz de usuario de {{site.data.keyword.cloud_notm}}, siga los pasos siguientes:

1. Inicie una sesión en su cuenta de {{site.data.keyword.cloud_notm}}.

    Pulse el [panel de control de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window} para iniciar el panel de control de {{site.data.keyword.cloud_notm}}.

	Cuando inicia una sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.cloud_notm}}.

2. Pulse **Catálogo**. Se abrirá la lista de servicios disponibles en {{site.data.keyword.cloud_notm}}.

3. Para filtrar la lista de servicios que se visualiza, seleccione la categoría **Herramientas de desarrollador**.

4. Pulse el mosaico **{{site.data.keyword.mon_full_notm}}**. Se abre el panel de control *Observabilidad*.

5. Seleccione **Crear instancia**. 

6. Especifique un nombre para la instancia de servicio.

7. Seleccione el grupo de recursos **predeterminado**. 

    De forma predeterminada, se selecciona el grupo de recursos **predeterminado**.

8. Seleccione el plan de servicio **Lite**. 

    De forma predeterminada, se establece el plan **Lite**.

    Para obtener más información acerca de los otros planes de servicio, consulte [Planes de servicio](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Para suministrar el servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos de {{site.data.keyword.cloud_notm}} en el que ha iniciado la sesión, pulse **Crear**.

Después de suministrar una instancia, se abre el panel de control *Observabilidad*. 


**Nota:** para suministrar una instancia mediante la CLI, consulte [Suministro de una instancia mediante la CLI de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Paso 2: Configurar el servidor Ubuntu para que envíe métricas a la instancia
{: #ubuntu_step2}

Para configurar el servidor Ubuntu para que envíe métricas a la instancia de {{site.data.keyword.mon_full_notm}}, debe instalar un agente de Sysdig. 

Siga los pasos siguientes desde la línea de mandatos:

1. Abra un terminal. A continuación, inicie una sesión en {{site.data.keyword.cloud_notm}}. Ejecute el mandato siguiente y siga las indicaciones:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    Seleccione la cuenta en la que ha suministrado la instancia de {{site.data.keyword.mon_full_notm}}.

2. Obtenga la clave de acceso de Sysdig. Para obtener más información, consulte [Obtención de la clave de acceso mediante la IU de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

3. Obtenga el URL de ingestión. Para obtener más información, consulte [Puntos finales del recopilador de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

4. Despliegue el agente de Sysdig. Ejecute el mandato siguiente:

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    donde

    * SYSDIG_ACCESS_KEY es la clave de ingestión para la instancia.

    * COLLECTOR_ENDPOINT es el URL de ingestión para la región en la que está disponible la instancia de supervisión.

    * TAG_DATA son etiquetas separadas por comas con el formato *NOMBRE_ETIQUETA_VALOR:ETIQUETA*. Puede asociar una o varias etiquetas al agente de Sysdig. Por ejemplo: *role:serviceX,location:us-south*. Más adelante podrá utilizar estas etiquetas para identificar las métricas del entorno en el que se ejecuta el agente.

    * Establezca **sysdig_capture_enabled** en *false* para inhabilitar la característica de captura de Sysdig. De forma predeterminada, está establecido en *true*. Para obtener más información, consulte [Cómo trabajar con capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

Si se produce un error al instalar el agente de Sysdig, instale las cabeceras de kernel manualmente. Seleccione una distribución y ejecute el mandato para dicha distribución. A continuación, intente de nuevo realizar un despliegue del agente de Sysdig.

* **Para las distribuciones de Linux Debian y Ubuntu**, ejecute el mandato siguiente:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **Para las distribuciones de Linux RHEL, CentOS y Fedora**, ejecute el siguiente mandato:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## Paso 3: Iniciar la interfaz de usuario web de Sysdig
{: #ubuntu_step3}

Siga los pasos siguientes para iniciar la interfaz de usuario web:

1. Inicie una sesión en su cuenta de {{site.data.keyword.cloud_notm}}.

    Pulse el [panel de control de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window} para iniciar el panel de control de {{site.data.keyword.cloud_notm}}.

	Cuando inicia una sesión con su ID de usuario y su contraseña, se abre el panel de control de {{site.data.keyword.cloud_notm}}.

2. En el menú de navegación, seleccione **Observabilidad**. 

3. Seleccione **Supervisión**. 

    Se muestra la lista de instancias que están disponibles en {{site.data.keyword.cloud_notm}}.

4. Seleccione su instancia. A continuación, pulse **Ver Sysdig**.

Si el agente de Sysdig se ha configurado correctamente, se abrirá la vista *EXPLORAR*.

Sin embargo, si el agente de Sysdig no se ha instalado correctamente, si apunta a un punto final de ingestión incorrecto o si la clave de acceso es incorrecta, la página que se abre le indica qué debe hacer a continuación.

Solo puede tener una sesión de interfaz de usuario web abierta por navegador.
{: tip}


## Paso 4: Supervisar el servidor Ubuntu
{: #ubuntu_step4}

Puede supervisar el servidor Ubuntu en la vista **EXPLORAR** que está disponible a través de la interfaz de usuario web. Esta vista constituye el punto de partida para solucionar problemas y supervisar la infraestructura. Es la página de inicio predeterminada de la interfaz de usuario web para los usuarios.

En la sección *Host y contenedores*, encontrará la entrada correspondiente al servidor Ubuntu. Pulse **Host y contenedores**![Host y contenedores](../images/switch_hosts.png) para cambiar los orígenes de datos. A continuación, seleccione el servidor Ubuntu. Los datos que se muestran corresponden al servidor Ubuntu que ha seleccionado.

Por ejemplo, para configurar códigos de colores para una columna, siga los pasos siguientes:

1. Seleccione una columna. Mueva el puntero del ratón sobre el título de la columna. A continuación, seleccione el icono de lápiz.
2. Conmute la barra para habilitar la codificación por colores.
3. Defina valores para los distintos umbrales.



## Pasos siguientes
{: #ubuntu_next_steps}

Cree un panel de control personalizado. Para obtener más información, consulte [Cómo trabajar con paneles de control](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

También puede aprender sobre las alertas. Para obtener más información, consulte [Cómo trabajar con alertas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






