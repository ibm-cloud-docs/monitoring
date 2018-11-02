---

copyright:
  years:  2018
lastupdated: "2018-11-02"

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

When you have an additional firewall set up, or you have customized the firewall settings in your {{site.data.keyword.Bluemix_notm}} infrastructure (SoftLayer), you need to allow outgoing network traffic to the IBM Cloud Log Analysis with LogDNA service. 
{:shortdesc}


## Network traffic for custom firewall configurations in the {{site.data.keyword.Bluemix_notm}}
{: #ips}

You must allow outgoing traffic on TCP port 443 and TCP port 80 in your firewall. For example, you must open TCP port 443 and TCP port 80 from each worker to the IBM Log Analysis with LogDNA service.

**Note:** The API endpoint is required for LogDNA agent authentication. The LogDNA agent gets a token that you can use to send logs to the Ingestion endpoint.

The following tables list the IP addresses per region that you must configure in your firewall to allow outgoing traffic:

| Region      | Ingestion endpoint                          | Public IP addresses               | Ports   |
|-------------|---------------------------------------------|-----------------------------------|---------|
| US South    | logs.us-south.logging.cloud.ibm.com         | 169.48.237.108                    | TCP 443 | 
{: caption="Table 1. IP addresses to send logs" caption-side="top"}


| Region      | Authentication endpoint                     | Public IP addresses               | Ports   |
|-------------|---------------------------------------------|-----------------------------------|---------|
| US South    | api.us-south.logging.cloud.ibm.com          | 169.60.166.43                     | TCP 80  |
{: caption="Table 2. IP addresses used by the LogDNA agent" caption-side="top"}

