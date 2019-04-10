---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam, access groups

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

 
# Utilizzo delle politiche IAM e dei gruppi di accesso
{: #iam_work}

{{site.data.keyword.iamlong}} (IAM) ti abilita ad autenticare in modo sicuro gli utenti e a controllare l'accesso a tutte le risorse cloud in modo congruente in {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

Per concedere i privilegi di amministratore Sysdig a un utente, puoi assegnargli uno dei seguenti ruoli:

* Ruolo della piattaforma `Administrator`: concedi questo ruolo se l'utente è anche un amministratore del servizio Sysdig in {{site.data.keyword.cloud_notm}}.
* Ruolo della piattaforma `Editor`: concedi questo ruolo se l'utente deve poter eseguire il provisioning o rimuovere le istanze Sysdig in {{site.data.keyword.cloud_notm}}.
* Ruolo del servizio `Manager`: concedi questo ruolo se l'utente non deve essere in grado di gestire il servizio Sysdig in {{site.data.keyword.cloud_notm}}.

Per concedere i privilegi utente Sysdig a un utente, puoi assegnargli un ruolo del servizio `Writer`.

**Nota:** per gestire l'accesso o assegnare un nuovo accesso agli utenti utilizzando le politiche IAM, devi essere il proprietario dell'account, l'amministratore di tutti i servizi nell'account o un amministratore di un particolare servizio o istanza del servizio. 

Come **proprietario dell'account** o un **amministratore del servizio {{site.data.keyword.mon_full_notm}}**, devi disporre delle autorizzazioni per eseguire le seguenti azioni della piattaforma: 

* Concedi ad altri membri dell'account l'accesso per utilizzare il servizio
* Esegui il provisioning di un'istanza del servizio
* Elimina un'istanza del servizio
* Visualizza i dettagli di un'istanza del servizio
* Crea un ID del servizio

Come un **utente Devops**, devi disporre delle autorizzazioni per eseguire le seguenti azioni della piattaforma: 

* Esegui il provisioning di un'istanza del servizio
* Elimina un'istanza del servizio
* Visualizza i dettagli di un'istanza del servizio
* Crea un ID del servizio


## Concessione delle autorizzazioni a un utente per diventare un amministratore del servizio nell'account {{site.data.keyword.cloud_notm}}
{: #admin_account}

Per concedere a un utente il ruolo di amministratore per gestire il servizio nell'account, l'utente deve disporre di una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo della piattaforma **Amministratore**. Devi assegnare questo accesso utente a una singola risorsa nell'account. 

Completa la seguente procedura per assegnare a un utente il ruolo di amministratore del servizio {{site.data.keyword.mon_full_notm}} nell'account: 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso alle risorse**.
4. Seleziona **{{site.data.keyword.mon_full_notm}}**.
5. Seleziona **Tutte le regioni correnti**.
6. Seleziona **Tutte le istanze del servizio correnti**.
7. Seleziona il ruolo della piattaforma **Amministratore**.
8. Fai clic su Assegna.


## Concessione delle autorizzazioni a un utente per diventare un amministratore del servizio all'interno di un gruppo di risorse
{: #admin_rg}

Per concedere a un utente il ruolo di amministratore per gestire le istanze all'interno di un gruppo di risorse nell'account, l'utente deve disporre di una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo della piattaforma **Amministratore** all'interno del contesto del gruppo di risorse. 

Completa la seguente procedura per assegnare a un utente il ruolo di amministratore del servizio {{site.data.keyword.mon_full_notm}} all'interno del contesto di un gruppo di risorse: 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso in un gruppo di risorse**.
4. Seleziona un gruppo di risorse.
5. Se l'utente non ha un ruolo già concesso per il gruppo di risorse selezionato, scegli un ruolo per il campo **Assegna accesso a un gruppo di risorse**. 

    A seconda del ruolo che selezioni, l'utente può visualizzare il gruppo di risorse sul proprio dashboard, modificarne il nome o gestire l'accesso utente al gruppo. 
    
    Puoi selezionare **Nessun accesso**, se vuoi che l'utente abbia accesso solo al servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse.

6. Seleziona **{{site.data.keyword.mon_full_notm}}**.
7. Seleziona il ruolo della piattaforma **Amministratore**.
8. Fai clic su **Assegna**.


## Concessione delle autorizzazioni a un utente Devops per gestire il servizio nell'account {{site.data.keyword.cloud_notm}}
{: #devops_account}

Devi disporre di una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo della piattaforma **Editor**.

Completa la seguente procedura per assegnare a un utente il ruolo di editor del servizio {{site.data.keyword.mon_full_notm}} nell'account: 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso alle risorse**.
4. Seleziona **{{site.data.keyword.mon_full_notm}}**.
5. Seleziona **Tutte le istanze del servizio**.
6. Seleziona il ruolo della piattaforma **Editor**.
7. Fai clic su Assegna.

## Concessione delle autorizzazioni a un utente Devops per gestire un'istanza nell'account {{site.data.keyword.cloud_notm}}
{: #devops_account_instance}

Completa la seguente procedura per assegnare a un utente il ruolo di editor su un'istanza del servizio {{site.data.keyword.mon_full_notm}} nell'account: 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso alle risorse**.
4. Seleziona **{{site.data.keyword.mon_full_notm}}**.
5. Seleziona l'istanza.
6. Seleziona il ruolo della piattaforma **Editor**.
7. Fai clic su Assegna.



## Concessione delle autorizzazioni a un utente Devops per gestire il servizio all'interno di un gruppo di risorse
{: #devops_rg}

Hai bisogno di una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo della piattaforma **Editor**.

Completa la seguente procedura per assegnare a un utente il ruolo di editor del servizio {{site.data.keyword.mon_full_notm}} all'interno del contesto di un gruppo di risorse: 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso in un gruppo di risorse**.
4. Seleziona un gruppo di risorse.
5. Se l'utente non ha un ruolo già concesso per il gruppo di risorse selezionato, scegli un ruolo per il campo **Assegna accesso a un gruppo di risorse**. 

    A seconda del ruolo che selezioni, l'utente può visualizzare il gruppo di risorse sul proprio dashboard, modificarne il nome o gestire l'accesso utente al gruppo. 
    
    Puoi selezionare **Nessun accesso**, se vuoi che l'utente abbia accesso solo al servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse.

6. Seleziona **{{site.data.keyword.mon_full_notm}}**.
7. Seleziona il ruolo della piattaforma **Editor**.
8. Fai clic su **Assegna**.

## Concessione delle autorizzazioni per gestire le metriche e configurare gli avvisi in Sysdig
{: #admin_user_sysdig}

Come un **utente amministratore** in Sysdig, devi disporre delle autorizzazioni per eseguire le seguenti azioni: 

* Aggiungere origini delle metriche
* Visualizzare le metriche
* Ricercare le metriche
* Filtrare le metriche
* Configurare gli avvisi

Pertanto, hai bisogno delle seguenti politiche:

* Una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo della piattaforma **Editor**. Questa politica ti consente di visualizzare i dettagli dell'istanza del servizio tramite la riga di comando nel dashboard {{site.data.keyword.cloud_notm}}.
* Una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo del servizio **Gestore**. Questa politica ti consente di monitorare, filtrare e ricercare le metriche e definire gli avvisi tramite l'IU web Sysdig.

**Nota:** come amministratore del servizio, quando concedi a un utente queste politiche, considera di farlo all'interno di un gruppo di risorse. Viene eseguito il provisioning di un'istanza {{site.data.keyword.mon_full_notm}} all'interno del contesto di un gruppo di risorse. Pertanto, devi concedere le autorizzazioni di accesso all'interno del contesto di un gruppo di risorse.


Completa la seguente procedura per assegnare a un utente entrambe le politiche per il servizio {{site.data.keyword.mon_full_notm}} all'interno del contesto di un gruppo di risorse: 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso in un gruppo di risorse**.
4. Seleziona un gruppo di risorse.
5. Se l'utente non ha un ruolo già concesso per il gruppo di risorse selezionato, scegli un ruolo per il campo **Assegna accesso a un gruppo di risorse**. 

    A seconda del ruolo che selezioni, l'utente può visualizzare il gruppo di risorse sul proprio dashboard, modificarne il nome o gestire l'accesso utente al gruppo. 
    
    Puoi selezionare **Nessun accesso**, se vuoi che l'utente abbia accesso solo al servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse.

6. Seleziona **{{site.data.keyword.mon_full_notm}}**.
7. Seleziona il ruolo della piattaforma **Editor**.
8. Seleziona il ruolo del servizio **Gestore**.
8. Fai clic su **Assegna**.

## Concessione delle autorizzazioni a un utente per visualizzare le metriche in Sysdig
{: #user_sysdig}

Come **utente**, **revisore** o **sviluppatore**, potresti aver bisogno di autorizzazioni per eseguire le seguenti azioni: 

* Visualizzare le metriche
* Ricercare le metriche
* Filtrare le metriche

Pertanto, hai bisogno delle seguenti politiche:

* Una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo della piattaforma **Visualizzatore**. Questa politica ti consente di visualizzare i dettagli dell'istanza del servizio tramite la riga di comando nel dashboard {{site.data.keyword.cloud_notm}}.
* Una politica IAM per il servizio {{site.data.keyword.mon_full_notm}} con il ruolo del servizio **Scrittore**. Questa politica ti consente di visualizzare, filtrare e ricercare le metriche tramite l'IU web Sysdig.

**Nota:** come amministratore del servizio, quando concedi a un utente queste politiche, considera di farlo all'interno di un gruppo di risorse. Viene eseguito il provisioning di un'istanza {{site.data.keyword.mon_full_notm}} all'interno del contesto di un gruppo di risorse. Pertanto, devi concedere le autorizzazioni di accesso all'interno del contesto di un gruppo di risorse.

Completa la seguente procedura per assegnare a un utente entrambe le politiche per il servizio {{site.data.keyword.mon_full_notm}} all'interno del contesto di un gruppo di risorse: 

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Accesso (IAM)** e seleziona **Utenti**.
2. Dalla riga per l'utente a cui vuoi assegnare l'accesso, seleziona il menu **Azioni** e fai quindi clic su **Assegna accesso**.
3. Seleziona **Assegna l'accesso in un gruppo di risorse**.
4. Seleziona un gruppo di risorse.
5. Se l'utente non ha un ruolo già concesso per il gruppo di risorse selezionato, scegli un ruolo per il campo **Assegna accesso a un gruppo di risorse**. 

    A seconda del ruolo che selezioni, l'utente può visualizzare il gruppo di risorse sul proprio dashboard, modificarne il nome o gestire l'accesso utente al gruppo. 
    
    Puoi selezionare **Nessun accesso**, se vuoi che l'utente abbia accesso solo al servizio {{site.data.keyword.mon_full_notm}} nel gruppo di risorse.

6. Seleziona **{{site.data.keyword.mon_full_notm}}**.
7. Seleziona il ruolo della piattaforma **Visualizzatore**.
8. Seleziona il ruolo del servizio **Scrittore**.
8. Fai clic su **Assegna**.

