---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# Personalizzazione degli agent Sysdig Linux
{: #change_linux_agent}

Per impostazione predefinita, l'agent Sysdig raccoglie i dati da una serie di piattaforme e applicazioni. Puoi modificare il file di configurazione dell'agent per modificarne i comportamenti predefiniti e includere o escludere i dati. Puoi personalizzare il file di configurazione dell'agent Sysdig in modo che includa delle metriche personalizzate come ad esempio JMX, StatsD e Prometheus. Puoi anche filtrare le metriche e i contenitori.
{:shortdesc}

L'agent Sysdig utilizza due file di configurazione che specificano quali dati raccogliere automaticamente:

| File                   | Descrizione                                                     | Ubicazione                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | File di configurazione principale </br>**Nota:****non modificare questo file.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | File di configurazione che modifichi per personalizzare l'agent Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabella 1. File di configurazione dell'agent Sysdig" caption-side="top"} 

Puoi modificare il file *dragent.yaml* per personalizzare i dati che vengono raccolti. Le modifiche hanno effetto immediatamente dopo che salvi il file. L'agent rileva la modifica ed esegue un riavvio in automatico. Puoi trovare la frequenza e i file che un agent Sysdig controlla nel file *dragent.default.yaml*.

Ad esempio, un *dragent.default.yaml* include le seguenti informazioni:

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## Modifica del file yaml dragent
{: #change_linux_agent_edit_agent}

Il file yaml è ubicato in */opt/draios/etc/*.

Completa la seguente procedura per modificare il file e applicare le modifiche:

1. Accedi a *dragent.yaml* direttamente. Il file è ubicato in `/opt/draios/etc/dragent.yaml`.
2. Modifica il file. Utilizza una sintassi YAML valida.
3. Riavvia l'agent. Immetti il seguente comando:

    ```
    service dragent restart
    ```
    {: codeblock}


## Blocco delle porte
{: #change_linux_agent_block_ports}

Per bloccare le metriche e il traffico di rete dalle porte di rete, devi personalizzare la sezione **blacklisted_ports** nel file *dragent.yaml*. Devi elencare le porte da cui vuoi filtrare tutti i dati.

**Nota:** la porta 53 (DNS) è sempre nella blacklist. 

Ad esempio, il seguente esempio illustra come configurare la sezione *blacklisted_ports* di un agent Sysdig per escludere i dati provenienti dalle porte 6666 e 6379:

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## Inclusione ed esclusione delle metriche
{: #change_linux_agent_inc_exc_metrics}

Per filtrare le metriche personalizzate, devi personalizzare la sezione **metrics_filter** nel file *dragent.yaml*. Puoi specificare quali metriche includere e quali filtrare configurando i parametri di filtro **include** e **exclude**.

**Nota:** l'ordine della regola di filtro viene impostato nel seguente modo: viene applicata la prima regola che corrisponde a una metrica.

Ad esempio, se la sezione *metrics_filter* di un agent Sysdig è simile alla seguente:

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* Stai configurando l'agent Sysdig in modo che raccolga tutti i dati dalle metriche che iniziano con *metricA*, *metricB* e *haproxy.backend*. 
* Puoi filtrare le metriche che iniziano con *metricC* e le altre metriche che iniziano con *haproxy*. 
* La voce `exclude: metricA.*` viene ignorata.


## Modifica del livello di log
{: #change_linux_agent_log_level}

Per configurare il livello di log, devi personalizzare la sezione **log** nel file *dragent.yaml*. 

L'agent Sysdig genera le voci di log in */opt/draios/logs/draios.log*. 
* Il file di log ruota quando raggiunge 10MB di dimensione.
* I 10 file di log più recenti vengono conservati. La data che viene accodata al nome del file viene utilizzata per determinare quali file vengono conservati.
* I livelli di log validi sono: *none*, *error*, *warning*, *info*, *debug*, *trace*
* Il livello di log predefinito è *info*, i cui viene creata una voce per ogni trasmissione di metriche aggregate ai server di backend, una al secondo, in aggiunta alle voci di ogni avvertenza e errore.
* Puoi personalizzare il tipo di log e le voci che vengono raccolte configurando il file di configurazione dell'agent Sysdig **/opt/draios/etc/dragent.yaml**. Dopo aver modificato il file, devi riavviare l'agent alla shell con `service dragent restart` per attivare le modifiche.

| Casi di utilizzo                                     | Voce sezione log           |
|-----------------------------------------------|-----------------------------|
| Risoluzione dei problemi con il comportamento dell'agent                   | `file_priority: debug`      |
| Riduzione dell'output della console contenitore               | `console_priority: warning` |
| Filtro degli eventi per severità                  | `event_priority: warning`   |
| Verifica di quali metriche sono incluse od escluse  | `metrics_excess_log: true`  |
{: caption="Tabella 2. Voci della sezione di log" caption-side="top"} 
