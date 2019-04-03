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


# Configuración de métricas de CPU para un contenedor en Grafana
{: #config_cpu_containers}

En {{site.data.keyword.Bluemix}}, las métricas de CPU seleccionadas para un contenedor se recopilan automáticamente. Para supervisarlas mediante {{site.data.keyword.monitoringlong}}, debe definir una consulta de Grafana. 
{:shortdesc}

Para obtener una lista de las métricas de CPU que se recopilan automáticamente, consulte [Métricas de CPU para contenedores](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers).


## Paso 1: Recopilar los datos para el contenedor que desea supervisar
{: #step15}

Obtenga la información siguiente para el contenedor que desea supervisar:

* **Región** donde se está ejecutando el clúster.
* **Nombre de clúster** donde se está ejecutando el contenedor. 	
* **Espacio de nombres** donde se despliega el contenedor. 

    Un espacio de nombres se utiliza para agrupar recursos de clúster.
	
* **Nombre de pod** que está asociado con el contenedor que desea supervisar. 

    Un pod define un grupo de 1 o más contenedores, con almacenamiento y red compartidos, y detalles sobre cómo ejecutar los contenedores en el clúster.
	
* **Nombre de contenedor** del contenedor que desea supervisar.

Descubra si las métricas se reenvían a un dominio de espacio o al dominio de cuenta.

Para identificar dónde reenvía el clúster las métricas, ejecute el mandato siguiente:

```
$ ibmcloud cs cluster-get ClusterName --json
```
{: codeblock}

donde *ClusterName* es el nombre del clúster.

En la salida, los campos siguientes proporcionan la información sobre dónde se reenvían métricas:

* **logOrg** define el ID de una organización de CF.
* **logOrgName** define el nombre de una organización de CF.
* **logSpace** define el ID de un espacio de CF.
* **logSpaceName** define el nombre de un espacio de CF.

Si los campos están vacíos, las métricas se reenviarán al dominio de la cuenta.
Si los campos tienen una organización de CF y un espacio de CF establecidos, las métricas se reenviarán al dominio de espacio asociado con este espacio.

## Paso 2: Iniciar Grafana
{: #step24}

Inicie Grafana desde un navegador. Para obtener más información, consulte [Navegación al panel de control de Grafana desde un navegador web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).

Asegúrese de que, en Grafana, haya iniciado sesión en la cuenta donde el clúster está en ejecución. 

1. Desde un navegador, inicie Grafana. 

    Especifique el URL del servicio {{site.data.keyword.monitoringshort}} para la región en la que ha creado el clúster. 
    
    Para obtener los URL por región, consulte [URL para el servicio de supervisión](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

    Por ejemplo, para la región EE.UU. sur, inicie: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Establezca el dominio de {{site.data.keyword.monitoringshort}} donde puede ver las métricas de clúster.

    En Grafana, seleccione el ID. A continuación, compruebe que está en la cuenta correcta, y elija un dominio.

    Los clústeres que tienen un espacio de CF asociado reenvían métricas al dominio de métricas de espacio. Seleccione `Dominio = espacio`, y la organización y el espacio asociados con el clúster.

    Los clústeres creados a nivel de cuenta reenvían métricas al dominio de métricas de la cuenta. Seleccione `Dominio = cuenta`




## Paso 3: Definir una consulta en Grafana para una métrica de CPU
{: #step33}

Realice los pasos siguientes para crear un panel de control de Grafana y definir una consulta para supervisar el uso de CPU de un contenedor:

1. Cree un panel de control nuevo.

    * Seleccione el conmutador de la barra de menús lateral ![Barra de menús lateral de Grafana](images/grafana_settings.gif "Barra de menús lateral de Grafana").
    * Seleccione **Paneles de control**.
    * Pulse **Nuevo**

    Se abre un panel de control. El panel de control incluye una fila vacía que está lista para la configuración.

2. Añada un panel *Gráfico* para supervisar la métrica CPU para un pod.

    1. Seleccione **Gráfico**.

    2. Pulse en el título del gráfico y seleccione **editar**.

        Se abre el separador *Métricas*. Aquí puede ver el origen de datos predeterminado.

3. Defina la consulta que filtra los datos que se muestran en el gráfico. 

    Para obtener información sobre el formato de la consulta, consulte [Formato de consulta para las métricas de CPU recopiladas para contenedores](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers).

    En el separador *Métricas*, seleccione **Añadir consulta**. </br>Se añade una entrada de consulta. Cada consulta está etiquetada con una letra.
	
	Siga los siguientes pasos para definir la consulta:
	
    1. Pulse **Seleccionar métrica** para especificar el origen y, a continuación, elija `ibmcloud`.
    
    2. Pulse **Seleccionar métrica** para especificar el tipo de nube y, a continuación, elija `public`.
    
    3. Pulse **Seleccionar métrica** para especificar el nombre del servicio y elija `containers-kubernetes`.
	
    4. Pulse **Seleccionar métrica** para especificar la región y, a continuación, elija la región donde el clúster está en ejecución. Por ejemplo, `us-south`.
    
    5. Pulse **Seleccionar métrica** para especificar el nombre de clúster y, a continuación, elija el nombre del clúster donde el contenedor está en ejecución.
		
	6. Pulse **Seleccionar métrica** para especificar el origen de métrica. Seleccione **contenedor**.
		
	7. Pulse **Seleccionar métrica** para especificar el espacio de nombres. A continuación, escriba el nombre del espacio de nombres en el clúster asociado con el contenedor.
		
	8. Pulse **Seleccionar métrica** para especificar el nombre de pod.
	
	9. Pulse **Seleccionar métrica** para especificar el nombre de contenedor del contenedor que desea supervisar.
	
	10. Pulse **Seleccionar métrica** para especificar el tipo de métrica y, a continuación, pulse **Seleccionar métrica** para especificar el subtipo de métrica.
	
	    Para obtener una lista de las métricas de CPU, consulte [Métricas de CPU para contenedores](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers).
	
	11. Pulse la imagen del símbolo más ![Añadir iconos](images/grafana_plus_image.gif "Imagen del símbolo Más") y elija una función. Puede añadir una función para transformar, combinar y realizar cálculos sobre los datos disponibles para una métrica.

        Por ejemplo, puede añadir la función **alias(newName)** para añadir un alias a una métrica. Este alias se utiliza para mostrar una serie de caracteres en lugar del nombre de la métrica en la descripción que se muestra en el gráfico.

        Para añadir un alias a una métrica, siga estos pasos:

        1. Pulse el símbolo más.
        2. Seleccione **Especial**.
        3. Seleccione **alias**.
        4. Escriba una serie de caracteres, como por ejemplo `Mi métrica de ejemplo`.


## Paso 4: Guardar el panel de control para utilizarlo más adelante
{: #step43}

Realice los siguientes pasos:

1. Pulse la imagen de guardar panel de control ![Imagen Guardar panel de control](images/grafana_save_image.gif "Imagen Guardar panel de control").
2. Escriba el nombre del panel de control.
3. Pulse **Guardar**.

