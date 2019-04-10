---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, overview

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


# Acerca de {{site.data.keyword.mon_full_notm}}
{: #about}

{{site.data.keyword.mon_full}} es un sistema de gestión inteligente de contenedores de terceros nativo de la nube que puede incluir como parte de la arquitectura {{site.data.keyword.cloud_notm}}. Utilícelo para obtener visibilidad operativa sobre el rendimiento y el estado de las aplicaciones, los servicios y las plataformas. Ofrece a los administradores, a los equipos DevOps y a los desarrolladores telemetría de pila completa con funciones avanzadas para supervisar y solucionar problemas, definir alertas y diseñar paneles de control personalizados. {{site.data.keyword.mon_full_notm}} es una característica gestionada por Sysdig en asociación con {{site.data.keyword.IBM_notm}}.
{:shortdesc}


Para añadir características de supervisión con {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}, debe suministrar una instancia del servicio {{site.data.keyword.mon_full_notm}}.

Antes de suministrar una instancia, tenga en cuenta la información siguiente:

* Los datos se envían a un tercero.
* El propietario de la cuenta puede crear, ver y suprimir una instancia de un servicio en {{site.data.keyword.cloud_notm}}, y puede otorgar permisos a otros usuarios para que trabajen con el servicio {{site.data.keyword.mon_full_notm}}.
* Otros usuarios de {{site.data.keyword.cloud_notm}} con permisos de `administrador` o de `editor` pueden gestionar el servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}. Estos usuarios también deben tener permisos de la plataforma para crear recursos dentro del contexto del grupo de recursos en el que van a suministrar la instancia.

Una instancia se suministra dentro del contexto de un grupo de recursos. Un grupo de recursos le permite organizar los servicios para el control de accesos y para la facturación. Puede suministrar la instancia de {{site.data.keyword.mon_full_notm}} en el grupo de recursos *predeterminado* o en un grupo de recursos personalizado.

Cuando se [suministra una instancia](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision), se obtiene automáticamente una clave de ingestión, conocida como [clave de acceso de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key).

Después de suministrar una instancia, debe configurar un agente de {{site.data.keyword.mon_full_notm}} para cada origen de métrica. Un origen de métrica es un recurso de la nube que desea supervisar y cuyo rendimiento y estado desea controlar. Debe configurar un agente de {{site.data.keyword.mon_full_notm}} en cada entorno que desee supervisar. Por ejemplo, un origen de métrica puede ser un clúster de Kubernetes. Utilice la clave de acceso de Sysdig para configurar el agente de Sysdig que es responsable de recopilar y reenviar los datos de métrica a la instancia.

Después de desplegar el agente de {{site.data.keyword.mon_full_notm}} en un origen de métrica, la recopilación y el reenvío de métricas a la instancia son automáticos. El agente de {{site.data.keyword.mon_full_notm}} recopila e informa automáticamente sobre métricas predefinidas. Puede configurar qué métricas se deben supervisar en un entorno.

Puede [supervisar](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring) y [gestionar](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage) los datos a través de la interfaz de usuario web de {{site.data.keyword.mon_full_notm}}.  

En la figura siguiente se muestra una visión general de los componentes del servicio {{site.data.keyword.mon_full_notm}} que se ejecuta en {{site.data.keyword.cloud_notm}}:

![Visión general de los componentes de {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}](images/components.png "Visión general de los componentes de {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}")



## Recopilación de datos
{: #overview_collection}

Cuando configura un agente de Sysdig para que recopile y reenvíe datos a una instancia de {{site.data.keyword.mon_full_notm}}, los datos se recopilan automáticamente y pasan a estar disponibles para su análisis en la interfaz de usuario web.

Los datos se recopilan con una frecuencia de 10 segundos. 

## Disponibilidad de datos
{: #overview_availability}

Los datos están disponibles durante un máximo de 15 meses.

Después de eliminar un agente de Sysdig de un host o de un contenedor, los datos históricos no se suprimen. Los datos están disponibles para su análisis a través de la interfaz de usuario web durante el periodo de tiempo en que el agente esté instalado y genere informes.

Después de suprimir una instancia del servicio {{site.data.keyword.mon_full_notm}}, los datos no están disponibles para la búsqueda y el análisis.



## Retención de datos
{: #overview_retention}

Se retienen datos correspondientes a cada instancia según una política de *acumulación*.

Con el tiempo, los datos se acumulan, primero con mayor granularidad y luego con menos, hasta alcanzar los 3 meses.

La política de acumulación describe la granularidad de los datos a lo largo del tiempo:

* Los datos se conservan a una resolución de 10 segundos durante las 6 primeras horas.
* Los datos se conservan a una resolución de 1 minuto durante 2 días.
* Los datos se conservan a una resolución de 10 minutos durante 2 semanas.
* Los datos se conservan a una resolución de 1 hora durante 3 meses.
* Los datos se conservan a una resolución de 1 día durante un año.

## Supresión de datos
{: #overview_data_deletion}

Cuando suprima una instancia de {{site.data.keyword.mon_full_notm}} de {{site.data.keyword.cloud_notm}}, debe abrir un caso a través del sistema de soporte para solicitar que se supriman los datos. Para obtener más información, consulte [cómo ponerse en contacto con el servicio de soporte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp).

Cuando se suprime una captura, el archivo de datos correspondiente a dicha captura se suprime automáticamente.

**NOTA: la supresión de los datos que se recopilan desde un solo agente de Sysdig en una instancia de {{site.data.keyword.mon_short}} no recibe soporte.**



## Ubicación de los datos
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}} recopila y agrega métricas. 

* Los datos de métricas se alojan en {{site.data.keyword.cloud_notm}}.
* Cada ubicación de región multizona (MZR) recopila y agrega métricas correspondientes a cada instancia de {{site.data.keyword.mon_full_notm}} que se ejecuta en dicha ubicación.
* Los datos se
coubican en la región donde se ha suministrado la instancia de {{site.data.keyword.mon_full_notm}}. Por ejemplo, los datos de métricas correspondientes a una instancia suministrada en EE. UU. sur se alojan en la región EE. UU. sur.



## Agentes de {{site.data.keyword.mon_full_notm}}
{: #overview_sysdig_agent}

El agente de {{site.data.keyword.mon_full_notm}} recopila e informa automáticamente sobre métricas predefinidas. 

En la lista siguiente se muestran los agentes de {{site.data.keyword.mon_full_notm}} que están disponibles:

* Agente de {{site.data.keyword.mon_full_notm}} para Kubernetes, GKE y OpenShift.
* Agente de {{site.data.keyword.mon_full_notm}} para contenedores Docker y servicios no contenerizados.
* Agente de {{site.data.keyword.mon_full_notm}} para Mesos, Marathon y DCOS.
* Agente de {{site.data.keyword.mon_full_notm}} para instalaciones manuales de Linux.

Para obtener más información, consulte [Configuración de un agente de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) y [Eliminación de un agente de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove).


## Visualización del uso
{: #overview_usage}

Para supervisar el uso y los costes de su servicio, consulte [Visualización del uso](/docs/billing-usage/viewing_usage.html#viewingusage).


## Planes de servicio
{: #overview_plans}

Dispone de varios planes de precios para una instancia de {{site.data.keyword.mon_full_notm}}. Para obtener más información, consulte el apartado sobre [Tarifas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).


## Consideraciones sobre seguridad
{: #overview_security}

**Capturas**

Una captura es un archivo de rastreo que se puede generar para analizar lo que sucede en un host durante un periodo de tiempo. Las capturas contienen llamadas del sistema y otros sucesos del sistema operativo. Puede habilitar o inhabilitar esta característica por nodo cuando configure el agente de Sysdig que recopila métricas de ese nodo. De forma predeterminada, las *Capturas* se habilitan cuando se configura un agente de Sysdig. Un nodo puede ser un host, un contenedor, una máquina virtual, un servidor nativo o cualquier origen de métricas en el que se instala un agente de Sysdig.

**IMPORTANTE** Cuando las capturas están habilitadas, tenga en cuenta que Sysdig tendrá una visibilidad profunda en sus operaciones. Para evitar una incidencia de seguridad y la potencial exposición de datos fuera de su organización, compruebe las políticas de seguridad de su organización antes de habilitar capturas en un nodo. Tenga en cuenta la posibilidad de inhabilitar la característica de *Captura* para todos los agentes de Sysdig.
{: tip}

