---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# Utilizzo dei canali di notifica
{: #notifications}

Configura i canali di notifica per essere avvertito quando viene attivato un avviso. Gestisci i canali di notifica tramite il pannello *Settings* nell'IU web.
{:shortdesc}
 

## Configurazione di un canale di notifica
{: #notifications_create}

Completa la seguente procedura per aggiungere un canale di notifica:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, scegli **Settings**.

3. Seleziona **Notification Channels**.

4. Fai clic su **MY CHANNELS** ![icona aggiungi](../images/add.png). Quindi, seleziona un canale.

    **Nota** la prima volta che configuri un canale di notifica, fai clic su uno qualsiasi dei canali.

5. Configura un canale di notifica:

    * Immetti il nome del canale.

    * Abilita il campo *Notify when OK* per ricevere una notifica quando la condizione di avviso non è più attivata.

    * Abilita la condizione *Notify when Resolved* per ricevere una notifica quando l'avviso è stato risolto manualmente da un utente.

    * Per un canale di notifica **email**, aggiungi l'elenco dei destinatari, separati da virgole.

    * Per un canale di notifica **slack**, aggiungi il nome del *canale slack*.

    * Per un canale di notifica **Webhook**, aggiungi l'*URL webhook*. **Nota:** quando viene attivato un avviso, la notifica viene inviata come un POST nel formato JSON al tuo endpoint webhook. Per ulteriori informazioni, consulta [Configuring a Webhook channel ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}. Ad esempio, Sysdig può essere integrato con ServiceNow utilizzando un webhook personalizzato. Per ulteriori informazioni sulla configurazione di Sysdig con ServiceNow, consulta [Configure ServiceNow ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}.

    * Per un canale di notifica **VictorOps**, aggiungi la *chiave API* e la *chiave di instradamento*.

    * Per un canale di notifica **OpsGenie**, aggiungi la *chiave API OpsGenie*. Tieni presente che devi configurare l'integrazione con Sysdig in OpsGenie. Per ulteriori informazioni, consulta [Add Sysdig Cloud Integration in Opsgenie ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}.

    * Per un canale di notifica **PagerDuty**, devi prima autorizzare Sysdig per l'integrazione con il tuo account. Quando selezioni PagerDuty, si apre una procedura guidata per configurare l'integrazione con Sysdig. Fai clic su **Authorize Integration** o **Sign In Using Your Identity Provider** per autorizzare PagerDuty. Scegli un servizio esistente o configurane uno nuovo per le notifiche Sysdig, poi fai clic su **Finish Integration**. Seleziona la politica di escalation da utilizzare per gli incidenti Sysdig. Successivamente, nella scheda *Notifications*, conferma il tuo account PagerDuty, il tuo nome del servizio e la chiave del servizio. 

    * Facoltativamente, e per le integrazioni che permettono un test, abilita la condizione *Test notification* in modo da ricevere una notifica di test. Se non ricevi una notifica di test entro 10 minuti, controlla la tua configurazione del canale. 

6. Fai clic su **CREATE CHANNEL**. 



## Modifica di un canale di notifica
{: #notifications_update}

Completa la seguente procedura per modificare un canale di notifica:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, scegli **Settings**.

3. Seleziona **Notification Channels**.

4. Identifica il canale di destinazione che vuoi modificare e fai clic su **EDIT**.

5. Dopo aver apportato le modifiche, fai clic su **SAVE CHANGES**.



## Verifica di un canale di notifica
{: #notifications_test}

Completa la seguente procedura per verificare un canale di notifica:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, scegli **Settings**.

3. Seleziona **Notification Channels**.

4. Identifica il canale di destinazione che vuoi modificare e fai clic su **TEST**.



## Disabilitazione di un canale di notifica
{: #notifications_disable}

Completa la seguente procedura per disabilitare temporaneamente un canale di notifica:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, scegli **Settings**.

3. Seleziona **Notification Channels**.

4. Nella sezione *Notifications*, abilita *Downtime* per disabilitare gli avvisi temporaneamente e silenziare tutte le notifiche.

## Eliminazione di un canale di notifica
{: #notifications_delete}

Completa la seguente procedura per eliminare un canale di notifica:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. Dal pulsante *Selector* nella barra di navigazione, scegli **Settings**.

3. Seleziona **Notification Channels**.

4. Identifica il canale di destinazione che vuoi modificare e fai clic su **EDIT**.

5. Fai clic su **DELETE CHANNEL**.

6. Conferma l'eliminazione del canale. Fai clic su **SAVE CHANGES**.




