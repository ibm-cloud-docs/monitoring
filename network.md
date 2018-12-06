---

copyright:
  years:  2018
lastupdated: "2018-12-06"

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


## Allowing traffic from your host to send metrics
{: #send}

To send metric data to the IBM Cloud Monitoring with Sysdig service, you must define the following firewall rule in your host:

| Region      | Ingestion endpoint                                | Public IP addresses               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| US South    | ingest.us-south.monitoring.cloud.ibm.com          | 169.48.237.108                    | TCP 6443 | 
{: caption="Table 1. IP addresses to send metrics" caption-side="top"}


## Allowing traffic from your host to access the web UI
{: #web}

To access the IBM Cloud Monitoring with Sysdig web UI, you must define the following firewall rule in your host:

| Region      | Web UI endpoint                                   | Public IP addresses               | Ports   |
|-------------|---------------------------------------------------|-----------------------------------|---------|
| US South    | us-south.monitoring.cloud.ibm.com                 | 169.48.237.108                    | TCP 443 | 
{: caption="Table 2. IP addresses to access the IBM Cloud Monitoring with Sysdig web UI" caption-side="top"}

