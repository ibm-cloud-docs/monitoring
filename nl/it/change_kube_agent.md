---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# Personalizzazione degli agent Sysdig Kubernetes
{: #change_kube_agent}

In {{site.data.keyword.mon_full_notm}}, puoi personalizzare la configurazione dell'agent Sysdig per impostare un livello di log, le porte di blocco, includere o escludere i dati delle metriche, aggiungere o rimuovere gli eventi e filtrare i contenitori. 
{:shortdesc}

Per personalizzare un agent Sysdig Kubernetes, potresti dover configurare delle sezioni in tutti i seguenti file:

| Nome file                        | Azioni       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modifica livello di log. |
| `sysdig-agent-configmap.yaml`    | Blocca le porte. </br>Includi o escludi i dati delle metriche. </br>Aggiungi o rimuovi eventi. </br>Filtra i contenitori. |
{: caption="Tabella 1. File di configurazione dell'agent Sysdig Kubernetes" caption-side="top"} 

Per modificare un agent Sysdig Kubernetes, potresti dover modificare *sysdig-agent-configmap.yaml*, *sysdig-agent-daemonset-v2.yaml* o entrambi.
{: tip}

Esistono due metodi che puoi utilizzare per modificare un file di configurazione:
* Metodo 1: modifica il file direttamente sul cluster in cui è in esecuzione l'agent.
* Metodo 2: modifica il file localmente e applica le modifiche al cluster.

## Modifica della configurazione dell'agent Sysdig Kubernetes utilizzando kubectl edit
{: #change_kube_agent_edit_kube_agent_method1}

Completa la seguente procedura per modificare una configurazione dell'agent Sysdig Kubernetes:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-configmap.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Apporta le modifiche. **Nota:** fai riferimento alle istruzioni dell'editor `vi` per informazioni su come apportare le modifiche.

    Salva la modifiche. Le modifiche vengono applicate automaticamente. 

3. Modifica il file *sysdig-agent-daemonset-v2.yaml*. 

    Immetti il seguente comando: 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Apporta le modifiche. **Nota:** fai riferimento alle istruzioni dell'editor `vi` per informazioni su come apportare le modifiche.

    Salva la modifiche. Le modifiche vengono applicate automaticamente.

## Modifica della configurazione dell'agent Sysdig Kubernetes utilizzando kubectl apply
{: #change_kube_agent_edit_kube_agent_method2}

Utilizza questo metodo se i tuoi file yaml di configurazione sono archiviati e gestiti in un sistema di controllo di origine.

Completa la seguente procedura per modificare una configurazione dell'agent Sysdig Kubernetes:

1. Richiama l'ultima copia di ogni file dal controller di origine. 

    Per creare un file locale con la configurazione distribuita in un cluster, puoi anche eseguire il comando:
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    o 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. Modifica la configurazione.

3. Applica le modifiche utilizzando i seguenti comandi:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    o
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

L'esecuzione degli agent sceglierà automaticamente la nuova configurazione dopo che Kubernetes esegue il push delle modifiche a tutti i nodi nel cluster.


## Aggiunta di ulteriori tag ai dati raccolti da un agent Sysdig Kubernetes
{: #change_kube_agent_add_tags}

Completa la seguente procedura per aggiungere ulteriori tag a una configurazione dell'agent Sysdig Kubernetes che hai già distribuito:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-configmap.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. **Nota:** fai riferimento alle istruzioni dell'editor `vi` per informazioni su come apportare le modifiche.

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 

Per l'esempio fornito, sarebbero le tag **agent.tag.cluster_version** e **agent.tag.region**. Puoi utilizzarle per definire avvisi, ambiti personalizzati e altro.



## Raccolta di una serie di eventi Kubernetes
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} supporta le integrazioni degli eventi con Kubernetes. Gli agent Sysdig rilevano automaticamente questi servizi e raccolgono i dati degli eventi da esse. Puoi modificare il file di configurazione dell'agent per modificarne i comportamenti predefiniti e includere o escludere dei dati evento. 

Per impostazione predefinita, viene raccolta solo una serie limitata di eventi. Per ulteriori informazioni sugli eventi raccolti per impostazione predefinita, consulta [Kubernetes events ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}.

Per aggiungere o rimuovere degli eventi, devi personalizzare il file *sysdig-agent-configmap.yaml* e specificare quali eventi includere e quali filtrare. **Nota:** una voce in una sezione in *sysdig-agent-configmap.yaml* sovrascrive l'intera sezione nella configurazione predefinita.
{: tip}

Per filtrare gli eventi dai pod Kubernetes, completa la seguente procedura:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-configmap.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *events* o aggiorna la sezione.

    **Nota:** fai riferimento alle istruzioni dell'editor `vi` per informazioni su come apportare le modifiche.

    Ad esempio, potresti voler raccogliere gli eventi di pull del pod Kubernetes e filtrare altri eventi del pod raccolti per impostazione predefinita. Vuoi ancora raccogliere gli eventi Kubernetes predefiniti per i nodi e replicationControllers.

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 


Un altro esempio in cui puoi vedere come raccogliere un sottoinsieme di eventi Kubernetes: vuoi solo monitorare gli eventi dei pod in pull di cui è stato eseguito il pull e che hanno riscontrato dei problemi.

* Opzione 1: definisci la sequenza sulle voci come un elenco puntato:

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* Opzione 2: definisci la sequenza sulle voci in una sola riga tra parentesi:

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

Per ulteriori informazioni su come utilizzare gli eventi personalizzati, consulta [Working with custom events ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


## Disabilitazione della raccolta di eventi
{: #change_kube_agent_disable_events}

Per disabilitare un agent Sysdig dal raccogliere gli eventi Kubernetes, devi modificare il file *sysdig-agent-configmap.yaml*. Imposta la voce **Kubernetes** nella sezione **events** su *none*. 

Completa la seguente procedura:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-configmap.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *events* o aggiorna la sezione.

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 






## Inclusione ed esclusione delle metriche
{: #change_kube_agent_inc_exc_metrics}

Per filtrare le metriche personalizzate, devi personalizzare la sezione **metrics_filter** nel file *sysdig-agent-configmap.yaml*. Puoi specificare quali metriche includere e quali filtrare configurando i parametri di filtro **include** e **exclude**.

<p class="important">L'ordine della regola di filtro viene impostato nel seguente modo: viene applicata la prima regola che corrisponde a una metrica. Le regole seguenti per tale metrica vengono ignorate.</p>

Completa la seguente procedura:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-configmap.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *metrics_filter* o aggiorna la sezione.

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

4. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 




## Filtro degli oggetti e dei contenitori Kubernetes da cui vengono raccolti i dati.
{: #change_kube_agent_filter_data}

Un agent Sysdig Kubernetes raccoglie automaticamente le metriche da *tutti i contenitori* che rileva in un cluster, incluse le metriche Prometheus, StatsD, JMX, dei controlli dell'applicazione e integrate.
 
Puoi personalizzare l'agent Sysdig in modo che escluda dei contenitori dalla raccolta di metriche. 

Quando escludi dei contenitori, considera le seguenti informazioni:
* Riduci il carico dell'agent e di backend.
* Raccogli solo i dati dai contenitori che vuoi monitorare.
* Puoi controllare i costi considerando i contenitori importanti e filtrando i contenitori non necessari o non critici.

Per abilitare la funzione in cui un agent Sysdig filtra i contenitori, devi personalizzare il file *sysdig-agent-configmap.yaml*. Imposta la voce **use_container_filter** nella sezione **containers** su *true*. **Nota:** per impostazione predefinita, questa funzione è disattivata. Successivamente, definisci le regole che includono una o più condizioni che vuoi applicare.

La seguente tabella illustra i parametri che puoi definire per configurare le regole di filtro in un cluster:

| Parametro                          | Condizione                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | Nome immagine contenitore                           |
| `container.name`                   | Nome contenitore                                 |
| `container.label.*`                | Etichetta contenitore                                |
| `kubernetes.object.*`             | Oggetto Kubernetes. Un oggetto può essere un pod, uno spazio dei nomi, ecc.   |
| `kubernetes.object.annotation.*`  | Annotazione oggetto Kubernetes                   |
| `kubernetes.object.label.*`       | Etichetta oggetto Kubernetes                        |
| `all`                              | Regola predefinita per specificare tutti gli oggetti            |
{: caption="Tabella 2. Parametri per definire le condizioni sui contenitori" caption-side="top"} 

Prendi in considerazione le seguenti informazioni su come l'agent Sysdig applica le regole che definisci nella sezione **container_filter**:
* Definisci le condizioni configurandole con i parametri di filtro **include** e **exclude**. 
* La prima regola di corrispondenza nell'elenco determina se il contenitore viene incluso o escluso.
* Le condizioni sono formate da un valore e un nome della chiave. Se la chiave selezionata per un contenitore corrisponde al valore, la regola viene applicata.
* Quando una regola contiene più condizioni, tutte le condizioni (`all the conditions`) devono corrispondere alla regola che deve essere applicata.

Completa la seguente procedura per filtrare i contenitori che un agent Sysdig monitora in un cluster:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-configmap.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *metrics_filter* o aggiorna la sezione.

    Ad esempio, vedi il seguente estratto di una mappa di configurazione:

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 


## Blocco delle porte
{: #change_kube_agent_block_ports}

Per bloccare le metriche e il traffico di rete dalle porte di rete, devi personalizzare la sezione **blacklisted_ports** nel file *sysdig-agent-configmap.yaml*. Devi elencare le porte da cui vuoi filtrare tutti i dati.

**Nota:** la porta 53 (DNS) è sempre nella blacklist. 

Completa la seguente procedura:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-configmap.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *metrics_filter* o aggiorna la sezione.

    Ad esempio, il seguente esempio illustra come configurare la sezione *blacklisted_ports* di un agent Sysdig per escludere i dati provenienti dalle porte 6666 e 6379:

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 



## Modifica del livello di log
{: #change_kube_agent_log_level}

Per configurare il livello di log, devi personalizzare la sezione **log** nel file *sysdig-agent-daemonset-v2.yaml*. 

L'agent Sysdig genera le voci di log in */opt/draios/logs/draios.log*. 
* Il file di log ruota quando raggiunge 10MB di dimensione.
* I 10 file di log più recenti vengono conservati. La data che viene accodata al nome del file viene utilizzata per determinare quali file vengono conservati.
* I livelli di log validi sono: *none*, *error*, *warning*, *info*, *debug*, *trace*
* Il livello di log predefinito è *info*, i cui viene creata una voce per ogni trasmissione di metriche aggregate ai server di backend, una al secondo, in aggiunta alle voci di ogni avvertenza e errore.
* Puoi personalizzare il tipo di log e le voci che vengono raccolte configurando il file di configurazione dell'agent Sysdig **/opt/draios/etc/dragent.yaml**. Dopo aver modificato il file, devi riavviare l'agent alla shell con `service dragent restart` per attivare le modifiche.

La seguente tabella elenca alcuni scenari comuni e il valore che devi configurare per ognuno di essi:

| Casi di utilizzo                                     | Voce sezione log           |
|-----------------------------------------------|-----------------------------|
| Risoluzione dei problemi con il comportamento dell'agent                   | `file_priority: debug`      |
| Riduzione dell'output della console contenitore               | `console_priority: warning` |
| Filtro degli eventi per severità                  | `event_priority: warning`   |
| Verifica di quali metriche sono incluse od escluse  | `metrics_excess_log: true`  |
{: caption="Tabella 2. Voci della sezione di log" caption-side="top"} 

Completa la seguente procedura per configurare il livello di log:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-daemonset-v2.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *log* o aggiorna la sezione.

    Ad esempio, per filtrare gli eventi di severità bassa (*notice*, *information*, *debug*), devi impostare la voce **metrics_excess_log** nella sezione **log** su *true*:

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 


## Filtro degli eventi Kubernetes in base alla severità
{: #change_kube_agent_filterby_severity}

Per filtrare gli eventi per severità, devi modificare il file *sysdig-agent-daemonset-v2.yaml*. Imposta la voce **event_priority** nella sezione **log** su *none*. 

Il livello di log predefinito è **information**. Questo significa che vengono trasmessi solo gli eventi di severità warning o superiore.

I livelli validi sono: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* e *none*. **Nota**: i valori sono elencati dalla priorità più alta a quella più bassa.

Completa la seguente procedura:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-daemonset-v2.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *log* o aggiorna la sezione.

    Ad esempio, per filtrare gli eventi di severità bassa (*notice*, *information*, *debug*), devi impostare la sezione di log **event_priority** su *warning*:

    ```
    log:
  event_priority: warning
    ```
    {: codeblock}

6. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 

## Registrazione in un file di quali metriche sono incluse o escluse
{: #change_kube_agent_log_metrics}

Per registrare in un file le informazioni su quali metriche personalizzate sono incluse e quali escluse, devi personalizzare il file *sysdig-agent-daemonset-v2.yaml*. Imposta la voce **metrics_excess_log** su **true** nella sezione **log**.

* La registrazione è disabilitata per impostazione predefinita. 
* La registrazione si verifica al livello informativo ogni 30 secondi e ha una durata di 10 secondi. 
* Il file di log è disponibile in */opt/draios/logs/draios.log*.
* La registrazione dei dati viene formattata nel seguente modo:

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* è un simbolo che indica se la metrica viene inclusa o esclusa. Il più (*+*) indica che una metrica viene inclusa. Il meno (*-*) indica che una metrica viene esclusa. 

    * *[type]* specifica il tipo di metrica, ad esempio, *statsd*.
    
    * *[metric included/excluded]* indica in modo leggibile se la metrica viene inclusa o esclusa.

    *  *metric.name* indica il nome della metrica.

    * *(filter: +/-[metric.filter])* fornisce le informazioni su tutti i filtri definiti nella sezione **metrics_filter** nel file *sysdig-agent-daemonset-v2.yaml*.

Una voce di esempio è simile alla seguente:

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

Completa la seguente procedura:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Modifica il file *sysdig-agent-daemonset-v2.yaml*. 

    Immetti il seguente comando:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Apporta le modifiche. Aggiungi la sezione *log* o aggiorna la sezione.

    Ad esempio, per filtrare gli eventi di severità bassa (*notice*, *information*, *debug*), devi impostare la voce **metrics_excess_log** nella sezione **log** su *true*:

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. Salva la modifiche. 

Le modifiche vengono applicate automaticamente. 


## File yaml configmap di esempio
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:    
      kubernetes:
        node: 
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter: 
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## File yaml daemonset di esempio
{: #change_kube_agent_sample_daemonset}

```
 Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

