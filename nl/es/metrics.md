---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, metrics

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

# Cómo trabajar con métricas
{: #metrics}

Después de suministrar una instancia del servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.Bluemix}} y de configurar un agente de Sysdig para un origen de métricas, puede ver, supervisar y gestionar métricas mediante la interfaz de usuario Web de {{site.data.keyword.mon_full_notm}}. Utilice métricas para analizar los datos estadísticos que tienen valores numéricos. 
{:shortdesc}


**Una métrica es una medida cuantitativa que tiene una o varias etiquetas para definir sus características.**

Una métrica se representa mediante series temporales. 

Una serie temporal es un conjunto de puntos de datos numéricos durante un periodo de tiempo. 

Las métricas se clasifican en dos grupos: 

* Métricas predeterminadas 
* Métricas personalizadas


## Etiquetas
{: #metrics_labels}

**Las etiquetas definen las características de una métrica.**

Las etiquetas se clasifican como etiquetas de infraestructura y etiquetas de descriptores de métricas. Cada métrica tiene un conjunto de etiquetas predefinidas. Para las métricas personalizadas, puede configurar más etiquetas. 

Puede utilizar etiquetas para identificar y diferenciar las características de una métrica, por ejemplo:
* Puede agrupar objetos de la infraestructura en jerarquías lógicas. 
* Puede filtrar datos. 
* Puede dividir datos agregados en segmentos. 


## Métricas predeterminadas 
{: #metrics_default}

**Las métricas predeterminadas informan sobre el sistema, el orquestador y la infraestructura de red.**

El servicio de supervisión añade automáticamente etiquetas a cada métrica.


## Métricas personalizadas
{: #metrics_custom}

**Las métricas personalizadas varían en función del tipo de infraestructura y de las aplicaciones que se supervisan. Algunos ejemplos son JMX, Prometheus y StatsD.**

Estas métricas tienen un conjunto de etiquetas predefinidas. Puede añadir etiquetas personalizadas adicionales.

El servicio de supervisión mantiene un índice de todas las métricas personalizadas y las etiquetas personalizadas que han notificado datos en los últimos 14 días. Puede utilizar estas métricas para configurar paneles de control, ámbitos y alertas.

Tenga en cuenta la información siguiente sobre cómo gestiona el servicio de supervisión las entradas de índice:
*  Una métrica se elimina automáticamente del índice de servicio de supervisión y se marca como que falta cuando se produce cualquiera de las condiciones siguientes:
    
    * El servicio de supervisión no recibe ningún dato para una métrica o etiqueta durante más de 14 días.
    
    * Una métrica o una etiqueta nunca ha notificado datos.

* No se pueden configurar artefactos nuevos cuando falta una métrica o una etiqueta. 
* No se pueden actualizar artefactos existentes hasta que las métricas y etiquetas que faltan se eliminan de la configuración actual.
* Puede utilizar una métrica o una etiqueta que falta en consultas de datos y en gráficos. 
* Los artefactos existentes no se ven afectados si incluyen una métrica o una etiqueta que falta.
* Cuando se reciben datos correspondientes a una métrica o etiqueta que falta, la métrica o la etiqueta se vuelve a añadir al índice.



