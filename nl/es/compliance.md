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


# Conformidad
{: #compliance}

[{{site.data.keyword.Bluemix}} proporciona una plataforma y servicios de Cloud que se crean en los estrictos estándares de seguridad de IBM.](/docs/security/compliance.html#compliance). El servicio {{site.data.keyword.monitoringlong}} es un servicio DevOps creado para {{site.data.keyword.Bluemix_notm}}. 
{:shortdesc}


## Reglamento General de Protección de Datos

El Reglamento General de Protección de Datos (GDPR) busca crear una infraestructura de leyes de protección de datos armonizada en toda la UE y tiene como objetivo volver a proporcionar el control a los ciudadanos de sus datos personales, a la vez que impone reglas estrictas a la hora de alojar y ‘procesar’ estos datos, en cualquier lugar del mundo. La Regulación también introduce reglas relacionadas con el movimiento libre de datos personales dentro y fuera de la UE. 

**Aviso:** El servicio {{site.data.keyword.monitoringshort}} almacena y muestra métricas desde recursos de Cloud que se ejecutan en la cuenta en {{site.data.keyword.Bluemix_notm}}, y métricas que podría enviar desde fuera de {{site.data.keyword.Bluemix_notm}}. La información personal (PI) no debe estar incluida en ninguna de las entradas de métricas almacenadas en {{site.data.keyword.monitoringshort}}, ya que otros usuarios de su empresa pueden acceder a estos datos, así como {{site.data.keyword.IBM_notm}} puede dar soporte al Servicio de Cloud.

### Regiones
{: #regions}

El servicio {{site.data.keyword.monitoringshort}} está en conformidad con GDPR en las regiones Públicas de {{site.data.keyword.Bluemix_notm}} donde el servicio esté disponible.


### Retención de datos
{: #data_retention}

El servicio {{site.data.keyword.monitoringshort}} almacena métricas durante 15 días para el plan de servicio estándar o lite, y durante 45 días para el plan premium.


### Supresión de datos
{: #data_deletion}

Tenga en cuenta la información siguiente:

* Las métricas se suprimirán automáticamente tras 15 días para el plan estándar o lite del servicio {{site.data.keyword.monitoringshort}}.
* Las métricas se suprimirán automáticamente tras 45 días para el plan premium del servicio {{site.data.keyword.monitoringshort}}.
* Las métricas que no estén activas se suprimirán automáticamente tras 7 días.


 En cualquier momento, puede utilizar la API de métricas para suprimir las métricas. 



### Más información
{: #info}

Para obtener más información, consulte:

[Conformidad de seguridad de {{site.data.keyword.Bluemix_notm}}](/docs/security/compliance.html#compliance)

[GDPR - página oficial de {{site.data.keyword.IBM_notm}}](https://www.ibm.com/data-responsibility/gdpr/)



