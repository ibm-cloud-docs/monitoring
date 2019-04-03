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


# Analizar métricas en Grafana para una app CF
{: #cfapps_metrics}

Utilice esta guía de aprendizaje para aprender a utilizar el servicio de {{site.data.keyword.monitoringlong}} para supervisar el rendimiento de una app Cloud Foundry (CF) que se ejecuta en {{site.data.keyword.Bluemix_notm}} Public. 
{:shortdesc}


## Objetivos
{: #objectives}

Aprenda a buscar y analizar métricas para una app CF:

1. Despliegue una app CF.
2. Inicie Grafana y establezca el dominio de {{site.data.keyword.monitoringshort}} donde puede ver las métricas de la app CF.
3. Busque y analice las métricas para una app CF que se ejecuta en un espacio de {{site.data.keyword.Bluemix_notm}}.

Esta guía de aprendizaje presupone que está trabajando en la región EE.UU. sur.


## Requisitos previos
{: #cfapps_prereqs}

1. Ser miembro o propietario de una cuenta de {{site.data.keyword.Bluemix_notm}} con permisos para la prestación de servicios en un espacio, para el despliegue de apps CF y para la consulta de métricas de {{site.data.keyword.Bluemix_notm}} mediante el servicio {{site.data.keyword.monitoringshort}}.

    El ID de usuario para {{site.data.keyword.Bluemix_notm}} debe tener un rol de CF para el espacio donde se proporciona el servicio {{site.data.keyword.monitoringshort}} y la app CF. El rol necesario es *desarrollador*.
    
    Para obtener más información, consulte [Otorgar un rol de CF a un usuario mediante la IU de IBM Cloud](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#grant_permissions_ui_space).

2. Suministre el servicio {{site.data.keyword.monitoringshort}} en un espacio donde tiene permisos para suministrar servicios en la región EE.UU. sur.

    Para obtener más información, consulte [Suministro del servicio {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/how-to?topic=cloud-monitoring-provision#provision).

## Paso 1: Otorgar permisos de usuario para trabajar con apps CF y el servicio {{site.data.keyword.monitoringshort}}
{: #cfapps_step1}

Para otorgar permisos a un usuario para desplegar apps CF en un espacio o para ver las métricas en un dominio de espacio, debe asignar a dicho usuario un rol CF que describa las acciones que puede realizar este usuario con el servicio {{site.data.keyword.monitoringshort}} en el espacio y en {{site.data.keyword.Bluemix_notm}}. 

**Nota:** Esta guía de aprendizaje presupone que usted es el propietario de la cuenta o que tiene permisos para añadir roles al ID de usuario. Si no tiene permisos, solicite al propietario que realice este paso.

Complete los pasos siguientes para otorgar permisos a un usuario para completar la guía de aprendizaje:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web e inicie el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Busque el nombre de usuario en la lista y pulse **Gestionar usuario** desde el menú *Acciones*.

4. Seleccione **Acceso de Cloud Foundry** y, a continuación, seleccione **Asignar organización**.

5. Especifique los valores siguientes: 

    <table>
      <caption>Lista de valores a seleccionar</caption>
      <tr>
        <th>Campo</th>
        <th>Valor</th>
      </tr>
      <tr>
        <td>Organización</td>
        <td>MyOrg</td>
      </tr>
      <tr>
        <td>Rol de organización</td>
        <td>Sin rol de organización</td>
      </tr>
      <tr>
        <td>Región</td>
        <td>EE.UU. sur</td>
      </tr>
      <tr>
        <td>Espacio</td>
        <td>desarrollo</td>
      </tr>
      <tr>
        <td>Rol de espacio</td>
        <td>desarrollador</td>
      </tr>
    </table>
	
6. Pulse **Guardar rol**.
 

## Paso 2: Desplegar una app CF
{: #cfapps_step2}

Siga estos pasos desde la consola de {{site.data.keyword.Bluemix_notm}}:

1. Pulse **Catálogo** en la barra de herramientas de {{site.data.keyword.Bluemix_notm}}.

2. Pulse **Apps de Cloud Foundry > Liberty for Java**. 

3. Especifique la información siguiente:

    * **Nombre de app**: Nombre de la aplicación. Debe ser exclusivo.
    * **Región**: Elija EE.UU. sur.
    * **Organización**: Elija la organización donde se suministra el servicio {{site.data.keyword.monitoringshort}}.
    * **Espacio**: Elija el espacio donde se suministra el servicio {{site.data.keyword.monitoringshort}}.

3. Pulse **Crear**.

Tan pronto como la app CF esté en ejecución, las métricas se recopilarán y reenviarán al servicio {{site.data.keyword.monitoringshort}}.

## Paso 3: Iniciar Grafana y establecer el dominio de métricas
{: #cfapps_step3}

Inicie Grafana desde un navegador y establezca el dominio de {{site.data.keyword.monitoringshort}} donde puede ver las métricas de la app CF.

1. Desde un navegador, inicie Grafana. 

    Especifique el URL del servicio {{site.data.keyword.monitoringshort}} para la región donde se suministra el servicio {{site.data.keyword.monitoringshort}}.
    
    Para obtener los URL por región, consulte [URL para el servicio de supervisión](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

    Por ejemplo, para la región EE.UU. sur, inicie: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Establezca el dominio de {{site.data.keyword.monitoringshort}} donde puede ver las métricas de clúster.

    En Grafana, seleccione el ID. A continuación, compruebe que está en la cuenta correcta, y elija `Dominio = espacio`.

    Verifique que el nombre de la organización y el nombre de espacio se correspondan con aquellos donde ha desplegado la app CF y ha suministrado el servicio {{site.data.keyword.monitoringshort}}.


## Paso 4: Crear un panel de control de Grafana para supervisar una métrica
{: #cfapps_step4}


Complete los pasos siguientes para crear un nuevo panel de control en Grafana:

1. Seleccione el conmutador de la barra de menús lateral ![Barra de menús lateral de Grafana](images/grafana_settings.gif "Barra de menús lateral de Grafana").
2. Seleccione **Paneles de control**.
3. Pulse **Nuevo**

Se abre un panel de control. El panel de control incluye una fila vacía que está lista para la configuración.

![Panel de control de Grafana](images/grafana4_f1.gif "Panel de control de Grafana")

En Grafana, puede añadir filas para dividir el panel de control en secciones. Una fila agrupa 1 o varios paneles. Dentro de una fila, un panel es la unidad de visualización más pequeña que se puede configurar para visualizar datos correspondientes a una métrica; por ejemplo, puede elegir un panel gráfico o un panel de tabla. Puede arrastrar y soltar paneles para cambiar la disposición de los paneles en un panel de control. Los datos que muestra un panel se configuran mediante consultas. Puede definir una o varias consultas en un panel. Cada consulta representa un conjunto de datos distinto. También puede definir el intervalo de tiempo para un panel. Normalmente, el intervalo de tiempo se establece mediante el selector de tiempo del *Panel de control*.

Defina la consulta que filtra los datos que se muestran en el gráfico. Esta consulta supervisa el porcentaje de utilización de CPU hacia el límite del contenedor.

Para obtener información sobre el formato de la consulta, consulte [Formato de consulta de Grafana para apps CF](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-cfapps_metrics_format#cfapps_metrics_format).
    
1. Añada un panel *Gráfico* para supervisar los nanosegundos de tiempo de cpu en todos los núcleos de un contenedor.
    
    1. Seleccione **Gráfico**.
    
    2. Pulse en el título del gráfico y seleccione **editar**.
    
        Se abre el separador *Métricas*. Aquí puede ver el origen de datos predeterminado.
    
        ![Panel gráfico que incluye separadores de configuración](images/grafana4_f2.gif "Panel gráfico que incluye separadores de configuración")
    
2. Defina la consulta que filtra los datos que se muestran en el gráfico. 
    
    En el separador *Métricas*, seleccione **Añadir consulta**. <br>Se añade una entrada de consulta. Cada consulta está etiquetada con una letra.
    
    ![Entrada de nueva consulta](images/grafana4_query_f1.gif "Entrada de nueva consulta")
        
    1. Pulse **Seleccionar métrica** y elija el origen: `ibmcloud`.
    
    2. Pulse **Seleccionar métrica** y elija el tipo de nube: `public`.
    
    3. Pulse **Seleccionar métrica** y elija `cloud-foundry`.
    
    4. Pulse **Seleccionar métrica** y elija la región desde la que está trabajando, por ejemplo, `us-south` para la región EE.UU. sur.
    
    5. Pulse **Seleccionar métrica** y elija el nombre de app CF, por ejemplo, `logtester`.
    
    6. Pulse **Seleccionar métrica** y elija el índice de instancia de app CF, por ejemplo, `0`.

    7. Pulse **Seleccionar métrica** y elija `contenedor`.
    
    9. Pulse **Seleccionar métrica** y elija una métrica. Para supervisar el *Porcentaje de uso de la CPU* de un contenedor, elija `cpu-utilization`.

    10. Pulse la imagen del símbolo más ![Añadir iconos](images/grafana_plus_image.gif "Imagen del símbolo Más") y elija una función. Puede añadir una función para transformar, combinar y realizar cálculos sobre los datos disponibles para una métrica.
        
        Por ejemplo, puede añadir la función **alias(newName)** para añadir un alias a una métrica. Este alias se utiliza para mostrar una serie de caracteres en lugar del nombre de la métrica en la descripción que se muestra en el gráfico.
        
        Para añadir un alias a una métrica, siga estos pasos:
        
        1. Pulse el símbolo más.
        2. Seleccione **Especial**. 
        3. Seleccione **alias**.
        4. Escriba una serie de caracteres, como por ejemplo `Mi métrica de ejemplo`.
        

## Paso 5: Guardar el panel de control
{: #cfapps_step5}

Guarde el panel de control para utilizarlo más adelante.

1. Pulse la imagen de guardar panel de control ![Imagen Guardar panel de control](images/grafana_save_image.gif "Imagen Guardar panel de control").

    ![Guardar panel de control](images/grafana_save_dashboard.gif "Guardar panel de control")

2. Escriba el nombre del panel de control.
3. Pulse **Guardar**.


## Pasos siguientes
{: #cfapps_next_steps}

Defina una alerta para una métrica. Para obtener más información, consulte [Configuración de alertas](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).
