---

copyright:
  years: 2018, 2019
lastupdated: "2018-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Personalizzazione degli agent Sysdig del contenitore
{: #change_agent}

In {{site.data.keyword.mon_full_notm}}, puoi personalizzare la configurazione dell'agent Sysdig per impostare un livello di log, le porte di blocco, includere o escludere i dati delle metriche, aggiungere o rimuovere gli eventi e filtrare i contenitori. 
{:shortdesc}




## Modifica del file yaml dragent
{: #edit_agent}

Il file yaml è ubicato in */opt/draios/etc/*.

Completa la seguente procedura per modificare il file e applicare le modifiche:

1. Accedi a *dragent.yaml* direttamente da `/opt/draios/etc/dragent.yaml`.
2. Modifica il file. Utilizza una sintassi YAML valida.
3. Riavvia l'agent. Immetti il seguente comando:

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## Blocco delle porte
{: #ports}

Per bloccare le metriche e il traffico di rete dalle porte di rete, devi personalizzare la sezione **blacklisted_ports** nel file *dragent.yaml*. Devi elencare le porte da cui vuoi filtrare tutti i dati.

**Nota:** la porta 53 (DNS) è sempre nella blacklist. 

Ad esempio, il seguente esempio illustra come configurare la sezione *blacklisted_ports* di un agent Sysdig per escludere i dati provenienti dalle porte 6666 e 6379:

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## Raccolta di una serie di eventi Docker
{: #docker}

{{site.data.keyword.mon_full_notm}} supporta l'integrazione degli eventi con Docker. Gli agent Sysdig rilevano automaticamente le origini Docker e raccolgono i dati degli eventi da esse. Puoi modificare il file di configurazione dell'agent per modificarne i comportamenti predefiniti e includere o escludere dei dati evento. 

Per impostazione predefinita, viene raccolta solo una serie limitata di eventi. Il file di configurazione delle impostazioni predefinito */opt/draios/etc/dragent.default.yaml* include gli eventi che vengono raccolti. Per ulteriori informazioni sugli eventi raccolti per impostazione predefinita, consulta [Docker events ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}.

Per aggiungere o rimuovere degli eventi, devi personalizzare il file *dragent.yaml* e specificare quali eventi includere e quali filtrare. **Nota:** una voce in una sezione in *dragent.yaml* sovrascrive l'intera sezione nella configurazione predefinita.
{: tip}

Ad esempio, per filtrare gli eventi delle immagini Docker e raccogliere solo gli eventi per le azioni attach, commit e copy, devi configurare la sezione *docker* nel seguente modo:

* Opzione 1: definisci la sequenza sulle voci come un elenco puntato:

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* Opzione 2: definisci la sequenza sulle voci in una sola riga tra parentesi:

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## Disabilitazione della raccolta di eventi
{: #disable}

Per disabilitare la raccolta di eventi di un agent Sysdig, modifica il file *dragent.default.yaml*. Imposta la sezione **events** su *none* nel file *dragent.yaml*.

Ad esempio, per filtrare gli eventi Docker, devi impostare la sezione *events* nel file *dragent.yaml* nel seguente modo:

```
events:
  docker: none
```
{: codeblock}



## Filtro degli eventi per severità
{: #severity}

Per filtrare gli eventi per severità, puoi anche modificare il tipo di voce di log nel file *dragent.yaml*. 

Il livello di log predefinito è **information**. Questo significa che vengono trasmessi solo gli eventi di severità warning o superiore.

I livelli validi sono: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* e *none*. **Nota**: i valori sono elencati dalla priorità più alta a quella più bassa.

Ad esempio, per filtrare gli eventi di severità bassa (*notice*, *information*, *debug*), devi impostare la sezione di log **event_priority** su *warning*:

```
log:
  event_priority: warning
```
{: codeblock}


Per bloccare la raccolta di eventi, devi impostare la sezione di log **event_priority** su *none*:

```
log:
  event_priority: none
```
{: codeblock}




## Inclusione ed esclusione delle metriche
{: #params}

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
{: #log_level}

Per configurare il livello di log, devi personalizzare la sezione **log** nel file *dragent.yaml*. 

L'agent Sysdig genera le voci di log in */opt/draios/logs/draios.log*. 
* Il file di log ruota quando raggiunge 10MB di dimensione.
* I 10 file di log più recenti vengono conservati. La data che viene accodata al nome del file viene utilizzata per determinare quali file vengono conservati.
* I livelli di log validi sono: *none*, *error*, *warning*, *info*, *debug*, *trace*
* Il livello di log predefinito è *info*, i cui viene creata una voce per ogni trasmissione di metriche aggregate ai server di backend, una al secondo, in aggiunta alle voci di ogni avvertenza e errore.
* Puoi personalizzare il tipo di log e le voci che vengono raccolte configurando il file di configurazione dell'agent Sysdig **/opt/draios/etc/dragent.yaml**. Dopo aver modificato il file, devi riavviare l'agent alla shell con `docker restart sysdig-agent` per attivare le modifiche.

| Casi di utilizzo                                     | Voce sezione log           |
|-----------------------------------------------|-----------------------------|
| Risoluzione dei problemi con il comportamento dell'agent                   | `file_priority: debug`      |
| Riduzione dell'output della console contenitore               | `console_priority: warning` |
| Filtro degli eventi per severità                  | `event_priority: warning`   |
| Verifica di quali metriche sono incluse od escluse  | `metrics_excess_log: true`  |
{: caption="Tabella 2. Voci della sezione di log" caption-side="top"} 


