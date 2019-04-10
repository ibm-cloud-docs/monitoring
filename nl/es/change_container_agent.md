---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Personalización de agentes de Sysdig de contenedor
{: #change_container_agent}

En {{site.data.keyword.mon_full_notm}}, puede personalizar la configuración de un agente de Sysdig para establecer un nivel de registro, bloquear puertos, incluir o excluir datos de métricas, añadir o eliminar sucesos y filtrar contenedores. 
{:shortdesc}


## Edición del archivo yaml de dragent
{: #change_container_agent_edit_config}

El archivo yaml se encuentra en */opt/draios/etc/*.

Siga los pasos siguientes para editar el archivo y aplicar los cambios:

1. Acceda al archivo *dragent.yaml* directamente en `/opt/draios/etc/dragent.yaml`.
2. Edite el archivo. Utilice una sintaxis de YAML válida.
3. Reinicie el agente. Ejecute el mandato siguiente:

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## Bloqueo de puertos
{: #change_container_agent_block_ports}

Para bloquear el tráfico de red y las métricas procedentes de los puertos de red, debe personalizar la sección **blacklisted_ports** en el archivo *dragent.yaml*. Debe obtener una lista de los puertos de los que desea filtrar los datos.

**Nota:** el puerto 53 (DNS) siempre está en la lista negra. 

Por ejemplo, en el ejemplo siguiente se muestra cómo establecer la sección *blacklisted_ports* de un agente de Sysdig para excluir datos procedentes de los puertos 6666 y 6379:

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## Recopilación de un conjunto de sucesos de Docker
{: #change_container_agent_collect_docker_events}

{{site.data.keyword.mon_full_notm}} da soporte a la integración de sucesos con Docker. Los agentes de Sysdig descubren automáticamente los orígenes de Docker y recopilan datos de sucesos de los mismos. Puede editar el archivo de configuración del agente para cambiar su comportamiento predeterminado e incluir o excluir datos de sucesos. 

De forma predeterminada, solo se recopila un conjunto limitado de sucesos. El archivo de configuración de valores predeterminado */opt/draios/etc/dragent.default.yaml*
incluye los sucesos que se recopilan. Para obtener más información sobre los sucesos que se recopilan de forma predeterminada, consulte [Sucesos de Docker ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}.

Para añadir o eliminar sucesos, debe personalizar el archivo *dragent.yaml* y especificar qué sucesos se deben incluir y cuáles se van a filtrar. **Nota:** una entrada en una sección de *dragent.yaml* prevalece sobre toda la sección de la configuración predeterminada.
{: tip}

Por ejemplo, para filtrar los sucesos de imagen de Docker y recopilar solo sucesos correspondientes a las acciones adjuntar (attach), confirmar (commit) y copiar (copy), debe establecer la sección *docker* de la forma siguiente:

* Opción 1: defina la secuencia de entradas como una lista:

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* Opción 2: defina la secuencia de entradas en una sola línea entre corchetes:

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## Inhabilitación de la recopilación de sucesos
{: #change_container_agent_disable_events}

Para hacer que un agente de Sysdig deje de recopilar sucesos, debe modificar el archivo *dragent.default.yaml*. Establezca la sección **events** en *none* en el archivo *dragent.yaml*.

Por ejemplo, para filtrar los sucesos de Docker, debe establecer la sección *events* del archivo *dragent.yaml* tal como se muestra a continuación:

```
events:
  docker: none
```
{: codeblock}



## Filtrado de sucesos según su gravedad
{: #change_container_agent_filterby_severity}

Para filtrar sucesos por gravedad, también puede cambiar el tipo de entrada de registro para los sucesos en el archivo *dragent.yaml*. 

El nivel de registro predeterminado es **information**. Esto significa que solo se transmiten los sucesos de aviso y de gravedad superior.

Los valores válidos son: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* y *none*. **Nota**: los valores se muestran de prioridad más alta a prioridad más baja.

Por ejemplo, para filtrar los sucesos de gravedad baja (*notice*, *informaton*, *debug*), debe establecer la sección log **event_priority** en *warning*:

```
log:
  event_priority: warning
```
{: codeblock}


Para bloquear la recopilación de sucesos, debe establecer la sección de registro **event_priority** en *none*:

```
log:
  event_priority: none
```
{: codeblock}




## Inclusión y exclusión de métricas
{: #change_container_agent_inc_exc_metrics}

Para filtrar métricas personalizadas, debe personalizar la sección **metrics_filter** en el archivo *dragent.yaml*. Puede especificar las métricas que se deben incluir y las que se deben filtrar configurando los parámetros de filtro **include** y **exclude**.

**Nota:** el orden de la regla de filtrado se establece de la forma siguiente: se aplica la primera regla que coincide con una métrica.

Por ejemplo, si la sección *metrics_filter* de un agente de Sysdig tiene el aspecto siguiente:

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* Está configurando el agente de Sysdig para que recopile todos los datos de métricas que empiezan por *metricA*, *metricB* y *haproxy.backend*. 
* Está filtrando las métricas que empiezan por *metricC* y otras métricas que empiezan por *haproxy*. 
* La entrada `exclude: metricA.*` se pasa por alto.


## Cambio del nivel de registro
{: #change_container_agent_log_level}

Para configurar el nivel de registro, debe personalizar la sección **log** del archivo *dragent.yaml*. 

El agente de Sysdig genera entradas de registro en */opt/draios/logs/draios.log*. 
* El archivo de registro rota cuando alcanza los 10 MB de tamaño.
* Se conservan los 10 archivos de registro más recientes. La indicación de fecha y fecha que se añade al nombre de archivo se utiliza para determinar qué archivos se deben conservar.
* Los niveles de registro válidos son: *none*, *error*, *warning*, *info*, *debug* y *trace*
* El nivel de registro predeterminado es *info*, donde se crea una entrada para cada transmisión de métricas agregada a los servidores de fondo, una vez por segundo, además de las entradas correspondientes a avisos y errores.
* Puede personalizar el tipo de registro y las entradas que se recopilan configurando el archivo de configuración del agente de Sysdig **/opt/draios/etc/dragent.yaml**. Después de editar el archivo, debe reiniciar el agente en el shell con `docker restart sysdig-agent` para activar los cambios.

| Casos de uso                                     | Entrada en la sección log           |
|-----------------------------------------------|-----------------------------|
| Resolución de problemas del comportamiento del agente                   | `file_priority: debug`      |
| Reducción de la salida de la consola del contenedor               | `console_priority: warning` |
| Filtrado de sucesos según su gravedad                  | `event_priority: warning`   |
| Verificación de las métricas que se incluyen o se excluyen  | `metrics_excess_log: true`  |
{: caption="Tabla 2. Entradas de la sección log" caption-side="top"} 


