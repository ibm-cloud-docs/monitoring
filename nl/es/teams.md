---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, teams

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

# Cómo trabajar con equipos
{: #teams}

Un administrador o un gestor de una instancia de {{site.data.keyword.mon_full_notm}} puede crear, suprimir, añadir miembros y cambiar el ámbito de los equipos de dicha instancia. 
{:shortdesc} 

Un administrador o un gestor de una instancia de {{site.data.keyword.mon_full_notm}} debe cambiar al equipo de *Operaciones de supervisión* para poder crear equipos y gestionar los equipos existentes.
{: tip}

## Creación de un equipo
{: #teams_create}

Siga los pasos siguientes para crear un equipo:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Operaciones de supervisión**. A continuación, seleccione **Valores**.

3. Seleccione **Equipos**. Se muestra la lista de equipos existentes.

4. Pulse **Añadir equipo**. Se abre la página de configuración del equipo.

5. Configure los detalles del equipo. 

    * Elija un color.

    * Escriba el nombre del equipo.

    * [Opcional] Especifique una descripción para este equipo.

    * [Opcional] Establezca el parámetro **Equipo predeterminado** si desea que este equipo se convierta en el equipo predeterminado para los nuevos usuarios.

    * Establezca el **Punto de entrada predeterminado** para especificar la vista en la interfaz de usuario web que se abrirá cada vez que un usuario inicie una sesión. Los puntos de entrada válidos son: vista *Explorar*, vista *Paneles de control*, vista *Sucesos*, vista *Alertas* y vista *Valores*. De forma predeterminada, se establece la vista *Explorar*.

6. Configure el ámbito del equipo. 

    * [Opcional] Establezca **Ámbito por** para especificar el nivel de datos a los que tienen acceso los miembros del equipo. Los valores válidos son *host* y *contenedor*. Si el parámetro se establece en *Host*, los miembros pueden ver toda la información de nivel de host y de nivel de contenedor. Si el parámetro se establece en *Contenedor*, los miembros solo pueden ver información de nivel de contenedor.

    * Establezca el **Ámbito** para limitar los datos que pueden ver los usuarios. Puede establecer una o varias condiciones mediante la especificación de expresiones para métricas. De forma predeterminada, el ámbito se establece en *en todas partes*.
	
    * [Opcional] Habilite o inhabilite **Capturas de Sysdig**. Marque este recuadro para permitir que este equipo tome capturas de Sysdig. Los archivos de captura solo resultarán visibles para los miembros de este equipo. **Nota:** las capturas incluyen información detallada de cada contenedor de un host, independientemente del ámbito del equipo.

    * [Opcional] Habilite o inhabilite **Sucesos de infraestructura**. Marque este recuadro para permitir que los miembros vean todos los sucesos personalizados de la infraestructura de cada usuario y agente de Sysdig. Cuando no se está seleccionado, los usuarios pueden ver los sucesos de la infraestructura que se envían específicamente a este equipo. 

6. Añada miembros al equipo. Pulse **Asignar usuario**. Busque un usuario y añádalo.



## Cambio del ámbito de un equipo
{: #teams_scope}

Para cambiar el ámbito de los datos que pueden ver los miembros de un equipo, siga los pasos siguientes: 

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Operaciones de supervisión**. A continuación, seleccione **Valores**.

3. Seleccione **Equipos**. Se muestra la lista de equipos existentes.

4. Identifique el equipo y selecciónelo. Se muestran los detalles del equipo.

5. Cambie los detalles de la configuración en la sección *Visibilidad*.

6. Pulse **Guardar**. 


## Adición de usuarios a un equipo
{: #teams_users}

Para añadir miembros a un equipo, siga los pasos siguientes: 

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Operaciones de supervisión**. A continuación, seleccione **Valores**.

3. Seleccione **Equipos**. Se muestra la lista de equipos existentes.

4. Identifique el equipo y selecciónelo. Se muestran los detalles del equipo.

5. Pulse **Asignar usuario** en la sección *Usuarios del equipo*.

6. Pulse **Guardar**. 


## Supresión de un equipo
{: #teams_delete}

El equipo predeterminado, **Operaciones de supervisión**, no se puede suprimir. 

Siga los pasos siguientes para suprimir un equipo:

1. Inicie la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. En el botón *Selector* de la barra de navegación, seleccione **Operaciones de supervisión**. A continuación, seleccione **Valores**.

3. Seleccione **Equipos**. Se muestra la lista de equipos existentes.

4. Identifique el equipo que desea suprimir y selecciónelo. Se muestran los detalles del equipo.

5. Pulse **Suprimir equipo**.

**Nota:** cuando se suprime un equipo, los usuarios que solo pertenecen a dicho equipo se mueven al equipo predeterminado.



