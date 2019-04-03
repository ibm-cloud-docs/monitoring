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

# Envío de datos mediante el plugin Supervisión (collectd)
{: #conf_monitoring_plugin}

Puede configurar collectd para recopilar métricas en un entorno. Utilice el plugin de {{site.data.keyword.monitoringshort}} para enviar dichas métricas a un dominio de espacio desde su entorno. 
{: shortdesc}

La figura siguiente muestra una vista de nivel alto sobre cómo utilizar el plugin de {{site.data.keyword.monitoringshort}} para enviar métricas al servicio {{site.data.keyword.monitoringshort}}:

![Vista de nivel alto sobre cómo utilizar el plugin de {{site.data.keyword.monitoringshort}} ](images/monitoring_plugin_ov.png "Vista de nivel alto sobre cómo utilizar el plugin de {{site.data.keyword.monitoringshort}} ")



## Instalación del plugin de Supervisión
{: #install}

En un terminal, siga los pasos siguientes: 

1. (Requisito previo) Instalar la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa).
   
   Si la CLI está instalada, continúe en el paso siguiente.
	
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
	ibmcloud target -o MyOrg -s MySpace
    ```
    {: codeblock}

    Siga las instrucciones. Escriba sus credenciales de {{site.data.keyword.Bluemix_notm}}, seleccione una organización y un espacio.

### Paso 1: Instalar collectd
{: #collectd}

Como administrador, realice los pasos siguientes para instalar collectd:

1.	Inicie sesión como usuario root. 

    ```
    sudo -s
    ```
    {: codeblock}

2.	Instale el paquete Network Time Protocol (NTP) para sincronizar la hora de los registros. 

    Por ejemplo, para un sistema Ubuntu, compruebe si `timedatectl status` muestra *Network time on: yes*. Si es así, significa que el sistema Ubuntu ya está configurado para utilizar ntp y puede saltarse este paso.
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    Siga los siguientes pasos para instalar ntp en un sistema Ubuntu:

    1.	Ejecute el siguiente mandato para actualizar los paquetes. 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	Ejecute el siguiente mandato para instalar el paquete ntp. 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	Ejecute el siguiente mandato para instalar el paquete ntpdate. 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	Ejecute el siguiente mandato para detener el servicio 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	Ejecute el siguiente mandato para sincronizar el reloj del sistema. 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        El resultado confirma que se ha ajustado la hora, por ejemplo:
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	Ejecute el siguiente mandato para volver a iniciar ntpd. 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        El resultado confirma que el servicio se está iniciando.

3. Instale collectd. Ejecute el mandato siguiente:

    ```
	apt-get install collectd 
	```
	{: codeblock}


### Paso 2: Instale el plugin Supervisión
{: #plugin}

Siga estos pasos para instalar el plugin de {{site.data.keyword.monitoringshort}}:

1. 	Inicie sesión como usuario root. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2. Añada el repositorio del servicio {{site.data.keyword.monitoringshort}}. Ejecute el mandato siguiente:

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
   {: codeblock}
   
3. Instale el plugin. Ejecute el mandato siguiente:

    ```
	apt-get install ibmcloud-monitoring
	```
	{: codeblock}


## Configure el plugin Supervisión
{: #configure}

Para configurar el plugin de {{site.data.keyword.monitoringshort}}, complete los pasos siguientes:
	
### Paso 1: Asigne una política de IAM al usuario
{: #iam_policy}

Para enviar métricas a un dominio, es necesario otorgar un rol de IAM al ID de usuario con permisos para enviar métricas al servicio de supervisión.
 
* Los permisos se establecen asignando una política de IAM al usuario en IBM Cloud. 
* Los siguientes roles de IAM permiten a un usuario enviar métricas: *Administrador*, *Editor*, *Operador*. 

Para asignar a un usuario una política de IAM, elija uno de los métodos siguientes:

* Mediante la IU de {{site.data.keyword.Bluemix_notm}}: Para obtener más información, consulte [Asignación de una política de IAM a un usuario mediante la IU de {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui).
* Mediante la línea de mandatos: Para obtener más información, consulte [Asignación de una política de IAM a un usuario mediante la línea de mandatos](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_commandline).
 
### Paso 2: Obtener una clave de API
{: #api_key}
 
Para enviar métrica a un espacio, debe disponer de una clave de API para autenticarse con el servicio {{site.data.keyword.monitoringshort}}.

Para obtener más información sobre cómo obtener una clave de API, consulte [Obtención de una clave de API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
En el mismo terminal en el que ha iniciado sesión en {{site.data.keyword.Bluemix_notm}}, establezca la variable APIKEY para la señal.

Por ejemplo,

```
export APIKEY="kjshdgf.....ldkdjdj"
```
{: screen}
	
### Paso 3: Obtenga información acerca del punto final
{: #endpoint}

Para determinar el punto final de {{site.data.keyword.monitoringshort}} al que va a enviar las métricas, consulte la lista de puntos finales por región, consulte [Puntos finales](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints) e identifique uno para la región a la que desea enviar las métricas.

En el mismo terminal en el que ha iniciado sesión en {{site.data.keyword.Bluemix_notm}}, establezca la variable **METRIC_ENDPOINT**. Por ejemplo,

```
export METRIC_ENDPOINT="metrics.ng.bluemix.net"
```
{: screen}



### Paso 4: Obtenga información acerca del ID de dominio de espacio 
{: #domain}

Para obtener el ID de dominio del espacio, [obtener del GUID de espacio](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid). A continuación, establezca el ID de dominio como se indica a continuación: `s-SpaceID` donde SpaceID es el GUID del espacio.

En el mismo terminal en el que ha iniciado sesión en {{site.data.keyword.Bluemix_notm}}, establezca la variable SpaceID:

```
export SpaceID="kjshdgf.....ldkdjdj"
```
{: screen}



### Paso 5: Ejecute el script de configuración
{: #script}

Ejecute el script siguiente para configurar el plugin de {{site.data.keyword.monitoringshort}} para enviar métricas a un espacio:

```
/opt/ibmcloud_monitoring/configure -e $METRIC_ENDPOINT -a $APIKEY -s s-$SpaceID
```
{: codeblock}


El script añade automáticamente la stanza **Include** al archivo principal collectd.conf:

```
<LoadPlugin IBMCloudMonitoring>
   FlushInterval 60
</LoadPlugin>
<Plugin IBMCloudMonitoring>
  <Endpoint "ng">
     Host "metrics.ng.bluemix.net"
     Port 9095
     ApiKey "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
     SkipInternalPrefixForStatsd false
     RateCounter false
     ScopeId "s-cedc73c5-6d55-4193-a9de-378620d6fab5"
  </Endpoint>
</Plugin>
```
{: screen}


### Paso 6: Reinicie el daemon collectd
{: #restart}

Realice los siguientes pasos:

1. 	Inicie sesión como usuario root. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2.  Reinicio collectd.

   Si se ha añadido el daemon collectd como un servicio, ejecute el mandato siguiente:
	
	```
	service collectd restart
	```
	{: codeblock}

Las métricas que están habilitadas en collectd son las mismas que están disponibles en Grafana para su análisis.


