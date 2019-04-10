---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# Cómo trabajar con capturas
{: #captures}

Una captura es un archivo de rastreo que se puede generar para analizar lo que sucede en un host durante un periodo de tiempo. Por ejemplo, puede utilizar una captura para analizar cuellos de botella o interacciones de componentes. En el servicio {{site.data.keyword.mon_full_notm}}, puede crear, explorar, descargar y suprimir *capturas* correspondientes a nodos individuales. 
{:shortdesc}

Para obtener más información, consulte [Capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


## Creación de una captura
{: #captures_create}

Las capturas se crean en la vista *Explorar*.

Siga los pasos siguientes para crear un archivo de captura:

1. Vaya a la sección *EXPLORAR* de la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. Pulse el icono de conmutación de host ![icono de conmutación de host](images/switch_hosts.png).

3. Seleccione un host o un contenedor.

4. Pulse el icono de acciones ![icono con tres puntos](images/actions.png) y seleccione **Captura de Sysdig**.

    Se abre la ventana *Captura de Sysdig*.

5. En la ventana *Captura de Sysdig*, defina los parámetros siguientes:

    1. En el campo *Vía de acceso y nombre de captura*, especifique el nombre del archivo de captura. Puede dejar el valor predeterminado o modificarlo. El nombre predeterminado incluye la indicación de fecha y hora en que se ha creado la captura. 

    2. Establezca un *Intervalo de tiempo* para especificar el número de segundos para recopilar datos. El tiempo de captura predeterminado es de 15 segundos. El tiempo máximo de captura es de 86400 segundos (24 horas). 

    3. (Opcional) Añada un filtro para restringir la cantidad de información de rastreo que se recopila. 

6. Pulse **Iniciar captura**. Se envía una señal al agente de Sysdig para que inicie una captura y devuelva el archivo de rastreo resultante. 

7. Pulse **Ir a página de capturas** para ver la lista de capturas en la sección *Capturas* de la interfaz de usuario web. 

La página *Capturas* contiene una tabla que muestra el nombre del archivo de captura, el host del que se ha recuperado, el intervalo de tiempo y el tamaño de la captura. 

El estado de un archivo de captura puede ser uno de los siguientes:
* **Solicitado**: se está generando un archivo.
* **Cargado**: hay un archivo disponible para que se descargue y se analice.
* **Error**: no se ha generado un archivo porque se ha excedido el tiempo de espera, nunca se han recibido los datos o se ha producido un error del agente.



## Supresión de una captura
{: #captures_delete}

Siga los pasos siguientes para suprimir un archivo de captura:

1. Vaya a la sección *CAPTURAS* de la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifique y seleccione el archivo de captura que desea suprimir.
3. Pulse **Suprimir**.



## Exploración de una captura
{: #captures_explore}

Siga los pasos siguientes para explorar un archivo de captura:

1. Vaya a la sección *CAPTURAS* de la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifique y seleccione el archivo de captura que contiene los datos correspondientes al host que desea analizar.
3. Pulse **EXPLORAR**.



## Descarga de una captura
{: #captures_download}

Siga los pasos siguientes para descargar un archivo de captura:

1. Vaya a la sección *CAPTURAS* de la interfaz de usuario web. Para obtener más información sobre cómo iniciar la interfaz de usuario web, consulte [Navegación a la interfaz de usuario web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifique y seleccione el archivo de captura que contiene los datos que desea descargar.
3. Pulse **DESCARGAR**.


## Chisels
{: #captures_chisels}

Un chisel de Sysdig es un script escrito en Lua, un lenguaje de script. Puede utilizarlo para analizar los datos de un archivo de captura. 

Para obtener más información acerca de cómo utilizar un chisel, consulte esta guía del usuario: [Chisels User Guide ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}



## Csysdig
{: #captures_csysdig}

Csysdig es una herramienta de código abierto para Linux que está diseñada para la supervisión y la depuración. Puede utilizarla para analizar archivos de captura. 

Para más información, consulte los siguientes recursos:
* [Blog de Csysdig ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Vídeo de Csysdig ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


