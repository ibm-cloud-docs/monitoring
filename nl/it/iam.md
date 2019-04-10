---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

 
# Gestione dell'accesso utente in {{site.data.keyword.cloud_notm}}
{: #iam}

{{site.data.keyword.iamlong}} (IAM) ti abilita ad autenticare in modo sicuro gli utenti e a controllare l'accesso a tutte le risorse cloud in modo congruente in {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

**Ad ogni utente che accede al servizio {{site.data.keyword.mon_full_notm}} nel tuo account deve essere assegnata una politica di accesso con un ruolo utente IAM definito.** La politica determina quali azioni possono essere effettuate dall'utente all'interno del contesto del servizio o dell'istanza che selezioni. Le azioni consentite vengono personalizzate e definite come operazioni che possono essere eseguite sul servizio. Le azioni vengono quindi associate ai ruoli utente IAM.

Le *politiche* consentono di concedere l'accesso a diversi livelli. Alcune delle opzioni includono quanto segue: 

* Accesso a tutti i servizi abilitati IAM nel tuo account
* Accesso a tutte le istanze del servizio in una sola regione nel tuo account
* Accesso a una singola istanza del servizio nel tuo account
* Accesso a tutte le istanze del servizio all'interno del contesto di un gruppo di risorse
* Accesso a tutte le istanze del servizio in una sola regione all'interno del contesto di un gruppo di risorse
* Accesso a tutti i servizi abilitati IAM all'interno del contesto di un gruppo di risorse

I *ruoli* definiscono le azioni che un utente o un ID servizio può eseguire. Esistono diversi tipi di ruoli in {{site.data.keyword.cloud_notm}}:
* I *ruoli di gestione della piattaforma* consentono agli utenti di eseguire delle attività sulle risorse del servizio al livello della piattaforma, ad esempio assegnare l'accesso utente per il servizio, creare o eliminare gli ID servizio, creare le istanze, assegnare le politiche per il tuo servizio ad altri utenti e associare le istanze alle applicazioni.
* I *ruoli di accesso al servizio* consentono di assegnare agli utenti diversi livelli di autorizzazione per richiamare l'API del servizio.

**Per organizzare una serie di utenti e ID servizio in una sola entità che ti semplifica la gestione delle autorizzazioni IAM, utilizza i **gruppi di accesso*.** Puoi assegnare una sola politica al gruppo invece di assegnare lo stesso accesso più volte per ogni utente o ID del servizio individuale.
{: tip}


## Gestione dell'accesso utilizzando i gruppi di accesso
{: #iam_groups}

Per gestire l'accesso o assegnare un nuovo accesso agli utenti utilizzando i gruppi di accesso, devi essere il proprietario dell'account, l'amministratore o l'editor di tutti i servizi abilitati per l'identità e l'accesso nell'account o l'amministratore o l'editor assegnato il servizio Gruppi di accesso IAM. 

Scegli una delle seguenti azioni per gestire i gruppi di accesso in {{site.data.keyword.cloud_notm}}:

* [Creazione di un gruppo di accesso](/docs/iam?topic=iam-groups#create_ag).
* [Assegnazione dell'accesso a un gruppo](/docs/iam?topic=iam-groups#access_ag).


## Gestione dell'accesso assegnando le politiche direttamente agli utenti.
{: #iam_users}

Per gestire l'accesso o assegnare un nuovo accesso agli utenti utilizzando le politiche IAM, devi essere il proprietario dell'account, l'amministratore di tutti i servizi nell'account o un amministratore di un particolare servizio o istanza del servizio. 

Scegli una delle seguenti azioni per gestire le politiche IAM in {{site.data.keyword.cloud_notm}}:

* Per modificare le autorizzazioni di un utente, consulta [Modifica dell'accesso esistente](/docs/iam?topic=iam-iammanidaccser#edit_existing).
* Per concedere le autorizzazioni a un utente, consulta [Assegna nuovo accesso](/docs/iam?topic=iam-iammanidaccser#assign_new_access).
* Per revocare le autorizzazioni, consulta [Rimozione dell'accesso](/docs/iam?topic=iam-iammanidaccser#removing_access).
* Per controllare le autorizzazioni di un utente, consulta [Controllo del tuo accesso assegnato](/docs/iam?topic=iam-iammanidaccser#review_your_access).


## Ruoli della piattaforma {{site.data.keyword.cloud_notm}}
{: #iam_platform}

Utilizza la seguente tabella per identificare il ruolo della piattaforma che puoi concedere a un utente in {{site.data.keyword.cloud_notm}} in modo che possa eseguire tutte le seguenti azioni della piattaforma:

| Azioni della piattaforma                                                        | Ruoli della piattaforma {{site.data.keyword.cloud_notm}}    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `Grant other account members access to work with the service`           | Amministratore                                        | 
| `Provision a service instance`                                          | Amministratore </br>Editor                            | 
| `Delete a service instance`                                             | Amministratore </br>Editor                            | 
| `Create a service ID`                                                   | Amministratore </br>Editor                            |
| `View details of a service instance`                                    | Amministratore </br>Editor </br>Operatore </br>Visualizzatore  | 
| `View service instances in the Observability Monitoring dashboard`      | Amministratore </br>Editor </br>Operatore </br>Visualizzatore  | 
{: caption="Tabella 1. Azioni e ruoli utente IAM" caption-side="top"}



## Ruoli Sysdig
{: #iam_sysdig_roles}

La seguente tabella illustra le azioni e i ruoli Sysdig per ruolo:

| Azioni                                                                    | Ruolo Sysdig                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Reset the Sysdig access key`                                              | Amministratore                                                |
| `Manage users`                                                             | Amministratore                                                |
| `Create, configure, and delete teams`                                      | Amministratore                                                |
| `Configure and remove notifications channels`                              | Amministratore                                                | 
| `Configure and remove Sysdig agents`                                       | Amministratore                                                |
| `Create, delete, and edit content in the Sysdig web UI`                    | Amministratore </br>Utente                                      |  
| `View metrics through the Sysdig Web UI`                                   | Amministratore </br>Utente                                      |  
| `Create and delete alerts`                                                 | Amministratore </br>Utente                                      | 
| `Create and delete captures`                                               | Amministratore </br>Utente                                      |   
{: caption="Tabella 2. Azioni e ruoli Sysdig" caption-side="top"}


## Associazione dei ruoli Sysdig ai ruoli {{site.data.keyword.cloud_notm}}
{: #iam_sysdig}

Utilizza la seguente tabella per vedere come un ruolo {{site.data.keyword.cloud_notm}} viene associato a un ruolo Sysdig:

| Tipo di ruolo        | Ruolo               | Ruolo Sysdig                | Descrizione                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| Ruolo piattaforma       | Amministratore      | Amministratore                      | Concede all'utente i privilegi di amministratore Sysdig.   | 
| Ruolo servizio        | Gestore            | Amministratore                      | Concede all'utente i privilegi di amministratore Sysdig.   | 
| Ruolo servizio        | Scrittore             | Utente                       | Concede all'utente i privilegi utente Sysdig.    |
| Ruolo servizio        | Lettore             |                            | Non viene concessa alcuna autorizzazione.                 |
{: caption="Tabella 3. Ruoli Sysdig" caption-side="top"}


