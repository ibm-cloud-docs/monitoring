---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-22"

keywords: Sysdig, IBM Cloud, monitoring, network traffic, firewall

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

 
# Gestione del traffico di rete per le configurazioni del firewall personalizzate
{: #network}

Quando disponi di un ulteriore firewall configurato o hai personalizzato le impostazioni del firewall nella tua infrastruttura {{site.data.keyword.cloud_notm}} (SoftLayer), devi consentire il traffico di rete in uscita al servizio {{site.data.keyword.mon_full_notm}}. 
{:shortdesc}


## Endpoint di inserimento
{: #network_send}

Per inviare i dati della metrica al servizio {{site.data.keyword.mon_full_notm}}, devi definire la seguente regola del firewall nel tuo host:

| Regione      | Endpoint di inserimento                                | Indirizzi IP pubblici               | Porte    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `US South`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | TCP 6443 | 
{: caption="Tabella 1. Indirizzi IP per inviare le metriche" caption-side="top"}



## Endpoint IU Web
{: #network_ui}

Per accedere all'IU web {{site.data.keyword.mon_full_notm}}, devi definire la seguente regola del firewall nel tuo host:

| Regione      | Endpoint IU Web                                   | Indirizzi IP pubblici                                    | Porte   |
|-------------|---------------------------------------------------|--------------------------------------------------------|---------|
| `US South`  | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
{: caption="Tabella 2. Indirizzi IP per accedere all'IU web {{site.data.keyword.mon_full_notm}}" caption-side="top"}


