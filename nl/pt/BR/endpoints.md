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


# Regiões e terminais
{: #endpoints}

Lista de regiões e terminais suportados para o serviço {{site.data.keyword.mon_full_notm}}:
{:shortdesc}

## Regiões
{: #endpoints_regions}

O serviço {{site.data.keyword.mon_full_notm}} está disponível nas regiões a seguir:

| Região                | Localização  | 
|-----------------------|-----------|
| `US SOUTH`            | Dallas    | 
| `EU-DE`               | Frankfurt | 
| `EU-GB`               | Londres    | 
| `JP-TOK`              | Tokyo     |
{: caption="Tabela 1. Lista de regiões nas quais o serviço está disponível" caption-side="top"} 

Atualmente, **Frankfurt** e **EU GB** são locais **não** gerenciados pela UE. Para obter mais informações, consulte [Ativando a configuração Suportado pela UE](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported).
{: important}


## Terminais do Sysdig Collector
{: #endpoints_ingestion}

Os terminais **Sysdig Collector** são terminais de ingestão que podem ser usados para enviar dados.

A tabela a seguir lista os **terminais de coletor do Sysdig** que estão
disponíveis por região:

| Região        | Terminal                                                  | Porta |
|---------------|-----------------------------------------------------------|------|
| `US South`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `JP TOK`      | `ingest.jp-tok.monitoring.cloud.ibm.com`                  | TCP 6443 | 
{: caption="Tabela 2. Lista de terminais de ingestão" caption-side="top"} 



## Terminais de Sysdig
{: #endpoints_sysdig}

A tabela a seguir lista os **terminais do Sysdig** que estão disponíveis por região:

| Região       | Terminal                                                  | Porta            |
|--------------|-----------------------------------------------------------|-----------------|
| `US South`   | `https://us-south.monitoring.cloud.ibm.com `               | HTTPS (TLS) 443 |  
| `EU DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `EU GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `JP TOK`     | `https://jp-tok.monitoring.cloud.ibm.com`                 | HTTPS (TLS) 443 |
{: caption="Tabela 3. Lista de terminais Sysdig" caption-side="top"} 


