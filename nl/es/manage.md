---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, manage

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

# Gestión de datos
{: #manage}

Utilice etiquetas para agrupar recursos de la infraestructura en jerarquías lógicas, filtrar datos y dividir en segmentos datos agregados. Personalice la forma en que se agregan los datos cuando se configura un gráfico o se crea una alerta para una métrica. Defina el ámbito de un panel de control, un panel o una alerta para filtrar puntos de datos. Restrinja el acceso a los datos gestionando el acceso a los datos de los usuarios mediante equipos. 
{:shortdesc}



## Etiquetas
{: #manage_labels}

Las **etiquetas** definen las características de una métrica. Puede utilizar etiquetas para identificar y diferenciar las características de una métrica. 

Las etiquetas se clasifican como etiquetas de infraestructura y etiquetas de descriptores de métricas. Cada métrica tiene un conjunto de etiquetas predefinidas. Para las métricas personalizadas, puede configurar más etiquetas. 

* Puede utilizar **etiquetas de infraestructura** para identificar los objetos dentro de la infraestructura. Estas etiquetas se obtienen de la infraestructura. Por ejemplo, una etiqueta puede ser *kubernetes.pod.name*.
* Puede utilizar **etiquetas de descriptores de métricas** para definir etiquetas personalizadas. Estas etiquetas son pares de clave-valor que se aplican directamente a las métricas y que se obtienen de integraciones, como StatsD, Prometheus y JMX. 

## Grupos
{: #manage_groups}

Los **grupos** organizan los objetos de la infraestructura en jerarquías lógicas. Utilice grupos para estructurar la infraestructura y facilitar la supervisión del entorno.

En la vista *Explorar* de la interfaz de usuario web, puede ejecutar cualquiera de las acciones siguientes:

| Tarea                                                                                        | Descripción     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Copiar un grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#copy_group)                | Copiar un grupo en otros equipos. |
| [Crear un grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#create_group)            | Crea un grupo nuevo. |
| [Suprimir un grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#delete_group)            | Suprimir un grupo. |
| [Renombrar un grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#rename_group)            | Cambiar el nombre de un grupo. |
| [Compartir un grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#share_group)              | Compartir un grupo con otros miembros del equipo. |
{: caption="Tabla 1. Etiquetas de agrupación de tareas" caption-side="top"} 



## Agregación
{: #manage_aggregation}

La **agregación** de datos se produce automáticamente cuando se configura un gráfico o se crea una alerta para una métrica. Hay dos tipos de agregación: agregación de tiempo y agregación de grupos. 
* La agregación de tiempo se realiza siempre antes que la agregación de grupos.
* Para crear comparaciones de varias series y varias alertas, también puede dividir los datos agregados en secciones de menor tamaño denominadas **segmentos** mediante el uso de etiquetas. 

Sysdig agrega datos a lo largo del tiempo. Luego toma estos puntos de datos y los agrupa para mostrar los datos en métricas y en paneles de control o para calcular umbrales de alertas. 
{: tip}

Puede personalizar la forma en que se agregan los datos al configurar un gráfico o al crear una alerta para una métrica.

Hay dos formas de agregación que se utilizan para las métricas: 
* Agregación de tiempo
* Agregación de grupos

**La agregación de tiempo se realiza siempre antes que la agregación de grupos.**


### Agregación de tiempo
{: #manage_time_aggregation}

**De forma predeterminada, un agente de Sysdig recopila y notifica métricas con una resolución de 10 segundos.**

En los gráficos de series temporales que incluyen datos de cinco minutos o menos, 
* Los puntos de datos se dibujan con una resolución de 10 segundos
* No se produce la agregación de tiempo.

La agregación de tiempo se produce automáticamente en las siguientes situaciones:

* En los gráficos de series temporales que incluyen datos correspondientes a un intervalo de tiempo de más de cinco minutos, los puntos de datos se dibujan como un agregado para un intervalo de tiempo adecuado. Por ejemplo, para un gráfico que muestra datos correspondientes a una hora, cada punto de datos representa un intervalo de un minuto.
* Cuando se muestran datos históricos. Los datos se acumulan con el tiempo. Puede elegir qué puntos de datos se utilizarán cuando se visualicen datos antiguos.

En la tabla siguiente se muestran distintos tipos de agregación para los gráficos de series de tiempo:

| Tipo de agregación | Descripción                                                              |
|------------------|--------------------------------------------------------------------------|
| average          | Promedio de los valores de las métricas recuperadas durante el periodo de tiempo evaluado. |
| rate (timeAvg)   | Valor medio de la métrica durante el periodo de tiempo evaluado.            |
| maximum	         | Valor más alto durante el periodo de tiempo evaluado.                          |
| minimum	         | Valor más bajo durante el periodo de tiempo evaluado.                           |
| sum              | Suma combinada de la métrica durante el periodo de tiempo evaluado.             |
{: caption="Tabla 2. Tipos de agregación para gráficos de series temporales" caption-side="top"} 

**Nota:** de forma predeterminada, se utiliza el promedio para mostrar puntos de datos correspondientes a un intervalo de tiempo.

Los tipos de agregación rate y average son muy parecidos. Generalmente proporcionan el mismo resultado. Sin embargo, cada uno se calcula de una forma diferente. Si el tiempo de la agregación se ha establecido en un minuto, el agente de Sysdig se establece para recuperar seis muestras, una cada 10 segundos. Tenga en cuenta que, en algunos casos, es posible que las muestras no se encuentren debido a desconexiones u otras circunstancias.


### Agregación de grupos
{: #manage_group_aggregation}

**De forma predeterminada, se calcula el promedio de las métricas que se aplican a un grupo de recursos, como por ejemplo varios contenedores, hosts o nodos, entre los miembros del grupo.**

Por ejemplo, si tres hosts notifican un uso de CPU distinto para un intervalo de muestreo, se calcula el promedio de los tres valores y se notifica en el gráfico como un único punto de datos para esa métrica.

En la tabla siguiente se muestran los distintos tipos de agregación de grupos:

| Tipo de agregación | Descripción                                        |
|------------------|----------------------------------------------------|
| average          | Valor medio de las muestras del intervalo.           |
| maximum	         | Valor más alto de las muestras del intervalo.           |
| minimum	         | Valor más bajo de las muestras del intervalo.            |
| sum              | Valor combinado de las muestras del intervalo.          |
{: caption="Tabla 3. Tipos de agregación para la agregación de grupos" caption-side="top"} 


**La agregación de grupos depende de la segmentación.** Para obtener una vista que muestre las métricas correspondientes a un grupo de elementos, si se cambia la selección *Segmentar por* para separar los elementos individuales, no se produce la agregación de grupos.



## Ámbito
{: #manage_scope}

El **ámbito** es una colección de etiquetas que definen las condiciones para filtrar puntos de datos cuando se crean paneles de control y paneles, se configuran alertas y se personalizan equipos. 

En la tabla siguiente se muestran las tareas que puede ejecutar para cambiar el ámbito del servicio de supervisión:

| Tarea                                                                                        | Descripción     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Cambio del ámbito de un panel de control](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Cambiar el ámbito de un panel de control para filtrar los puntos de datos para todas las métricas que se muestran en los paneles del panel de control. |
| [Cambio del ámbito de un panel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Cambiar el ámbito de un panel para filtrar los datos correspondientes a una métrica específica que se muestra en el panel. |
| [Cambio del ámbito de un equipo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope) | Cambiar el ámbito de los datos que pueden ver los usuarios que son miembros de un equipo. |
{: caption="Tabla 4. Tareas para cambiar el ámbito" caption-side="top"} 


## Equipos
{: #manage_teams}

Los **equipos** agrupan usuarios y controlan los datos y los permisos para trabajar con las capturas de Sysdig y los sucesos de la infraestructura para dichos usuarios. 

Un administrador de Sysdig puede definir tantos equipos como desee. Para cada equipo, puede configurar la información siguiente:
* El *equipo predeterminado*: puede definir este equipo de modo que sea el equipo al que se asigna de forma predeterminada cualquier usuario que inicie la sesión por primera vez en la interfaz de usuario web.
* El *punto de entrada predeterminado*: puede especificar la vista en la interfaz de usuario web que se abre cada vez que un usuario inicia una sesión. Los puntos de entrada válidos son: vista *Explorar*, vista *Paneles de control*, vista *Sucesos*, vista *Alertas* y vista *Valores*.
* El ámbito: puede limitar los datos que pueden ver los usuarios. Puede elegir *Host* o *Contenedor* para definir el nivel de datos que pueden ver. A continuación, puede añadir una o varias condiciones. Si el ámbito se establece en *Host*, los usuarios pueden ver toda la información a nivel de host y a nivel de contenedor. Si el ámbito se establece en *Contenedor*, los usuarios solo pueden ver la información a nivel contenedor.
* Permisos: puede habilitar o inhabilitar las características siguientes: *Capturas de Sysdig* y *Sucesos de la infraestructura*. Los archivos de captura solo resultarán visibles para los miembros del equipo. **Nota:** las capturas incluyen información detallada de cada contenedor de un host, independientemente del ámbito del equipo. Cuando los sucesos de infraestructura están habilitados, los usuarios pueden ver todos los sucesos personalizados de la infraestructura de cada usuario y agente de Sysdig de la instancia.

De forma predeterminada, hay un equipo de **Operaciones de supervisor** que está predefinido para cada instancia de {{site.data.keyword.mon_full_notm}}.
* Este equipo no se puede suprimir.
* Los usuarios se añaden automáticamente como miembros de este equipo y se les otorga visibilidad completa sobre todos los recursos disponibles en la instancia. 

**Nota:** 
* Un administrador debe cambiar al equipo de *Operaciones de supervisión* para poder crear equipos o cambiar los valores de otros equipos.
* Después de que un usuario inicie la sesión en {{site.data.keyword.cloud_notm}} e inicie la interfaz de usuario web de Sysdig, un administrador puede gestionar dicho usuario en la interfaz de usuario web de Sysdig. El usuario se crea en la base de datos de Sysdig cuando el usuario inicia la sesión en la interfaz de usuario web de Sysdig por primera vez. 

Para restringir los permisos de visualización de los usuarios, un administrador puede realizar cualquiera de las acciones siguientes:
* Cambiar el rol del usuario en el equipo de *Operaciones de supervisor* predeterminado por usuario de *Lectura*. 
* Crear un equipo predeterminado con un ámbito y una visibilidad limitados. A continuación, asigne manualmente usuarios a otros equipos. 

En la tabla siguiente se muestran las tareas que puede ejecutar cuando trabaje con equipos:

| Tarea                                                                            | Descripción                 |
|---------------------------------------------------------------------------------|-----------------------------|
| [Creación de un equipo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_create)      | Crear un equipo para controlar la visibilidad de los datos.  |
| [Supresión de un equipo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_delete)      | Suprimir un equipo. </br>**Nota:** cuando se suprime un equipo, los usuarios que solo pertenecen a dicho equipo se mueven al equipo predeterminado. |
| [Adición de miembros del equipo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_users)   | Añadir más usuarios a un equipo. |
| [Edición de un equipo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope)          | Cambiar el ámbito de los datos que pueden ver los usuarios que son miembros de un equipo.  |
{: caption="Tabla 5. Tareas para trabajar con equipos" caption-side="top"} 





    


