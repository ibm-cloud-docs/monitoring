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



# Domande e risposte frequenti
{: #qa}

Queste sono le risposte alle domande più frequenti sul servizio {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [Perché non riesco a visualizzare i miei vecchi dati per una metrica per la quale non ho inviato recentemente alcun valore?](#qa31)


## Perché non riesco a visualizzare i miei vecchi dati per una metrica per la quale non ho inviato recentemente alcun valore?
{: #qa31}

{{site.data.keyword.monitoringshort}} elimina tutti i dati per un percorso di metrica che sembra essere di natura transitoria identificando le metriche che non sono state scritte negli ultimi 7 giorni. 

Ad esempio:

* Quando un contenitore viene eliminato, le metriche associate a tale contenitore rimangono per 7 giorni, dopo di che vengono eliminate.
* Se hai un misuratore statsd denominato `<space_id>.test.statsd.gauge-hello` e non scrivi in esso per una settimana, la metrica verrà identificata come transitoria e quindi verrà eliminata insieme a tutte le relative informazioni sulla cronologia. 

