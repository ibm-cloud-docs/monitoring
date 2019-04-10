---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring,  predefined dashboards

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


# Paneles de control predefinidos
{: #default_dashboards}
Puede elegir cualquiera de los paneles de control predefinidos siguientes para supervisar su infraestructura:
{:shortdesc}


## Aplicaciones
{: #default_dashboards_applications}

En la tabla siguiente se muestran los paneles de control predefinidos que puede seleccionar para supervisar las aplicaciones y los componentes de la infraestructura:

| Nombre del panel de control        | Descripción                                                            | Uso             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| Visión general de HTTP         | Utilice este panel de control para supervisar el estado del servidor web. Muestra la carga en el servidor y su capacidad para dar servicio a las solicitudes de forma puntual. | Utilice los paneles Número de solicitudes y Tiempo medio/máx de solicitud para evaluar el funcionamiento global del servidor. </br>Busque las correlaciones entre los URL para encontrar oportunidades para mejorar el rendimiento. </br>Utilice la métrica Códigos de estado para supervisar los códigos de error 4xx y 5xx. |  
| Principales solicitudes HTTP  |  Utilice este panel de control para supervisar los URL más solicitados en el servidor web, como por ejemplo el número total de solicitudes, los tiempos medio y máximo en dar servicio a las solicitudes y la cantidad de tráfico contenido en las solicitudes y respuestas. |   |
| MongoDB  | Utilice este panel de control para supervisar el nivel de ocupación del servicio MongoDB, las recopilaciones con mayor demanda y las recopilaciones con un menor rendimiento.  |  Detecte las recopilaciones que se pueden beneficiar de un ajuste del rendimiento de consulta y de índice. |
| MySQL/PostgreSQL  | Utilice este panel de control para supervisar la carga global y el estado de rendimiento de las transacciones de base de datos SQL. Averigüe el número de solicitudes y la rapidez con la que se manejan.  | Mejore el rendimiento. Por ejemplo, supervise los tiempos de respuesta para las consultas más lentas e identifique los cambios realizados en la consulta o en los índices de las tablas.  |
| Principales MySQL/PostgreSQL  | Utilice este panel de control para supervisar las principales consultas SQL. Vea el número de consultas recibidas y la cantidad de tráfico enviado y recibido para la consulta.   | Busque las consultas más lentas, las consultas que se ejecutan más veces, las consultas con mayor tráfico.  |
| Nginx  | Utilice este panel de control para supervisar los recursos de host, las conexiones http, los URL principales y los más lentos y los códigos de respuesta de host. | Identifique los ajustes de equilibrio de carga supervisando las métricas siguientes: Escritura, Lectura, Conexiones en espera, Carga de CPU por máquina, Actividad de bytes de red, Solicitudes por segundo </br>Busque las páginas que se puedan optimizar examinando la métrica URL más lentos. </br>Detecte problemas examinando los códigos de respuesta.  |
{: caption="Tabla 1. Lista de paneles de control predefinidos de componentes de aplicaciones y de infraestructura" caption-side="top"} 


## Paneles de control de host y de contenedor
{: #default_dashboards_host_container}

En la tabla siguiente se muestran los paneles de control predefinidos que puede utilizar para supervisar la utilización de recursos y la actividad del sistema en los hosts y en los contenedores:


| Nombre del panel de control        | Descripción                                                            | Uso             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| *Límites de contenedor*    | Utilice este panel de control para ver las métricas de CPU y de memoria relacionadas con los recursos de host que se asignan a cada contenedor. | |
| *Sistema de archivos*         | Utilice este panel de control para ver los puntos de montaje de directorio, los dispositivos del sistema de archivos y la información de capacidad y de uso para los sistemas de archivos que están montados en la instancia.  </br>Los sistemas de archivos que están montados de forma remota no se muestran de forma predeterminada. Para ver los datos correspondientes a estos sistemas de archivos, añada la siguiente entrada **remotefs.enabled = true** al archivo */opt/draios/bin/dragent.properties* en cada instancia. </br>Cuando se seleccionan grupos, las métricas son promedios para puntos de montaje del sistema de archivos similares.| Averigüe qué sistemas de archivos se están llenando y cuáles están siendo infrautilizados. Clasifique por *fs.bytes.used*.|
| *Visión general por contenedor* | Utilice este panel de control para ver estadísticas de uso de recursos, como porcentaje de CPU, porcentaje de uso de memoria, total de bytes de red y total de bytes de archivos para los contenedores que se ejecutan en la instancia o en el grupo seleccionados.  </br>Utilice la característica *Time Travel* con la función *Compare* en esta vista para ver información histórica. En función de los datos, verifique si los procesos se ejecutan según lo esperado, si no se comportan correctamente o si requieren más recursos. | Averigüe qué contenedores están consumiendo muchos recursos.  </br>Utilice la información para determinar si una aplicación se debe mover a otro host. |
| *Visión general por imagen de contenedor* | Utilice este panel de control para obtener una visión general del tamaño, el rendimiento y las limitaciones de los servicios definidos en la imagen de contenedor. | |
| Visión general por host | Utilice este panel de control para ver estadísticas de uso general de recursos como porcentaje de CPU, porcentaje de uso de memoria, total de bytes de red, número de conexiones de red, total de bytes de archivo y uso de disco correspondientes a un host. </br>También puede utilizar este panel de control para supervisar un grupo de instancias. </br>Utilice la característica *Time Travel* con la función *Compare* en esta vista para ver información histórica. En función de los datos, verifique si los procesos se ejecutan según lo esperado, si no se comportan correctamente o si requieren más recursos. | Averigüe qué hosts no se están utilizando o cuáles se utilizan en exceso en un grupo de hosts con funciones de trabajo similares. | 
| Visión general por proceso | Utilice este panel de control para ver estadísticas de uso general de recursos como porcentaje de CPU, porcentaje de uso de memoria, total de bytes de red, número de conexiones de red, total de bytes de archivo y uso de disco correspondientes a los principales procesos de un host. </br>También puede utilizar este panel de control para supervisar un grupo de instancias. </br>Utilice la característica *Time Travel* con la función *Compare* en esta vista para ver información histórica. En función de los datos, verifique si los procesos se ejecutan según lo esperado, si no se comportan correctamente o si requieren más recursos. | Averigüe qué procesos están consumiendo muchos recursos.  </br>Utilice la información para determinar si una aplicación se debe mover a otro host. |
| Resumen del agente de Sysdig | Utilice este panel de control para ver el número de agentes de Sysdig que se han desplegado en el entorno y en sus versiones. |  | 
| Archivos principales | Utilice este panel de control para ver la lista de los archivos principales. Puede ver el nombre de archivo, el número total de bytes del archivo, el tiempo empleado en la E/S de archivo y el recuento de errores del archivo. | Descubra los principales consumidores de disco cuando clasifique por tamaño. </br>Encuentre los archivos más ocupados cuando clasifique por E/S. </br>Identifique errores potenciales al supervisar los datos de la columna *Recuento de errores de archivo*. |
| Procesos principales | Utilice este panel de control para ver la lista de procesos principales que se ejecutan en un host o en un grupo de hosts. Puede ver el nombre del proceso, su vía de acceso y todos los argumentos. </br>Utilice la función de filtro para restringir los procesos que aparecen en la lista. | Averigüe qué procesos son los principales consumidores en un entorno en el que el mismo proceso se genera varias veces. |
| Principales procesos de servidor | Utilice este panel de control para ver el consumo de recursos para los procesos identificados como orientados únicamente al servidor (httpd, java, ntpd, etc.). | Descubra el uso de recursos para los procesos de servidor. |
{: caption="Tabla 2. Lista de paneles de control predefinidos de host y de contenedor" caption-side="top"} 

## Red
{: #default_dashboards_network}

En la tabla siguiente se muestran los paneles de control predefinidos que puede seleccionar para supervisar las conexiones y la actividad de red:

| Nombre del panel de control        | Descripción                                                            | Uso             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| Tabla de conexiones     | Utilice este panel de control para ver las conexiones entre las instancias y los nodos remotos. Supervise el tráfico para cada conexión. | Encuentre los principales emisores que consumen más tráfico en la red. |
| Visión general              |  Utilice este panel de control para ver la utilización total de la red a lo largo del tiempo por dirección, aplicación, proceso y host.| Identifique cuáles son los recursos con mayor impacto sobre el rendimiento de la respuesta. |
| Tiempos de respuesta frente a Uso de recursos | Utilice este panel de control para ver métricas de recursos de host a lo largo del tiempo en comparación con el tiempo de respuesta del host en el proceso de solicitudes de red. |  |
| Puertos principales             |  Utilice este panel de control para ver los bytes entrantes, salientes y totales por puerto, así como para mostrar el número de conexiones con cada número de puerto. |  |
{: caption="Tabla 3. Lista de paneles de control predefinidos" caption-side="top"} 



## Servicio
{: #default_dashboards_service}


En la tabla siguiente se muestran los paneles de control predefinidos que puede utilizar para supervisar el rendimiento de los servicios, aunque estos servicios estén desplegados en contenedores orquestados:

| Nombre del panel de control        | Descripción                                                            | 
|-----------------------|------------------------------------------------------------------------|
| Visión general por servicio   | Utilice este panel de control para ver el tamaño, el rendimiento y las limitaciones de los servicios que se ejecutan en la misma imagen de contenedor. | 
| Visión general del servicio      | Utilice este panel de control para ver la utilización de recursos y los tiempos de respuesta de un solo servicio. | 
{: caption="Tabla 4. Lista de paneles de control predefinidos de servicio" caption-side="top"} 



## Topología
{: #default_dashboards_topology}

En la tabla siguiente se muestran los paneles de control predefinidos que puede utilizar para supervisar las dependencias lógicas de los niveles de aplicación:

| Nombre del panel de control        | Descripción                                                            | 
|-----------------------|------------------------------------------------------------------------|
| Uso de CPU             | Utilice este panel de control para supervisar la interacción entre el host y el resto de la infraestructura.  | 
| Tráfico de red       | Utilice este panel de control para supervisar el uso de ancho de banda de la instancia seleccionada entre procesos locales y procesos en nodos remotos. |
| Tiempos de respuesta        | Utilice este panel de control para supervisar las métricas de comunicación y de respuesta de red entre todos los procesos de los hosts seleccionados. </br>Los recuentos y los tiempos de respuestas se muestran en promedios con una granularidad de hasta 1 segundo.  |
{: caption="Tabla 5. Lista de paneles de control predefinidos de topología" caption-side="top"} 

**Nota:** cualquiera de estos paneles de control muestra líneas de guiones y recuadros grises para las instancias que no tienen instalado el agente de Sysdig y para las que se detecta comunicación.















