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


# {{site.data.keyword.containershort_notm}}
{: #metrics_format_containers}

Las consultas que defina en Grafana para supervisar el servicio {{site.data.keyword.containershort_notm}} siguen el patrón siguiente: 
{:shortdesc}



## Formato de consulta para métricas de CPU recopiladas para contenedores
{: #cpu_containers}

El formato de una consulta que defina en Grafana para supervisar una métrica de CPU para un contenedor que se ejecuta en el servicio {{site.data.keyword.containershort_notm}} se describe de la siguiente manera: 

```
{Origen}.{Tipo de nube}.{Nombre de servicio}.{Región}.{Nombre de clúster}.{Espacio de nombres}.{Origen de métrica}.{Nombre de pod}.{Nombre de contenedor}.{Tipo de métrica}.{Subtipo de métrica}.[Funciones]
```
{: codeblock}  

donde

<table>
  <caption>Campos necesarios para definir una métrica de CPU para un contenedor </caption>
  <tr>
    <th>Campo</th>
	  <th>Descripción</th>
	  <th>Valor</th>
  </tr>
  <tr>
    <td>Origen</td>
	  <td>Este es un nombre reservado. Las métricas bajo esta jerarquía proceden de aplicaciones y servicios de {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo de nube</td>
	  <td>Indica el tipo de nube. </td>
	  <td>Para la nube pública de {{site.data.keyword.Bluemix_notm}}, el valor es: *public*</td>
  </tr>
  <tr>
    <td>Nombre de servicio</td>
	  <td>Define el nombre del servicio en {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Para las apps de CF, el valor es: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Región</td>
	  <td>Define la región donde se está ejecutando el contenedor.</td>
	  <td>Para la región EE.UU. sur, el valor es: *us-south* <br>Para la región Reino Unido, el valor es: *united-kingdom*  <br>Para Alemania, el valor es: *frankfurt* <br>Para Sídney, el valor es: *sydney* </td>
  </tr>
  <tr>
    <td>Nombre de clúster</td>
	  <td>Nombre del clúster a supervisar.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Origen de métrica</td>
	  <td>Origen de los datos.</td>
	  <td>*contenedor* </td>
  </tr>
  <tr>
    <td>Espacio de nombres</td>
	<td>Espacio de nombres donde se despliega el contenedor en un clúster de Kubernetes.</td>
	<td></td>
  </tr>
   <tr>
    <td>Nombre de pod</td>
	<td>Nombre del pod.</td>
	<td></td>
  </tr>
  <tr>
    <td>Nombre de contenedor</td>
	<td>Nombre del contenedor.</td>
	<td></td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
	  <td>Tipo de métrica.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	  <td>Métrica que se visualizará.</td>
	  <td>*uso*, *num-núcleos*, *uso-pct*, *uso-contenedor-pct-solicitado*</td>
  </tr>
  <tr>
    <td>Funciones</td>
    <td>Funciones de consulta que puede seleccionar para visualizar una métrica de contenedor en el panel. </td>
    <td>[Funciones ![(Icono de enlace externo)](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Por ejemplo, una consulta para supervisar el uso de CPU para un contenedor que se ejecuta en un clúster de Kubernetes en la región EE.UU. sur se define de la forma siguiente:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## Formato de consulta para métricas de carga recopiladas para trabajadores
{: #load_workers}

El formato de una consulta que defina en Grafana para supervisar una métrica de carga para un trabajador que se ejecuta en el servicio {{site.data.keyword.containershort_notm}} se describe de la forma siguiente: 

```
{Origen}.{Tipo de nube}.{Nombre de servicio}.{Región}.{Nombre de clúster}.{Origen de métrica}.{Nombre del trabajador}.{Tipo de métrica}.{Subtipo de métrica}.[Funciones]
```
{: codeblock}  

donde

<table>
  <caption>Campos necesarios para definir una métrica de carga para un trabajador </caption>
  <tr>
    <th>Campo</th>
	<th>Descripción</th>
	<th>Valor</th>
  </tr>
  <tr>
    <td>Origen</td>
	  <td>Este es un nombre reservado. Las métricas bajo esta jerarquía proceden de aplicaciones y servicios de {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo de nube</td>
	  <td>Indica el tipo de nube. </td>
	  <td>Para la nube pública de {{site.data.keyword.Bluemix_notm}}, el valor es: *public*</td>
  </tr>
  <tr>
    <td>Nombre de servicio</td>
	  <td>Define el nombre del servicio en {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Para las apps de CF, el valor es: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Región</td>
	  <td>Define la región donde se está ejecutando el contenedor.</td>
	  <td>Para la región EE.UU. sur, el valor es: *us-south* <br>Para la región Reino Unido, el valor es: *united-kingdom*  <br>Para Alemania, el valor es: *frankfurt* <br>Para Sídney, el valor es: *sydney* </td>
  </tr>
  <tr>
    <td>Nombre de clúster</td>
	<td>Nombre del clúster a supervisar.</td>
	<td></td>
  </tr>
  <tr>
    <td>Origen de métrica</td>
	<td>Origen de los datos.</td>
	<td>*trabajador* </td>
  </tr>
   <tr>
    <td>Nombre del trabajador</td>
	<td>Nombre del trabajador.</td>
	<td></td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
	<td>Tipo de métrica.</td>
	<td>*carga*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	  <td>Métrica que se visualizará.</td>
	  <td>*avg-1*, *avg-5*, *avg-15*</td>
  </tr>
  <tr>
    <td>Funciones</td>
    <td>Funciones de consulta que puede seleccionar para visualizar una métrica de contenedor en el panel. </td>
    <td>[Funciones ![(Icono de enlace externo)](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Por ejemplo, una consulta para supervisar el uso de CPU para un trabajador que se ejecuta en un clúster de Kubernetes en la región EE.UU. sur se define de la forma siguiente:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## Formato de consulta para métricas de memoria recopiladas para contenedores
{: #mem_containers}

El formato de una consulta que defina en Grafana para supervisar una métrica de memoria para un contenedor que se ejecuta en el servicio {{site.data.keyword.containershort_notm}} se describe de la siguiente manera: 

```
{Origen}.{Tipo de nube}.{Nombre de servicio}.{Región}.{Nombre de clúster}.{Espacio de nombres}.{Origen de métrica}.{Nombre de pod}.{Nombre de contenedor}.{Tipo de métrica}.{Subtipo de métrica}.[Funciones]
```
{: codeblock}  

donde

<table>
  <caption>Campos necesarios para definir una métrica de memoria para un contenedor</caption>
  <tr>
    <th>Campo</th>
	<th>Descripción</th>
	<th>Valor</th>
  </tr>
  <tr>
    <td>Origen</td>
	  <td>Este es un nombre reservado. Las métricas bajo esta jerarquía proceden de aplicaciones y servicios de {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Tipo de nube</td>
	  <td>Indica el tipo de nube. </td>
	  <td>Para la nube pública de {{site.data.keyword.Bluemix_notm}}, el valor es: *public*</td>
  </tr>
  <tr>
    <td>Nombre de servicio</td>
	  <td>Define el nombre del servicio en {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Para las apps de CF, el valor es: *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Región</td>
	  <td>Define la región donde se está ejecutando el contenedor.</td>
	  <td>Para la región EE.UU. sur, el valor es: *us-south* <br>Para la región Reino Unido, el valor es: *united-kingdom*  <br>Para Alemania, el valor es: *frankfurt* <br>Para Sídney, el valor es: *sydney* </td>
  </tr>
  <tr>
    <td>Nombre de clúster</td>
	<td>Nombre del clúster a supervisar.</td>
	<td></td>
  </tr>
  <tr>
    <td>Origen de métrica</td>
	<td>Origen de los datos.</td>
	<td>*contenedor* </td>
  </tr>
  <tr>
    <td>Espacio de nombres</td>
	<td>Espacio de nombres donde se despliega el contenedor en un clúster de Kubernetes.</td>
	<td></td>
  </tr>
   <tr>
    <td>Nombre de pod</td>
	<td>Nombre del pod.</td>
	<td></td>
  </tr>
  <tr>
    <td>Nombre de contenedor</td>
	  <td>Nombre del contenedor.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
  	<td>Tipo de métrica.</td>
  	<td>*memoria*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	  <td>Métrica que se visualizará.</td>
	  <td>*límite*, *actual*, *uso-pct*</td>
  </tr>
  <tr>
    <td>Funciones</td>
    <td>Funciones de consulta que puede seleccionar para visualizar una métrica de contenedor en el panel. </td>
    <td>[Funciones ![(Icono de enlace externo)](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Por ejemplo, una consulta para supervisar el uso de memoria para un contenedor que se ejecuta en un clúster de Kubernetes en la región EE.UU. sur se define de la forma siguiente:

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
