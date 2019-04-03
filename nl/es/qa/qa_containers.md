---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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



# Preguntas frecuentes para la supervisión de clústeres Kubernetes
{: #qa_containers}

Aquí encontrará las respuestas a preguntas comunes sobre el servicio {{site.data.keyword.monitoringshort}} y el servicio {{site.data.keyword.containershort_notm}}. 
{:shortdesc}

* [La consulta de Grafana para mis contenedores no muestra datos o tiene errores](/docs/services/cloud-monitoring/qa/qa_containers.html#metric_format_change)
* [¿Cómo puedo configurar un entorno de clúster en mi sesión de terminal?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1)
* [¿Dónde puedo obtener el nombre de clúster y el ID de clúster?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa3)
* [¿Cómo puedo obtener la lista de espacios de nombre?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa7)
* [¿Cómo puedo obtener la lista de pods de un espacio de nombres en un clúster Kubernetes?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa8)
* [¿Cómo puedo obtener todos los pods de un clúster por espacio de nombres?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa9)

## La consulta de Grafana para mis contenedores no muestra datos o tiene errores
{: #metric_format_change}

El formato de la consulta que puede definir para un contenedor ha cambiado.

El formato siguiente está en desuso: 

```
{Prefijo}.{Versión}.{Proveedor}.{Tipo}.{NombreServicio}.{Región}.{Cuenta}.{Clúster}.{Métrica}.{Contenedor en un pod}.{Funciones}
```
{: screen}

Los nuevos formatos que son válidos son los siguientes:

* [Formato de consulta de métricas de CPU para un contenedor](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers)
* [Formato de consulta de métricas de carga para un trabajador](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers)
* [Formato de consulta de métricas de memoria para un contenedor](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)

Migre sus consultas antiguas al formato nuevo para visualizar sus datos en Grafana.

Por ejemplo, si la consulta comienza como `crn.v1.bluemix.public.containers-kubernetes.us-south.`, debe migrar la consulta al formato nuevo, es decir, a `ibmcloud.public.containers-kubernetes.us-south`.

La tabla siguiente lista los campos en el formato que se ha quedado en desuso:

 <table>
      <caption>Tabla 1. Campos de consulta de Grafana para contenedores</caption>
      <tr>
        <th align="center">Campo</th>
        <th align="center">Descripción</th>
        <th align="center">Valores válidos</th>
      </tr>
      <tr>
        <td>Prefijo</td>
        <td>Prefijo que se utiliza para indicar que es un recurso de {{site.data.keyword.IBM_notm}} Cloud.</td>
        <td>`crn`</td>
      </tr>
      <tr>
        <td>Versión</td>
        <td>Versión que indica el formado y campos de los datos de métrica recopilados. </td>
        <td>`v1`</td>
      </tr>
      <tr>
        <td>Proveedor</td>
        <td>Proveedor de la nube en la que se han recopilado los datos. Este campo es un identificador alfanumérico.</td>
        <td>Para {{site.data.keyword.IBM_notm}} Cloud público, el valor es: `bluemix`</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>Entorno de nube en la que se han recopilado los datos.</td>
        <td>Para {{site.data.keyword.IBM_notm}} Cloud público, es valor es: `public`</td>
      </tr>
      <tr>
        <td>Nombre de servicio</td>
        <td>Infraestructura de nube en la que se han recopilado las métricas.</td>
        <td>Para el servicio {{site.data.keyword.monitoringshort}}, el valor es: `containers-kubernetes`</td>
      </tr>
      <tr>
        <td>Región</td>
        <td>Región de nube en la que se han recopilado las métricas.</td>
        <td>Para la región EE.UU. sur, el valor es: `ng` <br>Para la región Reino Unido, el valor es: `eu-gb` <br>Para Alemania, el valor es: `eu-de` <br>Para Sídney, el valor es: `au-syd` </td>
      </tr>
      <tr>
        <td>Cuenta</td>
        <td>GUID de la cuenta en la que se han recopilado las métricas. <br>El formato de este campo es el siguiente: `a_ID` donde ID es el GUID de la cuenta. <br>Para obtener el GUID de la cuenta, consulte [¿Cómo se obtiene el GUID de una cuenta?](/docs/services/cloud-monitoring/qa/cli_qa.html#account_guid).</td>
        <td>a_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Clúster</td>
        <td>GUID del clúster en el que se han recopilado las métricas.</td>
        <td>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Métrica</td>
        <td>La métrica recopilada automáticamente para un contenedor.</td>
        <td>Para obtener una lista de las métricas de CPU, consulte [Métricas de CPU para contenedores](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#cpu_metrics_containers) <br>Para obtener una lista de métricas de memoria, consulte [Métricas de memoria](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics) </td>
      </tr>
      <tr>
        <td>Contenedor en un pod</td>
        <td>Combinación de nombres de recurso de Kubernetes y GUID necesarios para identificar de forma exclusiva un contenedor que se ejecuta en un pod. <br>**Nota:** Cuando examine la lista de opciones disponibles para esta entrada de la consulta, observe que también hay una entrada con el formato siguiente: {espacionombres}{nombre_pod}{nombre_nombredespliegue}_POD{ID_contenedor}. Estas entradas corresponden a los ID internos de contenedor que crea Kubernetes.</td>
		<td>{espacionombres}_{nombre_pod}_{nombre_despliegue}_{id_contenedor}</td>
      </tr>
      <tr>
        <td>Funciones</td>
        <td>Funciones de consulta que puede seleccionar para visualizar una métrica de contenedor en el panel. <br>Para obtener más información, consulte [Funciones ![(Icono de enlace externo)](../../icons/launch-glyph.svg "Icono de enlace externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
        <td></td>
      </tr>
    </table>


## ¿Cómo puedo configurar un entorno de clúster en mi sesión de terminal?
{: #qa1}

Debe establecer el contexto de un clúster Kubernetes para gestionarlo mediante mandatos.

**Nota:** Para gestionar un clúster, necesita una política de IAM para el servicio {{site.data.keyword.containershort_notm}} asignado a su usuario con permisos para completar la tarea.

Siga estos pasos para configurar el contexto de un clúster:

1. Inicie la sesión en la región, organización y espacio en {{site.data.keyword.Bluemix_notm}} que están asociados al clúster que ha creado. Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Inicialice el plug-in del servicio {{site.data.keyword.containershort_notm}}. Ejecute el mandato siguiente:

	```
	ibmcloud cs init
	```
	{: codeblock}

3. Establezca el contexto del clúster en la sesión de terminal. Ejecute los mandatos siguientes:
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    El resultado de ejecutar este mandato muestra el mandato que debe ejecutar en el terminal para definir la vía de acceso a su archivo de configuración. Por ejemplo:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Copie y pegue el mandato para definir la variable de entorno en el terminal y luego pulse **Intro**.

 
 

## ¿Dónde puedo obtener el nombre de clúster y el ID de clúster?
{: #qa3}

Siga estos pasos para obtener el nombre de clúster y el ID mediante la IU:

1. Inicie sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}.

    El panel de control de {{site.data.keyword.Bluemix_notm}} se puede encontrar en: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}.
    
	Después de iniciar sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. Desde el *Panel de control* de {{site.data.keyword.Bluemix_notm}}, seleccione **Menú > Contenedores**.

    Se visualizará la lista de clústeres que están disponibles en la cuenta.

3. Para obtener el ID de clúster, seleccione una entrada de clúster. 

    Se abrirá la página de visión general. En esta página, puede obtener el ID de clúster.



Siga estos pasos para obtener el nombre y el ID de clúster mediante la línea de mandatos:

1. Inicie la sesión en la región, organización y espacio en {{site.data.keyword.Bluemix_notm}} que están asociados al clúster que ha creado. Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Liste los clústeres que están disponibles en la cuenta. Ejecute el mandato siguiente: 

    ```
	ibmcloud cs clusters
	``` 
	{: codeblock}
	
	La salida de este mandato lista todos los clústeres en la cuenta con su ID correspondientes.
	
3. Para obtener el ID de clúster, ejecute el mandato siguiente:

    ```
	ibmcloud cs cluster-get my_cluster
	```
    {: screen}	
 


## ¿Cómo puedo obtener la lista de espacios de nombres?
{: #qa7}

Para obtener una lista de todos los espacios de nombres en el clúster, siga estos pasos:

Realice los siguientes pasos:

1. Configure el contexto de clúster. Para obtener más información, consulte [¿Cómo puedo configurar un entorno de clúster en mi sesión de terminal?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Liste todos los espacios de nombres. Ejecute el mandato kubectl siguiente:

    ```
    kubectl get namespaces
	```
	{: codeblock}

## ¿Cómo puedo obtener la lista de pods por espacio de nombres en un clúster Kubernetes?
{: #qa8}
		
Para obtener la lista de los pods de un espacio de nombres, siga estos pasos:

1. Configure el contexto de clúster. Para obtener más información, consulte [¿Cómo puedo configurar un entorno de clúster en mi sesión de terminal?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Para obtener la lista de los pods por espacio de nombres en un clúster Kubernetes, ejecute el mandato siguiente:

    ```
	kubectl --namespace=NamespaceName get pods 
	```
	{: codeblock}
	
	donde Namespacename es el nombre del espacio de nombres, por ejemplo, *default*.

## ¿Cómo puedo obtener todos los pods de un clúster por espacio de nombres?
{: #qa9}
		
Realice los siguientes pasos:

1. Configure el contexto de clúster. Para obtener más información, consulte [¿Cómo puedo configurar un entorno de clúster en mi sesión de terminal?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).
	
2. Para obtener todos los pods de un clúster por espacio de nombres, ejecute el mandato siguiente:

	```
	kubectl get pods --all-namespaces
	```
	{: codeblock}
		


