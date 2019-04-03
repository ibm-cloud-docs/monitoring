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


# Seguridad
{: #security_ov}

Para controlar las acciones de servicio {{site.data.keyword.monitoringshort}} que un usuario puede realizar, puede asignar uno o más roles a un usuario. Para autenticar un usuario para que trabaje con métricas y alertas, puede utilizar una señal de UAA, una señal de IAM o una clave de API. 
{:shortdesc}





## Modelos de autenticación
{: #auth}

Para trabajar con métricas que se almacenan en el servicio {{site.data.keyword.monitoringshort}} para un espacio, necesita una señal de autenticación o una clave de API. 

Para obtener una señal de seguridad, consulte:

* [Obtención de una señal de UAA](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa)
* [Obtención de una señal de IAM](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)

Para obtener una clave de API, consulte [Generación de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key). Si la clave de API está en peligro, puede revocarla suprimiéndola. A continuación, puede volver a crear una nueva. Para obtener más información, consulte [Revocación de una clave de API mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#revoke_ui). 

Las señales UAA y las señales IAM caducan después de un periodo de tiempo. La clave de API no caduca. 

La tabla siguiente lista los modelos de seguridad que reciben soporte para cada tipo de dominio:

<table>
  <caption>Tabla 1. Modelos de seguridad soportados para cada dominio</caption>
  <tr>
    <th></th>
	<th align="right">Cuenta</th>
    <th align="right">Organización</th>
    <th align="right">Espacio</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">No</td>
	<td align="center">Sí</td>
	<td align="center">Sí</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">Sí</td>
	<td align="center">Sí</td>
	<td align="center">Sí</td>
  </tr>
</table>

El servicio {{site.data.keyword.monitoringshort}} utiliza la característica de control de accesos de IAM para controlar las acciones u operaciones que puede realizar un usuario o servicio sobre el dominio. Por ejemplo, puede definir una política de IAM para permitir que un usuario envíe y cree paneles de control sobre un dominio, pero no que recupere las métricas del dominio.



## Roles de Cloud Foundry
{: #bmx_roles}

En la tabla siguiente se muestran los privilegios de cada rol de Cloud Foundry para trabajar con el servicio {{site.data.keyword.monitoringshort}}:

<table>
  <caption>Tabla 2. Roles y privilegios de Cloud Foundry para trabajar con el servicio {{site.data.keyword.monitoringshort}}.</caption>
  <tr>
    <th>Rol</th>
	<th>Dominio</th>
	<th>Privilegios de acceso</th>
  </tr>
  <tr>
    <td>Gestor</td>
	<td>Organización <br>Espacio</td>
	<td>Todas las API RESTful</td>
  </tr>
  <tr>
    <td>Desarrollador</td>
	<td>Espacio</td>
	<td>Todas las API RESTful</td>
  </tr>
  <tr>
    <td>Auditor</td>
	<td>Organización <br>Espacio</td>
	<td>Solo las API RESTful que realizan operaciones de solo lectura, como por ejemplo consultar métricas.</td>
  </tr>
</table>

Para obtener información sobre la asignación de roles de usuario en la interfaz de usuario, consulte [Gestión del acceso de Cloud Foundry](/docs/iam?topic=iam-mngcf#mngcf).



## Roles de IAM
{: #iam_roles}

La tabla siguiente lista las acciones de servicio {{site.data.keyword.monitoringshort}} cuando trabaja con métricas y los roles de IAM que otorgan permisos a un usuario para ejecutar las tareas:

<table>
  <caption>Tabla 3. Trabajar con métricas </caption>
  <tr>
	<th>Acción</th>
	<th>Rol de IAM</th>
  </tr>
  <tr>
    <td>Enviar métricas al dominio</td>
	<td>Administrador, Editor, Operador</td>
  </tr>
  <tr>
    <td>Recuperar/consultas métricas</td>
	<td>Administrador, Editor, Visor</td>
  </tr>
  <tr>
    <td>Buscar métricas en el dominio</td>
	<td>Administrador, Editor</td>
  </tr>
</table>

La tabla siguiente lista las acciones de servicio {{site.data.keyword.monitoringshort}} cuando trabaja con alertas y los roles de IAM que otorgan permisos a un usuario para ejecutar las tareas:

<table>
  <caption>Tabla 4. Trabajar con alertas. </caption>
  <tr>
	<th>Acción</th>
	<th>Rol de IAM</th>
  </tr>
  <tr>
    <td>Crear, editar y suprimir reglas de alerta</td>
	<td>Administrador, Editor</td>
  </tr>
  <tr>
    <td>Ver alertas</td>
	<td>Administrador, Editor, Visor</td>
  </tr>
  <tr>
    <td>Crear, editar y suprimir notificaciones de alerta</td>
	<td>Administrador, Editor</td>
  </tr>
  <tr>
    <td>Ver notificaciones</td>
	<td>Administrador, Editor, Visor</td>
  </tr>
  <tr>
    <td>Ver historial de registros de alertas activas</td>
	<td>Administrador, Editor, Visor</td>
  </tr>
</table>

Para obtener información sobre la asignación de roles de usuario en la interfaz de usuario, consulte [Gestión del acceso IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

