---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# Navegación a la interfaz de usuario web
{: #launch}

Después de suministrar una instancia del servicio {{site.data.keyword.mon_full_notm}} en {{site.data.keyword.Bluemix}} y de configurar un agente de Sysdig para un origen de métricas, puede ver, supervisar y gestionar métricas mediante la interfaz de usuario web de {{site.data.keyword.mon_full_notm}}.
{:shortdesc}


## Cómo otorgar políticas de IAM a un usuario para que pueda ver datos 
{: #launch_step1}

**Nota:** debe ser un administrador del servicio {{site.data.keyword.mon_full_notm}} o un administrador de la instancia de {{site.data.keyword.mon_full_notm}} o debe tener permisos de IAM de la cuenta para poder otorgar políticas a otros usuarios.

En la tabla siguiente se muestran las políticas mínimas que debe tener un usuario para poder iniciar la interfaz de usuario web de {{site.data.keyword.mon_full_notm}} y poder ver datos:

| Servicio                        | Rol                      | Permiso otorgado     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | Rol de la plataforma: Visor     | Permite al usuario ver la lista de instancias de servicio en el panel de control Supervisión de la observabilidad. |
| `{{site.data.keyword.mon_full_notm}}` | Rol de servicio: Escritor      | Permite al usuario iniciar la interfaz de usuario web y ver métricas en la interfaz de usuario web.  |
{: caption="Tabla 1. Políticas de IAM" caption-side="top"} 

Para obtener más información sobre cómo configurar estas políticas para un usuario, consulte [Cómo otorgar permisos a un usuario para ver métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig).


## Inicio de la interfaz de usuario UI mediante la interfaz de usuario de {{site.data.keyword.cloud_notm}}
{: #launch_step2}

La interfaz de usuario web se inicia en el contexto de una instancia de {{site.data.keyword.mon_full_notm}}, desde la interfaz de usuario de {{site.data.keyword.cloud_notm}}. 

Siga los pasos siguientes para iniciar la interfaz de usuario web:

1. Inicie una sesión en su cuenta de {{site.data.keyword.cloud_notm}}.

    Pulse el [panel de control de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/login){:new_window} para iniciar el panel de control de {{site.data.keyword.cloud_notm}}.

	Cuando inicia una sesión con su ID de usuario y su contraseña, se abre el panel de control de {{site.data.keyword.cloud_notm}}.

2. En el menú de navegación, seleccione **Observabilidad**. 

3. Seleccione **Supervisión**. 

    Se muestra la lista de instancias que están disponibles en {{site.data.keyword.cloud_notm}}.

4. Seleccione una instancia. A continuación, pulse **Ver Sysdig**.

Se abre la interfaz de usuario web.


