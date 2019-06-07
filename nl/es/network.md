---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, network traffic, firewall

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

 
# Gestión del tráfico de red para configuraciones de cortafuegos personalizadas
{: #network}

Si tiene configurado un cortafuegos adicional o si ha personalizado los valores de cortafuegos en la infraestructura de {{site.data.keyword.cloud_notm}}, debe permitir el tráfico de red de salida al servicio {{site.data.keyword.mon_full_notm}}. 
{:shortdesc}


## Puntos finales de ingestión
{: #network_send}

Para enviar datos de métricas al servicio {{site.data.keyword.mon_full_notm}}, debe definir la siguiente regla de cortafuegos en el host:

| Región      | Punto final de ingestión                                | Direcciones IP públicas                                     | Puertos    |
|-------------|---------------------------------------------------|---------------------------------------------------------|----------|
| `EE. UU. sur`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | TCP 6443 | 
| `UE DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | TCP 6443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | TCP 6443 | 
{: caption="Tabla 1. Direcciones IP para enviar datos a {{site.data.keyword.mon_full_notm}}" caption-side="top"}


## Puntos finales de IU web
{: #network_ui}

Para acceder a la interfaz de usuario web de {{site.data.keyword.mon_full_notm}}, debe definir la siguiente regla de cortafuegos en el host:

| Región      | Punto final de IU web                                   | Direcciones IP públicas                                       | Puertos   |
|-------------|---------------------------------------------------|-----------------------------------------------------------|---------|
| `EE. UU. sur`  | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70        | https (TLS) 443 | 
| `UE DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38     | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238       | https (TLS) 443 |
{: caption="Tabla 2. Direcciones IP para acceder a la interfaz de usuario web de {{site.data.keyword.mon_full_notm}}" caption-side="top"}


