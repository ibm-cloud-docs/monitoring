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

# Personalización del agente de Sysdig para que controle datos
{: #customize_agent}

De forma predeterminada, el agente de Sysdig recopila datos de una gama de plataformas y aplicaciones. Puede editar el archivo de configuración del agente para cambiar su comportamiento predeterminado e incluir o excluir datos. Puede personalizar el archivo de configuración del agente de Sysdig para incluir métricas personalizadas como, por ejemplo, JMX, StatsD y Prometheus. También puede filtrar métricas, datos de sucesos y contenedores.
{:shortdesc}

## Personalización del agente de Sysdig de Kubernetes
{: #kube}

El agente de Sysdig de Kubernetes utiliza dos archivos de configuración que especifican los datos que se deben recopilar automáticamente:

| Nombre de archivo                        | Acciones           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modificar nivel de registro. |
| `sysdig-agent-configmap.yaml`    | Bloquear puertos. </br>Incluir o excluir datos de métricas. </br>Añadir o eliminar sucesos. </br>Filtre contenedores. |
{: caption="Tabla 1. Archivos de configuración del agente de Sysdig de Kubernetes" caption-side="top"} 

Para editar un agente de Sysdig de Kubernetes, es posible que tenga que editar el archivo *sysdig-agent-configmap.yaml*, el archivo *sysdig-agent-daemonset-v2.yaml* o ambos.

Puede utilizar uno de estos dos métodos para modificar un archivo de configuración:
* Método 1: modificar el archivo directamente en el clúster en el que se ejecuta el agente. Para obtener más información, consulte [Edición de la configuración del agente de Sysdig de Kubernetes mediante kubectl edit](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1).
* Método 2: modificar el archivo localmente y aplicar los cambios en el clúster. Para obtener más información, consulte [Edición de la configuración del agente de Sysdig de Kubernetes mediante kubectl apply](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2).

Puede añadir etiquetas a los datos que recopila el agente. 
* Utilice estas etiquetas como ayuda para gestionar los datos que supervisa. 

    * Utilice etiquetas para agrupar recursos de la infraestructura en jerarquías lógicas, filtrar datos y dividir en segmentos datos agregados. 
    
    * Personalice la forma en que se agregan los datos cuando se configura un gráfico o se crea una alerta para una métrica. 
    
    * Defina el ámbito de un panel de control, un panel o una alerta para filtrar puntos de datos. 
    
    * Restrinja el acceso a los datos gestionando el acceso a los datos de los usuarios mediante equipos. 
    
    * Para obtener más información sobre cómo gestionar los datos, consulte [Gestión de datos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

* Para obtener información sobre cómo añadir etiquetas, consulte [Adición de más etiquetas a los datos recopilados de un agente de Sysdig de Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags). 


**Puede personalizar los datos que recopila el agente de Sysdig.** 

Cuando excluya sucesos, métricas y contenedores, tenga en cuenta la información siguiente:
* Puede reducir la carga del agente y del programa de fondo.
* Solo se recopilan datos de los contenedores que desea supervisar.
* Puede controlar los costes informando sobre contenedores importantes y filtrando los contenedores innecesarios o no críticos.
* Puede configurar los sucesos de Kubernetes que desea supervisar. Para obtener más información, consulte [Recopilación de un conjunto de sucesos de Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events).

En la lista siguiente se indican las acciones que puede realizar para controlar los datos recopilados por el agente de Sysdig:
* [Inhabilitación de la recopilación de sucesos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [Inclusión y exclusión de métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [Filtrado de objetos de kubernetes y contenedores de los que se recopilan los datos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [Bloqueo de puertos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [Filtrado de sucesos de Kubernetes por gravedad](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

También puede personalizar el tipo de registro y las entradas que se recopilan. Para obtener más información, consulte [Cambio del nivel de registro](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level).

También puede registrar la lista de métricas para las que el agente notifica datos. Para obtener más información, consulte [Registro en un archivo de las métricas que se incluyen o se excluyen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics).

El agente de Sysdig genera entradas de registro en */opt/draios/logs/draios.log*. 
* El archivo de registro rota cuando alcanza los 10 MB de tamaño.
* Se conservan los 10 archivos de registro más recientes. La indicación de fecha y fecha que se añade al nombre de archivo se utiliza para determinar qué archivos se deben conservar.
* Los niveles de registro válidos son: *none*, *error*, *warning*, *info*, *debug* y *trace*
* El nivel de registro predeterminado es *info*, donde se crea una entrada para cada transmisión de métricas agregada a los servidores de fondo, una vez por segundo, además de las entradas correspondientes a avisos y errores.

En la tabla siguiente se muestran algunos casos de ejemplo comunes y el valor que debe establecer en cada uno de ellos:

| Casos de uso                                     | Entrada en la sección log           |
|-----------------------------------------------|-----------------------------|
| Resolución de problemas del comportamiento del agente                   | `file_priority: debug`      |
| Reducción de la salida de la consola del contenedor               | `console_priority: warning` |
| Filtrado de sucesos según su gravedad                  | `event_priority: warning`   |
| Verificación de las métricas que se incluyen o se excluyen  | `metrics_excess_log: true`  |

## Agente de Sysdig de contenedor
{: #container}


En la lista siguiente se indican las acciones que puede realizar para controlar los datos recopilados por el agente de Sysdig:
* [Inhabilitación de la recopilación de sucesos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [Inclusión y exclusión de métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [Filtrado de contenedores de los que se recopilan datos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [Bloqueo de puertos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [Filtrado de sucesos según su gravedad](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

También puede personalizar el tipo de registro y las entradas que se recopilan. Para obtener más información, consulte [Cambio del nivel de registro](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level).



## Agente de Sysdig de Linux
{: #linux}

El agente de Sysdig de Linux utiliza dos archivos de configuración que especifican los datos que se deben recopilar automáticamente:

| Archivo                   | Descripción                                                     | Ubicación                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Archivo de configuración principal </br>**Nota:****No edite este archivo.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Archivo de configuración que edita para personalizar el agente de Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabla 1. Archivos de configuración del agente de Sysdig" caption-side="top"} 

Puede editar el archivo *dragent.yaml* para personalizar los datos que se recopilan. Los cambios entran en vigor inmediatamente después de guardar el archivo. El agente detecta el cambio y se reinicia automáticamente. Encontrará la frecuencia y los archivos que un agente de Sysdig comprueba en el archivo *dragent.default.yaml*. Para obtener más información, consulte [Edición del archivo yaml de dragent](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent).

Por ejemplo, un archivo *dragent.default.yaml* incluye la siguiente información:

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

En la lista siguiente se indican las acciones que puede realizar para controlar los datos recopilados por el agente de Sysdig:
* [Inclusión y exclusión de métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [Bloqueo de puertos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

También puede personalizar el tipo de registro y las entradas que se recopilan. Para obtener más información, consulte [Cambio del nivel de registro](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level).


