---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Resolución de problemas de {{site.data.keyword.mon_full_notm}}
{: #troubleshoot}

Obtenga más información acerca de algunos problemas generales que puede encontrar cuando utilice el servicio {{site.data.keyword.mon_full_notm}}. En muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}

## ¿Recibe un error cuando crea una captura?
{: #troubleshoot-entry-1}

No puede crear un [archivo de captura](/docs/services/Monitoring-with-Sysdig/captures.html#captures) para un host en la infraestructura. 

En la sección *Capturas* de la interfaz de usuario web, recibe un error cuando intenta crear un archivo de captura para un host.
{: tsSymptoms}

El agente de Sysdig que se ejecuta en el host tiene la característica **sysdig_capture_enabled** establecida en *false*.
{: tsCauses}

Habilite la característica **sysdig_capture_enabled** en el agente de Sysdig que se ejecuta en el host.
{: tsResolve}


## ¿El estado del archivo de captura está establecido en *solicitado* y no pasa al estado *cargado*?
{: #troubleshoot-entry-2}

El estado de un [archivo de captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures) está establecido en *solicitado* y no pasa al estado *cargado*. Está esperando a que el archivo de captura esté disponible para analizarlo.

En la sección *Capturas* de la interfaz de usuario web, el estado del archivo de captura de un host no pasa a ser *uploaded*.
{: tsSymptoms}

El host tiene el puerto TCP 6443 inhabilitado.
{: tsCauses}


Compruebe que el puerto 6443 esté abierto. Para obtener más información, consulte [Gestión del tráfico de red](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send).
{: tsResolve}


