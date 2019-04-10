---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, panels

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


# Cómo trabajar con paneles
{: #panels}

Utilice un panel para visualizar una métrica o un grupo de métricas en un panel de control. Puede copiar, cambiar el ámbito, duplicar, suprimir, exportar y explorar paneles.
{:shortdesc}

Puede utilizar cualquiera de los siguientes tipos de panel:

| Tipo | Descripción |
|------|-------------|
| Línea | Utilice este panel para ver las tendencias a lo largo del tiempo para una o varias métricas.  |
| Área | Utilice este panel para ver las tendencias a lo largo del tiempo para una o varias métricas.  |
| Lista de principales | Utilice este panel para comparar una métrica entre grupos de entidades. El diagrama de barras se clasifica en orden descendente.  |
| Histograma | Utilice este panel para ver la distribución de la frecuencia de una métrica en grupos.  |
| Topología | Utilice este panel para visualizar la infraestructura como un mapa de topología y las relaciones entre las entidades del mapa.  |
| Número | Utilice este panel para ver un solo número que representa el valor de una métrica agregada a lo largo del tiempo para una o varias entidades.  |
| Tabla | Utilice este panel para visualizar los datos numéricos de la infraestructura en función de métricas y segmentos.  |
| Texto | Utilice este panel para añadir texto. Utilice anotaciones para añadir texto.  |
{: caption="Tabla 1. Tipos de paneles" caption-side="top"} 



## Copia de un panel en un panel de control
{: #panels_copy}

Siga los pasos siguientes para copiar un panel:

1. Vaya a la sección *PANEL DE CONTROL** de la interfaz de usuario web. Seleccione un panel de control. A continuación, identifique el panel que muestra la métrica que desea copiar.

2. Seleccione el icono *Más opciones* ![icono de tres puntos](images/actions.png) y seleccione **Copiar panel** ![icono copiar](images/actions.png).

3. Seleccione uno de los paneles de control que aparecen en la lista o especifique un nombre para un nuevo panel de control. 

4. Pulse **Copiar y abrir**.



## Cambio del ámbito de un panel
{: #panels_scope}

Siga los pasos siguientes para cambiar el ámbito de un panel:

1. Vaya a la sección *PANEL DE CONTROL** de la interfaz de usuario web. Seleccione un panel de control. A continuación, identifique el panel que muestra la métrica cuyo ámbito desea cambiar.

2. En el panel, pulse **Editar ámbito** para cambiar el ámbito predeterminado. 

    De forma predeterminada, está seleccionado **En todas partes**.
    
3. Seleccione el ámbito. 

4. Si lo desea, pulse **Modificar los ámbitos de paneles personalizados** para modificar el ámbito para todos los paneles que actualmente tienen definido un ámbito personalizado. 

    **Nota: esta acción no se puede deshacer.** 

    Para restablecer el ámbito del panel de control a toda la infraestructura, o para actualizar el ámbito de un panel de control existente a toda la infraestructura, seleccione **En todas partes**.
    {: tip}

5. Pulse **Guardar**.



## Duplicación de un panel
{: #panels_duplicate}

Siga los pasos siguientes para duplicar un panel en el panel de control actual:

1. Vaya a la sección *PANEL DE CONTROL** de la interfaz de usuario web. Seleccione un panel de control. A continuación, identifique el panel que muestra la métrica que desea copiar.

2. Seleccione el icono *Más opciones* ![icono de tres puntos](images/actions.png) y seleccione **Duplicar panel** ![icono copiar](images/duplicate.png).


## Supresión de un panel
{: #panels_delete}

Siga los pasos siguientes para suprimir un panel en el panel de control actual:

1. Vaya a la sección *PANEL DE CONTROL** de la interfaz de usuario web. Seleccione un panel de control. A continuación, identifique el panel que muestra la métrica que desea copiar.

2. Seleccione el icono *Más opciones* ![icono de tres puntos](images/actions.png) y seleccione **Suprimir panel** ![icono copiar](images/delete.png).

3. Pulse **Sí, suprimir panel** para confirmar la supresión del panel.



## Exportación de datos de un panel
{: #panels_export}

Tenga en cuenta la información siguiente cuando exporte datos:

* Puede exportar datos a un **archivo json** desde un gráfico de líneas.
* Puede exportar datos a un **archivo csv** desde un gráfico de tabla o desde un gráfico de líneas.

Siga los pasos siguientes para exportar datos de un panel:

1. Vaya a la sección *PANEL DE CONTROL** de la interfaz de usuario web. Seleccione un panel de control. A continuación, identifique el panel que muestra la métrica que desea copiar.

2. Seleccione el icono *Más opciones* ![icono de tres puntos](images/actions.png).

3. Elija una de las opciones siguientes:

    * Seleccione **Exportar JSON** para exportar datos a un archivo con formato json.

    * Seleccione **Exportar CSV** para exportar datos a un archivo con formato csv.

4. Pulse **Guardar el archivo**.




## Creación de alertas
{: #panels_alert}

Puede crear alertas directamente desde un panel.

Siga los pasos siguientes para crear una alerta:

1. Vaya a la sección *PANEL DE CONTROL** de la interfaz de usuario web. Seleccione un panel de control. A continuación, identifique el panel que muestra la métrica que desea copiar.

2. Seleccione el icono *Más opciones* ![icono de tres puntos](images/actions.png).

3. Seleccione **Crear alerta**.

4. Configure la alerta.

5. Pulse **Crear**.


