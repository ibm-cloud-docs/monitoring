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


# Navegación al panel de control de Grafana
{:#navigating_grafana}

En {{site.data.keyword.Bluemix}}, puede utilizar Grafana, una plataforma de visualización y análisis de código abierto, para supervisar, buscar, analizar y visualizar métricas en diversos gráficos, como diagramas y tablas. Utilice Grafana para realizar tareas avanzadas de análisis.
{:shortdesc}

Puede iniciar Grafana de cualquiera de estas formas:

* Desde {{site.data.keyword.Bluemix_notm}}

    Puede iniciar métricas de contenedor Docker específicas en Grafana, en el contexto de dicho contenedor en concreto. Esta característica únicamente se aplica a contenedores desplegados en la infraestructura gestionada de {{site.data.keyword.Bluemix_notm}}. 
    
    Para obtener más información, consulte [Navegación al panel de control de Grafana desde el panel de control de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_bluemix).

* Desde un enlace directo del navegador

    Puede iniciar Grafana para que los datos que ve agreguen registros de servicios de un espacio de {{site.data.keyword.Bluemix_notm}} especificado.
    
    Para obtener más información, consulte [Navegación al panel de control de Grafana desde un navegador web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).
    
Para obtener más información sobre Grafana, consulte la [Guía del usuario de Grafana ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Navegación al panel de control de Grafana desde el panel de control de IBM Cloud
{: #launch_grafana_from_bluemix}

**Nota:** Esta característica únicamente se aplica a contenedores desplegados en la infraestructura gestionada de {{site.data.keyword.Bluemix_notm}}. 

La consulta que se utiliza para filtrar los datos que aparecen en Grafana recupera los datos correspondientes al contenedor de {{site.data.keyword.Bluemix_notm}} desde el que ha iniciado Kibana. 

Para ver las métricas de un contenedor Docker en Grafana, siga los pasos siguientes:

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}} y pulse el contenedor desde el *Panel de control*. 
    
2. En la barra de navegación, pulse **Supervisión y registros**. Se abre el separador de supervisión. 
    
3. Pulse **Vista avanzada**. Se abre el panel de control de **Grafana**.


##  Navegación al panel de control de Grafana desde un navegador web
{: #launch_grafana_from_browser}

La consulta que se utiliza para filtrar los datos que aparecen en Grafana recupera datos de un espacio de la organización {{site.data.keyword.Bluemix_notm}}. La información de métricas que muestra Grafana incluye registros correspondientes a todos los recursos desplegados dentro del espacio de la organización {{site.data.keyword.Bluemix_notm}} en la que ha iniciado la sesión.

Siga los pasos siguientes para iniciar Grafana desde un navegador:

1. Abra un navegador web. 
2. Especifique el URL para la región en la que desea supervisar métricas. 

    La tabla siguiente lista los URL por región:
	<table>
      <caption>URL para iniciar Grafana en diferentes regiones</caption>
      <tr>
        <th>Región</th>
	    <th>Punto final</th>
      </tr>
      <tr>
        <td>Alemania</td>
	    <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
      </tr>
      <tr>
        <td>Reino Unido</td>
	    <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
      </tr>
      <tr>
        <td>EE.UU. sur</td>
    	<td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
      </tr>
      <tr>
        <td>Reino Unido</td>
	    <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
      </tr>
      
    </table>
	
2. Seleccione **Grafana**.
     

