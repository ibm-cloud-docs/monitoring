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


# Regionen und Endpunkte
{: #endpoints}

Liste der unterstützten Regionen und Endpunkte für den {{site.data.keyword.mon_full_notm}}-Service:
{:shortdesc}

## Regionen
{: #endpoints_regions}

Der {{site.data.keyword.mon_full_notm}}-Service ist in den folgenden Regionen verfügbar:

| Region                | Standort  | 
|-----------------------|-----------|
| `USA (Süden)`            | Dallas    | 
| `EU-DE`               | Frankfurt | 
| `EU-GB`               | London    | 
{: caption="Tabelle 1. Liste der Regionen, in denen der Service verfügbar ist" caption-side="top"} 

**Frankfurt** und **EU GB** sind zum gegenwärtigen Zeitpunkt **keine** Standorte mit EU-bezogener Verwaltung. Weitere Informationen hierzu finden Sie im Abschnitt [Unterstützte EU-Einstellung aktivieren](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported).
{: important}


## Sysdig-Collector-Endpunkte
{: #endpoints_ingestion}

**Sysdig-Collector**-Endpunkte sind Aufnahmeendpunkte, die Sie zum Senden von Daten verwenden können.

In der folgenden Tabelle sind die **Sysdig-Collector-Endpunkte** aufgelistet, die pro Region verfügbar sind:

| Region        | Endpunkt                                                  | Port |
|---------------|-----------------------------------------------------------|------|
| `USA (Süden)`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU-DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU-GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
{: caption="Tabelle 2. Liste der Aufnahmeendpunkte" caption-side="top"} 



## Sysdig-Endpunkte
{: #endpoints_sysdig}

In der folgenden Tabelle sind die **Sysdig-Endpunkte** aufgelistet, die pro Region verfügbar sind:

| Region       | Endpunkt                                                  | Port |
|--------------|-----------------------------------------------------------|------|
| `USA (Süden)`   | `https://us-south.monitoring.cloud.ibm.com `              | https (TLS) 443 |  
| `EU-DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
| `EU-GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
{: caption="Tabelle 3. Liste der Sysdig-Endpunkte" caption-side="top"} 


