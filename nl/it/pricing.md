---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, pricing

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


# Prezzi
{: #pricing_plans}

Sono disponibili diversi piani del servizio per un'istanza {{site.data.keyword.mon_full_notm}}.
{:shortdesc}
 

| Piani            | Livello         | Raccolta dei dati  |
|------------------|--------------|------------------|
| `Trial`          |              | I dati vengono raccolti per un massimo di 20 contenitori per nodo o per 200 metriche personalizzate per nodo per 30 giorni soltanto. |
| `Graduated tier` | `Basic`      | I dati vengono raccolti per un massimo di 20 contenitori per nodo o per 200 metriche personalizzate per nodo. |
| `Graduated tier` | `Pro`        | I dati vengono raccolti per un massimo di 50 contenitori per nodo o per 500 metriche personalizzate per nodo. |
| `Graduated tier` | `Advanced`   | I dati vengono raccolti per un massimo di 110 contenitori per nodo o per 1000 metriche personalizzate per nodo. |
{: caption="Tabella 1. Elenco dei piani del servizio" caption-side="top"} 


**Nota:** un nodo può essere un host, un contenitore, una macchina virtuale, un server bare metal o una qualsiasi origine della metrica in cui hai installato un agent Sysdig.

Quando il numero di contenitori per nodo o il numero delle metriche va al di sotto del limite della soglia del piano di livello graduale per un periodo di tempo, viene applicato il rilevamento del livello automatico. Viene attivata una notifica di avviso che segue la tua configurazione delle notifiche dell'utilizzo della fatturazione se abiliti il seguente avviso **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

Puoi richiedere una **quota dei prezzi personalizzata** per qualsiasi cosa oltre il limite superiore del *piano dei prezzi a pagamenti di livello graduale avanzato* aprendo un ticket con il [Supporto IBM Cloud ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window}.
{: tip}

I dati vengono raccolti e conservati per le linee guide standard in tutti i piani. Per ulteriori informazioni, consulta [raccolta dei dati](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection) e [conservazione dei dati](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention).


## Controllo del tuo utilizzo
{: #pricing_usage}

Per monitorare come il servizio {{site.data.keyword.mon_full_notm}} viene utilizzato e i costi associati al suo utilizzo, consulta [Visualizzazione del tuo utilizzo](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).



## Abilitazione dell'avviso che avverte riguardo una modifica del livello
{: #pricing_alert}

Per essere avvertito quando si verifica una modifica del livello, devi abilitare il seguente avviso: **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

Completa la seguente procedura per abilitare un avviso:

1. Avvia l'IU web. Per ulteriori informazioni su come avviare l'IU web, consulta [Passaggio alla IU web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
2. Crea un canale di notifica. Per ulteriori informazioni, consulta [Configurazione di un canale di notifica](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create). 
3. Fai clic su **ALERTS** per passare alla sezione *Alerts*.
2. Cerca **[IBM]: Usage Tier Change**.
3. Modifica l'avviso per aggiungere il canale di notifica.
4. Fai clic su **Save**.



## Come viene generato l'avviso del piano del servizio?
{: #pricing_how}

Per essere avvertito quando si verifica una modifica del livello, devi abilitare il seguente avviso: **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

**Nota:** quando abiliti questo avviso, devi specificare i canali di notifica tramite i quali vuoi essere avvertito.

L'utilizzo viene calcolato come la media del numero di nodi e delle metriche campionate ogni 10 secondi nel corso dell'ora precedente. Small, le fluttuazioni di breve durata non sono incluse. La differenza tra l'utilizzo precedente e corrente si verifica una volta all'ora.

Le soglie definite vengono impostate nel seguente modo:

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [21, 50]
    Advanced = [51, 100]
  }
  metricDensity {
    Basic = [0, 200]
    Pro = [201, 500]
    Advanced = [501, 1000]
}
```
{: screen}

La notifica di avviso viene generata nel seguente modo:
1. Ogni ora, se il numero di contenitori per nodo in un livello aumenta, viene generato un evento personalizzato.
2. La condizione di avviso controlla ogni evento personalizzato che fornisce informazioni sulle modifiche nel numero di contenitori per nodo. Se trova un evento in cui il numero di contenitori in un livello aumenta rispetto all'ultima volta che è stato calcolato l'utilizzo, invia una notifica.

La frequenza dell'avviso è una volta all'ora. Per un nodo fluttuante, la frequenza dell'avviso è al massimo ogni due ore.

Tieni presente che l'avviso viene generato solo se un nodo si sposta dal livello *Basic* al *Pro* o all'*Advanced*. 



### Esempi
{: #pricing_examples}

**Esempio 1** 

Se il numero di contenitori medio è il seguente: 

| Ora     | Numero di contenitori | Descrizione                                                                   | Viene generato un avviso? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 18                   | Il livello è impostato su **Basic**.                                                     | No                     |
| 11:00    | 21                   | Il numero di contenitori è al di sopra del livello *Basic*. Il livello passa a **Pro**.            | Sì                    |
| 12:00    | 19                   | Il numero di contenitori è al di sotto del livello *Basic*. Il livello ritorna **Basic**.     | No                    |
| 13:00    | 20                   | Nessuna modifica del livello. Il livello è impostato su **Basic**.                                     | No                     |
{: caption="Tabella 2. Esempio 1" caption-side="top"} 


**Esempio 2**

Se il numero di contenitori medio è il seguente: 

| Ora     | Numero di contenitori | Descrizione                                                                   | Viene generato un avviso? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Il livello è impostato su **Basic**.                                                     | No                     |
| 11:00    | 19                   | Il livello è impostato su **Basic**.                                                     | No                     |
| 12:00    | 20                   | Il livello è impostato su **Basic**.                                                     | No                    |
| 13:00    | 21                   | Il numero di contenitori è al di sopra del livello *Basic*. Il livello passa a **Pro**.            | Sì                     |
{: caption="Tabella 3. Esempio 2" caption-side="top"}


**Esempio 3**

Se il numero di contenitori medio è il seguente: 

| Ora     | Numero di contenitori | Descrizione                                                                   | Viene generato un avviso? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Il livello è impostato su **Basic**.                                                     | No                     |
| 11:00    | 20                   | Il livello è impostato su **Basic**.                                                     | No                    |
| 12:00    | 21                   | Il livello è impostato su **Basic**.                                                     | Sì                    |
| 13:00    | 20                   | Il numero di contenitori torna al livello *Basic*. Il livello passa a **Pro**.          | No                     |
{: caption="Tabella 3. Esempio 3" caption-side="top"}



