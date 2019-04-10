---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, dashboards

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


# Trabajar con paneles de control
{: #dashboards}

Utilice paneles de control para supervisar la infraestructura, las aplicaciones y los servicios. Puede utilizar paneles de control predefinidos. También puede crear paneles de control personalizados mediante la interfaz de usuario web o mediante programación. Puede realizar copias de seguridad y restaurar paneles de control mediante scripts Python.
{:shortdesc}

Un **panel de control** muestra grupos de métricas que informan sobre el estado y sobre el rendimiento de la infraestructura, de las aplicaciones y de los servicios para un solo host o para un grupo de hosts. Los paneles de control ofrecen una perspectiva especializada de los datos de red, los datos de aplicación, la topología, los servicios, los hosts y los contenedores.

En la sección **PANELES DE CONTROL** de la interfaz de usuario web, los paneles de control están organizados en tres grupos principales:

* *Mis paneles de control*: son los paneles de control creados por el usuario que actualmente ha iniciado la sesión.
* *Mis paneles de control compartidos*: son los paneles de control creados por el usuario que ha iniciado la sesión actualmente y que se comparten con otros usuarios.
* *Paneles de control compartidos conmigo*: son los paneles de control creados por otros usuarios y compartidos con el usuario actual.

En la sección **EXPLORAR** de la interfaz de usuario web, los paneles de control están organizados en dos grupos:
* *Paneles de control predeterminados*: son los paneles de control predefinidos.
* *Mis paneles de control*: son los paneles de control creados por el usuario que actualmente ha iniciado la sesión.

Puede copiar y compartir paneles de control mediante la interfaz de usuario web. 

Puede ejecutar scripts para completar cualquiera de las acciones siguientes mediante programación:
* Guardar paneles de control existentes en un archivo local.
* Crear nuevos paneles de control que sean idénticos que los paneles de control que guarde.
* Restaurar paneles de control.



## Paneles de control predefinidos
{: #dashboards_predefined}

Los paneles de control predefinidos se diseñan en torno a varias aplicaciones soportadas, topologías de red, diseños de infraestructura y servicios. 

Los paneles de control predefinidos incluyen una serie de paneles que ya están configurados.

En la tabla siguiente se muestran los distintos tipos de paneles de control predefinidos:

| Tipo | Descripción | Más información | 
|------|-------------|------------------|
| Aplicaciones | Paneles de control que se pueden utilizar para supervisar las aplicaciones y los componentes de la infraestructura.  | [Paneles de control de aplicación](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_applications) |
| Host y contenedores | Paneles de control que se pueden utilizar para supervisar la utilización de recursos y la actividad del sistema en los hosts y en los contenedores. | [Paneles de control de host y de contenedor](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_host_container) |
| Red | Paneles de control que puede utilizar para supervisar las conexiones y la actividad de red. | [Paneles de control de red](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_network) |
| Servicio | Paneles de control que puede utilizar para supervisar el rendimiento de sus servicios, aunque dichos servicios estén desplegados en contenedores orquestados. | [Paneles de control de servicio](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_service) |
| Topología | Paneles de control que puede utilizar para supervisar las dependencias lógicas de los niveles de aplicación y las métricas de superposición. | [Paneles de control de topología](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_topology) |
{: caption="Tabla 1. Lista de paneles de control predefinidos" caption-side="top"} 



## Creación de paneles de control personalizados en la interfaz de usuario web
{: #dashboards_create}

Cuando cree un panel de control personalizado, puede comenzar a partir de una plantilla como un panel de control predefinido o puede elegir un panel de control en blanco. Un panel de control incluye paneles que están configurados para mostrar datos específicos en diferentes formatos. También puede definir la forma en que se agregan los datos. El **ámbito** define qué datos se utilizan para la agregación y se muestran. Puede definir el ámbito a nivel de panel de control o puede modificar paneles individuales. 

Siga los pasos siguientes para crear un panel de control personalizado:

1. Vaya a la sección *PANEL DE CONTROL** de la interfaz de usuario web y seleccione * *Añadir panel de control**. Se abrirá la página * Crear un nuevo panel de control*.

    1. Seleccione un panel de control predefinido o elija el *Panel de control en blanco*. 

    2. Especifique un nombre para el panel de control.

    3. Pulse **Crear panel de control**.

2. Defina el ámbito del panel de control. Pulse **Editar ámbito** para cambiar el ámbito predeterminado. De forma predeterminada, está seleccionado **En todas partes**.
    
    1. Seleccione el ámbito. 

    2. Si lo desea, pulse **Modificar los ámbitos de paneles personalizados** para modificar el ámbito para todos los paneles que actualmente tienen definido un ámbito personalizado. **Nota: esta acción no se puede deshacer.** 

    **Nota:** para restablecer el ámbito del panel de control a toda la infraestructura, o para actualizar el ámbito de un panel de control existente a toda la infraestructura, seleccione **En todas partes**.

    3. Pulse **Guardar**.

3. Configure los paneles. Repita este paso para cada uno de los paneles del panel de control que desea modificar.

    1. Identifique el panel que desea modificar.

    2. Seleccione **Editar panel**. Es el icono de lápiz.
    
    3. Cambie el tipo de gráfico.

    4. Cambie la métrica y la tasa. La tasa define el tipo de agregación que se lleva a cabo en los datos.

    5. Cambie el ámbito del panel. Pulse **Modificar ámbito del panel de control**. A continuación, cambie el ámbito. Si tiene que restaurar el ámbito del panel de control en el panel, seleccione **Valor predeterminado para el ámbito de panel de control**.

    6. En el campo *Comparar con*, pulse **Configurar**. Defina el intervalo de tiempo para la comparación.

    7. Establezca el color de fondo del panel en función de los umbrales de métricas. Pulse **Modificar codificación de colores** y luego **Habilitar**. Defina valores para los distintos umbrales.

    8. Pulse **Guardar**.


## Modificación del ámbito
{: #dashboards_scope}

En lugar de cambiar el ámbito de un panel de control predefinido, copie el panel de control y cambie el ámbito en el panel de control copiado.
{: tip}

Siga los pasos siguientes para cambiar el ámbito de un panel de control:

1. Vaya a la sección **PANEL DE CONTROL** en la interfaz de usuario web y seleccione un panel de control.

2. Pulse **Editar ámbito** para cambiar el ámbito predeterminado. 

    De forma predeterminada, está seleccionado **En todas partes**.
    
3. Seleccione el ámbito. 

4. Si lo desea, pulse **Modificar los ámbitos de paneles personalizados** para modificar el ámbito para todos los paneles que actualmente tienen definido un ámbito personalizado. 

    **Nota: esta acción no se puede deshacer.** 

    Para restablecer el ámbito del panel de control a toda la infraestructura, o para actualizar el ámbito de un panel de control existente a toda la infraestructura, seleccione **En todas partes**.
    {: tip}

5. Pulse **Guardar**.



## Copia de un panel de control
{: #dashboards_copy}

Cuando se copia un panel de control, se crea un duplicado.

En la tabla siguiente se muestran las distintas acciones y permisos de usuario que se necesitan para que los usuarios puedan copiar un panel de control:

| Acción     |	Quién puede copiar     |	Instancia de panel de control	   | Quién puede ver el panel de control     | Quién puede editar el panel de control  |
|------------|-------------------|-------------------------|--------------------------------|-----------------------------|
| Copiar en equipo actual    |	Usuarios del equipo con permisos de editor | Nueva instancia del panel de control  | Miembros del equipo con permisos de visualización	 | Usuarios del equipo con permisos de editor |
| Copiar en otro equipo    | Usuarios del equipo con permisos de editor en ambos equipos | Nueva instancia del panel de control  | Si el panel de control original no se comparte, solo tiene acceso el usuario que copia el panel de control. </br>Si el panel de control original se comparte, todos los miembros del equipo tienen acceso. | Si el panel de control original no se comparte, solo el usuario que copia el panel de control. </br>Si el panel de control original se comparte, todos los miembros del equipo con permisos de editor. |
{: caption="Tabla 2. Información sobre usuarios y paneles de control relacionada con la copia de paneles de control" caption-side="top"} 

Siga los pasos siguientes para copiar un panel de control en la interfaz de usuario web:

1. Vaya a la sección *PANELES DE CONTROL* de la interfaz de usuario web.
2. Seleccione el panel de control en el panel de la izquierda.
3. Pulse **Valores** (icono de tres puntos) y seleccione **Copiar panel de control**. 
4. Seleccione dónde desea copiar el panel de control.

    1. Elija **Equipo actual** para copiar el panel de control para el equipo actual.
    
    2. Elija **Otros equipos** para copiar el panel de control en otros equipos. Seleccione los equipos en los que desea copiar el panel de control.

    3. Escriba un nombre para el panel de control.

    4. Pulse **Enviar copia**.
    
    5. Compruebe que el ámbito del panel de control del nuevo equipo se actualiza en función de los permisos del equipo de destino.

## Supresión de un panel de control
{: #dashboards_delete}

Siga los pasos siguientes para suprimir un panel de control en la interfaz de usuario web:

1. Vaya a la sección *PANELES DE CONTROL* de la interfaz de usuario web.
2. Seleccione el panel de control en el panel de la izquierda.
3. Pulse **Valores** ![icono de tres puntos](images/actions.png) y seleccione **Suprimir panel de control**. 
4. Para confirmar la supresión, pulse **Sí, suprimir panel de control**.


## Compartición de un panel de control
{: #dashboards_share}

Puede compartir paneles de control entre usuarios de un equipo y externamente mediante la configuración de un URL público para el panel de control.  

En la tabla siguiente se muestran las distintas acciones y permisos de usuario que se necesitan para que los usuarios puedan compartir o trabajar con un panel de control compartido:

| Acción      |	Quién puede compartir        |	Instancia de panel de control	       | Quién puede ver el panel de control        | Quién puede editar el panel de control  |
|-------------|-------------------|-----------------------------|------------------------------------|-----------------------------|
| Compartir con equipo actual |	Creador del panel de control         |	Compartir misma instancia del panel de control   | Miembros del equipo con permisos de visualización  | Miembros del equipo con permisos de edición   |
| Compartir públicamente como URL	  | Cualquier usuario del equipo que pueda editar |	Compartir misma instancia del panel de control   | Cualquier usuario     | Nadie                      |
{: caption="Tabla 3. Información sobre usuarios y paneles de control relacionada con la compartición de paneles de control" caption-side="top"} 


Siga los pasos siguientes para compartir un panel de control en la interfaz de usuario web:

1. Vaya a la sección *PANELES DE CONTROL* de la interfaz de usuario web.
2. Seleccione el panel de control en el panel de la izquierda.
3. Pulse **Valores** ![icono de tres puntos](images/actions.png) y seleccione **Compartir**.
4. Elija cómo desea compartir el panel de control:

    * Conmute el control deslizante **Compartir con equipo** para compartir el panel de control con el equipo actual. Se muestra el equipo en el que se comparte el panel de control.

    * Conmute el control deslizante **Compartir URL público** para revelar el URL público personalizado.

5. Pulse **Cerrar**.

Comparta un panel de control externamente para permitir que los usuarios externos vean las métricas del panel de control, al tiempo que restringe el acceso para modificar paneles y configuraciones.
{: tip}


## Gestión de paneles de control mediante programación
{: #dashboards_programmatically}

Utilice la API REST de Sysdig para automatizar las tareas rutinarias y supervisar las notificaciones. También puede utilizar la biblioteca de Python de Sysdig. 

**Nota:** la biblioteca de Python expone parte de la funcionalidad de la API REST de Sysdig. 


Cuando utilice la API desde scripts o programas personalizados, debe utilizar una señal de Sysdig para autenticarse con la instancia de {{site.data.keyword.mon_full_notm}}. Para obtener más información, consulte [Cómo trabajar con señales de API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token).


| Tarea                    | Utilización de la API REST                |
|-------------------------|-------------------------------|
| Crear un panel de control      | [Creación de un panel de control mediante la API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Suprimir un panel de control      | [Supresión de un panel de control mediante la API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Guardar paneles de control       | [Cómo guardar los paneles de control de un equipo mediante la API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabla 4. Tareas para gestionar paneles de control mediante programación" caption-side="top"} 


