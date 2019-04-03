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


# Apps CF
{: #cfapps_metrics_format}

Las consultas que defina en Grafana para supervisar una aplicación de Cloud Foundry que se ejecuta en {{site.data.keyword.Bluemix}} Public debe cumplir con el formato siguiente: 
{:shortdesc}

```
{Origen}.{Tipo de nube}.{Nombre de servicio}.{Región}.{Nombre de CFapp}.{Índice de CFapp}.{Contenedor de CFapp}.{Tipo de métrica}.{Subtipo de métrica}.[Funciones]
```
{: codeblock}

donde

<table>
  <caption>Campos comunes en una consulta</caption>
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
	<td>Define la región donde está en ejecución la instancia de la app de CF.</td>
	<td>Para la región EE.UU. sur, el valor es: *us-south* <br>Para la región Reino Unido, el valor es: *eu-gb*  <br>Para Alemania, el valor es: *eu-de* <br>Para Sídney, el valor es: *au-syd* </td>
  </tr>
  <tr>
    <td>Nombre de CFapp</td>
	<td>Nombre de la aplicación de CF.</td>
	<td></td>
  </tr>
  <tr>
    <td>Índice de CFapp</td>
	  <td>Índice de la instancia de aplicación de CF.</td>
	  <td>Por ejemplo: *0* </br>Si tiene una app de CF con una instancia, solo habrá un índice 0. Si escala la app de CF, por ejemplo a 10 instancias, tiene de 0 a 9 como valores de índice.</td>
  </tr>
  <tr>
    <td>Contenedor de CFapp</td>
	  <td>Valor fijo.</td>
	  <td>*contenedor*</td>
  </tr>
  <tr>
    <td>Tipo de métrica</td>
	  <td>Tipo de métrica. Disco, memoria y CPU son series de métricas recopiladas automáticamente.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Subtipo de métrica</td>
	  <td>Métrica que se visualizará. </br>[Métricas de CPU](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Métricas de disco](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[Métricas de memoria](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>Funciones</td>
    <td>Funciones de consulta que puede seleccionar para visualizar una métrica de contenedor en el panel. </td>
    <td>[Funciones ![(Icono de enlace externo)](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




