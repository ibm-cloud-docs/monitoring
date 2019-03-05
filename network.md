---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: monitoring, network traffic, firewall

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

 
# Managing network traffic for custom firewall configurations
{: #network}

When you have an additional firewall set up, or you have customized the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure (SoftLayer), you need to allow outgoing network traffic to the {{site.data.keyword.mon_full_notm}} service. 
{:shortdesc}


## Network traffic for custom firewall configurations in the US South region
{: #ips_us-south}

To send metric data to the {{site.data.keyword.mon_full_notm}} service, you must define the following firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `US South`    | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | TCP 6443 | 
{: caption="Table 1. IP addresses to send metrics" caption-side="top"}

To access the {{site.data.keyword.mon_full_notm}} web UI, you must define the following firewall rule in your host:

| Region      | Web UI endpoint                                   | Public IP addresses                                    | Ports   |
|-------------|---------------------------------------------------|--------------------------------------------------------|---------|
| `US South`    | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | https (TLS) 443 | 
{: caption="Table 2. IP addresses to access the {{site.data.keyword.mon_full_notm}} web UI" caption-side="top"}



## Network traffic for custom firewall configurations in the EU DE region
{: #ips_eu-de}

To send metric data to the {{site.data.keyword.mon_full_notm}} service, you must define the following firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
{: caption="Table 3. IP addresses to send metrics" caption-side="top"}

To access the {{site.data.keyword.mon_full_notm}} web UI, you must define the following firewall rule in your host:

| Region      | Web UI endpoint                                   | Public IP addresses               | Ports   |
|-------------|---------------------------------------------------|-----------------------------------|---------|
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | https (TLS) 443 | 
{: caption="Table 4. IP addresses to access the {{site.data.keyword.mon_full_notm}} web UI" caption-side="top"}

