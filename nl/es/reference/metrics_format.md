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


# Formato general
{: #metrics_format}

Las consultas que define en Grafana para supervisar el servicio {{site.data.keyword.Bluemix}} deben cumplir con el formato siguiente: 
{:shortdesc}

```
{Origen}.{Tipo de nube}.{Nombre de servicio}.{Región }.[campos de servicio].{Tipo de métrica}.{Subtipo de métrica}.[Funciones]
```
{: codeblock}

donde [campos de servicio] representa los campos específicos de la consulta de métrica de un servicio o app de CF. 

<table>
  <caption>Campos comunes en una consulta</caption>
  <tr>
    <th>Campo</th>
	<th>Descripción</th>
	<th>Valor</th>
  </tr>
  <tr>
    <td>Origen</td>
	<td>Este es un nombre reservado. Las métricas bajo esta jerarquía proceden de servicios de {{site.data.keyword.Bluemix_notm}}.</td>
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
	  <td>Para {{site.data.keyword.containershort}}, el valor es: *containers-kubernetes*</td>
  </tr>
  <tr>
    <td>Región</td>
	  <td>Define la región donde se está ejecutando el contenedor.</td>
	  <td>Para la región EE.UU. sur, el valor es: *us-south* <br>Para la región Reino Unido, el valor es: *united-kingdom*  <br>Para Alemania, el valor es: *frankfurt* <br>Para Sídney, el valor es: *sydney* </td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
	<td>Tipo de métrica.</td>
	<td>*cpu* <br>*carga* <br>*memoria*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	<td>Subtipo de la métrica.</td>
	<td>Por ejemplo: *uso*, *num-núcleos*, *uso-pct*, *uso-contenedor-pct-solicitado*</td>
  </tr>
  <tr>
    <td>Funciones</td>
    <td>Funciones de consulta que puede seleccionar para visualizar una métrica de contenedor en el panel. </td>
    <td>[Funciones ![(Icono de enlace externo)](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




