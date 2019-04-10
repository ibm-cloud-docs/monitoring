---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-22"

keywords: Sysdig, IBM Cloud, monitoring, regions, endpoints

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


# Regiones y puntos finales
{: #endpoints}

Lista de regiones y puntos finales admitidos para el servicio {{site.data.keyword.mon_full_notm}}:
{:shortdesc}

## Regiones
{: #endpoints_regions}

El servicio {{site.data.keyword.mon_full_notm}} está disponible en las regiones siguientes:

| Región                | Ubicación  | 
|-----------------------|-----------|
| `EE. UU. sur`            | Dallas    | 
| `UE-DE`               | Frankfurt | 
| `EU-GB`               | Londres    | 
{: caption="Tabla 1. Lista de regiones en las que está disponible el servicio" caption-side="top"} 

Actualmente, **Frankfurt** y **EU GB** son las ubicaciones que **no** están gestionadas por la UE. Para obtener más información, consulte [Habilitación del valor Soporte en la UE](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported).
{: important}


## Puntos finales de Sysdig Collector
{: #endpoints_ingestion}

Los puntos finales de **Sysdig Collector** son puntos finales de ingestión que puede utilizar para enviar datos.

La tabla siguiente contiene la lista de los **puntos finales de Sysdig Collector** disponibles por región:

| Región        | Punto final                                                  | Puerto |
|---------------|-----------------------------------------------------------|------|
| `EE. UU. sur`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `UE-DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU-GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
{: caption="Tabla 2. Lista de puntos finales de ingestión" caption-side="top"} 



## Puntos finales de Sysdig
{: #endpoints_sysdig}

La tabla siguiente contiene la lista de los **puntos finales de Sysdig** disponibles por región:

| Región       | Punto final                                                  | Puerto |
|--------------|-----------------------------------------------------------|------|
| `EE. UU. sur`   | `https://us-south.monitoring.cloud.ibm.com`              | https (TLS) 443 |  
| `UE-DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
| `EU-GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
{: caption="Tabla 3. Lista de puntos finales de Sysdig" caption-side="top"} 


