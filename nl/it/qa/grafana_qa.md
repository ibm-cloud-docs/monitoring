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



# Domande frequenti (FAQ) utilizzando Grafana
{: #grafana_qa}

Queste sono le risposte alle domande più frequenti sull'utilizzo di Grafana con il servizio {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [Non posso visualizzare gli avvisi che ho definito utilizzando l'API Avvisi nel mio dashboard Grafana](/docs/services/cloud-monitoring/qa/grafana_qa.html#alerts1)
* [Ricevo un errore BXNMSAL41E quando tento di salvare una modifica che ho effettuato nel mio dashboard Grafana](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL41E)
* [Ricevo un errore BXNMSAL36E quando tento di salvare una modifica dopo aver aggiunto un avviso al mio dashboard Grafana](/docs/services/cloud-monitoring/qa/grafana_qa.html#BXNMSAL36E)
* [Quando accedo alla IU web del servizio di monitoraggio ricevo un errore 404](/docs/services/cloud-monitoring/qa/grafana_qa.html#404)
* [Ho appena caricato i dati json per un dashboard Grafana, perché non vedo più la barra di scorrimento?](/docs/services/cloud-monitoring/qa/grafana_qa.html#2)


## Non posso visualizzare gli avvisi che ho definito utilizzando l'API Avvisi nel mio dashboard Grafana
{: #alerts1}

Gli avvisi che definisci utilizzando l'API Avvisi non vengono visualizzati nella scheda degli avvisi in Grafana. Per visualizzare gli avvisi in Grafana, devi definirli in un dashboard Grafana.

Per ulteriori informazioni, vedi [Configurazione degli avvisi in Grafana](/docs/services/cloud-monitoring/alerts/config_alerts_grafana.html#config_alerts_grafana).

## Ricevo un errore BXNMSAL41E quando tento di salvare una modifica che ho effettuato nel mio dashboard Grafana
{: #BXNMSAL41E}

Puoi definire gli avvisi e i canali di notifica in Grafana. Se elimini un canale di notifica in Grafana e non aggiorni la regola per rimuovere tale canale di notifica, ricevi un errore **BXNMSAL41E** quando tenti di salvare il tuo dashboard Grafana.

Per risolvere il problema, aggiorna la regola utilizzando l'API Avvisi e riprova a salvare il dashboard. Quando aggiorni la regola, rimuovi il canale di notifica che è stato eliminato.

Per ulteriori informazioni, vedi [API Avvisi](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction).

## Ricevo un errore BXNMSAL36E quando tento di salvare una modifica dopo aver aggiunto un avviso al mio dashboard Grafana
{: #BXNMSAL36E}

Se raggiungi la quota per il dominio in cui stai monitorando le metriche nel servizio {{site.data.keyword.monitoringshort}}, ricevi il seguente errore: **BXNMSAL36E**

Aggiorna il tuo piano e ritenta.

Per ulteriori informazioni su come aggiornare il tuo piano, vedi [Modifica del piano](/docs/services/cloud-monitoring/plan/change_plan.html#change_plan).


## Quando accedo alla IU web del servizio di monitoraggio utilizzando il modello di autenticazione UUA ricevo un errore 404
{: #404}

Se ricevi un errore 404 quando provi ad accedere alla IU web del servizio {{site.data.keyword.monitoringshort}} (Grafana), verifica che lo spazio esista e che tu abbia accesso ad esso.

Se utilizzi il [modello di autenticazione UAA](/docs/services/cloud-monitoring/security/auth_uaa.html#auth_uaa) per accedere al servizio {{site.data.keyword.monitoringshort}}, devi utilizzare lo stesso ID utente e password utilizzati per accedere alla console {{site.data.keyword.Bluemix_notm}}. 

Per verificare di disporre dell'accesso all'account, all'organizzazione e allo spazio a cui vuoi connetterti, accedi alla console {{site.data.keyword.Bluemix_notm}} e passa allo spazio. 

Per verificare di avere accesso a tale spazio, puoi utilizzare anche la riga di comando. Immetti il seguente comando per accedere a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}:

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

Segui le istruzioni. Immetti le tue credenziali {{site.data.keyword.Bluemix_notm}}, seleziona un'organizzazione e uno spazio.


## Ho appena caricato i dati JSON per un dashboard Grafana, perché non vedo più la barra di scorrimento?
{: #2}

Esiste un bug in Grafana che nasconde la barra di scorrimento dopo aver importato un dashboard. 

Per visualizzare la barra di scorrimento, salva il dashboard dopo averlo importato. 








