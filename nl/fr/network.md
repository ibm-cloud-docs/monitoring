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

 
# Gestion du trafic réseau pour les configurations de pare-feu personnalisées
{: #network}

Lorsqu'un pare-feu supplémentaire est configuré, ou si vous avez personnalisé les paramètres de pare-feu dans votre infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer), vous devez autoriser le trafic réseau sortant sur le service {{site.data.keyword.mon_full_notm}}. 
{:shortdesc}


## Noeuds finaux d'ingestion
{: #network_send}

Pour envoyer des données de métriques au service {{site.data.keyword.mon_full_notm}}, vous devez définir la règle de pare-feu suivante dans votre hôte :

| Région      | Noeud final d'ingestion                                | Adresses IP publiques               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `Sud des Etats-Unis`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | TCP 6443 | 
{: caption="Tableau 1. Adresses IP pour l'envoi de métriques" caption-side="top"}



## Noeuds finaux d'interface utilisateur Web
{: #network_ui}

Pour accéder à l'interface utilisateur Web {{site.data.keyword.mon_full_notm}}, vous devez définir la règle de pare-feu suivante dans votre hôte :

| Région      | Noeud final d'interface utilisateur Web                                   | Adresses IP publiques                                    | Ports   |
|-------------|---------------------------------------------------|--------------------------------------------------------|---------|
| `Sud des Etats-Unis`  | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
{: caption="Tableau 2. Adresses IP pour accéder à l'interface utilisateur Web {{site.data.keyword.mon_full_notm}}" caption-side="top"}


