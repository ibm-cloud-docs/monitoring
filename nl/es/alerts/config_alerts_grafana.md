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

# Configuración de alertas en Grafana
{: #config_alerts_grafana}

El servicio {{site.data.keyword.monitoringshort}} proporciona un sistema de alertas basado en consultas. Puede configurar alertas en Grafana en paneles de control que no tienen variables de plantilla. 
{:shortdesc}

Para configurar una alerta en una consulta de métrica mediante la interfaz de usuario de Grafana, siga estos pasos:

1. Inicie Grafana.
2. Defina uno o varios canales de notificación.
3. Cree un panel de control de Grafana que incluya un gráfico y como mínimo una métrica de consulta. 
4. Configure la alerta a través del separador **Alertas** en un gráfico de Grafana.

## Paso 1: Iniciar Grafana
{: #step1_cag1}

Inicie Grafana desde un navegador. Por ejemplo, escriba el siguiente URL para abrir Grafana en la región EE.UU. sur: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

Para obtener una lista de URL de Grafana por región, consulte [URL para el servicio {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/monitoring_ov.html#region).

## Paso 2: Definir uno o varios canales de notificación
{: #step2_cag2}

Realice los siguientes pasos:

1. En Grafana, seleccione la barra de menús lateral.

2. Seleccione **Alertas > Canales de notificación > Nuevo canal**.

3. Escriba los datos para el canal nuevo. Añada un canal de notificación por correo electrónico, por ejemplo.

<table>
  <caption>Método y datos de notificación por correo electrónico que debe especificar para crear un canal nuevo</caption>
  <tr>
     <th>Campo</th>
     <th>Descripción</th>
  </tr>
  <tr>
    <td>Nombre</td>
    <td>Nombre del canal de notificación. Este valor debe ser exclusivo.</td>
  </tr>
  <tr>
    <td>Descripción</td>
    <td>La información adicional que desee incluir para fines de documentación.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Seleccione: **Correo electrónico**</td>
  </tr>
  <tr>
    <td>ID de correo electrónico</td>
    <td>Escriba la dirección de correo electrónico del destinatario. </br>Puede entrar varias direcciones de correo electrónico
separadas por comas.</td>
  </tr>
</table>

<table>
  <caption>Método y datos de notificación por Webhook que debe especificar para crear un canal nuevo</caption>
  <tr>
     <th>Campo</th>
     <th>Descripción</th>
  </tr>
  <tr>
    <td>Nombre</td>
    <td>Nombre del canal de notificación. Este valor debe ser exclusivo.</td>
  </tr>
  <tr>
    <td>Descripción</td>
    <td>La información adicional que desee incluir para fines de documentación.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Seleccione: **Webhook**</td>
  </tr>
  <tr>
    <td>URL POST de Webhook</td>
    <td>Escriba el URL en el que se debe realizar la acción POST.</td>
  </tr>
  <tr>
    <td>Cabeceras Webhook</td>
    <td>Escriba cualquier cabecera.</td>
  </tr>
  <tr>
    <td>Parámetros de consulta de Webhook</td>
    <td>Escriba cualquier parámetro de consulta.</td>
  </tr>
</table>

<table>
  <caption>Método y datos de notificación de PagerDuty que debe especificar para crear un canal nuevo</caption>
  <tr>
     <th>Campo</th>
     <th>Descripción</th>
  </tr>
  <tr>
    <td>Nombre</td>
    <td>Nombre del canal de notificación. Este valor debe ser exclusivo.</td>
  </tr>
  <tr>
    <td>Descripción</td>
    <td>La información adicional que desee incluir para fines de documentación.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Seleccione: **PagerDuty**</td>
  </tr>
  <tr>
    <td>Clave de API de PagerDuty</td>
    <td>Escriba la clave de PagerDuty.</td>
  </tr>
</table>

## Paso 3: Definir una métrica
{: #step3_cag3}

Siga los siguientes pasos para crear un nuevo panel de control:

1. Seleccione el conmutador de la barra de menús lateral ![Barra de menús lateral de Grafana](images/grafana_settings.gif "Barra de menús lateral de Grafana").
2. Seleccione **Paneles de control**.
3. Pulse **Nuevo**

Se abre un panel de control. El panel de control incluye una fila vacía que está lista para la configuración. 

A continuación, añada una consulta de métrica:

1. Añada un panel *Gráfico*.
2. Seleccione **Gráfico**.
3. Pulse en el título del gráfico y seleccione **editar**.
    
    Se abre el separador *Métricas*. Aquí puede ver el origen de datos predeterminado.
    
4. Defina la consulta de métrica que filtra los datos que se muestran en el gráfico. 


## Paso 4: Definir una alerta
{: #step4_cag4}

Siga los siguientes pasos para definir una alerta en la interfaz de usuario de Grafana:

1. Seleccione el separador **Alerta**.
2. En la sección **Configuración de alertas**, defina la regla que define las condiciones bajo las que se genera una notificación de alerta.

    Configure el campo **Evaluar cada** y la sección **Condiciones**.

3. En la sección **Notificaciones**, seleccione uno o varios canales de notificación.

**Nota:** 

* Cuando se establece una condición, puede ver una línea roja en el gráfico para definir el umbral establecido. Puede arrastrarla en el gráfico para cambiarla.
* Una vez creada la alerta, si desea modificarla, debe hacerlo utilizando la API de alertas.
* Si selecciona **Suprimir**, la alerta se suprimirá.

## Siguiente: Verifique que se haya generado una alerta
{: #next_cag5}

Por ejemplo, si ha creado un canal de notificación por correo electrónico, compruebe su correo electrónico.

Busque correos electrónicos con remitente **IBM Cloud Monitoring**.

Un correo electrónico incluye información sobre la alerta y un enlace al panel de control de Grafana donde puede ver la situación.

Por ejemplo:

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


