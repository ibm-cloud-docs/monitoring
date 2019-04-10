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


# Régions et noeuds finaux
{: #endpoints}

Liste des régions et noeuds finaux pris en charge pour le service {{site.data.keyword.mon_full_notm}} :
{:shortdesc}

## Régions
{: #endpoints_regions}

Le service {{site.data.keyword.mon_full_notm}} est disponible dans les régions suivantes :

| Région                | Emplacement  | 
|-----------------------|-----------|
| `Sud des Etats-Unis`            | Dallas    | 
| `EU-DE`               | Francfort | 
| `EU-GB`               | Londres   | 
{: caption="Tableau 1. Liste des régions où le service est disponible" caption-side="top"} 

Actuellement, **Francfort** et **EU GB** sont des emplacements qui ne sont **pas** gérés dans l'Union européenne. Pour plus d'informations, voir [Activation du paramètre Support dans l'Union européenne](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported).
{: important}


## Noeuds finaux de collecteur Sysdig
{: #endpoints_ingestion}

Les noeuds finaux de **collecteur Sysdig** sont des noeuds finaux d'ingestion que vous pouvez utiliser pour envoyer des données.

Le tableau suivant répertorie les **noeuds finaux de collecteur Sysdig** disponibles par région :

| Région        | Noeud final                                                  | Port |
|---------------|-----------------------------------------------------------|------|
| `Sud des Etats-Unis`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU-DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU-GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
{: caption="Tableau 2. Liste des noeuds finaux d'ingestion" caption-side="top"} 



## Noeuds finaux Sysdig
{: #endpoints_sysdig}

Le tableau suivant répertorie les **noeuds finaux Sysdig** disponibles par région :

| Région       | Noeud final                                                  | Port |
|--------------|-----------------------------------------------------------|------|
| `Sud des Etats-Unis`   | `https://us-south.monitoring.cloud.ibm.com `              | https (TLS) 443 |  
| `EU-DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
| `EU-GB`      | `https://eu-gb.monitoring.cloud.ibm.com `                 | https (TLS) 443 |
{: caption="Tableau 3. Liste des noeuds finaux Sysdig" caption-side="top"} 


