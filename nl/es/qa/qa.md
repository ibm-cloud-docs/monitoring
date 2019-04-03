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



# Preguntas frecuentes y respuestas
{: #qa}

Aquí encontrará las respuestas a las preguntas más comunes sobre el servicio {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [¿Por qué no puedo ver mis datos antiguos para una métrica para la que no he enviado valores de métricas últimamente?](#qa31)


## ¿Por qué no puedo ver datos antiguos para una métrica para la que no he enviado valores de métricas últimamente?
{: #qa31}

{{site.data.keyword.monitoringshort}} suprime todos los datos correspondientes a una vía de acceso a una métrica que parece transitoria por naturaleza, es decir, una métrica en la que no se ha grabado nada durante los últimos 7 días. 

Por ejemplo:

* Cuando se suprime un contenedor, las métricas asociadas a dicho contenedor se guardan durante 7 días; transcurrido este periodo, las métricas se suprimen.
* Si tiene un indicador de statsd denominado `<space_id>.test.statsd.gauge-hello` y no graba en el mismo durante una semana, la métrica se identificará como transitoria y dicha métrica se suprimirá, junto a toda su información histórica. 

