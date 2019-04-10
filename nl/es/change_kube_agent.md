---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# Personalización de agentes de Sysdig de Kubernetes
{: #change_kube_agent}

En {{site.data.keyword.mon_full_notm}}, puede personalizar la configuración de un agente de Sysdig para establecer un nivel de registro, bloquear puertos, incluir o excluir datos de métricas, añadir o eliminar sucesos y filtrar contenedores. 
{:shortdesc}

Para personalizar un agente de Sysdig de Kubernetes, es posible que tenga que configurar secciones en cualquiera de los archivos siguientes:

| Nombre de archivo                        | Acciones       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modificar nivel de registro. |
| `sysdig-agent-configmap.yaml`    | Bloquear puertos. </br>Incluir o excluir datos de métricas. </br>Añadir o eliminar sucesos. </br>Filtre contenedores. |
{: caption="Tabla 1. Archivos de configuración del agente de Sysdig de Kubernetes" caption-side="top"} 

Para editar un agente de Sysdig de Kubernetes, es posible que tenga que editar el archivo *sysdig-agent-configmap.yaml*, el archivo *sysdig-agent-daemonset-v2.yaml* o ambos.
{: tip}

Puede utilizar uno de estos dos métodos para modificar un archivo de configuración:
* Método 1: modificar el archivo directamente en el clúster en el que se ejecuta el agente.
* Método 2: modificar el archivo localmente y aplicar los cambios en el clúster.

## Edición de la configuración del agente de Sysdig de Kubernetes mediante kubectl edit
{: #change_kube_agent_edit_kube_agent_method1}

Siga los pasos siguientes para editar una configuración de agente de Sysdig de Kubernetes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-configmap.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Realice los cambios. **Nota:** consulte las instrucciones del editor `vi` para obtener información sobre cómo realizar cambios.

    Guarde los cambios. Los cambios se aplican automáticamente. 

3. Edite el archivo *sysdig-agent-daemonset-v2.yaml*. 

    Ejecute el mandato siguiente: 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Realice los cambios. **Nota:** consulte las instrucciones del editor `vi` para obtener información sobre cómo realizar cambios.

    Guarde los cambios. Los cambios se aplican automáticamente.

## Edición de la configuración del agente de Sysdig de Kubernetes mediante kubectl apply
{: #change_kube_agent_edit_kube_agent_method2}

Utilice este método si tiene los archivos de yaml de configuración almacenados y gestionados en un sistema de control de origen.

Siga los pasos siguientes para editar una configuración de agente de Sysdig de Kubernetes:

1. Obtenga la copia más reciente de cada archivo del controlador de origen. 

    Para crear un archivo local con la configuración que se despliega en un clúster, también puede ejecutar el mandato:
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    o 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. Edite la configuración.

3. Aplique los cambios con los mandatos siguientes:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    o
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

Los agentes en ejecución adoptarán automáticamente la nueva configuración después de que Kubernetes envíe los cambios a todos los nodos del clúster.


## Adición de más etiquetas a los datos recopilados de un agente de Sysdig de Kubernetes
{: #change_kube_agent_add_tags}

Siga los pasos siguientes para añadir más etiquetas a una configuración de agente de Sysdig de Kubernetes que ya ha desplegado:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-configmap.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. **Nota:** consulte las instrucciones del editor `vi` para obtener información sobre cómo realizar cambios.

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. Guarde los cambios. 

Los cambios se aplican automáticamente. 

En el caso del ejemplo proporcionado, obtendría las etiquetas **agent.tag.cluster_version** y **agent.tag.region**. Las podría utilizar para definir alertas, personalizar ámbitos y más.



## Recopilación de un conjunto de sucesos de Kubernetes
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} da soporte a integraciones de sucesos con Kubernetes. Los agentes de Sysdig descubren automáticamente estos servicios y recopilan datos de sucesos de los mismos. Puede editar el archivo de configuración del agente para cambiar su comportamiento predeterminado e incluir o excluir datos de sucesos. 

De forma predeterminada, solo se recopila un conjunto limitado de sucesos. Para obtener más información sobre los sucesos que se recopilan de forma predeterminada, consulte [Sucesos de Kubernetes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}.

Para añadir o eliminar sucesos, debe personalizar el archivo *sysdig-agent-configmap.yaml* y especificar qué sucesos se deben incluir y cuáles se van a filtrar. **Nota:** una entrada en una sección de *sysdig-agent-configmap.yaml* prevalece sobre toda la sección de la configuración predeterminada.
{: tip}

Para filtrar los sucesos de las pods de Kubernetes, siga los pasos siguientes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-configmap.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *events* o actualice la sección.

    **Nota:** consulte las instrucciones del editor `vi` para obtener información sobre cómo realizar cambios.

    Por ejemplo, quizás desee recopilar los sucesos de extracción de pod de Kubernetes y filtrar otros sucesos de pod que se recopilan de forma predeterminada. Pero desea recopilar los sucesos predeterminados de Kubernetes para los nodos y replicationControllers.

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. Guarde los cambios. 

Los cambios se aplican automáticamente. 


Otro ejemplo en el que puede ver cómo recopilar un subconjunto de sucesos de Kubernetes: supongamos que solo desea supervisar los sucesos de extracción, los extraídos y los anómalos de los pods.

* Opción 1: defina la secuencia de entradas como una lista:

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* Opción 2: defina la secuencia de entradas en una sola línea entre corchetes:

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

Para obtener más información sobre cómo trabajar con sucesos personalizados, consulte [Cómo trabajar con sucesos personalizados ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


## Inhabilitación de la recopilación de sucesos
{: #change_kube_agent_disable_events}

Para hacer que un agente de Sysdig deje de recopilar sucesos de Kubernetes, debe modificar el archivo *sysdig-agent-configmap.yaml*. Establezca la entrada **Kubernetes** de la sección **events** en *none*. 

Siga los pasos siguientes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-configmap.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *events* o actualice la sección.

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. Guarde los cambios. 

Los cambios se aplican automáticamente. 






## Inclusión y exclusión de métricas
{: #change_kube_agent_inc_exc_metrics}

Para filtrar métricas personalizadas, debe personalizar la sección **metrics_filter** en el archivo *sysdig-agent-configmap.yaml*. Puede especificar las métricas que se deben incluir y las que se deben filtrar configurando los parámetros de filtro **include** y **exclude**.

<p class="important">El orden de la regla de filtrado se establece de la forma siguiente: se aplica la primera regla que coincide con una métrica. Las siguientes reglas para esa métrica se pasan por alto.</p>

Siga los pasos siguientes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-configmap.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *metrics_filter* o actualice la sección.

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

4. Guarde los cambios. 

Los cambios se aplican automáticamente. 




## Filtrado de objetos de kubernetes y contenedores de los que se recopilan los datos
{: #change_kube_agent_filter_data}

Un agente de Sysdig de Kubernetes recopila automáticamente métricas de *todos los contenedores* que detecta en un clúster, lo que incluye Prometheus, StatsD, JMX, comprobaciones de apps y métricas incorporadas.
 
Puede personalizar el agente de Sysdig para que excluya contenedores de la recopilación de métricas. 

Cuando excluya contenedores, tenga en cuenta la información siguiente:
* Se reduce la carga del agente y del programa de fondo.
* Solo se recopilan datos de los contenedores que desea supervisar.
* Puede controlar los costes informando sobre contenedores importantes y filtrando los contenedores innecesarios o no críticos.

Para habilitar la característica en la que un agente de Sysdig filtra contenedores, debe personalizar el archivo *sysdig-agent-configmap.yaml*. Establezca la entrada **use_container_filter** de la sección **containers** en *true*. **Nota:** de forma predeterminada, esta característica está desactivada. A continuación, defina las reglas que incluyan una o varias condiciones y que desee aplicar.

En la tabla siguiente se describen los parámetros que puede definir para establecer las reglas de filtrado en un clúster:

| Parámetro                          | Condición                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | Nombre de imagen de contenedor                           |
| `container.name`                   | Nombre de contenedor                                 |
| `container.label.*`                | Etiqueta de contenedor                                |
| `kubernetes.object.*`             | Objeto de Kubernetes. Un objeto puede ser un pod, un espacio de nombres, etc.   |
| `kubernetes.object.annotation.*`  | Anotación de objeto de Kubernetes                   |
| `kubernetes.object.label.*`       | Etiqueta de objeto de Kubernetes                        |
| `all`                              | Regla predeterminada para especificar todos los objetos            |
{: caption="Tabla 2. Parámetros para definir condiciones en contenedores" caption-side="top"} 

Tenga en cuenta la información siguiente sobre cómo el agente de Sysdig aplica las reglas que defina en la sección **container_filter**:
* Las condiciones se definen configurándolas con los parámetros de filtro **include** y **exclude**. 
* La primera regla coincidente de la lista determina si el contenedor se incluye o se excluye.
* Las condiciones constan de un nombre de clave y un valor. Si la clave especificada para un contenedor coincide con el valor, la regla se aplica.
* Cuando una regla contiene varias condiciones, deben coincidir `todas las condiciones` para que la regla se aplique.

Siga los pasos siguientes para filtrar los contenedores que un agente de Sysdig supervisa en un clúster:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-configmap.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *metrics_filter* o actualice la sección.

    Por ejemplo, consulte el siguiente extracto de una correlación de configuración:

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. Guarde los cambios. 

Los cambios se aplican automáticamente. 


## Bloqueo de puertos
{: #change_kube_agent_block_ports}

Para bloquear el tráfico de red y las métricas procedentes de los puertos de red, debe personalizar la sección **blacklisted_ports** en el archivo *sysdig-agent-configmap.yaml*. Debe obtener una lista de los puertos de los que desea filtrar los datos.

**Nota:** el puerto 53 (DNS) siempre está en la lista negra. 

Siga los pasos siguientes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-configmap.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *metrics_filter* o actualice la sección.

    Por ejemplo, en el ejemplo siguiente se muestra cómo establecer la sección *blacklisted_ports* de un agente de Sysdig para excluir datos procedentes de los puertos 6666 y 6379:

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. Guarde los cambios. 

Los cambios se aplican automáticamente. 



## Cambio del nivel de registro
{: #change_kube_agent_log_level}

Para configurar el nivel de registro, debe personalizar la sección **log** del archivo *sysdig-agent-daemonset-v2.yaml*. 

El agente de Sysdig genera entradas de registro en */opt/draios/logs/draios.log*. 
* El archivo de registro rota cuando alcanza los 10 MB de tamaño.
* Se conservan los 10 archivos de registro más recientes. La indicación de fecha y fecha que se añade al nombre de archivo se utiliza para determinar qué archivos se deben conservar.
* Los niveles de registro válidos son: *none*, *error*, *warning*, *info*, *debug* y *trace*
* El nivel de registro predeterminado es *info*, donde se crea una entrada para cada transmisión de métricas agregada a los servidores de fondo, una vez por segundo, además de las entradas correspondientes a avisos y errores.
* Puede personalizar el tipo de registro y las entradas que se recopilan configurando el archivo de configuración del agente de Sysdig **/opt/draios/etc/dragent.yaml**. Después de editar el archivo, debe reiniciar el agente en el shell con `service dragent restart` para activar los cambios.

En la tabla siguiente se muestran algunos casos de ejemplo comunes y el valor que debe establecer en cada uno de ellos:

| Casos de uso                                     | Entrada en la sección log           |
|-----------------------------------------------|-----------------------------|
| Resolución de problemas del comportamiento del agente                   | `file_priority: debug`      |
| Reducción de la salida de la consola del contenedor               | `console_priority: warning` |
| Filtrado de sucesos según su gravedad                  | `event_priority: warning`   |
| Verificación de las métricas que se incluyen o se excluyen  | `metrics_excess_log: true`  |
{: caption="Tabla 2. Entradas de la sección log" caption-side="top"} 

Siga los pasos siguientes para configurar el nivel de registro:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-daemonset-v2.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *log* o actualice la sección.

    Por ejemplo, para filtrar los sucesos de gravedad baja (*notice*, *information*, *debug*), debe establecer la entrada **metrics_excess_log** de la sección **log** en *true*:

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. Guarde los cambios. 

Los cambios se aplican automáticamente. 


## Filtrado de sucesos de Kubernetes por gravedad
{: #change_kube_agent_filterby_severity}

Para filtrar los sucesos por gravedad, debe modificar el archivo *sysdig-agent-daemonset-v2.yaml*. Establezca la entrada **event_priority** de la sección **log** en *none*. 

El nivel de registro predeterminado es **information**. Esto significa que solo se transmiten los sucesos de aviso y de gravedad superior.

Los valores válidos son: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* y *none*. **Nota**: los valores se muestran de prioridad más alta a prioridad más baja.

Siga los pasos siguientes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-daemonset-v2.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *log* o actualice la sección.

    Por ejemplo, para filtrar los sucesos de gravedad baja (*notice*, *informaton*, *debug*), debe establecer la sección log **event_priority** en *warning*:

    ```
    log:
      event_priority: warning
    ```
    {: codeblock}

6. Guarde los cambios. 

Los cambios se aplican automáticamente. 

## Registro en un archivo de las métricas que se incluyen o se excluyen
{: #change_kube_agent_log_metrics}

Para registrar en un archivo información sobre qué métricas personalizadas se incluyen y cuáles se excluyen, debe personalizar el archivo *sysdig-agent-daemonset-v2.yaml*. Establezca la entrada **metrics_excess_log** en **true**
en la sección **log**.

* El registro está desactivado de forma predeterminada. 
* El registro se produce en el nivel INFO cada 30 segundos y se prolonga durante 10 segundos. 
* El archivo de registro está disponible en */opt/draios/logs/draios.log*.
* Los datos de registro se formatean de la forma siguiente:

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* es un símbolo que indica si la métrica se incluye o se excluye. El signo más (*+*) indica que una métrica se incluye. El signo menos (*-*) indica que una métrica se excluye. 

    * *[type]* especifica el tipo de métrica, por ejemplo *statsd*.
    
    * *[metric included/excluded]* indica en una forma legible por el usuario si la métrica se incluye o se excluye.

    *  *metric.name* indica el nombre de la métrica.

    * *(filter: +/-[metric.filter])* proporciona información sobre los filtros definidos en la sección **metrics_filter** del archivo *sysdig-agent-daemonset-v2.yaml*.

A continuación se muestra un ejemplo:

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

Siga los pasos siguientes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Edite el archivo *sysdig-agent-daemonset-v2.yaml*. 

    Ejecute el mandato siguiente:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Realice los cambios. Añada la sección *log* o actualice la sección.

    Por ejemplo, para filtrar los sucesos de gravedad baja (*notice*, *information*, *debug*), debe establecer la entrada **metrics_excess_log** de la sección **log** en *true*:

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. Guarde los cambios. 

Los cambios se aplican automáticamente. 


## Archivo yaml de configmap de ejemplo
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: |
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:
      kubernetes:
        node:
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter:
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## Archivo yaml de daemonset de ejemplo
{: #change_kube_agent_sample_daemonset}

```
 Edite el objeto siguiente. Las líneas que empiezan por '#' se pasarán por alto,
# y un archivo vacío terminará la edición de forma anómala. Si se produce un error al guardar este archivo, # se volverá a abrir con los errores relevantes.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

