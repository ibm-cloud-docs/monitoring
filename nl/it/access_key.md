---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# Utilizzo delle chiavi di accesso
{: #access_key}

La **Chiave di accesso** è un token che devi utilizzare per configurare gli agent Sysdig per inoltrare correttamente i dati alla tua istanza {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.Bluemix}}.   
{:shortdesc}


## Ottenimento della chiave di accesso tramite l'IU {{site.data.keyword.cloud_notm}}
{: #access_key_ibm_cloud_ui}

Per ottenere la chiave di accesso per un'istanza {{site.data.keyword.mon_full_notm}} tramite l'IU {{site.data.keyword.cloud_notm}}, completa la seguente procedura:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.

    Fai clic sul [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/login){:new_window} per avviare il dashboard {{site.data.keyword.cloud_notm}}.

	Dopo che hai eseguito l'accesso con il tuo ID utente e la tua password, viene aperta l'IU {{site.data.keyword.cloud_notm}}.

2. Nel menu di navigazione, seleziona **Osservabilità**. 

3. Seleziona **Monitoraggio**. Viene aperto il dashboard {{site.data.keyword.mon_full_notm}}. Puoi visualizzare l'elenco di istanze di monitoraggio disponibili su {{site.data.keyword.cloud_notm}}.

3. Identifica l'istanza per la quale desideri ottenere la chiave di accesso e fai clic su **Visualizza chiave di accesso**.

4. Si apre una finestra a comparsa in cui puoi fare clic su **Mostra** per visualizzare la chiave di accesso.



## Ottenimento della chiave di accesso tramite la CLI
{: #access_key_cli}

Per ottenere la chiave di accesso per un'istanza Sysdig tramite la riga di comando, completa la seguente procedura:

1. [Prerequisito] Installa la CLI {{site.data.keyword.cloud_notm}}.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

   Se la CLI è installata, vai al passo successivo.

2. Accedi alla regione in {{site.data.keyword.cloud_notm}} in cui è in esecuzione l'istanza Sysdig. Immetti il seguente comando: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Configura il gruppo di risorse in cui è in esecuzione l'istanza Sysdig. Immetti il seguente comando: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Per impostazione predefinita, è impostato il gruppo di risorse `default`.

4. Ottieni il nome dell'istanza. Immetti il seguente comando: [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Ottieni il nome della chiave API associata all'istanza Sysdig. Esegui il comando [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances):

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    dove INSTANCE_NAME è il nome dell'istanza che hai ottenuto nel passo precedente.

6. Ottieni la chiave di accesso. Esegui il comando [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key):

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    dove APIKEY_NAME è il nome della chiave API.
 
    L'output da questo comando include il campo **Sysdig Access Key** che contiene la chiave di accesso per l'istanza.


Ad esempio, il seguente comando mostra l'output di un ID del servizio di esempio:

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## Reimpostazione della chiave di accesso 
{: #access_key_reset}

Se la chiave di accesso è compromessa oppure hai una politica per rinnovarla dopo alcuni giorni, puoi generare una nuova chiave ed eliminare la vecchia.

Per rinnovare la chiave di accesso per un'istanza {{site.data.keyword.mon_full_notm}}, completa la seguente procedura:

1. Avvia l'IU web {{site.data.keyword.mon_full_notm}}. Per ulteriori informazioni, vedi [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. Dal pulsante *Selector* nella barra di navigazione, scegli **Settings**.

2. Nella sezione *Password management*, fai clic su **Reset your password**.

**Nota:** dopo aver reimpostato la chiave di accesso Sysdig, devi aggiornare la chiave di accesso di tutte le origini log che hai configurato per inoltrare le metriche a questa istanza {{site.data.keyword.mon_full_notm}}.
