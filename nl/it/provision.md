---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# Provisioning di un'istanza
{: #provision}

Prima di poter monitorare e gestire le metriche con Sysdig, devi eseguire il provisioning di un'istanza del servizio in {{site.data.keyword.cloud_notm}}.
{:shortdesc}


## Provisioning di un'istanza Sysdig dal catalogo
{: #provision_ui}

Per eseguire il provisioning di un'istanza di Sysdig dal catalogo {{site.data.keyword.cloud_notm}}, completa la seguente procedura:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperta l'IU {{site.data.keyword.cloud_notm}}.

2. Fai clic su **Catalogo**. Viene aperto l'elenco dei servizi disponibili su {{site.data.keyword.cloud_notm}}.

3. Per filtrare l'elenco dei servizi che viene visualizzato, seleziona la categoria **Strumenti per gli sviluppatori**.

4. Fai clic sul tile **{{site.data.keyword.mon_full_notm}}**. Si apre il dashboard *Osservabilità*.

5. Seleziona **Crea istanza**. 

6. Seleziona un piano di servizio. Per impostazione predefinita, è impostato il piano **Trial**.

    Per ulteriori informazioni sui piani di servizio, vedi [Piani di servizio](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

7. Seleziona un gruppo di risorse. Per impostazione predefinita, è impostato il gruppo di risorse **Default**.

8. Fai clic su **Crea**.

Dopo aver eseguito il provisioning di un'istanza, 

* Si apre il dashboard *Osservabilità*. 
* Viene automaticamente creato un ID del servizio. Puoi utilizzare questo ID del servizio per ottenere la chiave di accesso Sysdig per la tua istanza.

Successivamente, configura un'origine della metrica aggiungendo un agent Sysdig. Questo agent è responsabile della raccolta e dell'inoltro delle metriche a Sysdig. 



## Provisioning di un'istanza Sysdig tramite la CLI
{: #provision_cli}

Per eseguire il provisioning di un'istanza di Sysdig tramite la riga di comando, completa la seguente procedura:

1. [Prerequisito] Installazione della CLI {{site.data.keyword.cloud_notm}}. Se la CLI è installata, continua con il passo successivo.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

2. Accedi alla regione in {{site.data.keyword.cloud_notm}} in cui vuoi eseguire il provisioning dell'istanza. Immetti il seguente comando: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Configura il gruppo di sicurezza in cui vuoi eseguire il provisioning dell'istanza. Immetti il seguente comando: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Per impostazione predefinita, è impostato il gruppo di risorse `default`.

4. Crea l'istanza Sysdig. Esegui il comando [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create):

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    Dove

    * NAME è il nome dell'istanza Sysdig.
    
    * `sysdig-monitor` è il nome del nome del servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}.
    
    * SERVICE_PLAN_NAME è il tipo di piano. I valori validi sono *lite* e *graduated-tier*.
    
    * LOCATION è la regione in cui viene creata l'istanza.

    Ad esempio, per eseguire il provisioning di un'istanza con il piano a pagamento, immetti il seguente comando:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

