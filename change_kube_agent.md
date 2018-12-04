---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Customizing the Kubernetes Sysdig agent
{: #change_kube_agent}

In {{site.data.keyword.mon_full_notm}}, you can customize the Sysdig agent configuration file to filter metric data. 
{:shortdesc}



Kubernetes Infrastructure

When running in a Kubernetes infrastructure (installed using the v1 method),  comment in the "ADDITIONAL_CONF" line in the agent sysdig-daemonset.yaml manifest file,  and modify as needed:
- name: ADDITIONAL_CONF #OPTIONAL pass additional parameters to the agent
  value: "log:\n file_priority: debug\n console_priority: error"