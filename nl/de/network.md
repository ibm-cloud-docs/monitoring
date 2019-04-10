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

 
# Netzverkehr für angepasste Firewallkonfigurationen verwalten
{: #network}

Wenn Sie eine zusätzliche Firewall eingerichtet haben oder die Firewalleinstellungen in Ihrer {{site.data.keyword.cloud_notm}}-Infrastruktur (SoftLayer) angepasst haben, müssen Sie ausgehenden Netzverkehr für den {{site.data.keyword.mon_full_notm}}-Service zulassen. 
{:shortdesc}


## Aufnahmeendpunkte
{: #network_send}

Um Metrikdaten an den {{site.data.keyword.mon_full_notm}}-Service zu senden, müssen Sie die folgende Firewallregel in Ihrem Host definieren:

| Region      | Aufnahmeendpunkt                                | Öffentliche IP-Adresse               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `USA (Süden)`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | TCP 6443 | 
| `EU-DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | TCP 6443 | 
{: caption="Tabelle 1. IP-Adressen zum Senden von Metriken" caption-side="top"}



## Endpunkt der Webbenutzerschnittstelle
{: #network_ui}

Um auf die {{site.data.keyword.mon_full_notm}}-Webbenutzerschnittstelle zugreifen zu können, müssen Sie die folgende Firewallregel in Ihrem Host definieren:

| Region      | Endpunkt der Webbenutzerschnittstelle                                   | Öffentliche IP-Adresse                                    | Ports   |
|-------------|---------------------------------------------------|--------------------------------------------------------|---------|
| `USA (Süden)`  | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | https (TLS) 443 | 
| `EU-DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
{: caption="Tabelle 2. IP-Adressen für den Zugriff auf die {{site.data.keyword.mon_full_notm}}-Webbenutzerschnittstelle" caption-side="top"}


