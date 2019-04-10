---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

 
# Gestión del acceso de usuarios en {{site.data.keyword.cloud_notm}}
{: #iam}

{{site.data.keyword.iamlong}} (IAM) le permite autenticar usuarios de forma segura y controlar el acceso a todos los recursos de la nube de forma coherente en {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

**Todos los usuarios que acceden al servicio {{site.data.keyword.mon_full_notm}} en su cuenta deben tener asignada una política de acceso con un rol de usuario de IAM definido.** La política determina qué acciones puede llevar a cabo el usuario en el contexto del servicio o de la instancia que seleccione. Las acciones permitidas se pueden personalizar y se definen como operaciones que se permite realizar en el servicio. A continuación, las acciones se correlacionan con los roles de usuario de IAM.

Las *políticas* permiten otorgar acceso a distintos niveles. Algunas de las opciones son las siguientes: 

* Acceso a todos los servicios habilitados para IAM en su cuenta
* Acceso a todas las instancias del servicio en una sola región de la cuenta
* Acceso a una instancia de servicio individual en su cuenta
* Acceso a todas las instancias del servicio dentro del contexto de un grupo de recursos
* Acceso a todas las instancias del servicio en una sola región dentro del contexto de un grupo de recursos
* Acceso a todos los servicios habilitados para IAM dentro del contexto de un grupo de recursos

Los *roles* definen las acciones que puede ejecutar un usuario o un ID de servicio. Hay distintos tipos de roles en {{site.data.keyword.cloud_notm}}:
* Los *roles de gestión de la plataforma* permiten a los usuarios realizar tareas sobre los recursos de servicio a nivel de plataforma, por ejemplo asignar acceso de usuario para el servicio, crear o suprimir ID de servicio, crear instancias, asignar políticas para el servicio a otros usuarios y enlazar instancias a aplicaciones.
* Los *roles de acceso al servicio* permiten asignar a los usuarios distintos niveles de permiso para llamar a la API del servicio.

**Para organizar un conjunto de usuarios y de ID de servicio en una sola entidad que facilite la gestión de permisos de IAM, utilice **grupos de acceso*.** Puede asignar una sola política al grupo en lugar de asignar el mismo acceso varias veces por usuario o por ID de servicio individual.
{: tip}


## Gestión del acceso mediante grupos de acceso
{: #iam_groups}

Para gestionar el acceso o asignar un nuevo acceso a los usuarios mediante grupos de acceso, debe ser el propietario de la cuenta, el administrador o el editor de todos los servicios habilitados para Identity and Access de la cuenta, o el administrador o el editor asignado para el servicio de grupos de acceso de IAM. 

Elija cualquiera de las acciones siguientes para gestionar grupos de acceso en {{site.data.keyword.cloud_notm}}:

* [Creación de un grupo de acceso](/docs/iam?topic=iam-groups#create_ag).
* [Asignación de acceso a un grupo](/docs/iam?topic=iam-groups#access_ag).


## Gestión del acceso mediante la asignación de políticas directamente a los usuarios
{: #iam_users}

Para gestionar el acceso o para asignar un nuevo acceso para los usuarios mediante políticas de IAM, debe ser el propietario de la cuenta, el administrador de todos los servicios de la cuenta o un administrador para el servicio o la instancia de servicio en particular. 

Elija cualquiera de las acciones siguientes para gestionar políticas de IAM en {{site.data.keyword.cloud_notm}}:

* Para modificar los permisos de un usuario, consulte [Edición del acceso existente](/docs/iam?topic=iam-iammanidaccser#edit_existing).
* Para otorgar permisos a un usuario, consulte [Asignación de un nuevo acceso](/docs/iam?topic=iam-iammanidaccser#assign_new_access).
* Para revocar permisos, consulte [Eliminación del acceso](/docs/iam?topic=iam-iammanidaccser#removing_access).
* Para revisar los permisos de un usuario, consulte [Revisión del acceso asignado](/docs/iam?topic=iam-iammanidaccser#review_your_access).


## Roles de la plataforma {{site.data.keyword.cloud_notm}}
{: #iam_platform}

Utilice la tabla siguiente para identificar el rol de la plataforma que puede otorgar a un usuario en {{site.data.keyword.cloud_notm}} para ejecutar cualquiera de las siguientes acciones de la plataforma:

| Acciones de la plataforma                                                        | Roles de la plataforma {{site.data.keyword.cloud_notm}}    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `Otorgar a otros miembros de la cuenta acceso para trabajar con el servicio`           | Administrador                                        | 
| `Suministrar una instancia de servicio`                                          | Administrador </br>Editor                            | 
| `Suprimir una instancia de servicio`                                             | Administrador </br>Editor                            | 
| `Crear un ID de servicio`                                                   | Administrador </br>Editor                            |
| `Ver detalles de una instancia de servicio`                                    | Administrador </br>Editor </br>Operador </br>Visor  | 
| `Ver instancias de servicio en el panel de control Supervisión de la observabilidad`      | Administrador </br>Editor </br>Operador </br>Visor  | 
{: caption="Tabla 1. Roles de usuario y acciones de IAM" caption-side="top"}



## Roles de Sysdig
{: #iam_sysdig_roles}

En la tabla siguiente se describen los roles de Sysdig y las acciones por rol:

| Acciones                                                                    | Rol de Sysdig                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Restablecer la clave de acceso de Sysdig`                                              | Admin                                                |
| `Gestionar usuarios`                                                             | Admin                                                |
| `Crear, configurar y suprimir equipos`                                      | Admin                                                |
| `Configurar y eliminar canales de comunicación`                              | Admin                                                | 
| `Configurar y eliminar agentes de Sysdig`                                       | Admin                                                |
| `Crear, suprimir y editar contenido en la IU web de Sysdig`                    | Admin </br>Usuario                                      |  
| `Ver métricas mediante la IU web de Sysdig`                                   | Admin </br>Usuario                                      |  
| `Crear y suprimir alertas`                                                 | Admin </br>Usuario                                      | 
| `Crear y suprimir capturas`                                               | Admin </br>Usuario                                      |   
{: caption="Tabla 2. Roles y acciones de Sysdig" caption-side="top"}


## Correlación entre roles de Sysdig y roles de {{site.data.keyword.cloud_notm}}
{: #iam_sysdig}

Utilice la tabla siguiente para ver cómo se correlaciona un rol de {{site.data.keyword.cloud_notm}} con un rol de Sysdig:

| Tipo de rol        | Rol               | Rol de Sysdig                | Descripción                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| Rol de plataforma       | Administrador      | Admin                      | Otorga al usuario privilegios de administración de Sysdig.   | 
| Rol de servicio        | Gestor            | Admin                      | Otorga al usuario privilegios de administración de Sysdig.   | 
| Rol de servicio        | Escritor             | Usuario                       | Otorga al usuario privilegios de usuario de Sysdig.    |
| Rol de servicio        | Lector             |                            | No se otorga ningún permiso.                 |
{: caption="Tabla 3. Roles de Sysdig" caption-side="top"}


