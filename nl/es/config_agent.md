---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

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

# Configuración de un agente de Sysdig
{: #config_agent}

Después de suministrar una instancia del servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.cloud_notm}}, debe configurar un agente de Sysdig en cada entorno que desee supervisar. El agente de Sysdig recopila e informa de forma automática sobre métricas predefinidas. Puede configurar las métricas que se deben supervisar en cada entorno.
{:shortdesc}

Puede asociar una o varias etiquetas al agente de Sysdig. Las etiquetas son valores separados por comas con el formato **NOMBRE_ETIQUETA:VALOR_ETIQUETA**. Cuando supervise el entorno, puede utilizar estas etiquetas para identificar las métricas que están disponibles en un agente. Por ejemplo, puede incluir información sobre el nombre y la ubicación del servicio con todas las métricas recopiladas por este agente.
{: tip}

## Configuración de un agente de Sysdig en Linux
{: #config_agent_linux}

Siga los pasos siguientes para configurar un agente de Sysdig en Linux para que recopile y reenvíe métricas a una instancia del servicio {{site.data.keyword.mon_full_notm}}:

1. Obtenga la clave de acceso de Sysdig. Para obtener más información, consulte [Obtención de la clave de acceso mediante la IU de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenga el URL de ingestión. Para obtener más información, consulte [Puntos finales del recopilador de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Despliegue el agente de Sysdig. Ejecute el mandato siguiente desde un terminal.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Donde

    * SYSDIG_ACCESS_KEY es la clave de ingestión para la instancia.

    * COLLECTOR_ENDPOINT es el URL de ingestión para la región en la que está disponible la instancia de supervisión.

    * TAG_DATA son etiquetas separadas por comas con el formato *NOMBRE_ETIQUETA_VALOR:ETIQUETA*. Puede asociar una o varias etiquetas al agente de Sysdig. Por ejemplo: *role:serviceX,location:us-south*. 

    * Establezca **sysdig_capture_enabled** en *false* para inhabilitar la característica de captura de Sysdig. De forma predeterminada, está establecido en *true*. Para obtener más información, consulte [Cómo trabajar con capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    * Establezca **secure** en *true* para utilizar SSL con la comunicación.

Si se produce un error al instalar el agente de Sysdig, instale las cabeceras de kernel manualmente. Seleccione una distribución y ejecute el mandato para dicha distribución. A continuación, intente de nuevo realizar un despliegue del agente de Sysdig.

* **Para las distribuciones de Linux Debian y Ubuntu**, ejecute el mandato siguiente:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **Para las distribuciones de Linux RHEL, CentOS y Fedora**, ejecute el siguiente mandato:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Configuración de un agente de Sysdig en un contenedor Docker
{: #config_agent_docker}

Siga los pasos siguientes para configurar un agente de Sysdig en un contenedor Docker para que recopile y reenvíe métricas a una instancia del servicio {{site.data.keyword.mon_full_notm}}:

1. Obtenga la clave de acceso de Sysdig. Para obtener más información, consulte [Obtención de la clave de acceso mediante la IU de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenga el URL de ingestión. Para obtener más información, consulte [Puntos finales del recopilador de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Despliegue el agente de Sysdig. Ejecute el mandato siguiente:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    donde

    * SYSDIG_ACCESS_KEY es la clave de ingestión para la instancia.

    * COLLECTOR_ENDPOINT es el URL de ingestión para la región en la que está disponible la instancia de supervisión.

    * TAG_DATA son etiquetas separadas por comas con el formato *NOMBRE_ETIQUETA_VALOR:ETIQUETA*. Puede asociar una o varias etiquetas al agente de Sysdig. Por ejemplo: *role:serviceX,location:us-south*. 

    * Establezca **sysdig_capture_enabled** en *false* para inhabilitar la característica de captura de Sysdig. De forma predeterminada, está establecido en *true*. Para obtener más información, consulte [Cómo trabajar con capturas](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    * Establezca **SECURE** en *true* para utilizar SSL con la comunicación.

    **Nota:** el contenedor se ejecuta en modalidad desconectada. Para ver la salida del contenedor, elimine *-d*.




## Configuración de un agente de Sysdig en un clúster de Kubernetes mediante un script
{: #config_agent_kube_script}

Siga los pasos siguientes para configurar un agente de Sysdig en un clúster de Kubernetes que se ejecuta en {{site.data.keyword.containerlong_notm}}:

1. Obtenga la clave de acceso de Sysdig. Para obtener más información, consulte [Obtención de la clave de acceso mediante la IU de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenga el URL de ingestión. Para obtener más información, consulte [Puntos finales del recopilador de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

4. Despliegue el agente de Sysdig. Ejecute el mandato siguiente:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    donde

    * SYSDIG_ACCESS_KEY es la clave de ingestión para la instancia.

    * COLLECTOR_ENDPOINT es el URL de ingestión para la región en la que está disponible la instancia de supervisión.

    * TAG_DATA son etiquetas separadas por comas con el formato *NOMBRE_ETIQUETA_VALOR:ETIQUETA*. Puede asociar una o varias etiquetas al agente de Sysdig. Por ejemplo: *role:serviceX,location:us-south*. 

    * Establezca **sysdig_capture_enabled** en *false* para inhabilitar la característica de captura de Sysdig. De forma predeterminada, está establecido en *true*. Para obtener más información, consulte [Cómo trabajar con capturas](/docs/services/Monitoring-with-Sysdig/captures.html#captures).



## Configuración manual de un agente de Sysdig en un clúster de Kubernetes
{: #config_agent_kube_manually}

Siga los pasos siguientes para configurar un agente de Sysdig en un clúster de Kubernetes que se ejecuta en {{site.data.keyword.containerlong_notm}}:

1. Obtenga la clave de acceso de Sysdig. Para obtener más información, consulte [Obtención de la clave de acceso mediante la IU de {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenga el URL de ingestión. Para obtener más información, consulte [Puntos finales del recopilador de Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

4. Cree una cuenta de servicio denominada **sysdig-agent** para supervisar el clúster de kubernetes. Ejecute el mandato siguiente:

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Añada un secreto a su clúster de Kubernetes. Ejecute el mandato siguiente:

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY es la clave de ingestión para la instancia.

    El secreto de Kubernetes contiene la clave de ingestión que se utiliza para autenticar el agente de Sysdig con el servicio {{site.data.keyword.mon_full_notm}}. Se utiliza para abrir un socket web seguro en el servidor de ingestión en el sistema de fondo de supervisión.

6. Cree un rol de clúster y un enlace de rol de clúster. 

    Descargue el archivo [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml).
    
    Para añadir un rol de clúster, ejecute el mandato siguiente:
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    Para añadir un enlace de rol de clúster, ejecute el mandato siguiente:

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. Edite el archivo **sysdig-agent-configmap.yaml** y añada los parámetros necesarios para configurar el agente para que funcione en {{site.data.keyword.cloud_notm}}.

    Descargue el archivo [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml).

    Utilice un editor para abrir el archivo sysdig-agent-configmap.yaml. A continuación, añada los parámetros siguientes:

    * **k8s_cluster_name**: este parámetro especifica el nombre del clúster como una etiqueta de métrica. Puede utilizar la etiqueta *kubernetes.cluster.name* para navegar por los paneles de control de Kubernetes por nombre de clúster y filtrar las métricas asociadas con el clúster.

    * **collector**: este parámetro especifica el URL de ingestión para la región en la que está disponible la instancia de supervisión. 

    * **collector_port**: este parámetro indica el puerto en el que escucha el recopilador. Su valor debe ser *6443*.
    
    * **ssl**: este parámetro se debe establecer en *true*.
    
    * **ssl_verfiy_certificate**: este parámetro se debe establecer en *true*.
    
    * **new_k8s**: este parámetro se debe establecer en *true* para capturar métricas de estado de kube.

    * **sysdig_capture_enabled**: este parámetro habilita o inhabilita la característica de captura de Sysdig. De forma predeterminada, está establecido en *true*. Para obtener más información, consulte [Cómo trabajar con capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    A continuación se muestra un archivo yaml de ejemplo:

    ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: ingest.us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

8. Aplique la correlación de configuración al clúster. Ejecute el mandato siguiente:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. Aplique el archivo daemonset para desplegar el agente de Sysdig en el clúster. Ejecute el mandato siguiente:

    Descargue el archivo [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml).

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




