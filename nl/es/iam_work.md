---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam, access groups

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

 
# Cómo trabajar con políticas de IAM y grupos de acceso
{: #iam_work}

{{site.data.keyword.iamlong}} (IAM) le permite autenticar usuarios de forma segura y controlar el acceso a todos los recursos de la nube de forma coherente en {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

Para otorgar privilegios de administrador de Sysdig a un usuario, puede asignarle cualquiera de los roles siguientes:

* Rol de `Administrador` de la plataforma: otorgue este rol si el usuario es también un administrador del servicio de Sysdig en {{site.data.keyword.cloud_notm}}.
* Rol de `Editor` de la plataforma: otorgue este rol si el usuario debe poder suministrar o eliminar instancias de Sysdig en {{site.data.keyword.cloud_notm}}.
* Rol de `Gestor` de la plataforma: otorgue este rol si el usuario no debe poder gestionar el servicio Sysdig en {{site.data.keyword.cloud_notm}}.

Para otorgar a un usuario privilegios de usuario de Sysdig, puede asignarle el rol de `Escritor` del servicio.

**Nota:** para gestionar el acceso o para asignar un nuevo acceso para los usuarios mediante políticas de IAM, debe ser el propietario de la cuenta, el administrador de todos los servicios de la cuenta o un administrador para el servicio o la instancia de servicio en particular. 

Como **propietario de la cuenta** o como **administrador del servicio {{site.data.keyword.mon_full_notm}}**,
debe tener permisos para ejecutar las siguientes acciones de la plataforma: 

* Otorgar a otros miembros de la cuenta acceso para trabajar con el servicio
* Suministrar una instancia de servicio
* Suprimir una instancia de servicio
* Ver detalles de una instancia de servicio
* Crear un ID de servicio

Como **usuario de Devops**, debe tener permisos para ejecutar las siguientes acciones de la plataforma: 

* Suministrar una instancia de servicio
* Suprimir una instancia de servicio
* Ver detalles de una instancia de servicio
* Crear un ID de servicio


## Cómo otorgar permisos a un usuario para que se convierta en administrador del servicio en la cuenta de {{site.data.keyword.cloud_notm}}
{: #admin_account}

Para otorgar a un usuario el rol de administrador para gestionar el servicio en la cuenta, el usuario debe tener una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Administrador** de la plataforma. Debe asignar a este usuario acceso a un recurso individual de la cuenta. 

Siga los pasos siguientes para asignar a un usuario el rol de administrador sobre el servicio {{site.data.keyword.mon_full_notm}} en la cuenta: 

1. En la barra de menús, pulse **Gestionar** &gt; **Acceso (IAM)** y seleccione **Usuarios**.
2. En la fila del usuario al que desea asignar acceso, seleccione el menú **Acciones** y, a continuación, pulse **Asignar acceso**.
3. Seleccione **Asignar acceso a recursos**.
4. Seleccione **{{site.data.keyword.mon_full_notm}}**.
5. Seleccione **Todas las regiones actuales**.
6. Seleccione **Todas las instancias de servicio actuales**.
7. Seleccione el rol de **Administrador** de la plataforma.
8. Pulse Asignar.


## Cómo otorgar permisos a un usuario para que se convierta en administrador del servicio dentro de un grupo de recursos
{: #admin_rg}

Para otorgar a un usuario el rol de administrador para gestionar instancias dentro de un grupo de recursos en la cuenta, el usuario debe tener una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Administrador** de la plataforma
dentro del contexto del grupo de recursos. 

Siga los pasos siguientes para asignar a un usuario el rol de administrador sobre el servicio {{site.data.keyword.mon_full_notm}} dentro del contexto de un grupo de recursos: 

1. En la barra de menús, pulse **Gestionar** &gt; **Acceso (IAM)** y seleccione **Usuarios**.
2. En la fila del usuario al que desea asignar acceso, seleccione el menú **Acciones** y, a continuación, pulse **Asignar acceso**.
3. Seleccione **Asignar acceso dentro de un grupo de recursos**.
4. Seleccione un grupo de recursos.
5. Si el usuario aún no tiene un rol otorgado para el grupo de recursos seleccionado, elija un rol para el campo **Asignar acceso a un grupo de recursos**. 

    En función del rol que seleccione, el usuario puede ver el grupo de recursos en su panel de control, editar el nombre del grupo de recursos o gestionar el acceso de usuarios al grupo. 
    
    Puede seleccionar **Sin acceso** si desea que el usuario solo tenga acceso al servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos.

6. Seleccione **{{site.data.keyword.mon_full_notm}}**.
7. Seleccione el rol de **Administrador** de la plataforma.
8. Pulse **Asignar**.


## Cómo otorgar permisos a un usuario de Devops para gestionar el servicio en la cuenta de {{site.data.keyword.cloud_notm}}
{: #devops_account}

Es necesario que tenga una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Editor** de la plataforma.

Siga los pasos siguientes para asignar a un usuario el rol de editor sobre el servicio {{site.data.keyword.mon_full_notm}} en la cuenta: 

1. En la barra de menús, pulse **Gestionar** &gt; **Acceso (IAM)** y seleccione **Usuarios**.
2. En la fila del usuario al que desea asignar acceso, seleccione el menú **Acciones** y, a continuación, pulse **Asignar acceso**.
3. Seleccione **Asignar acceso a recursos**.
4. Seleccione **{{site.data.keyword.mon_full_notm}}**.
5. Seleccione **Todas las instancias de servicio**.
6. Seleccione el rol de **Editor** de la plataforma.
7. Pulse Asignar.

## Cómo otorgar permisos a un usuario de Devops para gestionar una instancia en la cuenta de {{site.data.keyword.cloud_notm}}
{: #devops_account_instance}

Siga los pasos siguientes para asignar a un usuario el rol de editor sobre una instancia del servicio {{site.data.keyword.mon_full_notm}} en la cuenta: 

1. En la barra de menús, pulse **Gestionar** &gt; **Acceso (IAM)** y seleccione **Usuarios**.
2. En la fila del usuario al que desea asignar acceso, seleccione el menú **Acciones** y, a continuación, pulse **Asignar acceso**.
3. Seleccione **Asignar acceso a recursos**.
4. Seleccione **{{site.data.keyword.mon_full_notm}}**.
5. Seleccione la instancia.
6. Seleccione el rol de **Editor** de la plataforma.
7. Pulse Asignar.



## Cómo otorgar permisos a un usuario de Devops para gestionar el servicio dentro de un grupo de recursos
{: #devops_rg}

Necesita una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Editor** de la plataforma.

Siga los pasos siguientes para asignar a un usuario el rol de editor sobre el servicio {{site.data.keyword.mon_full_notm}} dentro del contexto de un grupo de recursos: 

1. En la barra de menús, pulse **Gestionar** &gt; **Acceso (IAM)** y seleccione **Usuarios**.
2. En la fila del usuario al que desea asignar acceso, seleccione el menú **Acciones** y, a continuación, pulse **Asignar acceso**.
3. Seleccione **Asignar acceso dentro de un grupo de recursos**.
4. Seleccione un grupo de recursos.
5. Si el usuario aún no tiene un rol otorgado para el grupo de recursos seleccionado, elija un rol para el campo **Asignar acceso a un grupo de recursos**. 

    En función del rol que seleccione, el usuario puede ver el grupo de recursos en su panel de control, editar el nombre del grupo de recursos o gestionar el acceso de usuarios al grupo. 
    
    Puede seleccionar **Sin acceso** si desea que el usuario solo tenga acceso al servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos.

6. Seleccione **{{site.data.keyword.mon_full_notm}}**.
7. Seleccione el rol de **Editor** de la plataforma.
8. Pulse **Asignar**.

## Cómo otorgar permisos para gestionar métricas y configurar alertas en Sysdig
{: #admin_user_sysdig}

Como **usuario administrador** en Sysdig, debe tener permisos para ejecutar las acciones siguientes: 

* Añadir orígenes de métricas
* Ver métricas
* Buscar métricas
* Filtrar métricas
* Configurar alertas

Por lo tanto, necesita las políticas siguientes:

* Una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Editor** de la plataforma. Esta política le permite ver los detalles de la instancia de servicio mediante la línea de mandatos y en el panel de control de {{site.data.keyword.cloud_notm}}.
* Una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Gestor** del servicio. Esta política le permite supervisar, filtrar y buscar métricas, y definir alertas mediante la interfaz de usuario web de Sysdig.

**Nota:** como administrador del servicio, cuando otorgue a un usuario estas políticas, tenga en cuenta la posibilidad de hacerlo dentro del contexto de un grupo de recursos. Se suministra una instancia de {{site.data.keyword.mon_full_notm}} dentro del contexto de un grupo de recursos. Por lo tanto, debe otorgar permisos de acceso dentro del contexto del grupo de recursos.


Siga los pasos siguientes para asignar a un usuario ambas políticas sobre el servicio {{site.data.keyword.mon_full_notm}} dentro del contexto de un grupo de recursos: 

1. En la barra de menús, pulse **Gestionar** &gt; **Acceso (IAM)** y seleccione **Usuarios**.
2. En la fila del usuario al que desea asignar acceso, seleccione el menú **Acciones** y, a continuación, pulse **Asignar acceso**.
3. Seleccione **Asignar acceso dentro de un grupo de recursos**.
4. Seleccione un grupo de recursos.
5. Si el usuario aún no tiene un rol otorgado para el grupo de recursos seleccionado, elija un rol para el campo **Asignar acceso a un grupo de recursos**. 

    En función del rol que seleccione, el usuario puede ver el grupo de recursos en su panel de control, editar el nombre del grupo de recursos o gestionar el acceso de usuarios al grupo. 
    
    Puede seleccionar **Sin acceso** si desea que el usuario solo tenga acceso al servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos.

6. Seleccione **{{site.data.keyword.mon_full_notm}}**.
7. Seleccione el rol de **Editor** de la plataforma.
8. Seleccione el rol de **Gestor** del servicio.
8. Pulse **Asignar**.

## Cómo otorgar a un usuario permisos para ver métricas en Sysdig
{: #user_sysdig}

Como **usuario**, **auditor** o **desarrollador**, es posible que necesite permisos para ejecutar las siguientes acciones: 

* Ver métricas
* Buscar métricas
* Filtrar métricas

Por lo tanto, necesita las políticas siguientes:

* Una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Visor** de la plataforma. Esta política le permite ver los detalles de la instancia de servicio mediante la línea de mandatos y en el panel de control de {{site.data.keyword.cloud_notm}}.
* Una política de IAM para el servicio {{site.data.keyword.mon_full_notm}} con el rol de **Escritor** del servicio. Esta política le permite ver, filtrar y buscar métricas mediante la interfaz de usuario web de Sysdig.

**Nota:** como administrador del servicio, cuando otorgue a un usuario estas políticas, tenga en cuenta la posibilidad de hacerlo dentro del contexto de un grupo de recursos. Se suministra una instancia de {{site.data.keyword.mon_full_notm}} dentro del contexto de un grupo de recursos. Por lo tanto, debe otorgar permisos de acceso dentro del contexto del grupo de recursos.

Siga los pasos siguientes para asignar a un usuario ambas políticas sobre el servicio {{site.data.keyword.mon_full_notm}} dentro del contexto de un grupo de recursos: 

1. En la barra de menús, pulse **Gestionar** &gt; **Acceso (IAM)** y seleccione **Usuarios**.
2. En la fila del usuario al que desea asignar acceso, seleccione el menú **Acciones** y, a continuación, pulse **Asignar acceso**.
3. Seleccione **Asignar acceso dentro de un grupo de recursos**.
4. Seleccione un grupo de recursos.
5. Si el usuario aún no tiene un rol otorgado para el grupo de recursos seleccionado, elija un rol para el campo **Asignar acceso a un grupo de recursos**. 

    En función del rol que seleccione, el usuario puede ver el grupo de recursos en su panel de control, editar el nombre del grupo de recursos o gestionar el acceso de usuarios al grupo. 
    
    Puede seleccionar **Sin acceso** si desea que el usuario solo tenga acceso al servicio {{site.data.keyword.mon_full_notm}} en el grupo de recursos.

6. Seleccione **{{site.data.keyword.mon_full_notm}}**.
7. Seleccione el rol de **Visor** de la plataforma.
8. Seleccione el rol de **Escritor** del servicio.
8. Pulse **Asignar**.

