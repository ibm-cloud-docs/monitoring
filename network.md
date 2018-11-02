---

copyright:
  years:  2018
lastupdated: "2018-11-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

 
# Managing network traffic
{: #network}

When you have an additional firewall set up, or you have customized the firewall settings in your {{site.data.keyword.Bluemix_notm}} infrastructure (SoftLayer), you need to allow outgoing network traffic to the IBM Cloud Monitoring with Sysdig service. 
{:shortdesc}


## Network traffic for custom firewall configurations in the {{site.data.keyword.Bluemix_notm}}
{: #ips}

You must allow outgoing traffic on TCP port 443 and TCP port 6443 in your firewall. 

The following table lists the IP addresses and ports per region that you must configure in your firewall to allow outgoing traffic:

| Region      | Ingestion endpoint                                | Public IP addresses               | Ports    |
|-------------|---------------------------------------------------|-----------------------------------|----------|
| US South    | ingest.us-south.monitoring.cloud.ibm.com          | 169.48.237.108                    | TCP 6443 | 
{: caption="Table 1. IP addresses to send metrics" caption-side="top"}

The following table lists the IP addresses and ports per region that you must configure in your firewall to allow access to the IBM Cloud Monitoring with Sysdig Web UI:

| Region      | Web UI endpoint                                   | Public IP addresses               | Ports   |
|-------------|---------------------------------------------------|-----------------------------------|---------|
| US South    | us-south.monitoring.cloud.ibm.com                 | 169.48.237.108                    | TCP 443 | 
{: caption="Table 2. IP addresses to access the IBM Cloud Monitoring with Sysdig Web UI" caption-side="top"}

