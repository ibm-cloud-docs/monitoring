---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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


# Análisis de métricas para una app desplegada en un clúster de Kubernetes
{: #kubernetes_cluster}

Utilice esta guía de aprendizaje para aprender a configurar un clúster para que reenvíe métricas al servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Puede utilizar el servicio {{site.data.keyword.mon_full_notm}} para supervisar clústeres de Kubernetes.

Para configurar un clúster para que reenvíe métricas, debe instalar un agente en cada nodo trabajador en el clúster de Kubernetes mediante un DaemonSet. El agente de Sysdig utiliza una clave de acceso (señal) para autenticarse con la instancia de {{site.data.keyword.mon_full_notm}}. El agente de Sysdig actúa como recopilador de datos. Recopila automáticamente métricas como por ejemplo *CPU de nodo trabajador* y memoria de nodo trabajador*, *tráfico HTTP de entrada y salida de contenedores* y varias partes de software de infraestructura común. Además, el agente puede recopilar métricas de aplicación personalizadas mediante una herramienta de recopilación compatible con Prometheus o una interfaz de statsd. 

Las métricas se visualizan en una interfaz de usuario web de Sysdig.

![Visión general de los componentes de {{site.data.keyword.cloud_notm}}](../images/kube.png "Visión general de los componentes de {{site.data.keyword.cloud_notm}}")



## Antes de empezar
{: #kubernetes_cluster_prereqs}

Para seguir los pasos de esta guía de aprendizaje de iniciación, se ofrecen instrucciones para suministrar una instancia en {{site.data.keyword.mon_full_notm}} en la región EE. UU. sur. Puede utilizar un clúster existente o un nuevo **clúster de la versión 1.10**. El clúster puede estar disponible en otra región.  

Obtenga más información sobre {{site.data.keyword.mon_full_notm}}. Encontrará detalles en la sección [Acerca de](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Utilice un ID de usuario que sea miembro o propietario de una cuenta de {{site.data.keyword.cloud_notm}}. Para obtener un ID de usuario de {{site.data.keyword.cloud_notm}}, vaya a: [Registro ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window}.

El ID de {{site.data.keyword.IBM_notm}} debe tener asignadas políticas de IAM para cada uno de los siguientes recursos: 

| Recurso                             | Ámbito de la política de acceso | Rol    | Región    | Información                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Grupo de recursos **predeterminado**           |  Grupo de recursos            | Visor  | us-south  | Esta política es necesaria para permitir que el usuario vea las instancias de servicio en el grupo de recursos predeterminado.    |
| Servicio {{site.data.keyword.mon_full_notm}} |  Grupo de recursos            | Editor  | us-south  | Esta política es necesaria para permitir que el usuario suministre y administre el servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos predeterminado.   |
| Instancia de clúster de Kubernetes          |  Recurso                 | Editor  | us-south  | Esta política es necesaria para configurar el secreto y el agente de Sysdig en el clúster de Kubernetes. |
{: caption="Tabla 1. Lista de políticas de IAM necesarias para completar la guía de aprendizaje" caption-side="top"} 

Para obtener más información sobre los roles de IAM de {{site.data.keyword.containerlong}}, consulte [Permisos de acceso de usuario](/docs/containers?topic=containers-access_reference#access_reference).

Instale la CLI de {{site.data.keyword.cloud_notm}} y el plugin de la CLI de Kubernetes. Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Paso 1: Suministrar una instancia de {{site.data.keyword.mon_full_notm}}
{: #kubernetes_cluster_step1}

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

8. Seleccione el plan de servicio **Prueba**. 

    De forma predeterminada, se selecciona el plan de **Prueba**.

    Para obtener más información acerca de los otros planes de servicio, consulte [Planes de servicio](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Para suministrar el servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos de {{site.data.keyword.cloud_notm}} en el que ha iniciado la sesión, pulse **Crear**.

Después de suministrar una instancia, se abre el panel de control *Observabilidad*. 


**Nota:** para suministrar una instancia mediante la CLI, consulte [Suministro de una instancia mediante la CLI de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Paso 2: Configurar el clúster de Kubernetes para que envíe métricas a la instancia
{: #kubernetes_cluster_step2}

Para configurar el clúster de Kubernetes para que envíe métricas a su instancia de {{site.data.keyword.mon_full_notm}}, debe instalar un pod de agente de Sysdig en cada nodo del clúster. El agente de Sysdig se instala mediante un DaemonSet que garantiza que se ejecute una instancia del agente en cada nodo trabajador. El agente de Sysdig recopila métricas del pod en el que está instalado y los reenvía a la instancia.

**Nota:** para proporcionar la suite completa de métricas del sistema, el agente de Sysdig necesita tener un estado con privilegios.

Para configurar el clúster de Kubernetes para que reenvíe métricas a la instancia de {{site.data.keyword.mon_full_notm}}, siga los pasos siguientes desde la línea de mandatos:

1. Abra un terminal. A continuación, inicie una sesión en {{site.data.keyword.cloud_notm}}. Ejecute el mandato siguiente y siga las indicaciones:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    Seleccione la cuenta en la que ha suministrado la instancia de {{site.data.keyword.mon_full_notm}}.

2. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

3. Obtenga la clave de acceso de Sysdig. Para obtener más información, consulte [Obtención de la clave de acceso mediante la IU de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

4. Obtenga el URL de ingestión. Para obtener más información, consulte [Puntos finales del recopilador de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

5. Despliegue el agente de Sysdig. Ejecute el mandato siguiente:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    donde

    * SYSDIG_ACCESS_KEY es la clave de ingestión para la instancia.

    * COLLECTOR_ENDPOINT es el URL de ingestión para la región en la que está disponible la instancia de supervisión.

    * TAG_DATA son etiquetas separadas por comas con el formato *NOMBRE_ETIQUETA_VALOR:ETIQUETA*. Puede asociar una o varias etiquetas al agente de Sysdig. Por ejemplo: *role:serviceX,location:us-south*. Más adelante podrá utilizar estas etiquetas para identificar las métricas del entorno en el que se ejecuta el agente.

    * Establezca **sysdig_capture_enabled** en *false* para inhabilitar la característica de captura de Sysdig. De forma predeterminada, está establecido en *true*. Para obtener más información, consulte [Cómo trabajar con capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

6. Verifique que el agente de Sysdig se ha creado correctamente y compruebe su estado. Ejecute el mandato siguiente:

    ```
    kubectl get pods
    ```
    {: codeblock}



## Paso 3: Iniciar la interfaz de usuario web de Sysdig
{: #kubernetes_cluster_step3}

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


## Paso 4: Supervisar el clúster
{: #kubernetes_cluster_step4}

Puede supervisar el clúster en la vista **EXPLORAR** que está disponible a través de la interfaz de usuario web. Esta vista constituye el punto de partida para solucionar problemas y supervisar la infraestructura. Es la página de inicio predeterminada de la interfaz de usuario web para los usuarios.

En la sección *Host y contenedores*, puede ver la lista de nodos trabajadores de su clúster que están reenviando métricas a la instancia de supervisión. Cada entrada de nodo trabajador representa un grupo de objetos relacionados de la infraestructura para ese nodo trabajador.

Pulse **Host y contenedores**![Host y contenedores](../images/switch_hosts.png) para cambiar los orígenes de datos. A continuación, seleccione un nodo trabajador. Los datos que se muestran corresponden al nodo trabajador que ha seleccionado.

Si pulsa ** Volver a la tabla Explorar**, se muestra la *tabla Explorar*. Cada columna muestra una métrica diferente. Puede configurar cada métrica individualmente. Puede cambiar el orden de las columnas. Tenga en cuenta que, cuando se hacen cambios en el orden de las columnas existentes, el cambio se aplica a las distintas agrupaciones mientras dure la sesión. Si añade o elimina una columna, el cambio es permanente. También puede configurar colores para resaltar valores y facilitar su lectura.

Por ejemplo, para configurar códigos de colores para una columna, siga los pasos siguientes:

1. Seleccione una columna. Mueva el puntero del ratón sobre el título de la columna. A continuación, seleccione el icono de lápiz.
2. Conmute la barra para habilitar la codificación por colores.
3. Defina valores para los distintos umbrales.

Si selecciona un nodo trabajador, se muestra un panel de control predeterminado. Pulse ![cambiar panel de control](images/switch_dashboards_1.png) y explore los distintos paneles de control predeterminados y las distintas métricas. Tenga en cuenta que solo puede seleccionar métricas y paneles de control que sean relevantes para el nodo trabajador seleccionado.


## Pasos siguientes
{: #kubernetes_cluster_next_steps}

Cree un panel de control personalizado. Para obtener más información, consulte [Cómo trabajar con paneles de control](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

También puede aprender sobre las alertas. Para obtener más información, consulte [Cómo trabajar con alertas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






