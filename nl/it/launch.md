---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# Passaggio alla IU web
{: #launch}

Dopo aver eseguito il provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.Bluemix}} e configurato un agent Sysdig per un'origine delle metriche, puoi visualizzare, monitorare e gestire le metriche tramite l'IU web {{site.data.keyword.mon_full_notm}}.
{:shortdesc}


## Concedi le politiche IAM a un utente per visualizzare i dati 
{: #launch_step1}

**Nota:** devi essere un amministratore del servizio {{site.data.keyword.mon_full_notm}}, un amministratore dell'istanza {{site.data.keyword.mon_full_notm}} o disporre delle autorizzazioni IAM dell'account per concedere le politiche ad altri utenti.

La seguente tabella elenca le politiche minime di cui deve disporre un utente per poter avviare l'IU web {{site.data.keyword.mon_full_notm}} e visualizzare i dati:

| Servizio                        | Ruolo                      | Autorizzazione concessa     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | Ruolo piattaforma: visualizzatore     | Consente all'utente di visualizzare l'elenco di istanze del servizio nel dashboard di osservabilità e monitoraggio. |
| `{{site.data.keyword.mon_full_notm}}` | Ruolo del servizio: scrittore      | Consente all'utente di avviare l'IU web e di visualizzare le metriche in essa.  |
{: caption="Tabella 1. Politiche IAM" caption-side="top"} 

Per ulteriori informazioni su come configurare queste politiche per un utente, consulta [Concessione delle autorizzazioni a un utente per visualizzare le metriche in Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig).


## Avvia l'IU web tramite l'IU {{site.data.keyword.cloud_notm}}
{: #launch_step2}

Avvia l'IU web all'interno del contesto di un'istanza {{site.data.keyword.mon_full_notm}}, dall'IU {{site.data.keyword.cloud_notm}}. 

Completa la seguente procedura per avviare l'IU web:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperto il dashboard {{site.data.keyword.cloud_notm}}.

2. Nel menu di navigazione, seleziona **Osservabilità**. 

3. Seleziona **Monitoraggio**. 

    Viene visualizzato l'elenco di istanze disponibili su {{site.data.keyword.cloud_notm}}.

4. Seleziona un'istanza. Quindi, fai clic su **Visualizza Sysdig**.

Viene aperta l'IU web.


