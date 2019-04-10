---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# Personalización de agentes de Sysdig de Linux
{: #change_linux_agent}

De forma predeterminada, el agente de Sysdig recopila datos de una gama de plataformas y aplicaciones. Puede editar el archivo de configuración del agente para cambiar su comportamiento predeterminado e incluir o excluir datos. Puede personalizar el archivo de configuración del agente de Sysdig para incluir métricas personalizadas como, por ejemplo, JMX, StatsD y Prometheus. También puede filtrar las métricas y los contenedores.
{:shortdesc}

El agente de Sysdig utiliza dos archivos de configuración que especifican los datos que se deben recopilar automáticamente:

| Archivo                   | Descripción                                                     | Ubicación                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Archivo de configuración principal </br>**Nota:****No edite este archivo.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Archivo de configuración que edita para personalizar el agente de Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabla 1. Archivos de configuración del agente de Sysdig" caption-side="top"} 

Puede editar el archivo *dragent.yaml* para personalizar los datos que se recopilan. Los cambios entran en vigor inmediatamente después de guardar el archivo. El agente detecta el cambio y se reinicia automáticamente. Encontrará la frecuencia y los archivos que un agente de Sysdig comprueba en el archivo *dragent.default.yaml*.

Por ejemplo, un archivo *dragent.default.yaml* incluye la siguiente información:

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## Edición del archivo yaml de dragent
{: #change_linux_agent_edit_agent}

El archivo yaml se encuentra en */opt/draios/etc/*.

Siga los pasos siguientes para editar el archivo y aplicar los cambios:

1. Acceda al archivo *dragent.yaml* directamente. El archivo se encuentra en `/opt/draios/etc/dragent.yaml`.
2. Edite el archivo. Utilice una sintaxis de YAML válida.
3. Reinicie el agente. Ejecute el mandato siguiente:

    ```
    service dragent restart
    ```
    {: codeblock}


## Bloqueo de puertos
{: #change_linux_agent_block_ports}

Para bloquear el tráfico de red y las métricas procedentes de los puertos de red, debe personalizar la sección **blacklisted_ports** en el archivo *dragent.yaml*. Debe obtener una lista de los puertos de los que desea filtrar los datos.

**Nota:** el puerto 53 (DNS) siempre está en la lista negra. 

Por ejemplo, en el ejemplo siguiente se muestra cómo establecer la sección *blacklisted_ports* de un agente de Sysdig para excluir datos procedentes de los puertos 6666 y 6379:

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## Inclusión y exclusión de métricas
{: #change_linux_agent_inc_exc_metrics}

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
{: #change_linux_agent_log_level}

Para configurar el nivel de registro, debe personalizar la sección **log** del archivo *dragent.yaml*. 

El agente de Sysdig genera entradas de registro en */opt/draios/logs/draios.log*. 
* El archivo de registro rota cuando alcanza los 10 MB de tamaño.
* Se conservan los 10 archivos de registro más recientes. La indicación de fecha y fecha que se añade al nombre de archivo se utiliza para determinar qué archivos se deben conservar.
* Los niveles de registro válidos son: *none*, *error*, *warning*, *info*, *debug* y *trace*
* El nivel de registro predeterminado es *info*, donde se crea una entrada para cada transmisión de métricas agregada a los servidores de fondo, una vez por segundo, además de las entradas correspondientes a avisos y errores.
* Puede personalizar el tipo de registro y las entradas que se recopilan configurando el archivo de configuración del agente de Sysdig **/opt/draios/etc/dragent.yaml**. Después de editar el archivo, debe reiniciar el agente en el shell con `service dragent restart` para activar los cambios.

| Casos de uso                                     | Entrada en la sección log           |
|-----------------------------------------------|-----------------------------|
| Resolución de problemas del comportamiento del agente                   | `file_priority: debug`      |
| Reducción de la salida de la consola del contenedor               | `console_priority: warning` |
| Filtrado de sucesos según su gravedad                  | `event_priority: warning`   |
| Verificación de las métricas que se incluyen o se excluyen  | `metrics_excess_log: true`  |
{: caption="Tabla 2. Entradas de la sección log" caption-side="top"} 
