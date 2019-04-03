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


# Configuración de una consulta de métricas en Grafana
{: #define_query}

En {{site.data.keyword.Bluemix}}, las métricas de los servicios en la nube seleccionados se recopilan automáticamente. Para supervisarlas mediante {{site.data.keyword.monitoringlong}}, debe definir una consulta de Grafana. 
{:shortdesc}

## Paso 1: Recopilar los datos para el servicio o la app CF que desee supervisar
{: #step18}

Obtenga la información siguiente para el servicio o la app CF que desee supervisar:

* **Región** donde se ejecuta la app CF.
* **Organización** donde se ejecuta la app CF. 	
* **Espacio** donde se ejecuta la app CF. 
* **Nombre de app CF** de la app que desea supervisar o **Nombre de servicio**. 


## Paso 2: Iniciar Grafana
{: #step27}

Inicie Grafana desde un navegador. Para obtener más información, consulte [Navegación al panel de control de Grafana desde un navegador web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).

Asegúrese de que, en Grafana, haya iniciado sesión en la cuenta, organización y región donde se ejecuta el servicio o la app CF. 


## Paso 3: Definir una consulta en Grafana
{: #step36}

Realice los pasos siguientes para crear un panel de control de Grafana y definir una consulta:

1. Cree un panel de control nuevo.

    * Seleccione el conmutador de la barra de menús lateral ![Barra de menús lateral de Grafana](images/grafana_settings.gif "Barra de menús lateral de Grafana").
    * Seleccione **Paneles de control**.
    * Pulse **Nuevo**

    Se abre un panel de control. El panel de control incluye una fila vacía que está lista para la configuración.

2. Añada un panel *Gráfico*.

    1. Seleccione **Gráfico**.

    2. Pulse en el título del gráfico y seleccione **editar**.

        Se abre el separador *Métricas*. Aquí puede ver el origen de datos predeterminado.

3. Defina la consulta que filtra los datos que se muestran en el gráfico. 

    En el separador *Métricas*, seleccione **Añadir consulta**. <br>Se añade una entrada de consulta. Cada consulta está etiquetada con una letra.
    
    ![Entrada de nueva consulta](images/grafana4_query_f1.gif "Entrada de nueva consulta")
        
    1. Pulse **Seleccionar métrica** y elija el origen: `ibmcloud`.
    
    2. Pulse **Seleccionar métrica** y elija el tipo de nube: `public`.
    
    3. Pulse **Seleccionar métrica** y elija el nombre de servicio, por ejemplo, `cloud-foundry` para las métricas de la app CF o `message hub` para las métricas de {{site.data.keyword.messagehub}}.
    
    4. Pulse **Seleccionar métrica** y elija la región desde la que está trabajando, por ejemplo, `ng` para la región EE.UU. sur.
    
    5. Seleccione los campos de servicio específicos que se aplican al servicio o a la app CF que desea supervisar.

        <table>
          <caption>Formatos de consulta de métrica por servicio o app CF</caption>
          <tr>
            <th>Nombre de servicio</th>
            <th>Enlace al formato de consulta de métrica</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Formato de consulta para métricas de CPU recopiladas para contenedores](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers) </br>[Formato de consulta para métricas de carga recopiladas para trabajadores](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#load_workers) </br>[Formato de consulta para métricas de memoria recopiladas para contenedores](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#mem_containers)</td> 
          </tr>
          <tr>
            <td>Apps CF</td>
            <td>[Formato de consulta para apps CF](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-cfapps_metrics_format#cfapps_metrics_format)</td> 
          </tr>
        </table>

        Por ejemplo, para una app CF, seleccione:
    
        Pulse **Seleccionar métrica** y elija el nombre de app CF, por ejemplo, `logtester`.
    
        Pulse **Seleccionar métrica** y elija el índice de instancia de app CF, por ejemplo, `0`.

        Pulse **Seleccionar métrica** y elija `contenedor`.
    
    9. Pulse **Seleccionar métrica** y elija un tipo de métrica. Por ejemplo, **cpu** para métricas de CPU, **memoria** para métricas de memoria y **disco** para métricas de disco. 

        **Nota:** Omita este paso para apps CF. 

    10. Pulse **Seleccionar métrica** y elija una métrica. 

        <table>
          <caption>Lista de métricas por servicio o app CF</caption>
          <tr>
            <th>Nombre de servicio</th>
            <th>Enlace a las métricas</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Métricas de CPU](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[Métricas de disco](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics) </br>[Métricas de memoria](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td> 
          </tr>
          <tr>
            <td>Apps CF</td>
            <td>[Métricas de CPU](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics)  </br>[Métricas de disco](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics)   </br>[Métricas de memoria](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Métricas para un tema de Kafka](/docs/services/cloud-monitoring/mh?topic=cloud-monitoring-monitoring_mh_ov#kafka_topic_metrics) </br>[Métricas para una partición de Kafka](/docs/services/cloud-monitoring/mh?topic=cloud-monitoring-monitoring_mh_ov#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. Pulse la imagen del símbolo más ![Añadir iconos](images/grafana_plus_image.gif "Imagen del símbolo Más") y elija una función. Puede añadir una función para transformar, combinar y realizar cálculos sobre los datos disponibles para una métrica.
        
        Por ejemplo, puede añadir la función **alias(newName)** para añadir un alias a una métrica. Este alias se utiliza para mostrar una serie de caracteres en lugar del nombre de la métrica en la descripción que se muestra en el gráfico.
        
        Para añadir un alias a una métrica, siga estos pasos:
        
        1. Pulse el símbolo más.
        2. Seleccione **Especial**. 
        3. Seleccione **alias**.
        4. Escriba una serie de caracteres, como por ejemplo `Mi métrica de ejemplo`.


## Paso 4: Guardar el panel de control para utilizarlo más adelante
{: #step44}

Realice los siguientes pasos:

1. Pulse la imagen de guardar panel de control ![Imagen Guardar panel de control](images/grafana_save_image.gif "Imagen Guardar panel de control").
2. Escriba el nombre del panel de control.
3. Pulse **Guardar**.
