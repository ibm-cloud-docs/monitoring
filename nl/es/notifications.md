---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# Cómo trabajar con canales de notificación
{: #notifications}

Configure canales de notificación para que se notifique cuando se desencadene una alerta. Los canales de notificación se gestionan a través del panel *Valores* de la interfaz de usuario web.
{:shortdesc}
 

## Configuración de un canal de notificación
{: #notifications_create}

Siga los pasos siguientes para añadir un canal de notificación:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Valores**.

3. Seleccione **Canales de notificación**.

4. Pulse **MIS CANALES** ![icono añadir](../images/add.png). A continuación, seleccione un canal.

    **Nota:** la primera vez que configure un canal de notificación, pulse en cualquiera de los canales.

5. Configure un canal de notificación:

    * Escriba el nombre del canal.

    * Habilite el campo *Notificar cuando esté correcto* para recibir una notificación cuando se deje de desencadenar la condición de alerta.

    * Habilite el campo *Notificar cuando esté resuelto* para recibir una notificación cuando el usuario haya resuelto manualmente la alerta.

    * Para un canal de notificación por **correo electrónico**, añada la lista de destinatarios, separados por comas.

    * En el caso de un canal de notificación **slack**, añada el nombre del *Canal Slack*.

    * En el caso de un canal de notificación **Webhook**, añada el *URL de Webhook*. **Nota:** cuando se desencadena una alerta, la notificación se envía como un POST en formato JSON al punto final de webhook. Para obtener más información, consulte [Configuración de un canal Webhook ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}. Por ejemplo, Sysdig se puede integrar con ServiceNow mediante un webhook personalizado. Para obtener más información sobre la configuración de Sysdig con ServiceNow, consulte [Configuración de ServiceNow ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}.

    * En el caso de un canal de notificación **VictorOps**, añada la *Clave de API* y la *Clave de direccionamiento*.

    * Para un canal de notificación **OpsGenie**, añada la *Clave de API de OpsGenie*. Tenga en cuenta que debe configurar en OpsGenie la integración con Sysdig. Para obtener más información, consulte [Adición de la integración de nube de Sysdig en Opsgenie ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}.

    * Para un canal de notificación **PagerDuty**, primero debe autorizar la integración de Sysdig con la cuenta. Cuando se selecciona PagerDuty, se abre un asistente para configurar la integración con Sysdig. Pulse **Autorizar integración** o **Registrar mediante proveedor de identidad** para autorizar PagerDuty. Elija un servicio existente o configure un nuevo servicio para las notificaciones de Sysdig y luego pulse **Finalizar integración**. Seleccione la política de escalado que se utilizará para las incidencias de Sysdig. A continuación, en el separador *Notificaciones*, confirme su cuenta de PagerDuty, su nombre de servicio y la clave de servicio. 

    * Si lo desea, y para integraciones que permiten una prueba, habilite la condición *Notificación de prueba* para recibir una notificación de prueba. Si no recibe una notificación de prueba en 10 minutos, revise la configuración del canal. 

6. Pulse **CREAR CANAL**. 



## Modificación de un canal de notificación
{: #notifications_update}

Siga los pasos siguientes para modificar un canal de notificación:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Valores**.

3. Seleccione **Canales de notificación**.

4. Identifique el canal de destino que desea modificar y pulse **EDITAR**.

5. Después de realizar cambios, pulse **GUARDAR CAMBIOS**.



## Cómo probar un canal de notificación
{: #notifications_test}

Siga los pasos siguientes para probar un canal de notificación:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Valores**.

3. Seleccione **Canales de notificación**.

4. Identifique el canal de destino que desea modificar y pulse **PROBAR**.



## Inhabilitación de un canal de notificación
{: #notifications_disable}

Siga los pasos siguientes para inhabilitar temporalmente un canal de notificación:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Valores**.

3. Seleccione **Canales de notificación**.

4. En la sección *Notificaciones*, habilite *Tiempo de inactividad* para inhabilitar las alertas temporalmente y silenciar todas las notificaciones.

## Supresión de un canal de notificación
{: #notifications_delete}

Siga los pasos siguientes para suprimir un canal de notificación:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Valores**.

3. Seleccione **Canales de notificación**.

4. Identifique el canal de destino que desea modificar y pulse **EDITAR**.

5. Pulse **SUPRIMIR CANAL**.

6. Confirme la supresión del canal. Pulse **GUARDAR CAMBIOS**.




