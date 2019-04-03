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


# Analizar métricas en Grafana para un clúster de Kubernetes
{: #container_service_metrics}

Utilice esta guía de aprendizaje para aprender a utilizar el servicio {{site.data.keyword.monitoringlong}} para supervisar el rendimiento del contenedor. 
{:shortdesc}


## Objetivos
{: #ks_objectives}

Aprenda a buscar y analizar métricas de contenedor de una app que se despliega en un clúster de Kubernetes:

1. Identifique dónde se reenvían las métricas que se recopilan en un clúster al servicio {{site.data.keyword.monitoringshort}}. 
2. Inicie Grafana y establezca el dominio {{site.data.keyword.monitoringshort}} donde pueda ver las métricas del clúster.
3. Busque y analice métricas de contenedor de una app desplegada en un clúster de Kubernetes en {{site.data.keyword.Bluemix_notm}}.

Esta guía de aprendizaje le guiará por los pasos necesarios para que el siguiente caso de ejemplo completo funcione en {{site.data.keyword.Bluemix_notm}}: Suministro de un clúster, identificación de dónde envía métricas el clúster al servicio {{site.data.keyword.monitoringshort}} en {{site.data.keyword.Bluemix_notm}}, despliegue de una app en el clúster, y uso de Grafana para ver y filtrar métricas de contenedor para dicho clúster.


**Nota:** Para completar esta guía de aprendizaje, debe completar los requisitos previos y las guías de aprendizaje enlazados desde los distintos pasos.


## Requisitos previos
{: #ks_prereqs}

1. Ser miembro o propietario de una cuenta de {{site.data.keyword.Bluemix_notm}} con permisos para crear clústeres de Kubernetes estándares, desplegar apps en clústeres, y consultar métricas en {{site.data.keyword.Bluemix_notm}} para supervisión en Grafana.

    Su ID de usuario para {{site.data.keyword.Bluemix_notm}} debe tener las siguientes políticas asignadas:
    
    * Una política de IAM para {{site.data.keyword.containershort}} con permisos de *operador* o *administrador*.
    
    Para obtener más información, consulte [Asignar una política de IAM a un usuario mediante la IU de IBM Cloud](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui).

2. Tener una sesión de terminal desde la que gestionar el clúster de Kubernetes y desplegar apps desde la línea de mandatos. Los ejemplos en esta guía de aprendizaje se proporcionan para un sistema Ubuntu Linux.

3. Instalar las CLI para trabajar con {{site.data.keyword.containershort}} en el sistema Ubuntu.

    * Instale la CLI de {{site.data.keyword.Bluemix_notm}}. 
    * Instale la CLI de {{site.data.keyword.containershort}} para crear y gestionar los clústeres de Kubernetes en {{site.data.keyword.containershort}}, y para desplegar apps contenerizadas en el clúster.
    
    Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview).
    
    

    
 

## Paso 1: Suministrar un clúster de Kubernetes
{: #ks_step1}

Realice los siguientes pasos:

1. Cree un clúster de Kubernetes estándar. Para obtener más información, consulte [Cree un clúster de Kubernetes estándar](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial).

2. Configure el contexto del clúster en un terminal. Después de haber configurado el contexto, podrá gestionar el clúster de Kubernetes y desplegar la aplicación en dicho clúster de Kubernetes.

    Inicie la sesión en la región, organización y espacio en {{site.data.keyword.Bluemix_notm}} que están asociados al clúster que ha creado. Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).

	Inicialice el plug-in del servicio {{site.data.keyword.containershort}}.

	```
	ibmcloud cs init
	```
	{: codeblock}

    Establezca el contexto de terminal para el clúster.
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    El resultado de ejecutar este mandato muestra el mandato que debe ejecutar en el terminal para definir la vía de acceso a su archivo de configuración. Por ejemplo:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Copie y pegue el mandato para definir la variable de entorno en el terminal y luego pulse **Intro**.



## Paso 2: Otorgar permisos de usuario para ver métricas en el dominio de la cuenta
{: #ks_step2}

Para otorgar permisos a un usuario para ver métricas en un dominio de cuenta, debe asignar al usuario una política de IAM para el servicio {{site.data.keyword.monitoringshort}} con el rol **Visor**.

Complete los pasos siguientes para otorgar permisos a un usuario para trabajar con el servicio {{site.data.keyword.monitoringshort}}:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web e inicie el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Si el usuario es un miembro de la cuenta, seleccione el nombre de usuario de la lista, o pulse **Gestionar usuario** del menú *Acciones*.

    Si el usuario no es un miembro de la cuenta, consulte [Invitación a usuarios](/docs/iam?topic=iam-iamuserinv#iamuserinv).

4. Seleccione **Políticas de acceso > Asignar acceso > Asignar acceso a recursos**.

5. Elija el **{{site.data.keyword.monitoringlong}}** de servicio, seleccione la región donde está disponible el clúster, **US-South** para esta guía de aprendizaje, y seleccione un rol, **visor**.



## Paso 3: Otorgar los permisos de propietario de claves de {{site.data.keyword.containershort_notm}}
{: #ks_step3}

Para que el clúster reenvíe métricas al dominio de cuenta, el propietario de la clave {{site.data.keyword.containershort}} debe tener las siguientes políticas de IAM:

* Política de IAM con permisos de **editor** para el servicio {{site.data.keyword.monitoringshort}}.
* Política de IAM con permisos de **administrador** para {{site.data.keyword.containershort}}.


Realice los pasos siguientes para otorgar los permisos de propietario de claves de {{site.data.keyword.containershort}}:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web e inicie el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Busque el ID de usuario del propietario de claves de {{site.data.keyword.containershort}}.

    Ejecute el mandato `ibmcloud cs api-key-info ClusterName` para recibir el ID de usuario del propietario de claves de {{site.data.keyword.containershort}}.

4. Seleccione **Políticas de acceso > Asignar acceso > Asignar acceso a recursos**.

5. Elija el **{{site.data.keyword.monitoringlong}}** de servicio, seleccione la región donde está disponible el clúster, **US-South** para esta guía de aprendizaje, y seleccione un rol, **editor**.	

6. Repita los pasos 2 a 4, y elija el {{site.data.keyword.containershort}} de servicio. Seleccione **Todas las regiones**, y el rol **administrador**.	




## Paso 4: Desplegar una app de ejemplo en el clúster de Kubernetes
{: #ks_step4}

Desplegar y ejecutar una app de ejemplo en el clúster de Kubernetes. Complete los pasos de la siguiente guía de aprendizaje para desplegar la app de ejemplo: [Lección 1: Despliegue de apps de una sola instancia en clústeres de Kubernetes](/docs/containers?topic=containers-cs_apps_tutorial#cs_apps_tutorial_lesson1).

La app es una app Node.js Hello World:

```
var express = require('express')
var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

En esta app de ejemplo, cuando prueba la app en un navegador, la app escribe en la salida estándar el siguiente mensaje: `Sample app is listening on port 8080.`


## Paso 5: Iniciar Grafana y establecer el dominio de métricas
{: #ks_step5}

Inicie Grafana desde un navegador y establezca el dominio de {{site.data.keyword.monitoringshort}} donde puede ver las métricas de clúster.

Para analizar las métricas de un clúster, debe acceder a Grafana en la región pública de la nube en la que se ha creado el clúster. Para obtener más información, consulte [Navegación al panel de control de Grafana desde un navegador web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).

1. Desde un navegador, inicie Grafana. 

    Especifique el URL del servicio {{site.data.keyword.monitoringshort}} para la región en la que ha creado el clúster. 
    
    Para obtener los URL por región, consulte [URL para el servicio de supervisión](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

    Por ejemplo, para la región EE.UU. sur, inicie: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Establezca el dominio de {{site.data.keyword.monitoringshort}} en **Cuenta**.

    En Grafana, seleccione el ID. A continuación, compruebe que está en la cuenta correcta, y elija un dominio. Seleccione `Dominio = cuenta`.

    Los clústeres reenvían métricas al dominio de métricas de la cuenta. 

## Paso 6: Supervisar el clúster en Grafana
{: #ks_step6}

{{site.data.keyword.containershort}} proporciona un panel de control de Grafana que puede utilizar para supervisar las métricas del clúster. 

Realice los pasos siguientes para abrir el panel de control de ejemplo:

1. Seleccione el conmutador de la barra de menús lateral ![Barra de menús lateral de Grafana](images/grafana_settings.gif "Barra de menús lateral de Grafana").
2. Seleccione **Paneles de control**.
3. Pulse **Abrir**.
4. Seleccione **ClusterMonitoringDashboard_v1**.

Se abrirá el panel de control de ejemplo. 

![Panel de control de ejemplo de Grafana](images/cluster_grafana_sample_dashboard.png "Panel de control de ejemplo de Grafana")



## Pasos siguientes
{: #ks_next_steps}

Defina una alerta para una métrica. Para obtener más información, consulte [Configuración de alertas](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).
