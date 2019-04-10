---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Personalizzazione dell'agent Sysdig in modo che controlli i dati
{: #customize_agent}

Per impostazione predefinita, l'agent Sysdig raccoglie i dati da una serie di piattaforme e applicazioni. Puoi modificare il file di configurazione dell'agent per modificarne i comportamenti predefiniti e includere o escludere i dati. Puoi personalizzare il file di configurazione dell'agent Sysdig in modo che includa delle metriche personalizzate come ad esempio JMX, StatsD e Prometheus. Puoi anche filtrare le metriche, i dati evento e i contenitori.
{:shortdesc}

## Personalizzazione dell'agent Sysdig Kubernetes
{: #kube}

L'agent Sysdig Kubernetes utilizza due file di configurazione che specificano quali dati raccogliere automaticamente:

| Nome file                        | Azioni           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modifica livello di log. |
| `sysdig-agent-configmap.yaml`    | Blocca le porte. </br>Includi o escludi i dati delle metriche. </br>Aggiungi o rimuovi eventi. </br>Filtra i contenitori. |
{: caption="Tabella 1. File di configurazione dell'agent Sysdig Kubernetes" caption-side="top"} 

Per modificare un agent Sysdig Kubernetes, potresti dover modificare *sysdig-agent-configmap.yaml*, *sysdig-agent-daemonset-v2.yaml* o entrambi.

Esistono due metodi che puoi utilizzare per modificare un file di configurazione:
* Metodo 1: modifica il file direttamente sul cluster in cui è in esecuzione l'agent. Per ulteriori informazioni, consulta [Modifica della configurazione dell'agent Sysdig Kubernetes utilizzando kubectl edit](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1).
* Metodo 2: modifica il file localmente e applica le modifiche al cluster. Per ulteriori informazioni, consulta [Modifica della configurazione dell'agent Sysdig Kubernetes utilizzando kubectl apply](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2).

Puoi aggiungere delle tag ai dati raccolti dall'agent. 
* Utilizza queste tag per gestire i dati che monitori. 

    * Utilizza le etichette per raggruppare le risorse dell'infrastruttura in gerarchie logiche, filtrare i dati e suddividere i dati aggregati in segmenti. 
    
    * Personalizza come i dati vengono aggregati quando configuri un grafico o crei un avviso per una metrica. 
    
    * Configura l'ambito di un dashboard, un pannello o un avviso in modo che filtri i punti dati. 
    
    * Limita l'accesso ai dati gestendo l'accesso ai dati degli utenti tramite i team. 
    
    * Per ulteriori informazioni su come gestire i dati, consulta [Gestione dei dati](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

* Per informazioni su come aggiungere delle tag, consulta [Aggiunta di ulteriori tag ai dati raccolti da un agent Sysdig Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags). 


**Puoi personalizzare quali dati vengono raccolti dall'agent Sysdig.** 

Quando escludi eventi, metriche e contenitori, considera le seguenti informazioni:
* Puoi ridurre il carico dell'agent e di backend.
* Raccogli solo i dati dai contenitori che vuoi monitorare.
* Puoi controllare i costi considerando i contenitori importanti e filtrando i contenitori non necessari o non critici.
* Puoi configurare gli eventi Kubernetes che vuoi monitorare. Per ulteriori informazioni, vedi [Raccolta di una serie di eventi Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events).

Il seguente elenco illustra le azioni che puoi eseguire per controllare i dati che vengono raccolti dall'agent Sysdig:
* [Disabilitazione della raccolta di eventi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [Inclusione ed esclusione delle metriche](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [Filtro degli oggetti e dei contenitori Kubernetes da cui vengono raccolti i dati.](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [Blocco delle porte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [Filtro degli eventi Kubernetes in base alla severità](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

Puoi anche personalizzare il tipo di log e le voci che vengono raccolte. Per ulteriori informazioni. consulta [Modifica del livello di log](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level).

Puoi anche registrare l'elenco di metriche di cui l'agent riporta i dati. Per ulteriori informazioni, vedi [Registrazione in un file di quali metriche sono incluse o escluse](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics).

L'agent Sysdig genera le voci di log in */opt/draios/logs/draios.log*. 
* Il file di log ruota quando raggiunge 10MB di dimensione.
* I 10 file di log più recenti vengono conservati. La data che viene accodata al nome del file viene utilizzata per determinare quali file vengono conservati.
* I livelli di log validi sono: *none*, *error*, *warning*, *info*, *debug*, *trace*
* Il livello di log predefinito è *info*, i cui viene creata una voce per ogni trasmissione di metriche aggregate ai server di backend, una al secondo, in aggiunta alle voci di ogni avvertenza e errore.

La seguente tabella elenca alcuni scenari comuni e il valore che devi configurare per ognuno di essi:

| Casi di utilizzo                                     | Voce sezione log           |
|-----------------------------------------------|-----------------------------|
| Risoluzione dei problemi con il comportamento dell'agent                   | `file_priority: debug`      |
| Riduzione dell'output della console contenitore               | `console_priority: warning` |
| Filtro degli eventi per severità                  | `event_priority: warning`   |
| Verifica di quali metriche sono incluse od escluse  | `metrics_excess_log: true`  |

## Agent Sysdig contenitore
{: #container}


Il seguente elenco illustra le azioni che puoi eseguire per controllare i dati che vengono raccolti dall'agent Sysdig:
* [Disabilitazione della raccolta di eventi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [Inclusione ed esclusione delle metriche](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [Filtro dei contenitori da cui vengono raccolti i dati](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [Blocco delle porte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [Filtro degli eventi in base alla severità](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

Puoi anche personalizzare il tipo di log e le voci che vengono raccolte. Per ulteriori informazioni. consulta [Modifica del livello di log](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level).



## Agent Sysdig Linux
{: #linux}

L'agent Sysdig Linux utilizza due file di configurazione che specificano quali dati raccogliere automaticamente:

| File                   | Descrizione                                                     | Ubicazione                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | File di configurazione principale </br>**Nota:****non modificare questo file.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | File di configurazione che modifichi per personalizzare l'agent Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabella 1. File di configurazione dell'agent Sysdig" caption-side="top"} 

Puoi modificare il file *dragent.yaml* per personalizzare i dati che vengono raccolti. Le modifiche hanno effetto immediatamente dopo che salvi il file. L'agent rileva la modifica ed esegue un riavvio in automatico. Puoi trovare la frequenza e i file che un agent Sysdig controlla nel file *dragent.default.yaml*. Per ulteriori informazioni, consulta [Modifica del file yaml dragent](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent).

Ad esempio, un *dragent.default.yaml* include le seguenti informazioni:

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

Il seguente elenco illustra le azioni che puoi eseguire per controllare i dati che vengono raccolti dall'agent Sysdig:
* [Inclusione ed esclusione delle metriche](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [Blocco delle porte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

Puoi anche personalizzare il tipo di log e le voci che vengono raccolte. Per ulteriori informazioni. consulta [Modifica del livello di log](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level).


