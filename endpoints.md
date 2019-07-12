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

All connections to the Sysdig collector are available via the public network and the private network. 

Public endpoints send metrics to Sysdig using the public network. Your environment needs to have internet access to use the public endpoint.

Private endpoints are not accessible from the public internet. All traffic is routed to the IBM Cloud private network and an internet connection is not required to send metrics to your Sysdig instance. If you wish to use private endpoints, you need to ensure that VRF and Service Endpoints features are enabled for your account. Instructions can be found [here](https://cloud.ibm.com/docs/account?topic=account-vrf-service-endpoint)

Once the account is VRF and Service Endpoint enabled, the Sysdig agent can be configured to use the private network by using the Private Endpoint as the ingestion URL.

A list of supported regions and public and private endpoints for the {{site.data.keyword.mon_full_notm}} service:
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
| `US EAST`             | Washington|
{: caption="Table 1. List of regions where the service is available" caption-side="top"} 

Currently, **Frankfurt** and **EU GB** are locations that are **not** EU-managed. For more information, see [Enabling the EU Supported setting](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported).
{: important}


## Sysdig Collector endpoints
{: #endpoints_ingestion}

**Sysdig Collector** endpoints are ingestion endpoints that you can use to send data.

The following table lists the **Sysdig Collector endpoints** that are available per region:

| Region        | Public Endpoint                                 | Private Endpoint                                      | Port     |
|---------------|-------------------------------------------------|-------------------------------------------------------|----------|
| `US South`    | `ingest.us-south.monitoring.cloud.ibm.com`      | `private.ingest.us-south.monitoring.cloud.ibm.com`    | TCP 6443 |
| `EU DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`         | `private.ingest.eu-de.monitoring.cloud.ibm.com`       | TCP 6443 |
| `EU GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`         | `private.ingest.eu-gb.monitoring.cloud.ibm.com`       | TCP 6443 |
| `JP TOK`      | `ingest.jp-tok.monitoring.cloud.ibm.com`        | `private.ingest.jp-tok.monitoring.cloud.ibm.com`      | TCP 6443 |
| `US East`     | `ingest.us-east.monitoring.cloud.ibm.com`       | `private.ingest.us-east.monitoring.cloud.ibm.com`     | TCP 6443 |
{: caption="Table 2. List of ingestion endpoints" caption-side="top"} 

**NOTE:** 
Ensure that VRF and Service Endpoints is enabled for your account. Instructions can be found [here](https://cloud.ibm.com/docs/account?topic=account-vrf-service-endpoint)

## Sysdig endpoints
{: #endpoints_sysdig}

The following table lists the **Sysdig endpoints** that are available per region:

| Region       | Endpoint                                                  | Port            |
|--------------|-----------------------------------------------------------|-----------------|
| `US South`   | `https://us-south.monitoring.cloud.ibm.com`               | HTTPS (TLS) 443 |  
| `EU DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `EU GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | HTTPS (TLS) 443 |
| `JP TOK`     | `https://jp-tok.monitoring.cloud.ibm.com`                 | HTTPS (TLS) 443 |
| `US East`    | `https://us-east.monitoring.cloud.ibm.com`                | HTTPS (TLS) 443 |
{: caption="Table 3. List of Sysdig endpoints" caption-side="top"} 


