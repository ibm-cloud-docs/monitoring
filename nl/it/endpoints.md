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


# Regioni ed endpoint
{: #endpoints}

Elenco delle regioni e degli endpoint supportati per il servizio {{site.data.keyword.mon_full_notm}}:
{:shortdesc}

## Regioni
{: #endpoints_regions}

Il servizio {{site.data.keyword.mon_full_notm}} è disponibile nelle seguenti regioni:

| Regione                | Ubicazione  | 
|-----------------------|-----------|
| `US South`            | Dallas    | 
| `EU-DE`               | Francoforte | 
| `EU-GB`               | Londra    | 
{: caption="Tabella 1. Elenco di regioni in cui è disponibile il servizio" caption-side="top"} 

Al momento, **Francoforte** e **EU GB** sono ubicazioni **non** gestite dall'Unione Europea. Per ulteriori informazioni, consulta [Abilitazione dell'impostazione Supportato UE](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported).
{: important}


## Endpoint raccoglitore Sysdig
{: #endpoints_ingestion}

Gli endpoint del **Raccoglitore Sysdig** sono endpoint di inserimento che puoi utilizzare per inviare i dati.

La seguente tabella elenca gli **endpoint del raccoglitore Sysdig** disponibili per regione:

| Regione        | Endpoint                                                  | Porta |
|---------------|-----------------------------------------------------------|------|
| `US South`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU-DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU-GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
{: caption="Tabella 2. Elenco degli endpoint di inserimento" caption-side="top"} 



## Endpoint Sysdig
{: #endpoints_sysdig}

La seguente tabella elenca gli **endpoint Sysdig** disponibili per regione:

| Regione       | Endpoint                                                  | Porta |
|--------------|-----------------------------------------------------------|------|
| `US South`   | `https://us-south.monitoring.cloud.ibm.com `              | https (TLS) 443 |  
| `EU-DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
| `EU-GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
{: caption="Tabella 3. Elenco degli endpoint Sysdig" caption-side="top"} 


