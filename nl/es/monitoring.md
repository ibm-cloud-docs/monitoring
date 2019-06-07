---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring

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

# Supervisión del entorno
{: #monitoring}

Puede supervisar la infraestructura y las aplicaciones que se ejecutan en la misma con el servicio {{site.data.keyword.mon_full_notm}}. Puede solicitar una captura para analizar lo que sucede en un nodo durante un periodo de tiempo.
{:shortdesc}

En primer lugar, suministre una instancia del servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}. Luego configure agentes de Sysdig para los orígenes de métricas. Una vez configurados los orígenes, puede ver, supervisar y gestionar los datos a través de la interfaz de usuario web del servicio.

Los datos correspondientes a las métricas predeterminadas se recopilan automáticamente. Puede configurar métricas personalizadas y añadir etiquetas a esas métricas para describir sus características. También se recopilan automáticamente datos correspondientes a estas métricas personalizadas.

Puede analizar los datos en el separador *Explorar* y en el separador *Panel de control* de la interfaz de usuario web. Los datos se supervisan mediante vistas de métricas y paneles de control. 

* Utilice una vista de métricas para supervisar una métrica individual.
* Utilice paneles de control para obtener una visión especializada de los datos de red, los datos de aplicación, la topología, los servicios, los hosts y los contenedores mediante la supervisión de los datos a través de paneles. Un panel muestra una métrica o un grupo de métricas en un panel de control.

Para cada vista de métrica y para cada panel de control, puede definir el ámbito de los datos, cómo agregar los datos y qué filtros de tiempo y de grupo se deben aplicar a los datos. Para obtener más información, consulte [Gestión de datos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

En el separador *Explorar*, puede supervisar los datos utilizando métricas predeterminadas y paneles de control predeterminados. Puede utilizar etiquetas para definir nuevos grupos de infraestructura que puede utilizar para agregar datos de forma diferente y supervisar el entorno. También puede utilizar paneles de control personalizados que se definen mediante el separador *Panel de control*.

En el separador *Paneles de control*, puede supervisar los datos utilizando cualquiera de los paneles de control predeterminados o creando nuevos.

Puede configurar un panel de control predeterminado como punto de entrada predeterminado para un equipo, lo que le ayuda a unificar la experiencia de un equipo y a permitir que los usuarios centren su atención inmediata en la información más relevante para ellos. 
{: tip}

Puede utilizar alertas para notificar a los usuarios sobre problemas que requieren atención a través de uno o varios canales de notificación.
* La sección *Alertas* de la interfaz de usuario web muestra la lista de alertas predefinidas. Desde esta vista, puede habilitar e inhabilitar alertas predefinidas, modificar las alertas existentes y crear alertas nuevas.
* La sección *Valores* de la interfaz de usuario web es el lugar donde se configuran los canales de notificación.
 
Puede solicitar una captura en un nodo para analizar lo que sucede en dicho nodo durante un periodo de tiempo. Por ejemplo, puede utilizar una captura para analizar cuellos de botella o interacciones de componentes.

## Métricas
{: #monitoring_metrics}

Una métrica es una medida cuantitativa que tiene una o varias etiquetas para definir sus características. Utilice métricas para analizar los datos estadísticos que tienen valores numéricos. 

Una métrica se representa mediante series temporales. Una serie temporal es un conjunto de puntos de datos numéricos durante un periodo de tiempo. 

Las métricas se clasifican en dos grupos: 

* [Métricas predeterminadas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [Métricas personalizadas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

Las etiquetas se clasifican como etiquetas de infraestructura y etiquetas de descriptores de métricas. Cada métrica tiene un conjunto de etiquetas predefinidas. Para las métricas personalizadas, puede configurar más etiquetas. 

Puede utilizar etiquetas para identificar y diferenciar las características de una métrica, por ejemplo:
* Puede agrupar objetos de la infraestructura en jerarquías lógicas. 
* Puede filtrar datos. 
* Puede dividir datos agregados en segmentos. 

Para obtener más información, consulte [Etiquetas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels).

## Paneles
{: #monitoring_panels}

Un panel muestra una métrica o un grupo de métricas en un panel de control. 

Puede utilizar cualquiera de los siguientes tipos de panel para visualizar métricas:

| Tipo | Descripción |
|------|-------------|
| `Línea` | Utilice este panel para ver las tendencias a lo largo del tiempo para una o varias métricas.  |
| `Área` | Utilice este panel para ver las tendencias a lo largo del tiempo para una o varias métricas.  |
| `Lista de principales` | Utilice este panel para comparar una métrica entre grupos de entidades. El diagrama de barras se clasifica en orden descendente.  |
| `Histograma` | Utilice este panel para ver la distribución de la frecuencia de una métrica en grupos.  |
| `Topología` | Utilice este panel para visualizar la infraestructura como un mapa de topología y las relaciones entre las entidades del mapa.  |
| `Número` | Utilice este panel para ver un solo número que representa el valor de una métrica agregada a lo largo del tiempo para una o varias entidades.  |
| `Tabla` | Utilice este panel para visualizar los datos numéricos de la infraestructura en función de métricas y segmentos.  |
| `Texto` | Utilice este panel para añadir texto. Utilice anotaciones para añadir texto.  |
{: caption="Tabla 1. Tipos de paneles" caption-side="top"} 

Puede copiar, cambiar el ámbito, duplicar, suprimir, exportar y explorar paneles.

Puede exportar datos de un panel. Tenga en cuenta la información siguiente cuando exporte datos:

* Puede exportar datos a un **archivo json** desde un gráfico de líneas.
* Puede exportar datos a un **archivo csv** desde un gráfico de tabla o desde un gráfico de líneas.


En la tabla siguiente se muestran las tareas que puede ejecutar con paneles:

| Tarea | Descripción |
|------|-------------|
| [Copiar panel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | Copiar un panel en un nuevo panel de control.  |
| [Cambiar ámbito](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Cambiar el ámbito de un panel. |
| [Duplicar panel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | Copiar un panel en el mismo panel de control.  |
| [Suprimir panel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | Suprimir un panel del panel de control.  |
| [Exportar datos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | Exportar datos de un panel a un archivo csv o a un archivo json.  |
| [Crear alerta](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | Defina una alerta sobre una métrica. |
{: caption="Tabla 2. Tareas con paneles" caption-side="top"} 


## Paneles de control
{: #monitoring_dashboards}

Un **panel de control** muestra grupos de métricas que informan sobre el estado y sobre el rendimiento de la infraestructura, de las aplicaciones y de los servicios para un solo host o para un grupo de hosts. Los paneles de control ofrecen una perspectiva especializada de los datos de red, los datos de aplicación, la topología, los servicios, los hosts y los contenedores. Utilice paneles de control para supervisar la infraestructura, las aplicaciones y los servicios.


En la sección **PANELES DE CONTROL** de la interfaz de usuario web, los paneles de control están organizados en tres grupos principales:

* **Mis paneles de control**: son los paneles de control creados por el usuario que ha iniciado la sesión.
* **Mis paneles de control compartidos**: son los paneles de control creados por el usuario que ha iniciado la sesión y que se comparten con otros usuarios.
* **Paneles de control compartidos conmigo**: son los paneles de control creados por otros usuarios y compartidos con el usuario actual.

En la sección **EXPLORAR** de la interfaz de usuario web, los paneles de control están organizados en dos grupos:
* **Paneles de control predeterminados**: son los paneles de control predefinidos.
* **Mis paneles de control**: son los paneles de control creados por el usuario que ha iniciado la sesión.

Puede utilizar paneles de control predefinidos. También puede crear paneles de control personalizados mediante la interfaz de usuario web o mediante programación. Puede realizar copias de seguridad y restaurar paneles de control mediante scripts Python o mediante la API REST de Sysdig.

También puede copiar y compartir paneles de control mediante la interfaz de usuario web. 

En la tabla siguiente se describen las tareas que puede ejecutar para trabajar con paneles de control desde la interfaz de usuario:

| Tarea | Descripción |
|------|-------------|
| [Crear panel de control](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | Crear un panel de control personalizado en la interfaz de usuario web. |
| [Copiar un panel de control](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | Hacer una copia de un panel de control en el equipo actual en el que está disponible el panel de control o copiar un panel de control en otro equipo. |
| [Cambiar el ámbito](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Cambiar el ámbito de un panel de control.       |
| [Suprimir un panel de control](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  Suprimir un panel de control. |
| [Compartir un panel de control](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | Compartir paneles de control entre los usuarios de un equipo y externamente, mediante la configuración de un URL público para el panel de control. |
{: caption="Tabla 3. Tareas con paneles de control que puede ejecutar en la interfaz de usuario web" caption-side="top"} 

En la tabla siguiente se describen las tareas que puede ejecutar mediante programación para trabajar con paneles de control:

| Tarea                    |	Utilización de la API REST                |
|-------------------------|-------------------------------|
| Crear un panel de control      | [Creación de un panel de control mediante la API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Suprimir un panel de control      | [Supresión de un panel de control mediante la API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Guardar paneles de control       | [Cómo guardar los paneles de control de un equipo mediante la API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabla 4. Tareas para gestionar paneles de control mediante programación" caption-side="top"} 



## Sucesos
{: #monitoring_events}

Un suceso es una notificación que informa sobre algo que ocurre en cualquiera de los nodos que reenvían datos a la instancia de {{site.data.keyword.mon_full_notm}}. Utilice sucesos para revisar, realizar el seguimiento y resolver problemas. 

La lista siguiente muestra distintos tipos de sucesos: 

* Los *sucesos de alerta* son sucesos que se desencadenan mediante alertas configuradas por el usuario. Para obtener más información, consulte [Cómo trabajar con alertas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* Los *sucesos basados en infraestructura* son sucesos que se recopilan de los nodos Docker y Kubernetes. De forma predeterminada, el agente de Sysdig descubre y recopila automáticamente datos de un grupo de sucesos seleccionado. Puede editar el archivo de configuración del agente para habilitar más sucesos.
* *Sucesos personalizados* que se configuran a través de cualquiera de las siguientes integraciones: Slackbot, scripts Python previamente creados, scripts Python personalizados creados por el usuario o solicitudes cURL.

De forma predeterminada, un suceso tiene un estado: 
* **Activo**: este estado indica que las circunstancias que han desencadenado el suceso siguen en vigor; por ejemplo, un sigue estando inactivo.
* **Correcto**: este estado indica que la situación ha vuelto a la normalidad; por ejemplo, un nodo está activo y en ejecución.

Los sucesos se gestionan en la sección *Sucesos* de la interfaz de usuario web. 
* Puede ver los sucesos de alerta a través del separador *Sucesos de alerta*.
* Puede ver los sucesos basados en infraestructura a través del separador *Sucesos personalizados*.
* Puede ver los sucesos personalizados a través del separador *Sucesos personalizados*.
* Puede enviar sucesos personalizados a cualquiera de sus equipos mediante la [señal de API correspondiente a dicho equipo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token). Para obtener más información, consulte [Sucesos personalizados ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.
* Puede establecer el suceso como resuelto (**Resolved**) para notificar a otros usuarios que el problema se ha resuelto en lugar de esperar a que el estado se establezca en **OK**.
{: #tip}



## Alertas
{: #monitoring_alerts}

Una alerta es un suceso de notificación que puede utilizar para advertir acerca de situaciones que requieren atención. Cada alerta tiene un estado de gravedad. Este estado le informa acerca de la importancia de la información que notifica. 

Cuando defina una alerta, debe definir la condición que desencadena la notificación y uno o varios canales de notificación a través de los cuales desea que se le notifique. También debe definir la gravedad de la alerta y el tipo de alerta. 

Puede definir alertas para cualquiera de los siguientes tipos de alertas:

| Tipo              | Descripción |
|-------------------|-------------|
| Detección de anomalías | Se utiliza para supervisar hosts en función en sus comportamientos históricos y generar alertas cuando se desvíen. |
| Tiempo de inactividad          | Se utiliza para supervisar cualquier tipo de entidad, por ejemplo host, contenedor, proceso o servicio, y generar alertas cuando la entidad está inactiva. |
| Suceso             | Se utiliza para supervisar la aparición de determinados sucesos y generar alertas si el número total de apariciones supera un umbral. Por ejemplo, puede utilizarlo para generar alertas sobre los reinicios y despliegues de contenedores, orquestaciones y sucesos de servicio.|
| Valor atípico de grupo     | Se utiliza para supervisar un grupo de hosts y para que se le notifique cuando uno actúa de forma distinta al resto. |
| Métrica            | Se utiliza para supervisar métricas de series temporales y generar alertas si superan umbrales definidos por el usuario. |
{: caption="Tabla 5. Tipos de alertas" caption-side="top"} 

De forma predeterminada, la gravedad se establece en *warning*. Puede establecer los siguientes valores para la gravedad de una alerta: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *informational*, debug* 

Puede definir uno o varios canales de notificación para cualquiera de las siguientes integraciones de notificación:
* Notificaciones por correo electrónico
* Notificaciones por PagerDuty
* Notificaciones por Slack
* Notificaciones por VictorOps
* Notificaciones por OpsGenie
* Configurar un canal de Webhook

Para obtener más información, consulte [Configuración de un canal de notificación](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create).


Puede habilitar alertas predefinidas, modificar alertas y crear alertas personalizadas en la interfaz de usuario web y mediante la API de Sysdig.

Las alertas se gestionan en la vista *Alertas* de la interfaz de usuario web. Puede configurar las columnas de la tabla que se mostrarán en la vista *Alertas*. Las opciones válidas son: *Nombre*, *Ámbito*, *Alertar cuando*, *Segmentar por*, *Notificaciones*, *Habilitado*, *Modificado*, *Capturas*, *Canales*, *Creado*, *Descripción*, *Destinatarios de correo electrónico*, *Durante al menos*, *OpsGenie*, *PagerDuty*, *Gravedad*, *Slack*, *WebHook*, *Temas de SNS*, *Tipo* y *VictorOps*.

En la lista siguiente se describen las tareas principales cuando se trabaja con alertas:
* [Configuración de una alerta ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [Habilitación o inhabilitación de una alerta ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [Búsqueda de una alerta ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [Modificación de una alerta ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [Copia de una alerta en el mismo equipo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [Copia de una alerta en otro equipo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [Exportación de una alerta ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [Supresión de una alerta ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [Definición de umbrales de alerta como expresiones booleanas personalizadas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## Capturas
{: #monitoring_captures}

Una captura es un archivo de rastreo que se puede generar para analizar lo que sucede en un nodo durante un periodo de tiempo. El límite de tamaño de un archivo de captura es de 100 MB. Por ejemplo, puede utilizar una captura para analizar cuellos de botella o interacciones de componentes. 

Las capturas contienen llamadas del sistema y otros sucesos de sistema operativo, como latencias a nivel de sistema, duración de trabajos por lotes, tiempos de interrupción de despliegues, latencias de ajuste automático, tiempos de inicio de contenedor o tiempo de transacción de aplicación. Las capturas incluyen información detallada procedente de cada contenedor de un nodo. 

En función de las directrices de la organización, tenga en cuenta la posibilidad de inhabilitar las capturas. De forma predeterminada, las capturas se habilitan cuando se configura un agente de Sysdig en un nodo.
{: tip}

Puede crear, explorar, descargar y suprimir *capturas* para nodos individuales. Un nodo puede ser un host, un contenedor, una máquina virtual, un servidor nativo o cualquier origen de métricas en el que se instala un agente de Sysdig. 

* En la interfaz de usuario web, puede crear capturas en la sección *Explorar* y gestionar los archivos de captura mediante la sección *Capturas*.
* Puede visualizar los datos de una captura mediante *Csysdig* (la interfaz de usuario de línea de mandatos basada en curses para sysdig) o los programas de utilidad de código abierto de Sysdig para analizar los datos de una captura.
* Puede buscar datos en una captura utilizando filtros.
* Puede manipular los datos de una captura utilizando chisels (scripts). 

Cuando se habilita la característica de captura para un equipo, solo los miembros de dicho equipo pueden ver los archivos de captura.

En la lista siguiente se describen las tareas principales cuando se trabaja con capturas:
* [Creación de una captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [Supresión de una captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [Exploración de una captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [Descarga de una captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

Para obtener más información, consulte [Cómo trabajar con capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


