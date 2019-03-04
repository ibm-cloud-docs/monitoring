---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

 
# Managing network traffic for custom firewall configurations
{: #network}

When you have an additional firewall set up, or you have customized the firewall settings in your {{site.data.keyword.Bluemix_notm}} infrastructure (SoftLayer), you need to allow outgoing network traffic to the IBM Cloud Monitoring with Sysdig service. 
{:shortdesc}


## Network traffic for custom firewall configurations in the US South region
{: #ips_us-south}

To send metric data to the IBM Cloud Monitoring with Sysdig service, you must define the following firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `US South`    | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | TCP 6443 | 
{: caption="Table 1. IP addresses to send metrics" caption-side="top"}

To access the IBM Cloud Monitoring with Sysdig web UI, you must define the following firewall rule in your host:

| Region      | Web UI endpoint                                   | Public IP addresses                                    | Ports   |
|-------------|---------------------------------------------------|--------------------------------------------------------|---------|
| `US South`    | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70   | TCP 443 | 
{: caption="Table 2. IP addresses to access the IBM Cloud Monitoring with Sysdig web UI" caption-side="top"}



## Network traffic for custom firewall configurations in the EU DE region
{: #ips_eu-de}

To send metric data to the IBM Cloud Monitoring with Sysdig service, you must define the following firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
{: caption="Table 3. IP addresses to send metrics" caption-side="top"}

To access the IBM Cloud Monitoring with Sysdig web UI, you must define the following firewall rule in your host:

| Region      | Web UI endpoint                                   | Public IP addresses               | Ports   |
|-------------|---------------------------------------------------|-----------------------------------|---------|
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 443 | 
{: caption="Table 4. IP addresses to access the IBM Cloud Monitoring with Sysdig web UI" caption-side="top"}

