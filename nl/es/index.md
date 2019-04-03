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


# Guía de aprendizaje de iniciación
{: #getting-started-with-ibm-cloud-monitoring}

Utilice esta guía de aprendizaje para aprender a empezar a trabajar con el servicio {{site.data.keyword.monitoringlong}} en {{site.data.keyword.Bluemix}}.
{:shortdesc}

De forma predeterminada, {{site.data.keyword.Bluemix_notm}} ofrece funciones de supervisión integradas para los servicios seleccionados. Puede utilizar el servicio {{site.data.keyword.monitoringlong_notm}} para ampliar la capacidad de recopilación y retención cuando trabaje con métricas, y para poder definir reglas y alertas que le notifiquen sobre las condiciones que requieran atención. El servicio {{site.data.keyword.monitoringshort}} ofrece características que le dan información sobre el rendimiento y el consumo de recursos de sus apps, y le ayudan a identificar rápidamente tendencias, a detectar y diagnosticar problemas de forma inmediata a fin de reducir el coste total del uso de recursos. Supervise su entorno mediante Grafana. 

## Antes de empezar
{: #cm_prereqs}

Debe tener un ID de usuario que sea miembro o propietario de una cuenta de {{site.data.keyword.Bluemix_notm}}. Para obtener un ID de usuario de {{site.data.keyword.Bluemix_notm}}, vaya a: [Registro de ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/registration/){:new_window}

## Paso 1: Elegir un recurso de nube que desee supervisar
{: #cm_step1}

En {{site.data.keyword.Bluemix_notm}}, las aplicaciones CF, los contenedores que se ejecutan en {{site.data.keyword.containershort}} y los servicios seleccionados recopilan datos de series de métricas automáticamente y los reenvían al servicio {{site.data.keyword.monitoringshort}}.

La tabla siguiente lista distintos recursos de nube. Complete la guía de aprendizaje de un recurso para empezar a trabajar con el servicio {{site.data.keyword.monitoringshort}}:

<table>
  <caption>Guías de aprendizaje para empezar a trabajar con el servicio {{site.data.keyword.monitoringshort}} </caption>
  <tr>
    <th>Recurso</th>
    <th>Guía de aprendizaje</th>
    <th>Entorno de nube</th>
    <th>Caso de ejemplo</th>
  </tr>
  <tr>
    <td>Contenedores que se ejecutan en {{site.data.keyword.containershort}}</td>
    <td>[Analizar métricas en Grafana para una app desplegada en un clúster Kubernetes](/docs/services/cloud-monitoring/tutorials/container_service_metrics.html#container_service_metrics)</td>
    <td>Public </br>Dedicated</td>
    <td>![Visión general de los componentes de alto nivel de los contenedores desplegados en un clúster Kubernetes](containers/images/containers_kube_metrics_dedicated.png "Visión general de los componentes de alto nivel de los contenedores desplegados en un clúster Kubernetes")</td>
  </tr>
  <tr>
    <td>Apps CF</td>
    <td>[Analizar métricas en Grafana para una app CF](/docs/services/cloud-monitoring/tutorials/cfapps_metrics.html#cfapps_metrics)</td>
    <td>Public</td>
    <td>![Vista de nivel alto de supervisión de las apps de CF en {{site.data.keyword.Bluemix_notm}}](cf/images/cfapp_metrics_ov.png "Vista de nivel alto de supervisión de las apps de CF en {{site.data.keyword.Bluemix_notm}}")</td>
  </tr>
</table>



## Paso 2: Establecer permisos para un usuario para ver las métricas
{: #cm_step2}

Para controlar las acciones de {{site.data.keyword.monitoringshort}} que un usuario puede realizar, puede asignar roles y políticas a un usuario. 

Hay dos tipos de permisos de seguridad en {{site.data.keyword.Bluemix_notm}} que controlan las acciones que los usuarios pueden llevar a cabo al trabajar con el servicio {{site.data.keyword.monitoringshort}}:

* Roles de Cloud Foundry (CF): Otorgue a un usuario un rol de CF para definir los permisos que el usuario tiene para ver métricas en un espacio.
* Roles de IAM: Otorgue a un usuario una política de IAM para definir los permisos que el usuario tiene para ver métricas en el dominio de la cuenta.


Complete los pasos siguientes para otorgar permisos a un usuario para ver métricas en un espacio:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Si el usuario es un miembro de la cuenta, seleccione el nombre de usuario de la lista, o pulse **Gestionar usuario** del menú *Acciones*.

    Si el usuario no es un miembro de la cuenta, consulte [Invitación a usuarios](/docs/iam/iamuserinv.html#iamuserinv).

4. Seleccione **Acceso de Cloud Foundry** y seleccione la organización.

    Se listan los espacios disponibles en dicha organización.

5. Seleccione el espacio donde se suministra el servicio {{site.data.keyword.monitoringshort}}. A continuación, desde la acción de menú, seleccione **Editar rol de espacio**.

6. Seleccione *Auditor*. 

    Puede seleccionar 1 o más roles de espacio. Todos los roles siguientes permiten que un usuario vea registros: *Gestor*, *Desarrollador* y *Auditor*
	
7. Pulse **Guardar rol**.


Para obtener más información, consulte [Concesión de permisos](/docs/services/cloud-monitoring/security/assign_policy.html#grant_permissions).

Para verificar que el usuario puede ver los datos de métrica, inicie Grafana en la región de nube donde haya completado una de las guías de aprendizaje. Por ejemplo, para la región EE.UU. sur, abra un navegador web y escriba el URL siguiente: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)


Para obtener más información sobre cómo iniciar Grafana en otras regiones, consulte [Navegación a Grafana desde un navegador web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#navigating_grafana).

**Nota:** Cuando inicie Grafana, si obtiene un mensaje que indica *señal de transporte no válida*, compruebe los permisos en el espacio. Este mensaje es una indicación de que el ID de usuario no tiene permisos para ver las métricas.
    

## Pasos siguientes 
{: #cm_next_steps}

Defina una alerta para una métrica. Para obtener más información, consulte [Configuración de alertas](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).
