---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# Rimozione di un'istanza
{: #remove}

Puoi rimuovere un'istanza del servizio {{site.data.keyword.mon_full_notm}} dall'IU {{site.data.keyword.Bluemix}} o tramite la riga di comando.
{:shortdesc}

Quando rimuovi un'istanza da {{site.data.keyword.cloud_notm}}, considera le seguenti informazioni per riordinare:

1. Prendi nota dell'elenco delle origini che inoltrano le metriche all'istanza {{site.data.keyword.mon_full_notm}} che vuoi rimuovere. Devi rimuovere l'agent Sysdig da ogni origine.
2. Rimuovi le autorizzazioni concesse agli utenti per utilizzare l'istanza. 

    Se utilizzi un gruppo di accesso per gestire l'accesso all'istanza, devi rimuoverlo.

    Se utilizzi un gruppo di accesso per gestire l'accesso a istanze del servizio diverse, devi rimuovere le politiche che concedono le autorizzazioni all'istanza che vuoi rimuovere.
    
    Se hai concesso delle politiche individuali agli utenti, devi richiamare le informazioni di ogni utente che dispone dell'accesso e rimuovere una a una le politiche correlate all'istanza che vuoi eliminare.


Successivamente, rimuovi l'istanza dal dashboard {{site.data.keyword.cloud_notm}}.


## Rimozione di un'istanza tramite l'IU {{site.data.keyword.cloud_notm}}
{: #remove_ui}

Per rimuovere un'istanza di {{site.data.keyword.mon_full_notm}} utilizzando l'IU {{site.data.keyword.cloud_notm}}, completa la seguente procedura:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperta l'IU {{site.data.keyword.cloud_notm}}.

2. Seleziona **Osservabilità**. 

3. Seleziona **Monitoraggio**. Viene visualizzato l'elenco delle istanze.

4. Seleziona l'istanza che vuoi eliminare.

5. Dal menu *Azione*, seleziona **Rimuovi**.


## Rimozione di un'istanza tramite la CLI
{: #remove_cli}

Per rimuovere un'istanza di {{site.data.keyword.mon_full_notm}} tramite la riga di comando, completa la seguente procedura:

1. [Prerequisito] Installa la CLI {{site.data.keyword.cloud_notm}}.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

   Se la CLI è installata, continua con il passo successivo.

2. Accedi alla regione in {{site.data.keyword.cloud_notm}} in cui vuoi eseguire il provisioning dell'istanza. Immetti il seguente comando: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Configura il gruppo di risorse in cui è stato eseguito il provisioning dell'istanza. Immetti il seguente comando: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Per impostazione predefinita, è impostato il gruppo di risorse `default`.

4. Rimuovi l'istanza. Esegui il comando [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete):

    ```
    ibmcloud resource service-instance-delete NAME 
    ```
    {: codeblock}

    dove NAME è il nome dell'istanza

    Ad esempio, per rimuovere un'istanza, immetti il seguente comando:

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
