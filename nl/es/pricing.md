---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, pricing

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


# Tarifas
{: #pricing_plans}

Dispone de varios planes de precios para una instancia de {{site.data.keyword.mon_full_notm}}.
{:shortdesc}
 

| Planes            | Nivel         | Recopilación de datos  |
|------------------|--------------|------------------|
| `Prueba`          |              | Los datos se recopilan para un máximo de 20 contenedores por nodo o para 200 métricas personalizadas por nodo solo durante 30 días. |
| `Nivel graduado` | `Básico`      | Los datos se recopilan para un máximo de 20 contenedores por nodo o para 200 métricas personalizadas por nodo. |
| `Nivel graduado` | `Pro`        | Los datos se recopilan para un máximo de 50 contenedores por nodo o para 500 métricas personalizadas por nodo. |
| `Nivel graduado` | `Avanzado`   | Los datos se recopilan para un máximo de 110 contenedores por nodo o para 1000 métricas personalizadas por nodo. |
{: caption="Tabla 1. Lista de planes de servicio" caption-side="top"} 


**Nota:** un nodo puede ser un host, un contenedor, una máquina virtual, un servidor nativo o cualquier origen de métricas en el que se instala un agente de Sysdig.

Cuando el número de contenedores por nodo o el número de métricas sobrepasa el límite del umbral del plan de nivel graduado durante un periodo de tiempo, se aplica la detección automática de niveles. Se activa una notificación de alerta según la configuración de notificación de uso de facturación si ha habilitado la siguiente alerta **[{{site.data.keyword.IBM_notm}}]:  Cambio de nivel de uso**

Puede solicitar una **cotización de precio personalizada** para lo que sobrepase el límite del *plan de precios de pago del nivel graduado avanzado*; para ello debe abrir una incidencia con el [equipo de soporte de IBM Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window}.
{: tip}

Los datos se recopilan y conservan según las directrices estándares en todos los planes. Para obtener más información, consulte los apartados sobre [recopilación de datos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection) y [retención de datos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention).


## Comprobación del uso
{: #pricing_usage}

Para supervisar el uso del servicio {{site.data.keyword.mon_full_notm}} y los costes asociados a dicho uso, consulte [Visualización del uso](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).



## Habilitación de la alerta que notifica un cambio de nivel
{: #pricing_alert}

Para que se le notifique cuando hay un cambio de nivel, debe habilitar la siguiente alerta: **[{{site.data.keyword.IBM_notm}}]:  Cambio de nivel de uso**

Complete los pasos siguientes para habilitar una alerta:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
2. Cree un canal de notificación. Para obtener más información, consulte [Configuración de un canal de notificación](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create). 
3. Pulse **ALERTAS** para ir a la sección *Alertas*.
2. Busque **[IBM]:  Cambio de nivel de uso**.
3. Edite la alerta para añadir el canal de notificación.
4. Pulse **Guardar**.



## ¿Cómo se genera la alerta del plan de servicio?
{: #pricing_how}

Para que se le notifique cuando hay un cambio de nivel, debe habilitar la siguiente alerta: **[{{site.data.keyword.IBM_notm}}]:  Cambio de nivel de uso**

**Nota:** cuando habilite esta alerta, debe especificar los canales de notificación a través de los cuales desea que se le notifique.

El uso se calcula como el promedio del número de nodos y métricas de los que se toman muestras cada 10 segundos durante la hora anterior. No se incluyen las pequeñas fluctuaciones de corta duración. La diferencia entre el uso anterior y el actual se produce una vez por hora.

Los umbrales definidos se establecen de la siguiente forma:

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [21, 50]
    Advanced = [51, 100]
  }
  metricDensity {
    Basic = [0, 200]
    Pro = [201, 500]
    Advanced = [501, 1000]
}
```
{: screen}

La notificación de alerta se genera de la forma siguiente:
1. Cada hora se genera un suceso personalizado si aumenta el número de contenedores por nodo en un nivel.
2. La condición de alerta comprueba si hay sucesos personalizados que informen acerca de los cambios en el número de contenedores por nodo. Si encuentra un suceso en el que el número de contenedores de un nivel aumenta con respecto a la última vez que se calculó el uso, envía una notificación.

La frecuencia de la alerta es una vez cada hora. En el caso de un nodo fluctuante, la frecuencia de la alerta es como máximo de cada dos horas.

Tenga en cuenta que la alerta solo se genera si un nodo pasa del nivel *Básico* al *Pro* o al *Avanzado*. 



### Ejemplos
{: #pricing_examples}

**Ejemplo 1** 

Si el recuento medio de contenedores es el siguiente: 

| Hora     | Número de contenedores | Descripción                                                                   | ¿Se genera una alerta? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 18                   | El nivel está establecido en **Básico**.                                                     | No                     |
| 11:00    | 21                   | Número de contenedores por encima del nivel *Básico*. El nivel pasa a ser **Pro**.            | Sí                    |
| 12:00    | 19                   | Número de contenedores por debajo del nivel *Básico*. El nivel vuelve a ser el **Básico**.     | No                    |
| 13:00    | 20                   | No hay cambio de nivel. El nivel está establecido en **Básico**.                                     | No                     |
{: caption="Tabla 2. Ejemplo 1" caption-side="top"} 


**Ejemplo 2**

Si el recuento medio de contenedores es el siguiente: 

| Hora     | Número de contenedores | Descripción                                                                   | ¿Se genera una alerta? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | El nivel está establecido en **Básico**.                                                     | No                     |
| 11:00    | 19                   | El nivel está establecido en **Básico**.                                                     | No                     |
| 12:00    | 20                   | El nivel está establecido en **Básico**.                                                     | No                    |
| 13:00    | 21                   | Número de contenedores por encima del nivel *Básico*. El nivel pasa a ser **Pro**.            | Sí                     |
{: caption="Tabla 3. Ejemplo 2" caption-side="top"}


**Ejemplo 3**

Si el recuento medio de contenedores es el siguiente: 

| Hora     | Número de contenedores | Descripción                                                                   | ¿Se genera una alerta? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | El nivel está establecido en **Básico**.                                                     | No                     |
| 11:00    | 20                   | El nivel está establecido en **Básico**.                                                     | No                    |
| 12:00    | 21                   | El nivel está establecido en **Básico**.                                                     | Sí                    |
| 13:00    | 20                   | El número de contenedores vuelve al nivel *Básico*. El nivel pasa a ser **Pro**.          | No                     |
{: caption="Tabla 3. Ejemplo 3" caption-side="top"}



