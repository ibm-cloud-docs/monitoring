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



# Preguntas frecuentes sobre el uso de Grafana
{: #grafana_qa}

Aquí encontrará las respuestas a preguntas comunes sobre el uso de Grafana con el servicio {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [No puedo ver las alertas que he definido mediante la API de Alertas en mi panel de control de Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#alerts1)
* [Recibo un error BXNMSAL41E al intentar guardar un cambio que he realizado en mi panel de control de Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL41E)
* [Recibo un error BXNMSAL36E al intentar guardar un cambio después de añadir una alerta a mi panel de control de Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL36E)
* [Recibo un error 404 cuando inicio una sesión en la interfaz de usuario web del servicio de supervisión](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#404)
* [Acabo de cargar datos json para un panel de control de Grafana; ¿por qué he perdido la barra de desplazamiento?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#2)


## No puedo ver las alertas que he definido mediante la API de Alertas en mi panel de control de Grafana
{: #alerts1}

Las alertas que defina mediante la API de Alertas no se muestran en el separador de alertas en Grafana. Para ver alertas en Grafana, debe definirlas directamente en un panel de control de Grafana.

Para obtener más información, consulte [Configuración de alertas en Grafana](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-config_alerts_grafana#config_alerts_grafana).

## Recibo un error BXNMSAL41E al intentar guardar un cambio que he realizado en mi panel de control de Grafana
{: #BXNMSAL41E}

Puede definir canales de notificación y alertas en Grafana. Si suprime un canal de notificación en Grafana, y no actualiza la regla para eliminar dicho canal de notificación, recibirá un error **BXNMSAL41E** al intentar guardar el panel de control de Grafana.

Para solucionar el problema, actualice la regla utilizando la API de Alertas y vuelva a intentar guardar el panel de control. Cuando se actualice la regla, elimine el canal de notificación que se ha suprimido.

Para obtener más información, consulte [API de Alertas](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction).

## Recibo un error BXNMSAL36E al intentar guardar un cambio después de añadir una alerta a mi panel de control de Grafana
{: #BXNMSAL36E}

Si se llega a la cuota para el dominio donde está supervisando las métricas en el servicio {{site.data.keyword.monitoringshort}}, recibirá el error siguiente: **BXNMSAL36E**

Actualice su plan y vuelva a intentarlo.

Para obtener más información sobre cómo actualizar su plan, consulte [Cambio del plan](/docs/services/cloud-monitoring/plan?topic=cloud-monitoring-change_plan#change_plan).


## Recibo un error 404 cuando inicio una sesión en la interfaz de usuario web del servicio de supervisión utilizando el modelo de autorización UUA
{: #404}

Si recibe un error 404 al intentar iniciar una sesión en la interfaz de usuario web (Grafana) del servicio {{site.data.keyword.monitoringshort}}, compruebe que el espacio exista y que tenga acceso al mismo.

Si utiliza el [modelo de autenticación UAA](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa) para acceder al servicio {{site.data.keyword.monitoringshort}}, debe utilizar el mismo ID de usuario y contraseña que ha utilizado para iniciar la sesión en la consola de {{site.data.keyword.Bluemix_notm}}. 

Para comprobar que tiene acceso a la cuenta, organización y espacio donde desea iniciar la sesión, inicie la sesión en la consola de {{site.data.keyword.Bluemix_notm}} y vaya al espacio. 

También puede utilizar la línea de mandatos para comprobar que tiene acceso a dicho espacio. Ejecute el siguiente mandato para iniciar una sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}:

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

Siga las instrucciones. Escriba sus credenciales de {{site.data.keyword.Bluemix_notm}}, seleccione una organización y un espacio.


## Acabo de cargar datos JSON para un panel de control de Grafana; ¿por qué he perdido la barra de desplazamiento?
{: #2}

Existe un error en Grafana que oculta la barra de desplazamiento después de importar un panel de control. 

Para ver la barra de desplazamiento, guardar el panel de control después de importarlo. 








