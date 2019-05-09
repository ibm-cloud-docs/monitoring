---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

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


# Regions and endpoints
{: #endpoints}

List of supported regions and endpoints for the {{site.data.keyword.mon_full_notm}} service:
{:shortdesc}

## Regions
{: #endpoints_regions}

The {{site.data.keyword.mon_full_notm}} service is available in the following regions:

| Region                | Location  | 
|-----------------------|-----------|
| `US SOUTH`            | Dallas    | 
| `EU-DE`               | Frankfurt | 
| `EU-GB`               | London    | 
| `JP-TOK`              | Tokyo     |
{: caption="Table 1. List of regions where the service is available" caption-side="top"} 

Currently, **Frankfurt** and **EU GB** are locations that are **not** EU-managed. For more information, see [Enabling the EU Supported setting](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported).
{: important}


## Sysdig Collector endpoints
{: #endpoints_ingestion}

**Sysdig Collector** endpoints are ingestion endpoints that you can use to send data.

The following table list the **Sysdig Collector endpoints** that are available per region:

| Region        | Endpoint                                                  | Port |
|---------------|-----------------------------------------------------------|------|
| `US South`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU-DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU-GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `JP-TOK`      | `ingest.jp-tok.monitoring.cloud.ibm.com`                  | TCP 6443 | 
{: caption="Table 2. List of ingestion endpoints" caption-side="top"} 



## Sysdig endpoints
{: #endpoints_sysdig}

The following table list the **Sysdig endpoints** that are available per region:

| Region       | Endpoint                                                  | Port |
|--------------|-----------------------------------------------------------|------|
| `US South`   | `https://us-south.monitoring.cloud.ibm.com`               | https (TLS) 443 |  
| `EU-DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
| `EU-GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
| `JP-TOK`      | `https://jp-tok.monitoring.cloud.ibm.com`                 | https (TLS) 443 |
{: caption="Table 3. List of Sysdig endpoints" caption-side="top"} 


