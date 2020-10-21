---

copyright:
  years:  2018, 2020
lastupdated: "2020-07-16"

keywords: Sysdig, IBM Cloud, monitoring, prometheus, exporters, promcat

subcollection: Monitoring-with-Sysdig

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

---

# Collecting Prometheus metrics
{: #prometheus}

The Prometheus Blackbox exporter allows blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP.  The Sysdig agent can be used in conjunction with the Blackbox exporter to collect availability metrics. The availability metrics can then be alerted upon within Sysdig to alert users on the availability of the endpoints.
{:shortdesc}


Sysdig Monitor can collect Prometheus metrics from remote endpoints with minimum configuration. Remote endpoints (remote hosts) refer to hosts where Sysdig Agent cannot be deployed. For example, a Kubernetes master node on managed Kubernetes services such as GKE and EKS where user workload cannot be deployed, which in turn implies no Agents involved. Enabling remote scraping on such hosts is as simple as identifying an Agent to perform the scraping and declaring the endpoint configurations with a remote services section in the Agent configuration file.






