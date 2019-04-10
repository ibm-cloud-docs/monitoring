---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, delete agent

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

# Eliminación de un agente de Sysdig
{: #remove_agent}

Cuando suprima una instancia de {{site.data.keyword.mon_full_notm}}, o si desea detener la recopilación de métricas de un origen, debe desinstalar el agente de Sysdig.
{:shortdesc}


## Eliminación de un agente de Sysdig de un clúster de Kubernetes
{: #remove_agent_kube}

Siga los pasos siguientes para eliminar un agente de Sysdig de un clúster de Kubernetes:

1. Configure el entorno de clúster. Ejecute los mandatos siguientes:

    En primer lugar, obtenga el mandato para establecer la variable de entorno y descargar los archivos de configuración de Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Cuando termine la descarga de los archivos de configuración, se muestra un mandato que puede utilizar para establecer la vía de acceso al archivo de configuración de Kubernetes local como variable de entorno.

    A continuación, copie y pegue el mandato que se muestra en el terminal para definir la variable de entorno KUBECONFIG.

    **Nota:** cada vez que inicie una sesión en la CLI de {{site.data.keyword.containerlong}} para trabajar con clústeres, debe ejecutar estos mandatos para establecer la vía de acceso al archivo de configuración del clúster como una variable de sesión. La CLI de Kubernetes utiliza esta variable para buscar un archivo de configuración local y los certificados necesarios para conectar con el clúster en {{site.data.keyword.cloud_notm}}.

2. Elimine el enlace del rol del clúster. Ejecute el mandato siguiente:

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. Elimine la cuenta de servicio. Ejecute el mandato siguiente:

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. Elimine el daemonset. Ejecute el mandato siguiente:

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Elimine el secreto. Ejecute el mandato siguiente:

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Eliminación de un agente de Sysdig en Linux
{: #remove_agent_linux}

Siga los pasos siguientes para eliminar un agente de Sysdig en Linux:

* Para desinstalar el agente de las **distribuciones de Linux Debian y Ubuntu**, ejecute el mandato siguiente como usuario **sudo** desde un terminal:

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* Para desinstalar el agente de las **distribuciones de Linux RHEL, CentOS y Fedora**, ejecute el mandato siguiente como usuario **sudo** desde un terminal:

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


