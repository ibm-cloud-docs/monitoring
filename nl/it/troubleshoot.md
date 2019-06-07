---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Risoluzione dei problemi di {{site.data.keyword.mon_full_notm}}
{: #troubleshoot}

Ottieni ulteriori informazioni su alcuni problemi generali che puoi riscontrare quando utilizzi il servizio {{site.data.keyword.mon_full_notm}}. In molti casi, puoi risolvere questi problemi seguendo pochi semplici passi.
{:shortdesc}

## Stai ricevendo un errore durante la creazione di un'acquisizione?
{: #troubleshoot-entry-1}

Non riesci a creare un [file acquisizione](/docs/services/Monitoring-with-Sysdig/captures.html#captures) per un host nella tua infrastruttura. 

Nella sezione *Captures* dell'IU web, ricevi un errore quando tenti di creare un file acquisizione per un host.
{: tsSymptoms}

L'agent Sysdig eseguito sull'host ha la funzione **sysdig_capture_enabled** impostata su *false*.
{: tsCauses}

Abilita la funzione **sysdig_capture_enabled** nell'agent Sysdig eseguito sull'host.
{: tsResolve}


## Lo stato del tuo file acquisizione è impostato su *requested* e non diventa *uploaded*?
{: #troubleshoot-entry-2}

Lo stato di un [file acquisizione](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures) è impostato su *requested* ma non diventa *uploaded*. Stai aspettando che il file acquisizione diventi disponibile per l'analisi.

Nella sezione *Captures* dell'IU web, lo stato del file acquisizione per un host non diventa *uploaded*.
{: tsSymptoms}

L'host ha la porta TCP 6443 disabilitata.
{: tsCauses}


Controlla che la porta 6443 sia aperta. Per ulteriori informazioni, consulta [Gestione del traffico di rete](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send)
{: tsResolve}


